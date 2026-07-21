# Badge-A-Minit Redesign — Local Prototype

Open `index.html` in a browser and click through. The header "Categories"
dropdown is now a full mega-menu matching every category on the live site,
with nested flyouts for Name Badges and Button Badge Machines.

**Local (built) pages** link to the matching file in this folder.
**Not-yet-built pages** link out to the real **badge-a-minit.com.au** —
that's intentional, a working fallback rather than a dead link.

## Full navigation map

**Home** → `index.html`

**Custom & Personalised Name Badges** → `category-name-badges.html`
- Full Colour Name Badges → `category-full-colour-name-badges.html`
- Engraved Name Badges → `category-engraved-name-badges.html`
- Chalkboard Name Badges → `category-chalkboard-name-badges.html`
- Engraved Wood Name Badges → `category-engraved-wood-name-badges.html`
- Reusable Name Badges → *live site* (not yet built)
- Framed Name Badges → *live site* (not yet built)

**Lapel Pins** → `category-lapel-pins.html`
**Custom Button Badges** → `category-button-badges.html`

**Button Badge Machines** → `category-button-badge-machines.html`
- Australian Made Button Badge Machine → *live site* (not yet built)
- Multi Press Button Badge Machine → *live site* (not yet built)

**ID Cards / Event Badges** → `category-id-cards.html`
**Lanyards** → `category-lanyards.html`
**Desk Name Plates** → `category-desk-name-plates.html`

**PVC Plaques** → `category-plaques.html` *(see note below)*
**Stainless Steel Plaques** → `category-plaques.html` *(see note below)*
**Aluminium Plaques** → `category-plaques.html` *(see note below)*

**Luggage Tags** → `category-luggage-tags.html`
**Badge Accessories** → `category-badge-accessories.html`
**Button Badge Accessories** → `category-button-badge-accessories.html`
**Button Badge Components** → *live site* (not yet built)
**Button Badge Die Cutting Tools** → `category-button-badge-die-cutting-tools.html`
**Button Badge Interchangeable Dies** → `category-button-badge-interchangeable-dies.html`

**Example product page** → `product-polyester-lanyard.html`
(linked from within `category-lanyards.html`; uses its own simplified PDP
header by design, not the full mega-menu)

### Note on the three Plaques links
The live site has PVC / Stainless Steel / Aluminium Plaques as three
separate pages. We've only built one consolidated **Plaques** page so far
(`category-plaques.html`, covering all three materials on one page), so
all three menu items currently point there rather than to the live site —
it's the closest built equivalent. Say the word if you'd rather these
three point to the live site individually until dedicated pages exist,
or if you want the three separate pages built out.

## Not yet built (menu items fall through to the live site)
- Reusable Name Badges, Framed Name Badges
- Australian Made Button Badge Machine, Multi Press Button Badge Machine
- Button Badge Components
- Any individual product pages besides the Polyester Lanyard example

## Note on SEO tags
Canonical URLs, Open Graph tags, and JSON-LD structured data in every
page's `<head>` were **not** rewritten — they still correctly point to
the real badge-a-minit.com.au URLs for search engines and social previews.
