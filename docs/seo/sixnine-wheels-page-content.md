# /sixnine-wheels: dealer content, SEO, AEO and GEO handoff

Target page: https://www.forgedsa.co.za/sixnine-wheels

Status: content and markup drafted, not yet applied. The site code lives in `FazalRSA/Forgedwebsite`, which this session could not attach. Apply the blocks below there.

Every fact in this file is taken from the live page as scraped on 23 Nov 2026 (wheel sizes, bolt patterns, weights, load ratings, finishes, prices, the Germany origin, the stock notes). Anything not on the page is left out. Re-check prices and stock before publishing, because they change.

Brand-use note: the page uses Sixnine's renders from `/images/sixnine/renders/`. Confirm the dealer agreement allows that before the page goes further.

---

## 1. Metadata

| Field | Value |
|---|---|
| `<title>` (58 chars) | Official Sixnine Wheels dealer in South Africa \| FORGED Custom Wheels |
| `meta description` (156 chars) | FORGED Custom Wheels is the official Sixnine Wheels dealer in South Africa. Forged FF-ONE, FF-THREE and EVO sets, with sizes, finishes and Rand prices. |
| `link rel=canonical` | https://www.forgedsa.co.za/sixnine-wheels |
| `og:title` | Official Sixnine Wheels dealer in South Africa \| FORGED Custom Wheels |
| `og:description` | Same as the meta description |
| `og:image` | Use a Sixnine FF-ONE or FF-THREE render at 1200×630 with the logo, not the generic share image |
| `html lang` | en-ZA |

---

## 2. Visible content to add

Place these after the existing "Designed and developed in Germany" section, so the dealer claim is stated near the top and again with detail.

### 2.1 Dealer statement (answer block, the first thing AI engines quote)

> FORGED Custom Wheels is the official dealer for Sixnine Wheels in South Africa. Sixnine is an aftermarket wheel brand from Neumarkt in der Oberpfalz, Germany, sold worldwide. Every Sixnine set FORGED supplies is forged. Sizes, finishes and prices for the sets in stock are listed below, and we confirm fitment for your car before you order.

Why this shape: it names the entity, the country, the category and the fitment step in one paragraph. That is the paragraph an assistant is most likely to lift.

### 2.2 "What makes us the official dealer" (E-E-A-T)

Short facts only, each one checkable:

- We are Sixnine's dealer in South Africa, so the Sixnine sets we sell come through the brand's dealer channel.
- Sixnine designs and develops its wheels in Germany and produces them with one of the largest alloy wheel manufacturers in the world.
- Our range covers six Sixnine designs: FF-ONE, FF-TWO, FF-THREE, EVO-ONE, EVO-TWO and OEM+ONE.
- Our installed cars are shown at /installs.

Do not add years in business, warranty terms, delivery times or fitment guarantees unless the business can document them. The page has none of these today.

### 2.3 Stock table (the "sets in stock" block)

Prices are per set of 4 at the time of writing. Update or remove each row when stock changes.

| Design | Finish | Size | Bolt pattern | Price (per set of 4) |
|---|---|---|---|---|
| FF-ONE | Hyper Silver | 20" / 21" | 5×112 | R 80,000 |
| FF-ONE | Liquid Metal | 20" / 21" | 5×112 | R 95,000 (2 sets in stock) |
| FF-THREE | Pure Bronze | 20" / 21" | 5×112 | R 80,000 |
| FF-THREE | Glossy Black | 20" / 21" | 5×112 | R 80,000 |
| FF-THREE | Liquid Metal | 20" / 21" | 5×112 | R 95,000 (2 sets in stock) |

Note under the table: Stock and prices change. Message us on WhatsApp to confirm what is available before you order.

### 2.4 Range table (AEO and GEO: a table is easy to extract)

| Design | Construction | Sizes | Bolt patterns | Concave | Weight (approx.) | Finishes |
|---|---|---|---|---|---|---|
| FF-ONE | Forged, one-piece with two-piece look | 19–22", 8.5–11.5J | 5×112, 5×114.3, 5×120 | up to 120 mm | 10–12.4 kg | Hyper Silver, Liquid Metal, Glossy Black |
| FF-TWO | Forged | 21", 10–10.5J | 5×112 | not stated | 11.6–11.8 kg | Hyper Silver, Glossy Black |
| FF-THREE | Forged | 20–22", 8.5–11.5J | 5×112, 5×114.3, 5×120, 5×132 | up to 120 mm | 11.1–14.8 kg | Liquid Metal, Glossy Black, Hyper Silver, Pure Bronze |
| EVO-ONE | Forged five-spoke | 18–20", 8.5–11J | 5×100, 5×110, 5×112, 5×114.3, 5×120 | up to 105 mm | 10.2–12.7 kg | Hyper Silver, Glossy Black, Pure White, Liquid Metal |
| EVO-TWO | Forged, one-piece with two-piece look | 20–21", 9–11.5J | 5×112, 5×120 | not stated | not stated | Hyper Silver, Glossy Black, Champagne Gold, Liquid Metal |
| OEM+ONE | Forged | 19", 8.5J | 5×100, 5×112 | 43 mm | about 11.4 kg | OEM Silver |

Load ratings are on the live page per design and can go in the table as a seventh column if the page has room.

Note under the table: Sixnine's figures are Sixnine's own. Confirm fitment before you order.

### 2.5 FF-ONE inlays (a product-specific answer)

FF-ONE and FF-THREE take bolt-on inlays (V-ONE, V-TWO and X-ONE) that change the spoke design without changing the wheel. The AeroRing is an option on FF-ONE. Inlay screws and centre caps come in their own colours. The inlays are parts, not paint, so a new look is a new set of inlays.

### 2.6 Pre-order and special editions (time-bound, keep dated)

- EVO-TWO: on pre-order with Sixnine.
- FF-THREE for Audi RS5 B10 (10.5×21): on pre-order, delivery stated as March 2027. Remove or update the date once it changes.
- FF-TWO Audi RS4/RS5 B9 one-piece forged (10.5×21 ET25): made to order, 8–10 weeks.
- FF-ONE BMW M5 G90/G99 two-piece forged set (11×21 front, 11.5×22 rear, 5×132).

### 2.7 FAQ (visible on the page and mirrored in the JSON-LD in section 3)

**Is FORGED Custom Wheels an official Sixnine Wheels dealer?**
Yes. We are the official Sixnine Wheels dealer in South Africa. Sixnine (Six Nine Wheels GmbH) is based in Neumarkt in der Oberpfalz, Germany.

**Are Sixnine wheels forged?**
Every Sixnine set we supply is forged. Some designs are one-piece forged with a two-piece look (FF-ONE, FF-THREE, EVO-TWO).

**Which Sixnine wheels can I buy from you right now?**
The FF-ONE and FF-THREE sets in stock, in Hyper Silver, Liquid Metal, Glossy Black and Pure Bronze, shown above. Other designs are made to order or on pre-order. Message us for availability.

**Will a Sixnine set fit my car?**
Message us with your car make, model and year. We confirm the size, offset and bolt pattern that fit your car before you order. Sixnine's sizes and bolt patterns are listed in the range table above.

**Which bolt patterns do Sixnine wheels come in?**
Depending on the design: 5×100, 5×110, 5×112, 5×114.3, 5×120 and 5×132. See the range table.

**Do you fit the wheels?**
[Business to confirm. The live page does not state this. Remove the question if fitting is not offered.]

**Can I see Sixnine wheels on real cars?**
Yes. Our fitted cars are shown at /installs.

**Where are Sixnine wheels made?**
Sixnine designs and develops its wheels in Germany and produces them with a global manufacturing partner.

**Can I change the look of an FF-ONE later?**
Yes. The FF-ONE takes swappable inlays (V-ONE, V-TWO, X-ONE) or the AeroRing. A new look is a new set of inlays, not a new set of wheels.

### 2.8 Closing CTA

Heading: Ask us about Sixnine wheels
Button: Enquire on WhatsApp (keep the existing link and pre-filled message, and add the design name to the message)

---

## 3. Structured data (JSON-LD)

Place one `<script type="application/ld+json">` block in the page `<head>` or at the end of `<body>`. Every fact here matches a visible sentence above. Google requires FAQ markup to match what is visible on the page.

```json
{
  "@context": "https://schema.org",
  "@graph": [
    {
      "@type": "WebPage",
      "@id": "https://www.forgedsa.co.za/sixnine-wheels#webpage",
      "url": "https://www.forgedsa.co.za/sixnine-wheels",
      "name": "Official Sixnine Wheels dealer in South Africa | FORGED Custom Wheels",
      "description": "FORGED Custom Wheels is the official Sixnine Wheels dealer in South Africa. Forged FF-ONE, FF-THREE and EVO sets, with sizes, finishes and Rand prices.",
      "inLanguage": "en-ZA",
      "isPartOf": { "@id": "https://www.forgedsa.co.za/#website" },
      "about": { "@id": "https://www.forgedsa.co.za/sixnine-wheels#brand" },
      "breadcrumb": { "@id": "https://www.forgedsa.co.za/sixnine-wheels#breadcrumb" }
    },
    {
      "@type": "BreadcrumbList",
      "@id": "https://www.forgedsa.co.za/sixnine-wheels#breadcrumb",
      "itemListElement": [
        { "@type": "ListItem", "position": 1, "name": "Home", "item": "https://www.forgedsa.co.za/" },
        { "@type": "ListItem", "position": 2, "name": "Sixnine Wheels", "item": "https://www.forgedsa.co.za/sixnine-wheels" }
      ]
    },
    {
      "@type": "Brand",
      "@id": "https://www.forgedsa.co.za/sixnine-wheels#brand",
      "name": "Sixnine Wheels",
      "alternateName": "Six Nine Wheels",
      "url": "https://sixnine-wheels.com",
      "description": "Aftermarket wheel brand from Neumarkt in der Oberpfalz, Germany, sold worldwide.",
      "logo": "https://www.forgedsa.co.za/images/partners/sixnine.webp"
    },
    {
      "@type": "Organization",
      "@id": "https://www.forgedsa.co.za/#organization",
      "name": "FORGED Custom Wheels",
      "url": "https://www.forgedsa.co.za/",
      "logo": "https://www.forgedsa.co.za/images/partners/sixnine.webp",
      "areaServed": { "@type": "Country", "name": "South Africa" },
      "knowsAbout": ["Sixnine Wheels", "Forged alloy wheels", "BMW M wheels"],
      "hasOfferCatalog": {
        "@type": "OfferCatalog",
        "name": "Sixnine Wheels",
        "itemListElement": [
          { "@type": "Offer", "itemOffered": { "@type": "Product", "name": "Sixnine FF-ONE", "brand": { "@id": "https://www.forgedsa.co.za/sixnine-wheels#brand" } } },
          { "@type": "Offer", "itemOffered": { "@type": "Product", "name": "Sixnine FF-TWO", "brand": { "@id": "https://www.forgedsa.co.za/sixnine-wheels#brand" } } },
          { "@type": "Offer", "itemOffered": { "@type": "Product", "name": "Sixnine FF-THREE", "brand": { "@id": "https://www.forgedsa.co.za/sixnine-wheels#brand" } } },
          { "@type": "Offer", "itemOffered": { "@type": "Product", "name": "Sixnine EVO-ONE", "brand": { "@id": "https://www.forgedsa.co.za/sixnine-wheels#brand" } } },
          { "@type": "Offer", "itemOffered": { "@type": "Product", "name": "Sixnine EVO-TWO", "brand": { "@id": "https://www.forgedsa.co.za/sixnine-wheels#brand" } } },
          { "@type": "Offer", "itemOffered": { "@type": "Product", "name": "Sixnine OEM+ONE", "brand": { "@id": "https://www.forgedsa.co.za/sixnine-wheels#brand" } } }
        ]
      }
    },
    {
      "@type": "FAQPage",
      "@id": "https://www.forgedsa.co.za/sixnine-wheels#faq",
      "mainEntity": [
        {
          "@type": "Question",
          "name": "Is FORGED Custom Wheels an official Sixnine Wheels dealer?",
          "acceptedAnswer": { "@type": "Answer", "text": "Yes. We are the official Sixnine Wheels dealer in South Africa. Sixnine (Six Nine Wheels GmbH) is based in Neumarkt in der Oberpfalz, Germany." }
        },
        {
          "@type": "Question",
          "name": "Are Sixnine wheels forged?",
          "acceptedAnswer": { "@type": "Answer", "text": "Every Sixnine set we supply is forged. Some designs are one-piece forged with a two-piece look (FF-ONE, FF-THREE, EVO-TWO)." }
        },
        {
          "@type": "Question",
          "name": "Which Sixnine wheels can I buy from you right now?",
          "acceptedAnswer": { "@type": "Answer", "text": "The FF-ONE and FF-THREE sets in stock, in Hyper Silver, Liquid Metal, Glossy Black and Pure Bronze, shown on the page. Other designs are made to order or on pre-order. Message us for availability." }
        },
        {
          "@type": "Question",
          "name": "Will a Sixnine set fit my car?",
          "acceptedAnswer": { "@type": "Answer", "text": "Message us with your car make, model and year. We confirm the size, offset and bolt pattern that fit your car before you order." }
        },
        {
          "@type": "Question",
          "name": "Which bolt patterns do Sixnine wheels come in?",
          "acceptedAnswer": { "@type": "Answer", "text": "Depending on the design: 5x100, 5x110, 5x112, 5x114.3, 5x120 and 5x132." }
        },
        {
          "@type": "Question",
          "name": "Can I see Sixnine wheels on real cars?",
          "acceptedAnswer": { "@type": "Answer", "text": "Yes. Our fitted cars are shown at forgedsa.co.za/installs." }
        },
        {
          "@type": "Question",
          "name": "Where are Sixnine wheels made?",
          "acceptedAnswer": { "@type": "Answer", "text": "Sixnine designs and develops its wheels in Germany and produces them with a global manufacturing partner." }
        },
        {
          "@type": "Question",
          "name": "Can I change the look of an FF-ONE later?",
          "acceptedAnswer": { "@type": "Answer", "text": "Yes. The FF-ONE takes swappable inlays (V-ONE, V-TWO, X-ONE) or the AeroRing. A new look is a new set of inlays, not a new set of wheels." }
        }
      ]
    }
  ]
}
```

Notes on the markup:
- The "Do you fit the wheels?" question is left out of the JSON-LD on purpose. Add it only once the business confirms the answer, in both the visible text and the markup.
- Product-level `Offer` with `price` and `priceCurrency: "ZAR"` is not included. Prices and stock change often, and stale structured prices are worse than none. If you want them, generate them from the same data source that drives the stock cards, and set `availability` from live stock.
- No address, phone or opening hours are included, because the live page does not state them. Add a `LocalBusiness` block with the real details if the business has a physical location.

---

## 4. Technical SEO checklist

- One `<h1>`: "Official Sixnine Wheels dealer". Keep it to the current wording.
- Headings in order: h2 for "Designed and developed in Germany", "Sixnine sets in stock", "The Sixnine range", "Ask us about Sixnine wheels". h3 for each design.
- Alt text: "Sixnine FF-ONE forged wheel in Hyper Silver, front view, FORGED Custom Wheels". Describe the finish and the angle. Do not write "image" or "photo".
- Image sizes: keep `width` and `height` set, `loading="lazy"` below the fold, and use WebP as the site already does.
- Internal links: link from the homepage, the nav and each design page back to `/sixnine-wheels`. Use the anchor text "Sixnine wheels dealer" or "Sixnine FF-ONE in South Africa", not "click here".
- Sitemap: confirm `/sixnine-wheels` is in `sitemap.xml` with a current `lastmod`.
- Indexing: request indexing in Google Search Console after the change goes live.
- Check the page at 390 px, 900 px and 1440 px for overflow. Check the stock table on phone widths.

---

## 5. GEO and AEO (answer engines and AI assistants)

- **llms.txt:** add a line to the site's `llms.txt` (the site already generates one):
  `- [Sixnine Wheels dealer in South Africa](https://www.forgedsa.co.za/sixnine-wheels): official South African dealer for Sixnine forged wheels. Range table, sizes, bolt patterns, finishes, stock and FAQ.`
- **Write answers, not slogans.** Every section above starts with a direct answer to a question someone would type: who sells Sixnine in South Africa, is it forged, which bolt patterns, will it fit my car.
- **Keep entity names consistent** everywhere on the site: "Sixnine Wheels" (brand), "Six Nine Wheels GmbH" (company, only where the legal name is needed), "FORGED Custom Wheels" (dealer). Use the same design names as the range table.
- **Dates and status:** keep pre-order and stock notes dated, so an assistant does not quote an old status as current.
- **Attribution:** keep the line that the figures are Sixnine's own, so claims are not read as the dealer's.
- **Reviews:** a Google Business Profile for the dealer, with the same name, is the strongest local signal. Check that it exists and says "Sixnine Wheels dealer" in its description.

---

## 6. Open questions for the business

1. Do you fit the wheels, or only supply them? (drives the FAQ and the local SEO)
2. Is there a physical showroom or address to add as LocalBusiness?
3. Does the dealer agreement allow the Sixnine renders and the Germany and company details on the page?
4. Is the FF-THREE RS5 B10 delivery date of March 2027 still current?
5. What is the lead time on made-to-order sets, and does the page need that stated?
