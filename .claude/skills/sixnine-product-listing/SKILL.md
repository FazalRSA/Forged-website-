---
name: sixnine-product-listing
description: Create or restyle wheel product listings the SIXNINE way - collection grids, filters, product pages, finish pickers, galleries, spec tables, titles, SKUs. Use for any wheel product or collection.
---

# SIXNINE product listings

How SIXNINE structures a wheel in its catalogue and shows it on collection and product pages, so the user's shop can do the same. Measured from the live shop on 19 Nov 2026 (88 products, 413 variants).

**Depends on `sixnine-website`.** Load it first: it holds the tokens (`--bg`, `--fg`, `--line`, `--glass`, `--pill` and so on), the shared CSS (buttons, product card, finish dots, finish picker), the finish swatch codes and the wheel image conventions. If it is not available, say so and ask the user for the design tokens before styling anything. The brand rule from that skill applies here too: this is the user's shop under the user's name, not a copy of SIXNINE's.

## 1. Get the data before writing

A listing is only as good as its specs, and wrong fitment data is a safety problem, so collect these first and ask for anything missing rather than inferring it from a similar wheel.

| Field | Example | Notes |
|---|---|---|
| Series or model name | FF-THREE | Uppercase code style |
| Width and diameter | 11.5J × 22 | |
| Offset | ET20 | Never guess |
| Bolt pattern | 5x132, or dual 5x112/5x120 | Never guess |
| Centre bore | 66.6 mm | Decides centring rings |
| Load rating | 910 kg | |
| Weight | about 14.6 kg | |
| Concavity or lip depth | 109 mm | Only if the maker states it |
| Construction | flow forged, forged, cast | |
| Finishes, each with price | HyperSilver, GlossyBlack, PureBronze, LiquidMetal (+surcharge) | Exact finish names |
| Regular price when on sale | per finish | Discounts can differ by finish |
| Stock state per finish | in stock, low, on request, pre-order with date | |
| Approval documents | certificate, type approval, manual | Only what exists for the user's market |
| Images | five angles per finish | See the image set in `sixnine-website` |

## 2. Catalogue model and naming

One **product** is one size-and-fitment: a width, diameter, offset and bolt pattern. **Finishes are its variants.** Different offsets or bolt patterns of the same size are separate products that share one image set.

| Thing | Pattern | Example |
|---|---|---|
| Product title | `SERIES | {W}x{D} ET{n} | {PCD}` | `FF-THREE | 11.5x22 ET20 | 5x132` |
| Special edition | add a fourth segment | `… | 5x112 | Audi RS5 B10` |
| On-page size line | `{W}x{D} ET{n} · {PCD}` with a middle dot | `11.5x22 ET20 · 5x132` |
| Dual bolt pattern | slash, no spaces | `5x112/5x120` |
| URL handle | lowercase, decimal as hyphen | `ff-three-11-5x22-et20-5x132` |
| Variant title | product title + ` - Finish` | `FF-THREE | 11.5x22 ET20 | 5x132 - HyperSilver` |
| SKU | series letters + diameter + width without the point + `ET` + offset + PCD digits + `-Finish` | `FFTHREE22115ET205132-HyperSilver` |
| Option name | `Colour` | values are the finish names, one CamelCase word each |
| Product type | `Wheels` | accessories are separate products |

## 3. Collection page

Order, top to bottom:

1. Breadcrumb: `Home / Series`, 13px in fg-3.
2. Head: `h1` at the h2 scale with the series name, then a lead paragraph of two to four short sentences: what the wheel is, where it is developed, the size range, the approval, and a pointer to the fitment tool.
3. Two columns: a sticky 272px filter sidebar and the results.
4. Results: product count on the left ("22 Products", fine print), sort select on the right, then a 3-column card grid (2 below 990px), then a pill pager.

**Filters** are collapsible groups with a 15px/600 heading and a chevron, each holding wrapping pills with a count: Price, Wheel model, Rim diameter (`20 inch`), Wheel width (`10.5J`), Bolt pattern, Center bore, Load rating (kg), Offset (ET). A selected pill inverts; a combination with no results is dimmed and not clickable. Below 990px the sidebar becomes a left drawer (width min(420px, 92vw)) with a header and a sticky footer holding reset and apply buttons.

**Sort options:** Featured, Most relevant, Best selling, Alphabetically A-Z and Z-A, Price low to high and high to low, Date old to new and new to old.

**Card rules** (markup and CSS are in `sixnine-website`):
- Image 1 is the default angle in the first finish; image 2 is the same angle in the next finish and cross-fades in on hover. Use the Side angle unless the series leads with another.
- Series label, then the size line as the title.
- Price is the lowest variant price. Prefix `from` only when variants differ in price. Show the regular price struck through when on sale.
- Dots: one per finish, in option order, using each finish's swatch.
- Badge, top-left, one at most: `{Sale name} · −N%`, or `up to −N%` when finishes are discounted differently; otherwise `New` or `Pre-order`. Use the muted badge for neutral notes.
- Sale line under the price: `Save up to {amount} on a set of 4`, where the amount is the largest per-wheel saving among the finishes multiplied by four. Hide it when nothing is on sale.

```css
.sn-crumbs{display:flex;flex-wrap:wrap;gap:8px;margin-bottom:18px;font-size:13px;color:var(--fg-3)}
.sn-coll-head{padding:clamp(48px,7vw,96px) 0 clamp(28px,4vw,40px)}
.sn-coll{display:grid;grid-template-columns:272px minmax(0,1fr);gap:clamp(24px,3vw,44px);align-items:start}
.sn-coll .sn-grid{--cols:3}
.sn-ff{display:grid;gap:4px;align-content:start;position:sticky;top:100px;max-height:calc(100vh - 120px);overflow:auto}
.sn-fg{border-bottom:1px solid var(--line)}
.sn-fg>summary{display:flex;align-items:center;justify-content:space-between;gap:10px;min-height:52px;cursor:pointer;list-style:none;font-size:15px;font-weight:600}
.sn-fg>summary::-webkit-details-marker{display:none}
.sn-fg__body{padding:2px 0 18px}
.sn-fpills{display:flex;flex-wrap:wrap;gap:6px}
.sn-fpill{position:relative;display:inline-flex;align-items:center;gap:8px;min-height:38px;padding:0 14px;border-radius:var(--pill);border:1px solid var(--line-2);font-size:13px;font-weight:600;color:var(--fg-2);cursor:pointer;font-variant-numeric:tabular-nums}
.sn-fpill input{position:absolute;opacity:0;pointer-events:none}
.sn-fpill small{font-size:11px;font-weight:500;opacity:.55}
.sn-fpill:has(input:checked){background:var(--fg);border-color:var(--fg);color:var(--bg)}
.sn-fpill:has(input:focus-visible){outline:2px solid var(--fg);outline-offset:2px}
.sn-fpill.is-off{opacity:.35;pointer-events:none}
.sn-toolbar{display:flex;align-items:center;justify-content:space-between;gap:12px;margin-bottom:20px}
.sn-select select{appearance:none;height:40px;padding:0 40px 0 16px;border-radius:var(--pill);border:1px solid var(--line);background:var(--sunk);color:var(--fg);font:600 14px/1 var(--font);cursor:pointer}
.sn-pager{display:flex;justify-content:center;gap:6px;margin-top:56px}
.sn-pager a,.sn-pager span{display:inline-grid;place-items:center;min-width:44px;height:44px;padding:0 14px;border-radius:var(--pill);font-size:14px;font-weight:600;color:var(--fg-2)}
.sn-pager [aria-current]{background:var(--fg);color:var(--bg)}
@media(max-width:989px){
  .sn-coll{display:block}
  .sn-coll .sn-grid{--cols:2}
  .sn-ff{position:fixed;top:0;left:0;bottom:0;z-index:91;width:min(420px,92vw);max-height:none;padding:0 22px 22px;background:var(--bg-2);border-right:1px solid var(--line);transform:translateX(-102%);transition:transform .26s var(--ease)}
  .sn-coll.is-open .sn-ff{transform:none}
}
```

```html
<details class="sn-fg" open>
  <summary><span>Rim diameter</span></summary>
  <div class="sn-fg__body sn-fpills">
    <label class="sn-fpill"><input type="checkbox" name="diameter" value="20">20 inch <small>13</small></label>
    <label class="sn-fpill"><input type="checkbox" name="diameter" value="21">21 inch <small>6</small></label>
  </div>
</details>
```

## 4. Product page

Two columns, gallery 1.4fr and buy column 1fr, stacking below 990px. Then a details block full width underneath.

**Gallery.** A 1:1 stage (radius 28px, tile background, image contained with 5% padding) with round prev and next buttons and an `n / total` counter, and a row of 84px thumbnails below. Images are ordered by angle, then finish, capped at 12. Choosing a finish jumps the stage to that finish's first image. The reference drives the gallery with hidden radio inputs so it works without JavaScript; a small state hook is fine in React.

**Buy box**, a glass panel, in this order:

1. Eyebrow with the series, then the `h1` size line.
2. Price, with the regular price struck through beside it.
3. Save banner when on sale: a percent pill, "You save {amount} per wheel", and "{amount × quantity} saved on {quantity} pcs".
4. Tax line in fine print with a shipping link (the reference reads "Unit price incl. VAT, plus shipping"). Use the wording that is true for the user's market.
5. Availability: a coloured dot, a main line and a sub line. States: in stock and ready to ship; low stock (the reference flags fewer than 5); on request; pre-order with the delivery month; sold out.
6. Finish picker: legend "Colour:" plus the selected name, then one pill per finish with its dot. Changing it updates price, save banner, availability and gallery.
7. Quantity stepper, **defaulting to 4**, beside a full-width primary "Add to cart" button.
8. Notes with small icons: the approval that comes with the wheel, and a link to the fitment tool ("Will it fit?"). Include only notes that are true for this shop.

Below the box:
- An optional configurator or accessories call-to-action card.
- **Matching accessories** panel ("Required depending on vehicle"): rows with a 56px thumbnail, name, price, a variant select and a small glass "Add" button. Typical rows: centring rings by bore size, wheel bolts and nuts by thread.

**Details block** (max 760px, hairline above, eyebrow "Details"): see the description template in section 5.

```css
.sn-pdp{display:grid;grid-template-columns:minmax(0,1.4fr) minmax(0,1fr);gap:clamp(28px,4vw,64px);align-items:start;padding:clamp(28px,4vw,48px) 0 clamp(64px,8vw,112px)}
@media(max-width:989px){.sn-pdp{grid-template-columns:1fr}}
.sn-gal{display:grid;gap:12px}
.sn-gal__stage{position:relative;aspect-ratio:1/1;border-radius:var(--r-xl);overflow:hidden;background:var(--tile);border:1px solid var(--line)}
.sn-gal__stage figure{position:absolute;inset:0;margin:0;opacity:0;transition:opacity .22s ease-out}
.sn-gal__stage figure.is-on{opacity:1}
.sn-gal__stage img{width:100%;height:100%;object-fit:contain;padding:5%}
.sn-gal__nav{position:absolute;top:50%;z-index:2;width:44px;height:44px;margin-top:-22px;display:grid;place-items:center;border-radius:var(--pill);border:1px solid var(--line);background:rgba(10,10,10,.55);color:#fff;backdrop-filter:blur(8px);cursor:pointer}
.sn-gal__nav--prev{left:12px}
.sn-gal__nav--next{right:12px}
.sn-gal__count{position:absolute;right:12px;bottom:12px;z-index:2;padding:4px 10px;border-radius:var(--pill);background:rgba(10,10,10,.55);color:#fff;font-size:12px;line-height:1.4}
.sn-gal__thumbs{display:flex;gap:10px;overflow-x:auto;scrollbar-width:none;padding:2px}
.sn-gal__thumbs button{flex:none;width:84px;aspect-ratio:1/1;padding:0;border-radius:var(--r-sm);overflow:hidden;background:var(--tile);border:1px solid var(--line);cursor:pointer;opacity:.6}
.sn-gal__thumbs button.is-on{opacity:1;border-color:var(--fg-3)}
.sn-gal__thumbs img{width:100%;height:100%;object-fit:contain;padding:8%}
.sn-buy{display:grid;gap:24px;padding:clamp(24px,3vw,36px)}
.sn-buy__title{font-size:clamp(28px,2.8vw,40px);line-height:1.08;letter-spacing:-.03em;font-variant-numeric:tabular-nums}
.sn-buy__price{display:flex;align-items:baseline;gap:10px;font-size:24px;font-weight:700;font-variant-numeric:tabular-nums}
.sn-buy__price s{font-size:16px;font-weight:500;color:var(--fg-3)}
.sn-buy__tax{margin-top:-18px;font-size:13px;color:var(--fg-3)}
.sn-save{display:flex;align-items:center;gap:12px;padding:12px 14px;border-radius:var(--r-sm);background:var(--glass);border:1px solid var(--line);margin-top:-6px}
.sn-save__pct{flex:none;padding:7px 11px;border-radius:var(--pill);background:var(--fg);color:var(--bg);font-size:15px;font-weight:800;font-variant-numeric:tabular-nums}
.sn-save__txt{display:grid;gap:2px;font-size:14px;line-height:1.35}
.sn-save__txt span{font-size:13px;color:var(--fg-2);font-variant-numeric:tabular-nums}
.sn-avail{display:grid;gap:2px;font-size:14px}
.sn-avail__row{display:flex;align-items:center;gap:8px;font-weight:600}
.sn-avail__dot{width:8px;height:8px;border-radius:50%;background:var(--ok)}
.sn-avail__sub{font-size:13px;color:var(--fg-3)}
.sn-buy__row{display:grid;grid-template-columns:auto minmax(0,1fr);gap:10px}
.sn-qty{display:flex;align-items:center;height:52px;border-radius:var(--pill);border:1px solid var(--line-2)}
.sn-qty button{width:44px;height:100%;border:0;background:transparent;color:var(--fg-2);font-size:18px;cursor:pointer}
.sn-qty input{width:34px;border:0;background:transparent;text-align:center;color:var(--fg);font:600 15px/1 var(--font)}
.sn-notes{display:grid;gap:10px;padding-top:20px;border-top:1px solid var(--line)}
.sn-note{display:flex;align-items:center;gap:12px;font-size:14px;color:var(--fg-2)}
.sn-note a{text-decoration:underline;text-underline-offset:3px}
.sn-ups{display:grid;gap:10px;padding:clamp(18px,2.4vw,24px)}
.sn-ups__item{display:grid;grid-template-columns:56px minmax(0,1fr) auto;gap:14px;align-items:center;padding:8px 0;border-top:1px solid var(--line)}
.sn-desc{max-width:760px;padding:clamp(48px,6vw,80px) 0;border-top:1px solid var(--line)}
.sn-desc h3{margin:28px 0 10px;font-size:22px;letter-spacing:-.015em}
.sn-desc ul{list-style:disc;padding-left:20px}
.sn-desc table{width:100%;border-collapse:collapse;font-variant-numeric:tabular-nums}
.sn-desc td,.sn-desc th{padding:10px 12px 10px 0;border-bottom:1px solid var(--line);text-align:left}
```

```html
<form class="sn-panel sn-buy">
  <div><span class="sn-eyebrow">Series</span><h1 class="sn-buy__title">11.5x22 ET20 · 5x132</h1></div>
  <div class="sn-buy__price">€841.49 <s>€989.99</s></div>
  <div class="sn-save"><span class="sn-save__pct">−15%</span>
    <div class="sn-save__txt"><b>You save €148.50 per wheel</b><span>€594.00 saved on 4 pcs</span></div></div>
  <p class="sn-buy__tax">Unit price incl. VAT, plus shipping · <a href="/shipping">Shipping</a></p>
  <div class="sn-avail"><div class="sn-avail__row"><span class="sn-avail__dot"></span>In stock</div><div class="sn-avail__sub">Ready to ship</div></div>
  <fieldset class="sn-opt"><legend>Colour:<span>HyperSilver</span></legend>
    <div class="sn-opt__list">
      <input type="radio" name="colour" id="c1" value="HyperSilver" checked>
      <label for="c1"><span class="sn-dot" style="background:linear-gradient(135deg,#E4E4E4,#A3A3A3)"></span>HyperSilver</label>
      <input type="radio" name="colour" id="c2" value="GlossyBlack">
      <label for="c2"><span class="sn-dot" style="background:linear-gradient(135deg,#3A3A3A,#050505)"></span>GlossyBlack</label>
    </div></fieldset>
  <div class="sn-buy__row">
    <div class="sn-qty"><button type="button" aria-label="Less">−</button><input type="number" name="quantity" value="4" min="1" aria-label="Quantity"><button type="button" aria-label="More">+</button></div>
    <button class="sn-btn sn-btn--primary sn-btn--block" type="submit">Add to cart</button>
  </div>
  <div class="sn-notes"><p class="sn-note">Including certificate for registration</p><p class="sn-note"><a href="/fitment">Will it fit? Check the fitment tool</a></p></div>
</form>
```

The sizes, radii and paddings above are the reference's. The gallery, availability block and results toolbar are written as plain classes here (the reference uses hidden radio inputs for the gallery and injects the availability widget by script), so wire them to the shop's own state.

## 5. Description template

Write it fresh for the user's wheel in their voice; follow the shape, not SIXNINE's sentences. About 180 to 260 words plus the table.

1. **Headline:** `{Series} {size} ET{n} – {four-to-six-word promise}`.
2. **Intro:** one or two sentences on what the wheel is and who it is for.
3. **Three feature sections**, each a short heading and one to three short sentences. Typical topics: the design idea, the engineering point (concavity, lip depth, weight, construction), and the approval or quality proof.
4. **Technical specifications** table, two columns, in this row order: Wheel size (`11.5Jx22`), Offset (ET) in mm, Load rating in kg, Center bore in mm, Concavity in mm when known, Weight with "≈".
5. **Highlights at a glance:** five bullets, each one line, restating the selling points.
6. **Documents:** links to the user manual and the approval document, if they exist.
7. **Render note** in italics when the images are renders: colours may vary slightly from the real product.

Bold the two or three phrases a skimming buyer should catch. Every number comes from section 1 data.

## 6. Search and sharing

| Element | Pattern from the reference |
|---|---|
| Product page title | `{Brand} {Series} {W}x{D} ET{n} {PCD} | {D} Inch Wheel – {Site name}` |
| Product meta description | `{Brand} {Series} {W}Jx{D} ET{n}, PCD {pcd}: {one-line benefit}. {Approval or fitment prompt}.` About 140 to 150 characters |
| Collection title | `{Brand} {Series} | {Construction} Wheels with {hook} – {Site name}` |
| Collection meta | The collection lead, trimmed to two sentences |
| Image alt | The product title on the main image; empty on hover image and thumbnails |

The reference pages carry no Product structured data. Adding schema.org `Product` with `Offer` per finish (price, currency, availability) is a worthwhile improvement; say it goes beyond the reference when you add it.

## 7. Check before finishing

- Offset, bolt pattern, centre bore and load rating match the source data exactly; nothing was inferred.
- Title, size line, handle and SKU follow section 2.
- Each finish has a variant, a price, a swatch and its own first-angle image.
- Card shows `from` only when prices differ, one badge at most, and the set-of-4 saving only on sale.
- Quantity defaults to 4; the save banner recalculates with quantity and finish.
- Approval, tax and shipping lines are true for the user's market.
- Renders carry the colour note.
- Page works at 390px: filters in a drawer, two-column grid, stacked product page, no horizontal scroll.
