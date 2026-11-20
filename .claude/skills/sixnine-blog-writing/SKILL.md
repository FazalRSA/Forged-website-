---
name: sixnine-blog-writing
description: Write wheel-site blog and news posts in the SIXNINE format - fitment and launch articles with a spec list, short H2 sections, FAQ, SEO title, slug and meta. Use for any wheel blog or SEO article.
---

# SIXNINE blog writing

SIXNINE's news posts are short, structured, spec-led articles built to answer one buyer question ("which wheels fit my car?") and to rank for it. This skill reproduces that format for the user's site. Measured from the live news section on 19 Nov 2026.

**Depends on `sixnine-website`** for tokens, type, buttons and the wheel image angles; load it first when the post also needs to be built as a page. The brand rule from that skill applies: write for the user's brand in fresh words. Follow the shape described here and never reuse SIXNINE's sentences, headlines or photos.

## 1. Collect the facts first

Fitment claims are safety-relevant and buyers act on them, so every specification in a post has to come from the user's data. Ask for anything missing; do not carry numbers over from a similar wheel or car.

| Needed | Example |
|---|---|
| Vehicle, generation code, body styles covered | Audi RS5 B10, Avant and saloon |
| Wheel series and size | FF-THREE 10.5x21 |
| Offset, bolt pattern, centre bore | vehicle-specific ET, 5x112, 66.6 mm |
| Load rating; concavity or lip depth if stated | 850 kg; 110 mm |
| Finishes | exact finish names |
| Tyres and clearance statements the maker stands behind | original tyres can be kept; clears stock height, springs, coilovers |
| Approval documents for the user's market | name them as that market does |
| Offer, price, availability, delivery date | pre-order, 10% off, delivery in March |
| Links | product page, fitment tool, series page |

If the user sells in a market where the maker's approvals do not apply, say what the buyer needs locally instead of repeating foreign approval terms.

## 2. Post types

| Type | Answers | Title shape |
|---|---|---|
| **Vehicle fitment** (the main type) | Which of our wheels fit this car, and what do I need to know? | `{Vehicle} Wheels: {Series} {size} for {body styles} – with {proof}` |
| **Launch or special edition** | What is new, for whom, and how do I get it? | `{Three clipped claims}: {the product} for your {vehicle}` |
| **Explainer** (an extension in the same shape; the reference has none yet) | What does this term mean and why should I care? | `{Term} explained: what it means for your wheels` |

## 3. Article structure

About 600 to 800 words. Many short sections beat a few long ones: a reader should find their answer by scanning the headings.

1. **Back link** to the news index, fine print.
2. **Title** (`h1`, set at the h2 size).
3. **Byline:** `DD.MM.YYYY · {Brand or author}`, fine print.
4. **Lead image,** 16:9, a real photo of the wheel on the car.
5. **Intro,** one paragraph of two or three sentences. Open with the reader's situation as a question or a direct statement, then name the wheel, the size and the single strongest proof.
6. **At a glance** (`h2`): a bullet list of six to nine specs, label in bold then the value. Size, offset, bolt pattern, centre bore, load rating, concavity, finishes, approval, availability.
7. **Six to eight short sections** (`h2` each, one to three sentences, key phrase in bold). For a fitment post, in roughly this order:
   - why this car needs its own size
   - which body styles and variants it fits
   - tyres (what can be reused, which sizes)
   - clearance at stock height and lowered
   - the design feature, with its number
   - customisation or accessories
   - the approval
   - the offer and how to order, ending in a link to the product
8. **FAQ** (`h2` "FAQ: wheels for the {vehicle}"), five to seven `h3` questions phrased the way a buyer would search them, each answered in one or two sentences that repeat the relevant number. The answers may restate facts from above; that repetition is deliberate, because each one has to stand alone in a search result.

Use two more images in the body: one after "At a glance" (render or composite of the wheel on the car) and one detail photo midway. Add four to six internal links: product page, fitment tool, series page, related accessory.

A launch post keeps the same skeleton and swaps the middle sections for: construction, sizes and fitment, approval, finishes and customisation, lead time and how to order.

## 4. Voice

- Second person, direct: "you can keep your original tyres".
- Short sentences. One fact per sentence. Numbers with units.
- Bold the answer inside each section so a skimmer gets it.
- Confident and plain. No hype words, no exclamation marks, no rhetorical build-up.
- Sizes read `10.5x21`, bolt patterns `5x112`, offsets `ET35`, bores and loads with units.
- Only promise what the data supports. "Fits" means the maker or an approval says so.

## 5. Search fields

| Field | Shape | Length |
|---|---|---|
| Title tag | `{Vehicle} Wheels {D} Inch with {proof} | {Brand} {Series} – {Site name}` | under 65 characters before the site name |
| Meta description | `Wheels for the {vehicle} {body styles}: {Brand} {Series} {size}, {load} load rating, with {proof}, {one practical benefit}. {Call to action}.` | 140 to 155 characters |
| Slug | `{vehicle}-wheels-{d}-inch-{series}` in lowercase with hyphens | |
| Image alt | What the image shows, with vehicle and wheel named | one phrase |

Put the vehicle name and the word "wheels" in the title, the first sentence, the FAQ heading and at least two FAQ questions. Do not stuff them elsewhere.

## 6. Page and index styling

Article page: container with `sn-page` padding, content column max 760px, body copy in the long-form font, `h2` and `h3` both 22px so the page stays calm.

```css
.sn-page{padding-top:clamp(40px,6vw,80px);padding-bottom:clamp(64px,8vw,112px)}
.sn-article__title{margin:10px 0 8px}
.sn-article__media{position:relative;aspect-ratio:16/9;margin:24px 0;border-radius:var(--r-lg);overflow:hidden;background:var(--tile)}
.sn-article__media img{position:absolute;inset:0;width:100%;height:100%;object-fit:cover}
.sn-prose{max-width:760px;font-family:var(--font-copy);font-size:16px;line-height:1.7;color:var(--fg-2)}
.sn-prose h2,.sn-prose h3{margin:32px 0 10px;font-family:var(--font);font-size:22px;line-height:1.25;letter-spacing:-.015em;color:var(--fg)}
.sn-prose p+p{margin-top:12px}
.sn-prose strong{color:var(--fg);font-weight:600}
.sn-prose a{text-decoration:underline;text-underline-offset:3px}
.sn-prose ul{list-style:disc;padding-left:20px}
.sn-prose img{width:100%;height:auto;margin:20px 0;border-radius:var(--r-lg)}
```

```html
<div class="sn-wrap sn-page"><article>
  <a class="sn-fine" href="/blog">← News</a>
  <h1 class="sn-h2 sn-article__title">{Title}</h1>
  <p class="sn-fine">19.11.2026 · {Brand}</p>
  <div class="sn-article__media"><img src="…" alt="{what the photo shows}"></div>
  <div class="sn-prose">
    <p>{Intro}</p>
    <h2>The {wheel} for the {vehicle} at a glance</h2>
    <ul><li><strong>Size:</strong> 10.5x21 inch</li></ul>
    <h2>{Section}</h2><p>{One to three sentences.}</p>
    <h2>FAQ: wheels for the {vehicle}</h2>
    <h3>{Question}</h3><p>{Answer}</p>
  </div>
</article></div>
```

News index: page title "News" at the h2 size, then a 3-column grid of cross-link cards (two columns below 990px, one below 750px). Each card is a 4:3 cover photo, the date in fine print, the title as an h3 and a round arrow button; the whole card is the link. Newest first. The card CSS (`sn-xcards`, `sn-xcard`) is in `sixnine-marketing-pages`.

## 7. What to hand back

Return the post in the format the user's site takes (Markdown unless told otherwise), with these parts in order:

```
title:
slug:
date:
meta title:
meta description:
lead image: {brief for the photo + alt text}

{body}

Images needed: {list with where each goes and its alt text}
Facts used: {each number or claim with where it came from}
Open questions: {anything you could not confirm}
```

The last three lists are for the user, not for publishing. "Facts used" lets them check every claim in a minute; "Open questions" is where a missing spec goes instead of into the article as a guess.

## 8. Check before finishing

- Every specification traces to the user's data; nothing is inferred from another wheel or car.
- Approval wording matches what the user actually holds, in their market's terms.
- Length 600 to 800 words; six to eight sections plus FAQ; no section over three sentences.
- "At a glance" list present with bold labels.
- FAQ has five to seven buyer-phrased questions with self-contained answers.
- Title, slug and meta follow section 5 and fit the lengths.
- Three images planned with alt text; four to six internal links.
- No sentence, headline or image taken from another brand's site.
