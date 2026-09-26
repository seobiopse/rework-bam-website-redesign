# Badge-A-Minit Beta Site Audit
**Site:** https://beta.badge-a-minit.com.au  |  **Audited:** 24 Sep 2026  |  **Scope:** Homepage, 18 category pages, 108 product pages (of 109 in the "Product URLs" sheet)
**Ignored as instructed:** broken images, robots.txt, meta robots.
**Appendix (per-URL data):** `BAM_Beta_Audit_Appendix_v3.xlsx`  |  **Metadata inspect captures:** `meta/` (45 pages)  |  **Beta vs redesign screenshots:** `compare/side_by_side/`  |  **Evidence:** `evidence/`, `shots/`, `videos/`, `lh/`

---
## 0. Executive summary – fix these first

| # | Issue | Where | Severity |
|---|---|---|---|
| 1 | **Product and Breadcrumb structured data is broken.** Raw template code (`!!json_encode($productSchema…) !!`) is printed into the JSON-LD instead of data. No Product rich results are possible. | 109 of 109 product pages and 18 of 18 category pages (checked 26 Sep). Homepage is fine. | Critical |
| 2 | **Performance is poor.** Mobile Lighthouse score is 31–34, LCP 9–24 s, TBT ~1 s. Server takes 3–5 s to send the HTML. | Home, category, product | Critical |
| 3 | **Beta page copy does not match the approved Google Docs.** Average match is 66%. 28 pages are below 60%. Order-process steps, "Why choose us" and feature intros are reworded, missing or generic. | Product pages | High |
| 4 | **Missing or weak metadata.** 14 product pages have no meta description. 11 titles are under 30 characters. 2 pairs of product pages share a title. | Product pages | High |
| 5 | **Mobile layout bugs.** A bare unstyled `<h5>` renders over the header, the fixed "QUICK CONTACT" tab covers content, and the phone number wraps to 3 lines. | All pages at 320–414 px | High |
| 6 | **Category pages are partly updated; homepage is not.** Dev added the new comparison, steps and reviews sections to all 18 category pages, but the hero block (H1, tagline, intro, feature bullets, dispatch banner) and all titles and meta descriptions are still the old ones, and three titles have typos. The homepage has a different title, meta description, ABN and footer (no Terms link). See section 1.5. | Homepage and category pages | High |
| 7 | **Inconsistent trust facts.** "48+ years" on the homepage versus "45+ years" on 116 pages, plus "four decades". | Site-wide | Medium |
| 8 | **Beta server instability.** The site hung and timed out under light crawl load (2–6 parallel requests). | Server | Medium (test on production infra) |

---
## 1. Content Audit

### 1.1 Method
- Source of truth: the 27 readable Google Docs behind column C. One doc, `1s2csQWL…`, is private and returned 401.
- Each doc holds several product tabs, so I split them by "Product URL" to get 107 product sections.
- Each product's approved copy was compared with the server-rendered beta page text using 6-word phrase matching.
- Metadata rows and the "Spec pills" line were excluded from the comparison.
- 107 of the 108 beta product pages matched a doc section. `cutter-circle-base-board` has no doc.
- `express-pvs-lapel-pin` from the sheet is not on beta. Beta uses `express-pvc-lapel-pin`, so the sheet has a typo.

### 1.2 Product pages (108)
| Check | Result |
|---|---|
| Copy match vs approved doc (avg) | **66%** |
| Pages below 60% match | **28** |
| Worst matches | retractable-clip 28%, multi-press-25mm-die-set 48%, multi-press-57mm/35mm-die-set ~55%, 35-mm-button-badge-keychain-kit 56%, australian-made-button-badge-machine 56% |
| Intro paragraph cut off with "…" in the hero | **108 of 108** (e.g. "…exposed for a distinc…"). The full text sits lower on the page. |
| Word count | Avg ~1,300, none thin. |
| Title under 30 chars | **11**. These are the lapel-pin and plaque pages, e.g. "Ribbon Lapel Pin", "Diamante Lapel Pin", "PVC Plaque-Laser Engraved". They lack keywords and brand. |
| Title over 60 chars | 3 (australian-made-button-badge-machine, full-colour-event-badge-pass-non-personalised, stainless-steel-plaque-laser-engraved) |
| Missing meta description | **14** (all lapel-pin variants plus the aluminium and PVC plaques) |
| Duplicate titles | 2 pairs. `button-badge-57-mm` and `fridge-badge-magnet-57-mm` share both title and meta description. `button-badge-85-mm` and `button-badge-magnet-faster-85-mm` share a title. (Some product titles also repeat their category page's title.) |
| H1 count ≠ 1 | 2 (cherry-wood-engraved-name-badge, double-layered-polyesterlanyard) |
| OG/social tags | **0 of 108** have them (categories and home do) |
| Image alt text | Every product page has at least one image with no alt text. Broken images are ignored per brief, but alt text is still needed. |
| Structured data | FAQPage is valid. **Product + BreadcrumbList are broken template code on all 109.** |

**Examples of approved copy missing or reworded on the page**
- `retractable-clip`: the "Every retractable clip is built to…" lead-in and the Step 1–3 order text are missing.
- `soft-enamel-lapel-pin`: "Step 4 Receive & Enjoy" differs, and "Sharper Pricing at Volume" and "Nothing Goes to Print Unapproved" are reworded.
- `button-badge-25-mm`: the feature lead-in and the Step 2 and Step 4 text differ from the doc.
- `australian-made-button-badge-machine`: 11 doc paragraphs are missing, including the "streamlined process" intro and Steps 1–2.

Full per-URL detail is in the appendix, sheet **Product URLs**.

### 1.3 Category pages (18)
- Every category has a unique title (45–59 chars), meta description (132–164 chars), a single H1 and about 1,600–2,300 words.
- The category "Custom Button Badges" (`/products/button-badge`) is fine. `/products/luggage-tags` has the longest description at 164 chars, so it will be truncated in results.
- The category and product intro teasers are cut off with "…".
- **All 18 category pages ship broken JSON-LD** (`!!json_encode($breadcrumbSchema…) !!` and `!!json_encode($schema…) !!`, unrendered template code), the same bug as the product pages. A valid WebPage and FAQPage block is also present. Evidence: `meta/` screenshots. (My earlier note that categories only had WebPage/WebSite schema was wrong.)
- Approved category copy comes from the redesign site: see section 1.5.

### 1.4 Homepage
- Title is 56 chars, description 142 chars, one H1 ("Badges, plaques & the gear to make your own"), about 2,800 words.
- The FAQ has 13 questions but no FAQPage schema. Only a LocalBusiness block is present.
- The canonical is `https://beta.badge-a-minit.com.au` (no trailing slash), while the site serves `/`.
- **Fact inconsistencies:**
  - "48+ years" on the homepage.
  - "45+ years" on 116 pages.
  - "four decades" on 84 pages.
  - "almost 50 years" on the About page.
  - Hero says "Same-Day dispatch available", but the product hero shows "36 Days" turnaround with no explanation.
- The two files provided earlier (`badge-a-minit homepage rendered code.txt` and `extracted_text.txt`) are binary and could not be decoded. Homepage and category content is compared with the redesign site instead (section 1.5).

### 1.5 Homepage and categories vs the redesign reference (added)
Reference: https://seobiopse.github.io/rework-bam-website-redesign/ (homepage `index.html` plus the 18 `category-*.html` pages linked from its nav menu). Full table: appendix sheet **Cat+Home vs Redesign**.

**Categories: re-checked on 26 Sep (corrects my 24 Sep result)**
Dev updated all 18 category pages between my two crawls (26 Sep pages are 20–50% shorter, old blocks are gone, new sections are in). My first comparison was also wrong: the redesign category pages build their content sections with JavaScript, and I had only read the static part. I re-rendered them and re-fetched beta. Full per-page table: appendix sheet **Category vs Redesign 26Sep**.

- **Updated by dev (new sections match the redesign wording):** the "Which X fits…" comparison guide, the "From browsing to your team, in 4 steps" block, reviews and "You may also like" on all 17 sub-categories. Old "How it works / Why choose us / Trusted by" blocks and the old "Find the Perfect Lapel Pin…" section were removed. The "UV Printed **Sof** Enamel" typo was fixed in the body.
- **Not updated on any page (hero block):**
  - H1 is still the old one on all 17 (redesign "Order Custom Lapel Pins Australia" vs beta "Lapel Pins").
  - The redesign tagline (e.g. "A custom lapel pin is a wearable medal of belonging…") is missing.
  - The longer intro paragraph is missing.
  - The 4–5 feature bullets are missing (e.g. "Free Pre-Press 1:1 Vector Proof").
  - The "Same-day dispatch on stock lines…" banner and the sort control are missing.
  - Product-card names differ from the redesign's shortened names.
- **Weakest pages:** `/products/name-badges` (only the steps block was added; the "Which name badge fits your team?" and "Five timber finishes" sections are missing, 1 of 8 headings found) and `/products/button-badge-machines` (body 4 of 48 lines matched).
- **Best matches:** `lapel-pins` (60 of 91 lines), `button-badge` and `button-badge-components`.
- **Metadata not updated:** every category title and meta description is unchanged since 24 Sep. The three typos remain ("Acessories", "Orer", "Ordrer"). The redesign only gives final titles for lapel-pins and button-badge-components.
- **Overall:** 15 of 17 are "Partially updated" (about 50–66% of the redesign lines are present) and 2 are "Barely updated". Category QS is now 70–77 for 15 pages, 56 for name-badges and 58 for button-badge-machines. The multi-press-button-badge-machine sub-category has no redesign page.

**Homepage** (body copy is ~99% the same length and structure as the redesign; 2,781 vs 2,800 words)
| Item | Redesign | Beta |
|---|---|---|
| Title tag | "Custom Badges, Lanyards & Promotional Items \| Badge-A-Minit" | "Buy Badge Accessories and Promotional Items in Australia" |
| Meta description | "Custom badges, lanyards, and name tags… Australian made since 1978. Get free design services, direct factory prices, and fast dispatch." | "Discover a wide range of badge accessories and promotional items…" (generic, off-topic for the H1) |
| Top promo bar | 3 messages: premier manufacturer since 1978; free design and vector proofing; fast tracked courier | Static strip ("Fastest Turnaround / Australian Owned / Free Design Service / Volume Pricing") plus a ticker that is clipped on mobile |
| Main nav | Home, Name Badges, Button Badges, Lanyards, Lapel Pins, About Us, Contact Us, phone, Get A Quote | Home, All Categories mega-menu, phone, Get A Quote (no About or Contact in the header) |
| Reviews | 4.9/5 from 200+ clients, named reviews | 5.0 from 97 Google reviews, different reviewers |
| Award ribbons, presentation packaging and challenge coin sections | Present | Absent |
| Footer: Terms & Conditions link | Present | **Absent** |
| Footer: newsletter sign-up | Present | **Absent** |
| Footer: ABN | 29 088 363 165 | **24 662 539 406 (different)** |
| Footer: phone and email | Not shown | Shown |
| Delivery estimator, FAQ (13), role sections, best-sellers list | Present | Present, with small wording changes (e.g. "How do i choose…" has a lowercase "i" typo on beta) |

Confirm the correct ABN before launch.

---
## 2. Responsive Audit
Tested 8 templates at 320, 375, 768 and 1440 px (home, 3 categories, 4 products). I checked overflow, tap targets (44 px), text size and layout. Six page/viewport loads timed out and are marked "ERROR" in the appendix.

**Good:** no horizontal page scrolling at any width.

| # | Issue | Evidence |
|---|---|---|
| R1 | **Unstyled `<h5>` block above the hero.** Default black 18 px text ("Australia's premier supplier of Name Badges…") sits in a 1,107 px wide element and is clipped at 375 px. The ticker strip above it is also cut off ("…supplier of Custon"). | `evidence/E1_mobile_home_fold_375.png`, video |
| R2 | **Fixed "QUICK CONTACT" tab** (40×140 px, max z-index) covers the right edge of content and text on every page. | `evidence/E2_mobile_quick_contact_overlap_375.png` |
| R3 | **Top bar cramped on mobile.** The phone number wraps to 3 lines, and the top-bar text is 11 px, with the cart count at 9 px. | E1 |
| R4 | **Small tap targets.** 22–89 targets are under 44 px per page. Examples: "Become a Reseller" 82×33, email link 123×33, cart 35×36, "Add" buttons 68×21–27. | `Responsive` sheet |
| R5 | **Hero text over a busy photo** on mobile reduces legibility of the subheading. | E1 |
| R6 | 12–20 text elements per page are under 12 px. | `Responsive` sheet |

Screenshots: `shots/<page>_<viewport>.png`. Issue frames: `shots/ISSUE_*`. Recordings: `videos/BAM_beta_mobile_375_walkthrough.webm` and `videos/BAM_beta_tablet_768_home_walkthrough.webm`.

---
## 3. PageSpeed Audit
The Experte tool cannot reach beta because it is behind a login (401). I ran Lighthouse locally with the login credentials instead. Reports are in `lh/`.

| Page | Device | Perf | A11y | BP | SEO | FCP | LCP | TBT | Server response |
|---|---|---|---|---|---|---|---|---|---|
| Home | Mobile | **31** | 89 | 96 | 85 | 8.3 s | **23.9 s** | 1.1 s | 5.1 s |
| Home | Desktop | 54 | 92 | 96 | 85 | 5.7 s | 9.1 s | 110 ms | 4.1 s |
| Category (lapel-pins) | Mobile | **34** | 88 | 96 | 85 | 8.6 s | 10.1 s | 980 ms | 3.0 s |
| Category | Desktop | 57 | 93 | 96 | 85 | 3.9 s | 4.7 s | 70 ms | 3.1 s |
| Product (soft-enamel) | Mobile | **33** | 88 | 77* | 85 | 6.6 s | 9.0 s | 1.1 s | 3.9 s |
| Product | Desktop | 62 | 93 | 77* | 85 | 2.6 s | 3.5 s | 60 ms | 5.0 s |

*The best-practices drop on product pages is "deprecated APIs". The console font (CORS) errors probably come from the login header Lighthouse sends to every request, so I treated them as a test artefact and ignored them. The Kaspersky console errors come from the test machine.

**Top fixes**
1. **Server response 3–5 s** (target under 0.6 s). Add caching (page, route and full-page cache), a CDN, and check hosting capacity. This is the largest LCP component.
2. **Payload 2–3.9 MB.** Cut 1.0–1.3 MB with efficient cache headers, and 185–488 KiB with image delivery fixes (the header logo is oversized). Use WebP/AVIF and lazy-load below the fold.
3. **Unused JavaScript ~495–518 KiB and unused CSS ~328 KiB.** Split bundles per template, purge Tailwind, and minify (about 70–87 KiB of JS and 11 KiB of CSS is unminified).
4. **Render-blocking requests** cost about 3.3–3.5 s on category and product pages. Defer scripts and inline critical CSS.
5. **Main thread 4.6–9.8 s and TTI 16–24 s.** Reduce JS execution (2.2–2.5 s).
6. **Fonts:** fix `font-display` (est. 0.5–1.2 s) and preload key fonts.
7. **Image dimensions:** add width and height (unsized images) to reduce CLS (0.03–0.06).
8. **Back/forward cache** is blocked on all templates.

**Accessibility fixes (all templates)**
- Colour contrast: the quick-contact button is 2.72:1, and other links and eyebrow text are 3.7–4.4:1.
- One link has no accessible name (the top bar icon link to `/get-quote`).
- Prohibited ARIA attributes are in use.
- Heading order is broken.

**SEO audit flags (excluding robots.txt):** `javascript:void(0)` anchors are not crawlable.

---
## 4. Page Quality / E-E-A-T Audit (Homepage landing page)
Score out of 100, rated from what is on the beta homepage.

| Factor | Score | Evidence for | Gaps |
|---|---|---|---|
| **Experience (25)** | **16** | 48+ years, 350,000+ badges, 74,560+ customers, 4-step process, in-house factory, showroom pickup. | No real photos of the factory, staff or finished orders. No case studies or customer stories. |
| **Expertise (25)** | **17** | Clear FAQ answers (soft vs hard enamel, button sizes, lanyard safety clips). Detailed product specs on inner pages. | No named designers or team. No guides or blog. About page is only 139 words. |
| **Authoritativeness (25)** | **13** | "Only company making Australian-made button badge machines" appears on the About page. Google 5.0 rating (97 reviews). | No client logos, awards, associations or press. "Australia's Best Promotional Metal Producer" is unsupported. Only 5 reviews are shown. |
| **Trustworthiness (25)** | **18** | Address (56a Prospect Rd, Prospect SA), phone, email, price-match, PO terms, proof guarantee, LocalBusiness schema. | No links to privacy, returns, terms or shipping pages in the crawled links. Facts conflict (48+ vs 45+ years). Aggressive competitor claims ("old fashioned and outdated"). Emails are Cloudflare-obfuscated. |
| **Total** | **64 / 100** | | |

**Quick wins to reach 80+:**
- Add team and designer bios plus factory photos.
- Add 3–5 named case studies or client logos.
- Publish policy pages (returns, privacy, terms, shipping) and link them in the footer.
- Standardise the years-in-business figure on every page.
- Add Organization, WebSite and Review schema and FAQPage schema on the homepage.
- Back the "best" and "guarantee" claims with proof, and soften the competitor jabs.

---
## 5. Limits of this audit
- **Server load:** the beta server hung during my crawl (I used 2–8 parallel requests). Response times measured then (avg ~10 s) are inflated. Lighthouse's 3–5 s is the reliable figure.
- **Six responsive loads** timed out (category-lapel@320, category-namebadges@320, category-machines@375, product-machine@375, category-lapel@768, product-badge@768).
- **Not covered:** the customisation and quote flows, cart and checkout, and 1 page that could not be fetched. Non-product rows in the sheet (`/customisation/…`) were excluded.
- **Doc coverage** is a phrase-matching score. It measures deviation from the approved text, not whether the beta copy is better or worse.
- **Public doc export:** one doc (`1s2csQWL…`) was private and not compared.
