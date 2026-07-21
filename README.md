# Badge-A-Minit Redesign — Local Prototype

Open `index.html` in a browser and click through. All navigation that has
a built page (header dropdown, hero, bento grid, category explorer,
best-sellers tabs, sidebars, breadcrumbs, comparison guides, cross-sell,
footer) now links to the matching local file in this folder instead of
the live site.

Any link to a page **not yet built** (e.g. Button Badge Components,
Reusable/Framed Name Badges, the two Button Badge Machine subpages,
individual PVC/Aluminium/Stainless Steel Plaque pages) still points to
the real **badge-a-minit.com.au** — clicking it leaves the prototype and
opens the live site. That's intentional: better a working fallback than
a dead link.

## Site map

**Home**
- `index.html`

**Depth 1 categories**
- `category-name-badges.html` — Custom & Personalised Name Badges
- `category-lapel-pins.html` — Lapel Pins
- `category-button-badges.html` — Custom Button Badges
- `category-button-badge-machines.html` — Button Badge Machines
- `category-id-cards.html` — ID Cards / Event Badges
- `category-lanyards.html` — Lanyards
- `category-desk-name-plates.html` — Desk Name Plates
- `category-plaques.html` — Plaques (new consolidated hub over PVC/Aluminium/Stainless Steel)
- `category-luggage-tags.html` — Luggage Tags
- `category-badge-accessories.html` — Badge Accessories
- `category-button-badge-accessories.html` — Button Badge Accessories
- `category-button-badge-die-cutting-tools.html` — Button Badge Die Cutting Tools
- `category-button-badge-interchangeable-dies.html` — Button Badge Interchangeable Dies

**Depth 2 subcategories** (all under Name Badges)
- `category-full-colour-name-badges.html`
- `category-engraved-name-badges.html`
- `category-chalkboard-name-badges.html`
- `category-engraved-wood-name-badges.html`

**Product page (depth 3, example)**
- `product-polyester-lanyard.html` — Heritage Modern colour scheme applied to the client-supplied PDP template

## Not yet built (links fall through to the live site)
- Button Badge Components (depth 1)
- Reusable Name Badges, Framed Name Badges (Name Badges subcategories)
- Australian Made / Multi Press Button Badge Machine (Button Badge Machines subcategories)
- Individual PVC Plaques / Aluminium Plaques / Stainless Steel Plaques pages
- Any other individual product pages besides the Polyester Lanyard example

## Note on SEO tags
Canonical URLs, Open Graph tags, and JSON-LD structured data in every
page's `<head>` were **not** rewritten — they still correctly point to
the real badge-a-minit.com.au URLs, since that metadata describes the
production page for search engines and social previews, not this local
prototype.
