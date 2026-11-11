# Website refactor: design system, routes and plan

Status: **proposed, not implemented.** Owner alignment is needed before any code moves.

Scope: the FORGED Custom Wheels site in `FazalRSA/Forgedwebsite`. This repo holds only a template README, so the evidence below comes from the website repo, read at commit `6b527e6` on its default branch.

Baseline: `npm install`, the tests and the build were not run. The install step was blocked by the session's permission policy, so every number here comes from reading the files.

## 1. What the evidence shows

| Finding | Measured | Why it matters |
|---|---|---|
| Colours are hardcoded, not tokenised | 411 hex literals in `src/**/*.ts(x)`; 335 arbitrary Tailwind colour classes such as `bg-[#18181D]` | The README says "do not add new colours", but nothing enforces it. A palette change means a repo-wide search. |
| Tokens do not generate utilities | Tokens sit in `:root` inside `src/index.css`, and there is no `@theme` block | Tailwind v4 emits utilities only from variables declared in `@theme`. The `:root` tokens are plain CSS variables, so components fall back to arbitrary values. |
| Off-palette colours are in use | At least 15 distinct hex values fall outside the token set, for example `#33333E` (16 uses), `#7C7C8A`, `#2B2D42`, `#D9D9D9`, `#C8102E`, `#C5B095` | Some are wheel finish swatches in `src/data/` and stay as data. The rest are drift. |
| Route paths are repeated | `/installs` appears in 13 files. Routes are defined in six places: `App.tsx`, `seo.ts`, `redirects.ts`, `legacy-pages.json`, the generated `render.yaml` block, and `llms.ts` | A renamed or removed page needs edits in all six. The tests catch some mismatches but not all. |
| Unused dependencies | `@google/genai`, `express` and `dotenv` have zero imports | They add install weight and attack surface for nothing. |
| Starter leftovers are tracked | `.aistudio/` (screenshots and an old plan), `metadata.json`, `.env.example` | The plan in `.aistudio/` uses `#FF5500`, which breaks the palette. Nothing reads these files. |
| Two deploy configs | `render.yaml` (the documented host) and `vercel.json` | One of them is probably stale. The owner must say which. |
| Large files | `WheelStudio.tsx` 1000 lines (shared viewer), `catalogue.ts` 723, `AdminWheelUploader.tsx` 719 (79 hex literals), `WheelShowcasePDP.tsx` 535 (19 hex literals) | The admin page is unlisted, so its colours matter least. The shared viewer must not change casually. |

## 2. Requirements (inferred, to confirm)

- **Goal.** Maintainability and one source of truth for colour and routes. No change to what visitors see or to the SEO output.
- **Scale.** Five public pages, one owner, a static host, low traffic. Optimise for clarity, not throughput.
- **Hard constraints.**
  - The 3D viewer is shared with the BMW configurator. Its public API must not change without a configurator pull.
  - Enquiries go through WhatsApp only. No new third-party scripts, because the privacy notice lists what the site contacts.
  - Phone width (390 px) must stay clean.
- **Preferences.** Keep the current build pipeline (prerendered meta, generated sitemap, `llms.txt`). It already works.

## 3. Options

**A. Tokens and one route table (recommended).**
- Move the palette into an `@theme` block, keeping the current names.
- Codemod the hex and arbitrary classes to utilities. Leave the wheel finish swatches as data.
- Add `src/config/routes.ts`: one array of `{ id, path, component, title, description, indexed, inSitemap }`. `App.tsx`, `seo.ts`, the sitemap and `llms.ts` read it. Components import route helpers instead of string literals.
- Delete the three unused dependencies and the tracked `.aistudio/` folder, after the owner agrees.
- Effort: small to medium. Risk: low, because the build output can be diffed.

**B. A plus splitting the large components.**
- Everything in A, then split `AdminWheelUploader.tsx` and `WheelShowcasePDP.tsx` into smaller modules.
- Effort: medium. Risk: low to medium. Benefit is mostly readability, since these files work today.

**C. Adopt a router library and a component library.**
- Replace the custom router and the `if` chain with a routing library, and build a shared component library with Storybook.
- Effort: large. Risk: medium to high, with a visual regression on every page.
- Rejected. Five pages do not justify the cost. The next 10x of this site is still a catalogue and a contact page.

## 4. Recommendation

Adopt A now. Revisit B when the admin uploader next changes. Keep the shared viewer out of this refactor.

The reasons are:
- Option A removes the two real sources of drift, colours and route strings, with the smallest blast radius.
- The viewer has its own stamp and copy process. Changing it here would also force a configurator pull.
- The build already prerenders routes, so a route table can drive it without a new framework.

## 5. Design system: the target contract

**Colour.** The palette in `@theme`, with the current names:

| Token group | Values | Use |
|---|---|---|
| Surfaces | `#111111` base, `#121215` surface, `#18181D` card, `#1E1E26` subtle border, `#26262E` border | Backgrounds and dividers |
| Text | `#EDEBE4` primary, `#C2C2CC` secondary, `#727280` muted | Copy |
| Action | `#1D4ED8` fill, `#2563EB` hover | Button fills and selected states only |
| Accent | `#F43F5E` | Accent text and keyboard focus only |
| Channel | `#25D366` WhatsApp, `#E1306C` Instagram | Those channels' own buttons only |

Rules to enforce in review:
- No new hex in components. Add a token first.
- Blue text on the black background is unreadable, so accent text is always rose.
- Logo reds and golds are never interface colours.

**Type.** Satoshi Black for `h1`, Nunito for other headings, Open Sans for body, Geist Mono for specs and labels. Keep the existing three-font rule.

**Components.** Use `SafeImage` for wheel photography, and `WheelStage` for any 3D view.

**Minimum text size.** The codebase uses 9, 10 and 11 px text in 26 arbitrary-size classes. Decide a floor, probably 11 px for labels, and enforce it.

## 6. Route contract

One table, `src/config/routes.ts`. Each entry defines:

| Field | Used by |
|---|---|
| `id` and `path` | `App.tsx` route match, component links |
| `component` key | `App.tsx` lazy import |
| `title` and `description` | `seo.ts` `metaForPath` |
| `indexed` | `noindex` and the sitemap filter |
| `inSitemap` and `prerender` | `scripts/generate-sitemap.ts`, `scripts/prerender-meta.ts` |

Keep the redirect data separate, because it is a list of old addresses, not routes. The generated `render.yaml` block must come out byte-identical after the change. The existing tests then check the rest.

## 7. Migration plan

Each step is its own pull request, and each keeps the checks green.

1. **Clean-up.** Remove the three unused dependencies and the tracked `.aistudio/` folder. Keep `.env.example` until the owner confirms. Run the build and diff `dist/`.
2. **Tokens.** Add `@theme`, keep the `:root` aliases for one release, then codemod the classes. Check screenshots at 390 px and 1280 px before and after.
3. **Route table.** Move the route data into `src/config/routes.ts` and switch `App.tsx`, `seo.ts` and the sitemap to read it. Diff `render.yaml`, `public/sitemap.xml` and the prerendered HTML. The diff must be empty.
4. **Components.** Replace route string literals with helpers. Remove the `:root` aliases.
5. **Optional.** Split the admin uploader and the PDP, if the owner wants it.

Verification at every step:
- `npm run lint`, `npm test` (which runs `wheel-viewer:verify`), and `npm run build`.
- A diff of `dist/` and `render.yaml` before and after. Only intended changes may appear.
- Screenshots of `/`, `/wheels/<slug>`, `/installs`, `/contact` at 390 px and 1280 px.

## 8. Failure modes and mitigations

| Failure | Detection | Mitigation |
|---|---|---|
| A codemod shifts a colour slightly | Screenshot diff | Codemod only from a fixed map, and review the diff |
| A route is missing from the table | Sitemap test, `seo.test.ts`, `redirects.test.ts` | Keep the tests; add one that checks every `App.tsx` route is in the table |
| The generated `render.yaml` drifts | Diff in step 3 | Generate from the table and fail the build on drift |
| The viewer changes without a stamp | `wheel-viewer:verify` in `npm test` | Do not touch `src/wheel-viewer/` in this work |
| Removing a dependency breaks something unseen | Build plus a grep for imports | Remove one dependency per pull request |

## 9. Decisions needed from the owner

1. **Which repo.** Confirm `FazalRSA/Forgedwebsite` is the live codebase. This repo (`Forged-website-`) holds only a template README.
2. **Option.** Approve A, or choose B or C.
3. **Deploy target.** Confirm Render is the host, so `vercel.json` can go.
4. **Starter files.** Confirm `.aistudio/`, `metadata.json` and `.env.example` can be removed.
5. **Text floor.** Choose the smallest allowed text size.

## 10. Reversibility

- Tokens and the route table: reversible by reverting the pull request.
- Removing dependencies: reversible from the lockfile, though it changes `bun.lock`.
- Deleting `.aistudio/`: reversible from git history, so low risk.
- The viewer and the configurator copy: not touched here. Any later change is one-way for the configurator until it pulls.
