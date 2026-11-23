---
name: sixnine-website
description: Master reference for a wheel-shop site in the SIXNINE Wheels style - tokens, shared CSS, product card, finish swatch codes, wheel image angles. Use for any SIXNINE-style UI work; load it first.
---

# SIXNINE website style: master reference

This is the shared foundation for making a wheel site look and work like the SIXNINE Wheels storefront (sixnine-wheels.com): dark, near-monochrome, pill-shaped, frosted glass, product renders on soft tiles. Everything below was measured from the live site on 19 Nov 2026 (theme CSS, product feed of 88 products, rendered pages, configurator script).

## Whose site this is

The reference is SIXNINE's design language and structure. The site being built belongs to the user and carries the user's brand. Keep their name, logo, photography and wording, and never produce a page that presents itself as SIXNINE or could be mistaken for their shop. If the user sells genuine SIXNINE wheels as a dealer, product names, sizes and finish names are facts and can be stated; SIXNINE's renders, photos and marketing copy need SIXNINE's permission, so ask whether the user has dealer assets before using any.

## Which skill does what

| Task | Skill |
|---|---|
| Tokens, shared components, header/footer, finishes, wheel images, anything cross-cutting | this one |
| Collection grids, product cards in context, filters, product pages, titles, SKUs, descriptions | `sixnine-product-listing` |
| Homepage, series landing pages, pre-order and sale campaigns, About | `sixnine-marketing-pages` |
| Blog and news posts, news index | `sixnine-blog-writing` |

The three task skills assume the tokens and classes defined here, so load this one first.

## How to work

1. Inspect the codebase before changing anything: framework, styling approach (Tailwind, CSS modules, plain CSS, Shopify theme), where global styles live, and which components render products, buttons, headers and forms. Map the classes below onto what exists; keep the user's naming if they have one.
2. Add the fonts and tokens first and confirm the site still renders. Then restyle shared controls, then page-specific work.
3. Leave business logic alone: routing, data fetching, cart and checkout stay as they are.
4. After each step check 1440, 900 and 390 px widths for overflow.
5. With Tailwind, put the tokens in the config (colors, borderRadius, fontFamily, boxShadow, screens 750 and 990) and reproduce the CSS below with utilities. With React, build one component per block.

## 1. Principles

- **Dark first, near-monochrome.** Canvas `#08080A`, white type. White is the primary action colour, not a brand hue.
- **One accent, used rarely.** Violet `#47276F` for the single promoted action and the focus glow. If a view has two violet elements, demote one.
- **Pills everywhere.** Every control is fully rounded (999px). Containers step 12, 16, 22, 28px.
- **Glass, not solid.** Translucent white fills, 1px hairlines, a 1px inner top highlight, backdrop blur on floating elements. Depth comes from borders and one long soft shadow.
- **Selected means inverted.** Active pills, filters and options flip to white fill with dark text; they do not turn violet.
- **Product first.** Transparent wheel renders, contained with padding on a soft radial tile, never cropped by the frame.
- **Calm motion.** One easing, tiny hover moves, press feedback by scale. Hover effects only on pointer devices; everything off under reduced motion.

## 2. Tokens

Fonts: Albert Sans 400/500/600/700 for everything, Montserrat 400/500 for long-form copy only (both on Google Fonts). Dark is the default; light mode is the same token set with other values and is optional.

```css
:root,[data-theme="dark"]{
  --bg:#08080A; --bg-2:#0F0F12;
  --fg:#FFFFFF; --fg-2:rgba(255,255,255,.70); --fg-3:rgba(255,255,255,.46);
  --line:rgba(255,255,255,.09); --line-2:rgba(255,255,255,.18);
  --glass:rgba(255,255,255,.055); --glass-2:rgba(255,255,255,.10); --sunk:rgba(0,0,0,.32);
  --violet:#47276F; --violet-2:#542E82; --sale:#B996FF; --ok:#3FB97A;
  --glow:rgba(84,46,130,.32);
  --tile:radial-gradient(90% 90% at 50% 35%,rgba(255,255,255,.075) 0%,rgba(255,255,255,.02) 70%);
  --shadow:0 24px 64px -24px rgba(0,0,0,.75);
  --hl:inset 0 1px 0 rgba(255,255,255,.10);
  --r-sm:12px; --r:16px; --r-lg:22px; --r-xl:28px; --pill:999px;
  --ease:cubic-bezier(.23,1,.32,1);
  --font:"Albert Sans","Helvetica Neue",Arial,sans-serif;
  --font-copy:"Montserrat","Helvetica Neue",Arial,sans-serif;
}
[data-theme="light"]{
  --bg:#F3F3F4; --bg-2:#FFFFFF;
  --fg:#0A0A0B; --fg-2:rgba(10,10,11,.68); --fg-3:rgba(10,10,11,.48);
  --line:rgba(0,0,0,.08); --line-2:rgba(0,0,0,.16);
  --glass:rgba(255,255,255,.72); --glass-2:#FFFFFF; --sunk:rgba(0,0,0,.04);
  --sale:#542E82; --glow:rgba(71,39,111,.12);
  --tile:radial-gradient(90% 90% at 50% 35%,#FFFFFF 0%,#ECECEE 80%);
  --shadow:0 24px 56px -28px rgba(20,16,28,.28);
  --hl:inset 0 1px 0 rgba(255,255,255,.9);
}
```

Roles: `fg` text and primary fills; `fg-2` secondary text; `fg-3` labels only (in light mode it is about 3.4:1, too low for body text); `line` default border, `line-2` hover and outlined controls; `glass` card fill, `glass-2` raised or hover fill; `sunk` inputs; `sale` the saving line on cards; `ok` success and stock.

| Scale | Value |
|---|---|
| h1 | clamp(48px, 7.2vw, 108px), line-height .98, tracking -0.04em, bold |
| h2 | clamp(32px, 4.4vw, 60px), 1.04, -0.032em |
| h3 | clamp(20px, 1.8vw, 26px), 1.2, -0.018em |
| lead | clamp(17px, 1.5vw, 20px), 1.55, fg-2, max 46ch |
| body / long copy | 16px/1.5 Albert Sans / 16px/1.7 Montserrat, max 58ch |
| eyebrow | 12px, 700, uppercase, 0.14em, fg-3 |
| container | max 1320px, side padding clamp(20px, 4vw, 40px) |
| section band | clamp(72px, 10vw, 136px) vertical; tight clamp(48px, 6vw, 80px) |
| product grid | 4 columns, 3 below 990px, 2 below 750px, gap clamp(12px, 2vw, 24px) |
| controls | 52px buttons and fields, 40px small, 42px option pills and icon buttons, 38px filter pills |
| breakpoints | 750px and 990px (nav also tunes at 900 and 1200) |

## 3. Shared component CSS

Put `class="sn"` on the page root. Class names follow block, `__element`, `--modifier`.

```css
.sn{background:var(--bg);color:var(--fg);font-family:var(--font);font-size:16px;line-height:1.5;-webkit-font-smoothing:antialiased}
.sn *,.sn *::before,.sn *::after{box-sizing:border-box}
/* zero-specificity resets, so any component class can override them */
:where(.sn) a{color:inherit;text-decoration:none}
:where(.sn) :is(h1,h2,h3,h4,p,ul,figure){margin:0;padding:0}

/* layout */
.sn-wrap{width:100%;max-width:1320px;margin:0 auto;padding:0 clamp(20px,4vw,40px)}
.sn-band{position:relative;padding:clamp(72px,10vw,136px) 0}
.sn-band--alt{background:var(--bg-2)}
.sn-band--tight{padding:clamp(48px,6vw,80px) 0}
.sn-head{display:grid;gap:14px;max-width:760px;margin-bottom:clamp(36px,5vw,56px)}
.sn-grid{display:grid;grid-template-columns:repeat(var(--cols,4),minmax(0,1fr));gap:clamp(12px,2vw,24px)}
@media(max-width:989px){.sn-grid{--cols:3}}
@media(max-width:749px){.sn-grid{--cols:2}}

/* type */
.sn-eyebrow{font-size:12px;font-weight:700;letter-spacing:.14em;text-transform:uppercase;color:var(--fg-3)}
.sn-h1{font-size:clamp(48px,7.2vw,108px);line-height:.98;letter-spacing:-.04em}
.sn-h2{font-size:clamp(32px,4.4vw,60px);line-height:1.04;letter-spacing:-.032em}
.sn-h3{font-size:clamp(20px,1.8vw,26px);line-height:1.2;letter-spacing:-.018em}
.sn-lead{font-size:clamp(17px,1.5vw,20px);line-height:1.55;color:var(--fg-2);max-width:46ch}
.sn-copy{font-family:var(--font-copy);font-size:16px;line-height:1.7;color:var(--fg-2);max-width:58ch}
.sn-fine{font-size:12px;line-height:1.5;color:var(--fg-3)}

/* buttons */
.sn-btn{display:inline-flex;align-items:center;justify-content:center;gap:10px;min-height:52px;padding:0 26px;border-radius:var(--pill);border:1px solid transparent;font:600 15px/1 var(--font);letter-spacing:-.005em;white-space:nowrap;cursor:pointer;transition:transform .16s var(--ease),background-color .2s var(--ease),opacity .2s var(--ease),color .2s var(--ease)}
.sn-btn:active{transform:scale(.97)}
.sn-btn svg{width:17px;height:17px;flex:none}
.sn-btn--primary{background:var(--fg);color:var(--bg)}
.sn-btn--glass{background:var(--glass);border-color:var(--line-2);color:var(--fg);box-shadow:var(--hl);backdrop-filter:blur(14px)}
.sn-btn--accent{background:var(--violet);color:#fff}
.sn-btn--ghost{background:transparent;color:var(--fg-2)}
.sn-btn--sm{min-height:40px;padding:0 18px;font-size:14px}
.sn-btn--block{width:100%}
.sn-btn[disabled],.sn-btn[aria-disabled=true]{opacity:.4;pointer-events:none}
.sn-iconbtn{display:inline-grid;place-items:center;width:42px;height:42px;border-radius:var(--pill);background:transparent;border:0;color:var(--fg-2);cursor:pointer}
@media(hover:hover) and (pointer:fine){
  .sn-btn--primary:hover{opacity:.88}
  .sn-btn--glass:hover{background:var(--glass-2)}
  .sn-btn--accent:hover{background:var(--violet-2)}
  .sn-btn--ghost:hover{color:var(--fg);background:var(--glass)}
  .sn-iconbtn:hover{background:var(--glass-2);color:var(--fg)}
}

/* badges, pills, panel, field */
.sn-badge{display:inline-flex;align-items:center;gap:8px;min-height:32px;padding:0 14px;border-radius:var(--pill);font-size:13px;font-weight:600;white-space:nowrap}
.sn-badge--accent{background:var(--violet);color:#fff}
.sn-badge--light{background:#fff;color:#0A0A0B}
.sn-badge--glass{background:rgba(255,255,255,.14);color:#fff;border:1px solid rgba(255,255,255,.2);backdrop-filter:blur(12px)}
.sn-pill{display:inline-flex;align-items:center;gap:8px;padding:8px 16px;border-radius:var(--pill);background:var(--glass-2);border:1px solid var(--line);box-shadow:var(--hl);font-size:12px;font-weight:700;letter-spacing:.12em;text-transform:uppercase;color:var(--fg-2);white-space:nowrap}
.sn-pill--accent{background:var(--violet);border-color:transparent;color:#fff;box-shadow:none}
.sn-panel{background:var(--glass);border:1px solid var(--line);border-radius:var(--r-lg);box-shadow:var(--shadow),var(--hl);backdrop-filter:blur(20px) saturate(150%)}
.sn-field{display:flex;align-items:center;gap:6px;height:52px;padding:0 5px 0 20px;border-radius:var(--pill);background:var(--sunk);border:1px solid var(--line);box-shadow:var(--hl)}
.sn-field:focus-within{border-color:var(--line-2);box-shadow:0 0 0 4px rgba(84,46,130,.22),var(--hl)}
.sn-field input{flex:1;min-width:0;height:100%;border:0;outline:0;background:transparent;color:var(--fg);font:500 15px/1 var(--font)}

/* product card */
.sn-card{display:grid;gap:14px;align-content:start;transition:transform .16s var(--ease)}
.sn-card:active{transform:scale(.985)}
.sn-card__media{position:relative;aspect-ratio:1/1;overflow:hidden;border-radius:var(--r-lg);background:var(--tile);border:1px solid var(--line);transition:border-color .2s ease}
.sn-card__media img{position:absolute;inset:0;width:100%;height:100%;object-fit:contain;padding:9%;transition:transform .4s var(--ease),opacity .24s ease}
.sn-card__media img+img{opacity:0}
.sn-card__badge{position:absolute;top:12px;left:12px;z-index:2;padding:6px 11px;border-radius:var(--pill);background:var(--fg);color:var(--bg);font-size:11px;font-weight:700;letter-spacing:.06em;text-transform:uppercase}
.sn-card__badge--muted{background:var(--glass-2);color:var(--fg-2);border:1px solid var(--line)}
.sn-card__body{display:grid;gap:5px;padding:0 4px}
.sn-card__series{font-size:11px;font-weight:700;letter-spacing:.14em;text-transform:uppercase;color:var(--fg-3)}
.sn-card__title{font-size:16px;font-weight:600;line-height:1.3;letter-spacing:-.01em;font-variant-numeric:tabular-nums}
.sn-card__row{display:flex;align-items:center;justify-content:space-between;gap:10px;margin-top:4px}
.sn-card__save{margin:6px 0 0;font-size:12.5px;font-weight:600;line-height:1.35;color:var(--sale)}
.sn-price{font-size:15px;font-weight:600;font-variant-numeric:tabular-nums}
.sn-price s{margin-left:6px;font-weight:500;color:var(--fg-3)}
.sn-price small{font-size:13px;font-weight:500;color:var(--fg-3)}
@media(hover:hover) and (pointer:fine){
  .sn-card:hover .sn-card__media{border-color:var(--line-2)}
  .sn-card:hover .sn-card__media img:first-of-type{transform:scale(1.03)}
  .sn-card:hover .sn-card__media img:first-of-type:not(:only-of-type){opacity:0}
  .sn-card:hover .sn-card__media img+img{opacity:1}
}
@media(hover:none){.sn-card__media img+img{display:none}}
@media(max-width:749px){.sn-card__badge{font-size:10px;padding:5px 9px;top:10px;left:10px}}

/* finish dots and finish picker */
.sn-dots{display:flex;align-items:center}
.sn-dot{width:16px;height:16px;border-radius:50%;border:2px solid var(--bg);margin-left:-5px;box-shadow:inset 0 0 0 1px rgba(255,255,255,.2)}
.sn-dot:first-child{margin-left:0}
.sn-opt{display:grid;gap:10px;border:0;margin:0;padding:0;min-width:0}
.sn-opt legend{padding:0;margin-bottom:10px;font-size:13px;font-weight:600;color:var(--fg-2)}
.sn-opt legend span{color:var(--fg);margin-left:4px}
.sn-opt__list{display:flex;flex-wrap:wrap;gap:8px}
.sn-opt__list input{position:absolute;opacity:0;pointer-events:none}
.sn-opt__list label{display:inline-flex;align-items:center;gap:8px;min-height:42px;padding:0 16px;border-radius:var(--pill);border:1px solid var(--line-2);font-size:14px;font-weight:600;color:var(--fg-2);cursor:pointer;transition:border-color .16s ease,background-color .16s ease,color .16s ease,transform .16s var(--ease)}
.sn-opt__list label:active{transform:scale(.97)}
.sn-opt__list input:checked+label{background:var(--fg);border-color:var(--fg);color:var(--bg)}
.sn-opt__list input:focus-visible+label{outline:2px solid var(--fg);outline-offset:2px}
.sn-opt__list .sn-dot{margin:0;border:0;width:18px;height:18px}
.sn-opt__list label.is-off{opacity:.45;text-decoration:line-through}

/* header */
.sn-ann{background:#000;color:#fff;padding:9px 16px;border-bottom:1px solid rgba(255,255,255,.08);font-size:12px;font-weight:600;letter-spacing:.08em;text-transform:uppercase;white-space:nowrap;overflow:hidden}
.sn-hdr{position:sticky;top:0;z-index:60;padding:12px clamp(12px,2vw,20px)}
.sn-hdr__bar{display:grid;grid-template-columns:auto 1fr auto;align-items:center;gap:16px;max-width:1320px;margin:0 auto;height:60px;padding:0 8px 0 22px;border-radius:var(--pill);background:rgba(20,20,24,.55);border:1px solid rgba(255,255,255,.09);backdrop-filter:blur(14px) saturate(140%);box-shadow:0 10px 30px -10px rgba(0,0,0,.55),0 2px 8px rgba(0,0,0,.25),inset 0 1px rgba(255,255,255,.08)}
.sn-hdr__nav{display:flex;justify-content:center;gap:2px}
.sn-nav__link{display:inline-flex;align-items:center;gap:6px;height:42px;padding:0 15px;border-radius:var(--pill);font-size:15px;font-weight:500;color:var(--fg-2);white-space:nowrap}
.sn-nav__link:hover{color:var(--fg);background:rgba(255,255,255,.06)}
.sn-nav__link[aria-current=page]{color:var(--fg);background:rgba(255,255,255,.10);font-weight:600}
@media(max-width:749px){.sn-hdr__nav{display:none}} /* replaced by a menu button that opens a sheet */

@media(prefers-reduced-motion:reduce){.sn *{transition:none!important;animation:none!important}}
```

Product card markup (the whole card is one link; the second image is optional and cross-fades in on hover):

```html
<a class="sn-card" href="/products/series-10-5x20-et15-5x112">
  <div class="sn-card__media">
    <span class="sn-card__badge">Sale · −10%</span>
    <img src="…_HyperSilver_Side.webp" alt="Series | 10.5x20 ET15 | 5x112" width="900" height="900" loading="lazy"
         srcset="…?width=352 352w, …?width=832 832w, …?width=900 900w" sizes="(min-width: 990px) 25vw, 50vw">
    <img src="…_GlossyBlack_Side.webp" alt="" width="900" height="900" loading="lazy">
  </div>
  <div class="sn-card__body">
    <span class="sn-card__series">Series</span>
    <h3 class="sn-card__title">10.5x20 ET15 · 5x112</h3>
    <div class="sn-card__row">
      <span class="sn-price"><small>from </small>€602.99<s>€669.99</s></span>
      <span class="sn-dots">
        <span class="sn-dot" style="background:linear-gradient(135deg,#3A3A3A,#050505)"></span>
        <span class="sn-dot" style="background:linear-gradient(135deg,#E4E4E4,#A3A3A3)"></span>
      </span>
    </div>
    <p class="sn-card__save">Save up to €318 on a set of 4</p>
  </div>
</a>
```

Other shared pieces:
- **Header:** black announcement bar (short uppercase lines in a marquee, the live promotion underlined) above a floating 60px pill bar: logo about 17px high, centred nav links, then a small glass action button, locale chip, theme toggle, search, account and cart icon buttons. The sticky wrapper is transparent so content scrolls behind the pill. Below 750px the nav becomes a sheet with 52px rows.
- **Footer:** hairline top border; grid of brand block with blurb and social icons (1.4fr), link columns (0.8fr each, 14px links in fg-3, 13px/600 headings) and a newsletter field (1.3fr); then a hairline and a 13px legal row.
- **Icons:** Lucide-style outline, 2px stroke, round caps, 14 to 19px, `currentColor`.
- **Motion:** easing `cubic-bezier(.23,1,.32,1)`; press `scale(.97)` on controls, `.985` on cards; hover image 1.03, tile lifted 2px, arrow nudged 2px; sections fade up 14px over .56s with 60ms staggers.

## 4. Component inventory

| Group | Blocks |
|---|---|
| Layout | wrap, band (alt, tight), grid, split, stack, head |
| Type | eyebrow, h1, h2, h3, lead, copy, fine, crumbs |
| Actions | btn (primary, glass, accent, ghost, sm, block), iconbtn, pill, badge, chip, tabs, qty |
| Navigation | ann, hdr, nav, mega menu, dropdown, mobile sheet, locale, theme toggle, footer |
| Commerce | card, price, dots, opt (finish picker), save banner, gallery, buy box, upsells, cart drawer |
| Collection | coll (sidebar or drawer), filter groups, fpill, select, pager |
| Marketing | hero, slides, marquee, split, tiles, stats, big number, colour switcher, cta, faq, promo tiles, xcards |
| Tools | fitment finder panel, accessory configurator, dealer locator |

## 5. Wheel finishes

Finish names are one CamelCase word with no space (`HyperSilver`, not "Hyper Silver"; `OEM-Silver` is the one hyphenated name). The site publishes no RAL, paint or powder-coat codes; the only colour codes it defines are these on-screen swatches, so present them as UI colours, never as paint references. "Look" is what the official renders show, because the site gives names only.

| Finish | Offered on | Price | Product swatch (135° gradient) | Configurator dot | Look, as rendered |
|---|---|---|---|---|---|
| HyperSilver | FF-ONE, FF-TWO, FF-THREE, EVO-ONE, EVO-TWO | standard | `#E4E4E4` → `#A3A3A3` | `#C9CDD2` | Bright metallic silver, satin sheen, soft highlights |
| GlossyBlack | FF-ONE, FF-TWO, FF-THREE, EVO-ONE, EVO-TWO | standard | `#3A3A3A` → `#050505` | `#111114` | Deep black under high-gloss clear, sharp white edge highlights |
| LiquidMetal | FF-ONE (17 of 21 sizes), FF-THREE (22 of 25), EVO-ONE, EVO-TWO | +€125 per wheel; +€150 on EVO-TWO and the FF-THREE RS5 B10 size | `#E2E6E9` → `#79808A` | `#E4E7EB` | Mirror, chrome-like, hard near-white to near-black reflections |
| PureBronze | FF-THREE (not the RS5 B10 size) | standard | `#B08452` → `#6A4723` | `#8A6A43` | Warm satin metallic bronze |
| ChampagneGold | EVO-TWO | standard | `#E6D3A8` → `#A48655` | none | Pale satin gold centre, bright silver outer lip |
| PureWhite | EVO-ONE | standard | none, falls back to `#9A9A9A` → `#5A5A5A` | none | Solid gloss white, no metallic flake |
| OEM-Silver | OEM+ONE (only finish) | standard | none, falls back to `#9A9A9A` → `#5A5A5A` | none | Bright silver spoke faces, dark grey recesses |

Write a swatch as `background:linear-gradient(135deg,FROM,TO)` on a `.sn-dot`. Give every new finish its own pair rather than relying on the grey fallback.

Further facts:
- On EVO-TWO the outer lip stays bright silver in HyperSilver, GlossyBlack and ChampagneGold; only LiquidMetal is one surface throughout. The inner barrel takes the finish colour.
- LiquidMetal image files are named either `LiquidMetal` or `HyperShine`.
- Forged sets are finished to order (the site says over 20 colours; brushed, polished, matt or gloss; centre and barrel combined freely). Options seen: GlossyBlack, HyperSilver, Brushed, Polished, BlackChrome, RedChrome.
- Accessory dots in the configurator: inlays GlossyBlack `#111114`, HyperSilver `#C9CDD2`, PureBronze `#8A6A43`; screws Stainless `#B9BDC2`, Red `#C8202D`, Gold `#C9A24A`, BlackChrome `#2B2C30`, TitanBlue `linear-gradient(135deg,#C9A24A 0%,#8A5FA6 45%,#3B5FA8 100%)`; GunMetal `#4B4E54`; anything unlisted `#8B9096`.
- Centre caps are two-tone (base / logo ink): Standard `#1A1A1D` / `#BFC3C8`; GlossyBlack `#0D0D0F` / `#CFD3D8`; HyperSilver `#CFD3D8` / `#111111`; GunMetal `#4B4E54` / `#E8E8E8`; GlossyBlack-X-RED `#0D0D0F` / `#D0202C`; Red-X-GlossyBlack `#C8202D` / `#0D0D0F`; GlossyBlack-X-Yellow `#0D0D0F` / `#F2C230`; GlossyBlack-X-BLUE `#0D0D0F` / `#2F6FE0`.
- 67 of 70 wheel pages carry a note that renderings are shown and colours may vary slightly. Keep an equivalent note wherever renders stand in for the product.

## 6. Wheel image set

Catalogue images are CGI renders: one wheel, no tyre, no car, transparent background, square, centred. The page supplies the tile behind them.

| Angle | What it shows | Used for |
|---|---|---|
| **Side** | Upright and almost edge-on: outer barrel fills the left, face in steep perspective on the right. Shows width, lip, concavity. | Default product image, collection card and its hover image, variant image |
| **Hero** | Tipped back and rotated, low three-quarter rear view: barrel in the lower-left foreground, face angled up and right. | Landing-page hero, promo tiles, colour switcher |
| **Front** | Dead-on face view, centred, about 90% of the frame. | Design sections, spec and fitment visuals |
| **Half** | Three-quarter front view, turned roughly 30 to 40 degrees: face plus some inner barrel. | Fitment and certificate sections |
| **Detail** | Macro crop of the spoke-to-rim junction and lip, bleeding off two edges. | Accessories, finish close-ups |

Older files also use `SideRight` (same as Side) and `TopRight` (same as Half). Use the five names above for new work.

**How many:** one image per angle and finish for each size code; products that share a size share the set, so offsets and bolt patterns get no renders of their own. FF-THREE and EVO-TWO: 5 angles × 4 finishes = 20. EVO-ONE: Side, Half, Hero, Detail × 4 = 16. FF-ONE: Side, Hero, Front × 3 = 9. OEM+ONE: 5.

**Naming:** `{SERIES}_{SIZECODE}_{Finish}_{Angle}.webp`, for example `FF-THREE_22115_PureBronze_Hero.webp`. SIZECODE is the diameter then the width without its decimal point (`22115` = 11.5J×22, `2085` = 8.5J×20, `2090` = 9J×20, `2010` = 10J×20); a trailing `B` marks a second barrel version of the same size.

**Files and sizes:**

| Item | Value |
|---|---|
| Master | 2000 to 3000 px square, WebP with alpha (PNG on older sets) |
| Product gallery | served at 1800 px; 1:1 tile, radius 28px, image contained with 5% padding |
| Thumbnails | 240 px source, 84px tiles, 8% padding |
| Collection card | srcset 352w, 832w, 900w; `sizes="(min-width: 990px) 25vw, 50vw"`; 9% padding |
| Tiles and hero stage | up to 2000 px, contained with 4 to 8% padding |
| Alt text | Product title on the main image, empty on the hover image and thumbnails |

**Order and behaviour:** gallery grouped by angle, then finish in option order (Side ×4, Hero ×4, Front ×4, Half ×4, Detail ×4); the gallery shows the first 12. Each finish variant points at its own first-angle image, so choosing a colour swaps the stage. Cards use the first image and cross-fade to the second (same angle, next finish) on hover. Landing pages show the Hero angle in every finish as a cross-fading colour switcher.

**Configurator layers:** the accessory configurator stacks transparent WebP layers per view. Views `front`, `side`, `detail` (labelled Front, Side, Hero). Files `cfg_{model}_{view}_{layer}.webp` at the nearest of 480, 640, 800, 1000, 1200 or 1600 px. Stacking order bottom to top: `base` (wheel in its finish), `mainShadow`, `extraShadow`, `main` (inlay), `extra`, `screwsMain`, `screwsExtra`, `aeroShadow`, `aero`, `cap`.

**Photography:** real photos of wheels on cars are used for full-bleed heroes and slides, series tiles (4:3), blog lead images (16:9) and forged-set galleries.

If the user has no renders yet, tell them the set they need (five angles per finish, transparent, square, 2000 px or more) and build with labelled placeholders rather than borrowing another brand's images.

## 7. Voice

Short, factual, spec-led. Sizes read `10.5x20 ET15 · 5x112` with a middle dot. Savings are stated concretely ("Save up to €318 on a set of 4"). Calls to action are verbs or product names. No hype words and no exclamation marks. State approvals and certificates only when the user has the documents for their market.

## 8. Acceptance checklist

- Canvas `#08080A`, white primary buttons, violet only on the one promoted action and the focus ring.
- Every interactive control is a pill; card tiles 22px, large tiles 28px.
- Selected states invert; nothing selected is violet.
- Product card matches the markup; second image fades in on pointer hover only.
- Prices and sizes use tabular numerals; old price struck through in fg-3.
- Grid is 4 / 3 / 2 columns with no horizontal scroll at 390px.
- Every finish shown has its swatch and its exact name; no paint codes are claimed.
- Wheel images are transparent, contained with padding, and named by the convention.
- Focus-visible outlines on all controls; body text at least 4.5:1.
- Reduced motion disables transitions.
- The user's brand, content and functionality are intact, and nothing reads as another company's site.
