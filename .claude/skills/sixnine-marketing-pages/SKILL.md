---
name: sixnine-marketing-pages
description: Build SIXNINE-style marketing pages - homepage, series landing, pre-order and sale campaigns, About. Covers section order, hero, CTA, FAQ, copy. Use for any wheel-site landing or campaign page.
---

# SIXNINE marketing pages

How SIXNINE assembles its homepage, series landing pages, campaign pages and About page, as a section library plus page recipes. Measured from the live site on 19 Nov 2026.

**Depends on `sixnine-website`.** Load it first for the tokens, buttons, pills, badges, product card, finish dots and swatch codes, and the wheel image angles. The brand rule from that skill applies: these pages carry the user's brand, photos and words. Follow the structure and rhythm here; write every sentence fresh.

## 1. How a page is built

A marketing page is a stack of full-width **bands**. Each band has one job and one idea. Bands alternate between the page background and the slightly lighter `--bg-2` (`sn-band--alt`) so the page reads as chapters. Inside a band, content sits in the 1320px container and usually opens with a **head**: an eyebrow of one or two words, then an h2 of six words or fewer.

Pick a recipe, fill it with the user's real facts, then cut any band you cannot fill with something true. A shorter honest page beats a padded one.

## 2. Page recipes

### Series or model landing page

1. **Hero, centred with stage:** pill, h1, one-sentence lead, two buttons, a row of three or four key facts, then a wide stage holding the Hero-angle render.
2. **Outline marquee** repeating the model name.
3. **Split: design.** Front-angle render beside eyebrow, h2 and two or three sentences.
4. **Split, reversed, on alt band: engineering point.** Side-angle render, with one **big number** under the copy (for example a lip depth in mm with a one-line caption).
5. **Numbered tiles:** three benefits, numbered 01 to 03, each a short h3 and one line.
6. **Colour switcher** on alt band: the Hero angle in every finish, cross-fading, with the finish picker beside it and one line on any surcharge.
7. **Split, reversed: accessories or detail.** Detail-angle render.
8. **Split: approval and fitment.** Half-angle render, typical vehicles in a sentence, a glass button to the fitment tool.
9. **CTA box** (accent version for a live campaign): big number, eyebrow, h2, one sentence, primary button to the collection.
10. **FAQ** on alt band: five or six questions.

A series page for an established model swaps in: a full-bleed photo hero, a configurator teaser, a four-item **stats** row, a development split, and an **All sizes** product grid with bolt-pattern tabs before the closing CTA.

### Homepage

1. **Slider** of full-bleed slides: up to two badges top-left, a pill, an h1-scale headline of at most 14 characters per line, one or two buttons. A counter ("1 / 7") and two arrow buttons sit under it.
2. **Outline marquee.**
3. **"New" head plus promo tiles:** a 2/3 tile and a 1/3 tile, each a render on a tile with an overlaid title, one line and an arrow.
4. **Tool band:** the fitment finder panel (vehicle selects, then approved sizes).
5. **Configurator teaser** on alt band, if the shop has one.
6. **"Series" head plus tiles** linking to every series.
7. **About split** with a glass "Learn more" button.
8. Footer with newsletter.

### Campaign page (pre-order, sale)

Hero with an accent pill stating the offer or delivery date and an accent primary button; the offer restated in an accent CTA box with the discount as the big number; an FAQ that answers delivery date, whether the discount covers every finish, and what happens to combined offers; a grid of the products in the offer. State the saving concretely and say when no code is needed.

### About page

Plain hero (pill "About us", h1, one-sentence lead), marquee, two alternating splits with real photos (who we are, who we work with), a "Discover the series" head over a 3-column grid of cross-link cards, a closing CTA.

## 3. Which image goes where

| Slot | Image |
|---|---|
| Landing hero stage, promo tiles, colour switcher | **Hero** angle render |
| Design or styling split | **Front** angle |
| Depth, lip, concavity split | **Side** angle |
| Accessories, hardware, finish close-up | **Detail** angle |
| Approval and fitment split | **Half** angle |
| Homepage slides, full-bleed heroes, About splits, series tiles | Real photography of the wheel on a car |

Renders are transparent and sit *contained* on the tile background with padding; photos *cover* their frame. Never put text straight on a photo without the bottom gradient.

## 4. Copy patterns

Write new copy to these shapes. Short declaratives, numbers over adjectives, no exclamation marks.

| Element | Shape | Example (invented) |
|---|---|---|
| Pill above h1 | 2 to 5 words, the offer or the claim | `Delivery March` |
| Hero h1 | Name, then one or two clipped phrases, each ending in a full stop | `APEX-ONE. Seven spokes. Zero compromise.` |
| Lead | One sentence, under 20 words | |
| Hero facts | 3 or 4 items, number in bold then a noun | **8** sizes · **20″ and 21″** · **5x112** bolt pattern |
| Eyebrow | 1 or 2 words naming the chapter | `Design`, `Engineering`, `Colours`, `FAQ` |
| h2 | 6 words or fewer, statement not question | `Two-piece look. One-piece strength.` |
| Section copy | 1 to 3 short sentences | |
| Numbered tile | h3 of 2 or 3 words plus one line | `No seals` / `Nothing to age or replace.` |
| Stat | Big number plus a 2 or 3 word label | `18` / `different sizes` |
| CTA | Big number, eyebrow, imperative h2, one sentence, one button | `−10 %` / `Pre-order now` |
| Buttons | Verb phrase or destination | `Sizes & prices`, `Check fitment`, `Configure now` |
| FAQ | Real buyer questions, answers of 1 or 2 sentences with the number in them | |

Claim an approval, certificate or test only when the user has it for their market, and name it the way that market does.

## 5. Section library

```css
/* hero */
.sn-hero{position:relative;overflow:hidden;padding:clamp(56px,8vw,112px) 0 clamp(40px,6vw,80px);text-align:center}
.sn-hero__inner{position:relative;display:grid;gap:22px;justify-items:center}
.sn-hero__meta{display:flex;flex-wrap:wrap;justify-content:center;gap:10px 28px;margin-top:8px;font-size:14px;color:var(--fg-3)}
.sn-hero__meta b{color:var(--fg);font-weight:600}
.sn-hero__stage{position:relative;margin-top:clamp(28px,4vw,56px);aspect-ratio:16/8;border-radius:var(--r-xl);overflow:hidden;background:var(--tile);border:1px solid var(--line)}
.sn-hero__stage>img{position:absolute;inset:0;width:100%;height:100%;object-fit:contain;padding:4% 8%}
.sn-hero--full{text-align:left;min-height:min(88vh,900px);display:grid;align-items:end;padding:0;color:#fff}
.sn-hero--full .sn-hero__bg{position:absolute;inset:0}
.sn-hero--full .sn-hero__bg img{width:100%;height:100%;object-fit:cover}
.sn-hero--full::after{content:"";position:absolute;inset:0;background:linear-gradient(to top,rgba(8,8,10,.92),rgba(8,8,10,.4) 45%,rgba(8,8,10,0) 75%)}
.sn-hero--full .sn-hero__inner{z-index:2;justify-items:start;padding-bottom:clamp(48px,7vw,96px);padding-top:120px}
.sn-glow{position:absolute;inset:0;pointer-events:none;background:radial-gradient(60% 50% at 50% 0%,var(--glow) 0%,transparent 70%)}
.sn-actions{display:flex;flex-wrap:wrap;gap:10px}

/* homepage slides */
.sn-slide{position:relative;display:grid;align-items:end;min-height:min(80vh,820px);border-radius:var(--r-xl);overflow:hidden;isolation:isolate;color:#fff}
.sn-slide__bg{position:absolute;inset:0;z-index:-1}
.sn-slide__bg img{width:100%;height:100%;object-fit:cover}
.sn-slide::after{content:"";position:absolute;inset:0;z-index:-1;background:linear-gradient(to top,rgba(8,8,10,.85),rgba(8,8,10,.25) 50%,rgba(8,8,10,0) 75%)}
.sn-slide__badges{position:absolute;top:clamp(16px,2.4vw,28px);left:clamp(16px,2.4vw,28px);z-index:2;display:flex;flex-wrap:wrap;gap:8px}
.sn-slide__body{display:grid;gap:20px;justify-items:start;padding:clamp(28px,5vw,72px)}
.sn-slide .sn-h1{max-width:14ch}
@media(min-width:750px){.sn-slide{min-height:0;aspect-ratio:3/1}}
@media(max-width:749px){.sn-slide{min-height:0;aspect-ratio:4/5}.sn-slide .sn-h1{font-size:clamp(34px,9vw,48px)}.sn-slide__body{padding:22px}}

/* outline marquee: duplicate the group once so the loop is seamless */
.sn-mq{overflow:hidden;padding:clamp(18px,3vw,36px) 0;border-top:1px solid var(--line);border-bottom:1px solid var(--line)}
.sn-mq__track{display:flex;width:max-content;animation:sn-mq 40s linear infinite}
.sn-mq__group{display:flex;flex:none;align-items:center}
.sn-mq__item,.sn-mq__sep{flex:none;padding:0 .4em;font-weight:700;line-height:1;letter-spacing:-.03em;white-space:nowrap;text-transform:uppercase;font-size:clamp(56px,10vw,140px)}
.sn-mq__item{color:transparent;-webkit-text-stroke:1px var(--fg-2)}
.sn-mq__sep{color:var(--fg-3)}
@media(hover:hover) and (pointer:fine){.sn-mq:hover .sn-mq__track{animation-play-state:paused}}
@keyframes sn-mq{from{transform:translateX(0)}to{transform:translateX(-50%)}}

/* split */
.sn-split{display:grid;grid-template-columns:minmax(0,1.15fr) minmax(0,1fr);gap:clamp(36px,6vw,96px);align-items:center}
.sn-split--rev>:first-child{order:2}
.sn-stack{display:grid;gap:20px;align-content:center;justify-items:start}
.sn-media{position:relative;overflow:hidden;border-radius:var(--r-lg);background:var(--tile);aspect-ratio:4/3}
.sn-media--square{aspect-ratio:1/1}
.sn-media>img{position:absolute;inset:0;width:100%;height:100%;object-fit:cover}
.sn-media--contain>img{object-fit:contain;padding:6%}
.sn-big{display:grid;gap:6px}
.sn-big__v{font-size:clamp(88px,12vw,180px);font-weight:700;line-height:.86;letter-spacing:-.055em;font-variant-numeric:tabular-nums}

/* numbered tiles and stats */
.sn-tiles{display:grid;grid-template-columns:repeat(3,minmax(0,1fr));gap:clamp(12px,1.6vw,20px)}
.sn-tile{display:grid;gap:12px;align-content:start;padding:clamp(24px,3vw,36px);border-radius:var(--r-lg);background:var(--glass);border:1px solid var(--line);box-shadow:var(--hl)}
.sn-tile__n{font-size:13px;font-weight:700;letter-spacing:.1em;color:var(--fg-3);font-variant-numeric:tabular-nums}
.sn-tile p{font-size:15px;line-height:1.6;color:var(--fg-2)}
.sn-stats{display:grid;grid-template-columns:repeat(4,minmax(0,1fr));gap:1px;border-radius:var(--r-lg);overflow:hidden;background:var(--line);border:1px solid var(--line)}
.sn-stat{display:grid;gap:8px;align-content:start;padding:clamp(24px,3vw,36px);background:var(--bg)}
.sn-stat__v{font-size:clamp(40px,5vw,68px);font-weight:700;line-height:.95;letter-spacing:-.045em;font-variant-numeric:tabular-nums}
.sn-stat__l{font-size:14px;line-height:1.4;color:var(--fg-3)}

/* colour switcher */
.sn-cfg{display:grid;grid-template-columns:minmax(0,1.2fr) minmax(0,1fr);gap:clamp(28px,5vw,80px);align-items:center}
.sn-cfg__stage{position:relative;aspect-ratio:1/1;border-radius:var(--r-xl);overflow:hidden;background:var(--tile);border:1px solid var(--line)}
.sn-cfg__stage>figure{position:absolute;inset:0;margin:0;opacity:0;transform:scale(.985);transition:opacity .22s ease-out,transform .28s var(--ease)}
.sn-cfg__stage>figure.is-on{opacity:1;transform:none}
.sn-cfg__stage img{width:100%;height:100%;object-fit:contain;padding:7%}

/* call to action */
.sn-cta{position:relative;overflow:hidden;display:grid;grid-template-columns:minmax(0,1fr) auto;align-items:center;gap:32px;padding:clamp(32px,5vw,64px);border-radius:var(--r-xl);background:var(--glass);border:1px solid var(--line);box-shadow:var(--hl)}
.sn-cta--accent{background:var(--violet);border-color:transparent;color:#fff}
.sn-cta--accent .sn-eyebrow,.sn-cta--accent .sn-copy{color:rgba(255,255,255,.82)}
.sn-cta__big{font-size:clamp(72px,10vw,150px);font-weight:700;line-height:.85;letter-spacing:-.055em}

/* faq */
.sn-faq{max-width:860px;border-top:1px solid var(--line)}
.sn-faq details{border-bottom:1px solid var(--line)}
.sn-faq summary{display:flex;align-items:center;justify-content:space-between;gap:24px;min-height:72px;padding:18px 0;list-style:none;cursor:pointer;font-size:18px;font-weight:600;letter-spacing:-.012em}
.sn-faq summary::-webkit-details-marker{display:none}
.sn-faq summary span{display:grid;place-items:center;flex:none;width:34px;height:34px;border-radius:50%;background:var(--glass-2);transition:transform .2s var(--ease)}
.sn-faq details[open] summary span{transform:rotate(45deg)}
.sn-faq__a{padding:0 56px 24px 0;font-family:var(--font-copy);font-size:15px;line-height:1.7;color:var(--fg-2)}

/* promo tiles and cross-link cards */
.sn-tilegrid{--g:clamp(12px,1.6vw,20px);display:flex;flex-wrap:wrap;gap:var(--g)}
.sn-tile2{position:relative;flex:1 1 calc(50% - var(--g));min-width:0;display:flex;flex-direction:column;border-radius:var(--r-xl);overflow:hidden;background:var(--glass);transition:transform .2s var(--ease)}
.sn-w-2-3{flex-basis:calc(66.666% - var(--g))}
.sn-w-1-3{flex-basis:calc(33.333% - var(--g))}
.sn-tile2__media{position:relative;flex:1 0 auto;overflow:hidden;background:var(--tile);aspect-ratio:16/9}
.sn-tile2__media img{position:absolute;inset:0;width:100%;height:100%;object-fit:contain;padding:7%}
.sn-tile2__over{position:absolute;inset:auto 0 0 0;z-index:2;display:flex;align-items:flex-end;justify-content:space-between;gap:16px;padding:clamp(18px,3vw,32px);background:linear-gradient(to top,rgba(8,8,10,.82) 0%,rgba(8,8,10,.35) 60%,transparent 100%);color:#fff}
.sn-tile2__over .sn-h3{font-size:clamp(22px,2.4vw,34px)}
.sn-tile2__over p{margin-top:8px;font-size:14px;color:rgba(255,255,255,.75)}
.sn-xcards{display:grid;grid-template-columns:repeat(3,minmax(0,1fr));gap:clamp(12px,1.6vw,20px)}
.sn-xcard{display:grid;grid-template-rows:auto auto;border-radius:var(--r-xl);overflow:hidden;background:var(--glass);border:1px solid var(--line);box-shadow:var(--hl);transition:border-color .2s ease,transform .2s var(--ease)}
.sn-xcard__media{position:relative;aspect-ratio:4/3;overflow:hidden;background:var(--tile)}
.sn-xcard__media img{position:absolute;inset:0;width:100%;height:100%;object-fit:cover}
.sn-xcard__body{display:flex;align-items:center;justify-content:space-between;gap:16px;padding:20px 22px}
.sn-xcard__go{display:grid;place-items:center;flex:none;width:42px;height:42px;border-radius:50%;background:var(--glass-2)}
@media(hover:hover) and (pointer:fine){
  .sn-tile2:hover,.sn-xcard:hover{transform:translateY(-2px)}
  .sn-xcard:hover{border-color:var(--line-2)}
  .sn-xcard:hover .sn-xcard__go,.sn-tile2:hover .sn-xcard__go{background:#fff;color:#000}
}

/* scroll reveal: a script adds .js to <html>, then .is-in as each element enters the viewport (content stays visible without JS); stagger with --delay in 60ms steps */
.js .sn-reveal:not(.is-in){opacity:0}
.sn-reveal.is-in{animation:sn-reveal .56s var(--ease) var(--delay,0ms) backwards}
@keyframes sn-reveal{from{opacity:0;translate:0 14px}to{opacity:1;translate:none}}

@media(max-width:989px){
  .sn-split,.sn-cfg,.sn-cta{grid-template-columns:1fr}
  .sn-split--rev>:first-child{order:0}
  .sn-tiles{grid-template-columns:1fr}
  .sn-xcards{grid-template-columns:repeat(2,minmax(0,1fr))}
  .sn-stats{grid-template-columns:repeat(auto-fit,minmax(180px,1fr))}
  .sn-hero__stage{aspect-ratio:4/3}
}
@media(max-width:749px){.sn-tile2{flex-basis:100%}.sn-xcards{grid-template-columns:1fr}.sn-faq__a{padding-right:0}}
```

Markup for the three patterns used most:

```html
<!-- centred hero with stage -->
<section class="sn-hero"><div class="sn-glow"></div><div class="sn-wrap">
  <div class="sn-hero__inner">
    <span class="sn-pill sn-pill--accent">Delivery March</span>
    <h1 class="sn-h1">APEX-ONE. Seven spokes. Zero compromise.</h1>
    <p class="sn-lead">One sentence on what it is and why it matters.</p>
    <div class="sn-actions"><a class="sn-btn sn-btn--accent" href="#">Pre-order now</a><a class="sn-btn sn-btn--glass" href="#">Sizes &amp; prices</a></div>
    <div class="sn-hero__meta"><span><b>8</b> sizes</span><span><b>20″ and 21″</b></span><span><b>5x112</b> bolt pattern</span></div>
  </div>
  <div class="sn-hero__stage"><img src="…_Hero.webp" alt="APEX-ONE"></div>
</div></section>

<!-- split section -->
<section class="sn-band"><div class="sn-wrap"><div class="sn-split">
  <div class="sn-media sn-media--square sn-media--contain sn-reveal"><img src="…_Front.webp" alt="The seven-spoke face"></div>
  <div class="sn-stack sn-reveal">
    <span class="sn-eyebrow">Design</span>
    <h2 class="sn-h2">Seven spokes, one line</h2>
    <div class="sn-copy"><p>Two or three short sentences.</p></div>
  </div>
</div></div></section>

<!-- accent call to action -->
<section class="sn-band sn-band--tight"><div class="sn-wrap"><div class="sn-cta sn-cta--accent">
  <div class="sn-stack"><span class="sn-cta__big">−10 %</span><span class="sn-eyebrow">Pre-order campaign</span>
    <h2 class="sn-h2">Pre-order now</h2><p class="sn-copy">One sentence with the offer and the delivery date.</p></div>
  <a class="sn-btn sn-btn--primary" href="#">View the collection</a>
</div></div></section>
```

Notes on behaviour:
- Full-bleed heroes and slides always use white text over the dark gradient, in light mode too.
- On an accent CTA the button is the white primary, never a second violet.
- The colour switcher shows one `figure.is-on` at a time; the finish picker from `sixnine-website` toggles it and the label beside it reads "Colour" plus the finish name.
- Image alt text on marketing sections is the section heading.
- FAQ items are `details` elements; the plus icon in the summary rotates 45 degrees when open.

## 6. Check before finishing

- Every band has one idea, a head, and nothing invented to fill space.
- Bands alternate background; no two accent elements in one view.
- Each image slot uses the angle from section 3, renders contained and photos covered.
- h1 follows the clipped pattern; h2s are six words or fewer; no exclamation marks.
- Every number and approval on the page comes from the user's data.
- There is one primary action per band and the page ends with a CTA and an FAQ.
- At 390px splits stack with the image first, tiles go to one column, and the marquee does not cause horizontal scroll.
- Reduced motion stops the marquee and the reveals.
