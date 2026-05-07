# Havoc Digital — Website Rebuild Design Document

**Date:** 2026-05-07
**Project:** Replace havoc.digital with a 2026-aligned WordPress site
**Stage:** Mockup / pre-build (HTML mockups for client approval before WordPress conversion)
**Author:** Designer of record (working with Claude Code)
**Status:** Approved — proceeding to implementation plan

---

## Executive Summary

Havoc Digital — a boutique digital marketing agency founded in 2012 by Ben Miranda, operating across Sydney, London, New York, and Bangkok — needs a complete website rebuild. The current site (havoc.digital) suffers from:

- Google Search Console crawling issues
- Inconsistent rendering on Chrome
- Weak content-to-design ratio: 7 real case studies and 14 years of experience are buried under generic copy
- A logo color palette the client describes as "too harsh"
- Missing E-E-A-T signals (no team bios, no certifications, no testimonial bodies, stale blog)
- Inconsistent pricing presentation
- Keyword-stuffed hero copy that won't survive 2026 SEO/GEO standards

The rebuild delivers **two strategic home page mockups** in static HTML/CSS — one positioned as **Editorial Authority** (Variant A), one as **Quiet Tech / Data-Forward** (Variant B). Both are built on a shared SEO/GEO/E-E-A-T scaffolding designed for 2026 standards (AI Overviews, ChatGPT/Perplexity citation, WCAG 2.2 AA, Core Web Vitals INP target).

The client picks one direction; that direction is then converted to a WordPress block theme in a follow-on phase (out of scope for this document).

---

## §1 — Project Architecture

```
HOVC Digital/
├── docs/plans/
│   └── 2026-05-07-havoc-digital-redesign-design.md   ← this file
├── mockups/
│   ├── variant-a-editorial/
│   │   ├── index.html
│   │   ├── styles.css
│   │   └── assets/
│   ├── variant-b-quiet-tech/
│   │   ├── index.html
│   │   ├── styles.css
│   │   └── assets/
│   └── README.md                  ← presentation guide for the client meeting
└── shared-seo/
    ├── llms.txt                   ← AI agent index
    ├── llms-full.txt              ← full-content markdown for AI ingestion
    ├── robots.txt                 ← AI crawler directives
    └── schema-snippets.json       ← reusable JSON-LD blocks
```

**Build philosophy:**
- Static HTML/CSS only — no JS frameworks, no build step, no dependencies.
- Each variant opens in any browser by double-clicking `index.html`.
- WordPress-ready structure (semantic HTML maps cleanly to Gutenberg blocks).
- Self-contained: each variant is independent so the client can be shown one without the other.

---

## §2 — Variant A: "Editorial Authority"

**Positioning:** *The thinking agency for serious operators.*
**Reference vibe:** Pentagram studio site × Stripe Press × New York Times opinion section.
**Best for:** Moving the brand upmarket, justifying higher retainer pricing, attracting strategic-minded SMB and mid-market buyers.

### Visual specification

| Element | Spec |
|---|---|
| Background | `oklch(96.5% 0.012 80)` — warm off-white, hex fallback `#F7F4EF` |
| Foreground | `oklch(15% 0.01 270)` — deep ink, hex fallback `#0E1116` |
| Accent | `oklch(38% 0.06 150)` — muted forest, hex fallback `#2F4A3A` |
| Headline font | **Fraunces** (variable, optical sizing) — editorial serif |
| Body font | **Inter** (variable) — humanist sans |
| Stats / labels | **JetBrains Mono** — uppercase, letter-spaced |
| Headline scale | `clamp(2.5rem, 5vw + 1rem, 5rem)` — fluid |
| Line-height (body) | 1.6 |
| Max content width | 72ch (body), 1280px (full layouts) |

### Page structure (top → bottom)

1. **Nav** — wordmark left, 4 links (Work, Services, About, Thinking), "Book a call" pill right. Sticky on scroll, semi-transparent backdrop.
2. **Hero** — single editorial H1 statement (~12 words), no image, dominant whitespace. H1: *"Marketing that compounds. Strategy that holds up under scrutiny."* Subhead one sentence below; primary CTA + ghost CTA.
3. **Trust strip** — 4 city names with phone numbers, "Est. 2012", placeholder cert badges (Google Partner, Meta Business Partner, GA4 certified — client supplies real assets).
4. **Services** — 3-column editorial *list* (titles + 1-line descriptors, not cards). Hover state reveals a learn-more arrow. 9 services grouped as: Search (SEO, On-page, Link building) / Paid (Google Ads, Social Ads) / Brand (Content, Social, Reputation, GMB).
5. **Selected work** — 3 featured case studies as pull-quote spreads. Each is a full-width section with: client name, sector, the metric in giant numerals, a 30-word client quote, the engagement length. Real cases: Allstate Insurance (reputation), Rhino Building (SEO), accounting firm (442 calls in 5 months via GMB).
6. **Approach** — short essay (~120 words) with a numbered 4-step process: Audit → Strategy → Execute → Measure. JetBrains Mono numerals.
7. **Founder** — Ben Miranda quote pulled large + 3-line bio + photo placeholder + LinkedIn link.
8. **Pricing** — 3 clean tiers, clearly priced (Social $199/mo / GMB+Maps $350/mo / LinkedIn Growth $450/mo). No inconsistencies. Each tier has 4 inclusion bullets. Annual discount note.
9. **FAQ** — 6 questions with concrete answers. Marked up as `FAQPage` schema. Topics: pricing, timelines, contracts, reporting cadence, results guarantees, channel choice.
10. **Recent thinking** — 3 blog cards (placeholder content, dated 2026). Author byline (Ben Miranda or Chris Jackson).
11. **Contact CTA** — large two-line headline, Calendly link + email, soft accent background.
12. **Footer** — sitemap, schema-rich addresses for all 4 cities, social links, ABN/registration line, llms.txt link.

---

## §3 — Variant B: "Quiet Tech / Data-Forward"

**Positioning:** *Digital marketing, measured.*
**Reference vibe:** Linear × Vercel × modern SaaS landing.
**Best for:** Tech-forward SMBs, SaaS clients, data-literate founders. Strong for clients who want dashboards over decks.

### Visual specification

| Element | Spec |
|---|---|
| Background | `oklch(99% 0 0)` — crisp white, hex fallback `#FCFCFC` |
| Foreground | `oklch(8% 0 0)` — near-black, hex fallback `#0A0A0A` |
| Accent | `oklch(58% 0.18 270)` — muted indigo, hex fallback `#5B6CFF` |
| Surface (cards) | `oklch(97% 0.005 270)` — pale tint |
| Border | `oklch(92% 0.005 270)` — hairline |
| Headline font | **Geist** (variable) — geometric sans |
| Body font | **Inter** (variable) |
| Numerals | Tabular figures everywhere stats appear |
| Headline scale | `clamp(2rem, 4vw + 1rem, 4rem)` |
| Border radius | 12px (cards), 6px (buttons) |

### Page structure (top → bottom)

1. **Nav** — wordmark, services dropdown (mega-menu), Work, Pricing, "Get free audit" button (filled accent).
2. **Hero** — H1 + subhead + animated stat ticker ("442 calls / 60× growth / 14 years / 4 offices"). H1: *"Digital marketing, measured."* Subhead 18-22 words.
3. **Bento services grid** — 6 service cards in irregular grid (large + medium + small tiles). Each card: mini-icon, service name, 1-line value prop, "Learn more →".
4. **Case studies as data tiles** — 4 tiles, each is a metric formatted as `442` (huge) + label (small mono) + client name + sector. Click → full case study.
5. **Methodology section** — visual diagram (Audit → Strategy → Execute → Report), monospace step labels, dotted connecting lines.
6. **Stack & certifications** — logos row (Google Ads, GA4, GSC, Meta Business, LinkedIn, GMB).
7. **Pricing** — 3 tiers as dashboard-style cards with feature checklists (✓ rows). Middle tier highlighted as "Most popular".
8. **FAQ** — accordion (CSS-only via `<details>`), schema-marked.
9. **Resources** — 3 blog cards.
10. **Contact** — split layout: form left (name, email, company, message), Calendly embed right.
11. **Footer** — minimal, technical. Status indicator ("All systems operational" — subtle SaaS touch).

---

## §4 — Shared SEO / GEO / E-E-A-T Scaffolding

Both variants inherit this foundation. This is the SEO recovery system.

### On-page SEO
- Single `<h1>` per page, semantic H2-H4 hierarchy, no skipped levels
- Descriptive `<title>` (≤60 chars), meta description (≤155 chars), canonical URL
- Open Graph + Twitter Card meta tags for rich link previews
- Image `alt` attributes on every `<img>`, decorative images marked `alt=""`
- Mobile-first responsive — CSS Grid + container queries, not viewport breakpoints alone

### Structured data (JSON-LD)
- `Organization` (founder = Ben Miranda, founded 2012, sameAs to socials)
- `LocalBusiness` × 4 (Sydney, London, NY, Bangkok with phones, hours, geo)
- `Service` × 10 (one per service offered, with `provider`, `serviceType`, `areaServed`)
- `FAQPage` (powers AI Overviews + ChatGPT citations)
- `BreadcrumbList`
- `Person` (Ben Miranda, with `sameAs` to LinkedIn/Twitter)
- `WebSite` with `SearchAction` (sitelinks search box)
- `OfferCatalog` wrapping pricing tiers
- `AggregateRating` + `Review` (when client supplies real testimonials)

### E-E-A-T (Experience, Expertise, Authoritativeness, Trustworthiness)
- Founder named with credentials and a photo (Experience)
- Real case studies with named clients & specific metrics (Expertise)
- Certifications row with badges (Authoritativeness)
- Author bylines on blog placeholders (Authoritativeness)
- 4 verifiable office locations with phone numbers (Trustworthiness)
- ABN/business registration line in footer (Trustworthiness)
- Year founded prominent ("Since 2012") (Experience)

### GEO (Generative Engine Optimization for AI Search)
- Definition-style H2s ("What is local SEO?", "How does Google Ads pricing work?")
- Quotable stat blocks formatted as standalone units
- Comprehensive FAQ section with concrete answers
- `llms.txt` at root listing key pages + summary
- `llms-full.txt` containing entire site content as clean markdown
- Clean text-to-HTML ratio, no JS-blocking content rendering
- TL;DR / summary blocks at top of long sections
- First-sentence optimization (every section's first sentence is a self-contained answer)

### Core Web Vitals (2026 targets: LCP < 2.5s, INP < 200ms, CLS < 0.1)
- System fonts as fallback before web fonts load (`font-display: swap`)
- No carousels (current site uses them — they hurt LCP)
- CSS-only interactions (no JS for hover, accordions, tabs — uses `<details>`, `:has()`, popover)
- Lazy-loaded below-fold images (`loading="lazy"`); `fetchpriority="high"` on hero
- Inline critical CSS for above-the-fold content
- Self-hosted variable fonts (one file covers all weights → faster LCP)
- `<link rel="preconnect">` to font origin
- Explicit `width`/`height` or `aspect-ratio` on every image (CLS prevention)

### Accessibility (WCAG 2.2 AA)
- 4.5:1 contrast minimum, with APCA contrast also checked
- Focus appearance — visible 2px outline with 3:1 contrast (WCAG 2.2 new requirement)
- Target size 24×24px minimum on interactive elements (WCAG 2.2 new)
- Skip-to-content link
- Landmark roles (`<header>`, `<main>`, `<nav>`, `<aside>`, `<footer>`)
- Keyboard-navigable (every interaction works without mouse)
- ARIA labels for icons and decorative elements
- `prefers-reduced-motion` respected on every animation

### Crawlability fixes (the GSC issue)
- Clean `robots.txt` allowing all major search + AI crawlers
- XML sitemap stub
- Stable URL structure documented for WordPress migration
- No reliance on JS for content rendering (current site's main issue)
- HTML validates; no broken links

---

## §5 — Copy Approach

### Preserved verbatim from current site
- Real case study facts: Allstate Insurance, Rhino Building, Eclypse Pest Control, "442 calls in 5 months" (accounting firm), "6 to 60 per week growth" (shopping cart subscription)
- Founder name: Ben Miranda
- Founded: 2012
- Locations + phone numbers for all 4 cities
- Service taxonomy (10 services)
- Email: info@havoc.digital

### Rewritten fresh (current copy is keyword-stuffed and weak)
- Hero H1 + subhead — current "Increase Visibility, Increase Ranking, Increase Visitors, Increase Revenue" is a comma-separated keyword list, not a positioning statement
- Service descriptions — current ones are generic
- "Approach" / "About" sections
- FAQ entirely (none exist on current site)
- Calls-to-action

### Tone
- Confident, plain English, no jargon
- "We" voice (founder-led)
- Statements before lists; numbers in numerals
- Active voice
- Reading level: Year 9-10 (broadly accessible without being dumbed down)

---

## §6 — Deliverables

1. `docs/plans/2026-05-07-havoc-digital-redesign-design.md` — this document (full design rationale)
2. `mockups/variant-a-editorial/index.html` + `styles.css` — fully working static page
3. `mockups/variant-b-quiet-tech/index.html` + `styles.css` — fully working static page
4. `mockups/README.md` — how to open + present to client, what feedback to ask for
5. `shared-seo/llms.txt` — AI agent index
6. `shared-seo/llms-full.txt` — full content for AI ingestion
7. `shared-seo/robots.txt` — annotated AI crawler directives
8. `shared-seo/schema-snippets.json` — extended JSON-LD blocks (9 schema types)

---

## §7 — 2026 Advanced Layer

This is what positions Havoc as "advanced level" rather than "current".

### 7.1 — GEO (Generative Engine Optimization)
- AI crawler directives in `robots.txt` for `GPTBot`, `ClaudeBot`, `Claude-Web`, `PerplexityBot`, `Google-Extended`, `ChatGPT-User`, `CCBot`, `OAI-SearchBot` — all allowed (we WANT to be cited)
- `llms.txt` (index) AND `llms-full.txt` (full content in markdown) — emerging 2025 industry convention
- TL;DR / summary blocks at top of every long section — AI Overviews lift these verbatim
- Definition-style H2s matching natural-language AI queries
- Citation-bait stat blocks — proprietary metrics formatted as standalone quotable units
- First-sentence optimization throughout
- One comparison table embedded ("SEO vs PPC: which fits your stage?")

### 7.2 — Schema enrichment (beyond basics)
- `WebSite` with `SearchAction` (sitelinks search box)
- `OfferCatalog` wrapping pricing tiers
- `AggregateRating` + `Review` (placeholder for testimonials)
- `Person` with `sameAs` for Ben Miranda
- `HowTo` embedded in "Our Approach"
- `Article` + `author` on blog cards
- `speakable` specification for voice assistants

### 7.3 — Modern CSS / Web Platform (2025–2026 features)
- OKLCH color space with hex fallback
- `light-dark()` color function for automatic dark mode
- Container queries (component responsive, not viewport-only)
- CSS Subgrid for proper baseline alignment
- `text-wrap: balance` on H1/H2 (kills hanging widow words)
- `text-wrap: pretty` on body paragraphs
- View Transitions API for page-to-page nav
- Speculation Rules API for prefetching
- `<dialog>` element + `popover` attribute for modals
- `:has()` selector for cleaner state styling
- Variable fonts (Fraunces, Inter, Geist all variable — one file, all weights)
- `font-display: swap` + preloaded critical fonts
- Fluid typography with `clamp()`

### 7.4 — Performance discipline
- LCP target < 2.5s — hero is text-only, fonts preloaded, critical CSS inlined
- INP target < 200ms — minimal JS, CSS-only interactions
- CLS target < 0.1 — explicit dimensions, `aspect-ratio`, no late-injecting elements
- AVIF + WebP fallback via `<picture>`
- `fetchpriority="high"` above fold, `loading="lazy"` below
- No render-blocking JS on initial load
- Self-hosted fonts (privacy + speed)

### 7.5 — Accessibility (WCAG 2.2 AA — current standard)
- New 2.2 focus-appearance and target-size rules met
- APCA contrast checked alongside 4.5:1
- Skip links, landmark roles, keyboard testing
- Screen reader-tested labels

### 7.6 — Internationalization (4 regions)
- `hreflang` tags for `en-AU`, `en-GB`, `en-US`, `en` (Bangkok)
- Locale-specific phone formatting
- Pricing currency context flagged for client decision

### 7.7 — Trust & Authority infrastructure
- Author bio page for Ben Miranda (full credentials, sameAs, photo)
- "How we measure" methodology page (transparency = authority)
- Editorial guidelines page (required for AI content trust)
- Live trust strip with freshness indicator
- First-party data report concept ("State of SEO/PPC for SMBs") — backlink magnet + AI citation source

---

## Open Questions / Client Decisions Required

These are not blockers for the mockups, but the client must answer them before WordPress conversion:

1. **Real testimonials** — current site has a "Love from Clients" header but no testimonial bodies. Client must supply 5-8 real testimonials (with permission) for production.
2. **Certification badges** — Google Partner / Meta Business Partner / GA4 — client supplies real badge images.
3. **Founder photo** — professional headshot of Ben Miranda required.
4. **Office addresses** — full street addresses for each of the 4 cities (currently only city names shown). Required for `LocalBusiness` schema.
5. **Pricing currency** — which region's $? Or display per-region? Decision affects pricing section.
6. **Blog plan** — current blog last updated July 2024. Client commits to content cadence (recommendation: 2 posts/month minimum) or removes blog from main nav.
7. **Hosting / WordPress stack** — managed (Kinsta / WP Engine) vs unmanaged. Affects performance baseline.
8. **Analytics** — GA4 + Google Search Console must be reconfigured; recommend adding Plausible or similar privacy-first secondary.

---

## Out of Scope (this phase)

- WordPress theme conversion (separate phase after client picks variant)
- Real content writing for blog
- Photography / illustration commission
- Custom illustration / icon set
- Migration plan from current site
- 301 redirect mapping
- Email marketing integration
- CRM integration

---

## References

- Current site: https://havoc.digital/
- Current pricing: $199/mo Social, $350/mo GMB, $450/mo LinkedIn (per discovery fetch)
- Current case studies: Allstate Insurance, Rhino Building, Eclypse Pest Control, accounting firm (442 calls), shopping cart subscription (60× growth), natural cosmetics (international in 2 years), furniture removalist
- WCAG 2.2: https://www.w3.org/TR/WCAG22/
- llms.txt convention: https://llmstxt.org/
- Core Web Vitals (2026 INP): https://web.dev/articles/inp

---

## Approval

- [x] Architecture (§1) — approved
- [x] Variant A specification (§2) — approved (forest accent confirmed)
- [x] Variant B specification (§3) — approved (indigo accent confirmed)
- [x] Shared SEO/GEO/E-E-A-T scaffolding (§4) — approved
- [x] Copy approach (§5) — approved (fresh copy preserving real facts)
- [x] Deliverables (§6) — approved
- [x] 2026 Advanced Layer (§7) — approved

**Next step:** Invoke the `superpowers:writing-plans` skill to convert this design into a sequenced, executable implementation plan.
