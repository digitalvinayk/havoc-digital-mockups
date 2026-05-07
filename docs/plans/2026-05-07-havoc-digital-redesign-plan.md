# Havoc Digital Website Rebuild — Implementation Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** Build two static HTML/CSS home page mockups (Variant A "Editorial Authority" + Variant B "Quiet Tech") plus shared SEO/GEO/EEAT scaffolding that the client can review and pick from before WordPress conversion.

**Architecture:** Pure static HTML5 + modern CSS (OKLCH, container queries, View Transitions, `:has()`, variable fonts). No build step, no JS frameworks, no dependencies. Each variant is self-contained and opens in any browser via `file://`. Both share the same SEO foundation (schema, llms.txt, robots.txt, accessibility primitives).

**Tech Stack:** HTML5 · CSS3 (modern features per §7 of design doc) · JSON-LD · No JavaScript except inline `<script type="application/ld+json">` for schema · Self-hosted variable fonts (Fraunces, Inter, Geist, JetBrains Mono via `@font-face` from public CDNs initially, with note to download for production).

**Reference:** Read [design doc](2026-05-07-havoc-digital-redesign-design.md) before each phase. All visual specs, palette values, copy direction, and section structures live there.

---

## Sequencing strategy

Five phases, each with a commit gate:

| Phase | What | Why this order |
|---|---|---|
| 1 | Shared SEO files | Foundational, lowest visual risk, sets schema patterns reused in both variants |
| 2 | Variant A (Editorial) | More constrained design — easier to nail first; establishes shared structural patterns |
| 3 | Variant B (Quiet Tech) | More complex (bento grid, accordion, form) — benefits from patterns proven in Phase 2 |
| 4 | README + presentation guide | Last because it references the finished mockups |
| 5 | QA pass | Cross-browser smoke test + Lighthouse + HTML validation |

**TDD note:** HTML/CSS doesn't unit-test naturally. The verification model is:
1. Write the file/section
2. Open in browser, visually inspect
3. Validate HTML (`html-validate` or W3C validator API)
4. Commit

End-of-phase gates run a full Lighthouse audit against the file.

---

## Phase 1 — Shared SEO Foundation

### Task 1.1: Create `shared-seo/robots.txt` with AI crawler directives

**Files:**
- Create: `shared-seo/robots.txt`

**Step 1: Write the file**

Content:
```
# Havoc Digital — robots.txt
# Last reviewed: 2026-05-07

# === Search engines ===
User-agent: Googlebot
Allow: /

User-agent: Bingbot
Allow: /

User-agent: DuckDuckBot
Allow: /

# === AI search crawlers (we WANT to be cited) ===
User-agent: GPTBot
Allow: /

User-agent: ChatGPT-User
Allow: /

User-agent: OAI-SearchBot
Allow: /

User-agent: ClaudeBot
Allow: /

User-agent: Claude-Web
Allow: /

User-agent: PerplexityBot
Allow: /

User-agent: Google-Extended
Allow: /

User-agent: CCBot
Allow: /

User-agent: Applebot-Extended
Allow: /

# === Default ===
User-agent: *
Allow: /

# === Sitemaps ===
Sitemap: https://havoc.digital/sitemap.xml
```

**Step 2: Verify**
Run: `cat "shared-seo/robots.txt" | head -5`
Expected: see header lines.

**Step 3: Commit**
```bash
git add shared-seo/robots.txt
git commit -m "feat(seo): add robots.txt with AI crawler directives"
```

---

### Task 1.2: Create `shared-seo/llms.txt`

**Files:**
- Create: `shared-seo/llms.txt`

**Step 1: Write the file** — concise index per [llmstxt.org](https://llmstxt.org/) convention.

Content (template — fill from design doc context):

```markdown
# Havoc Digital

> Boutique digital marketing agency founded in 2012 by Ben Miranda. Operating across Sydney, London, New York, and Bangkok. Specializes in SEO, Google Ads, social media marketing, content marketing, and reputation management for small to mid-sized businesses.

## Key facts
- Founded: 2012
- Founder: Ben Miranda
- Locations: Sydney, London, New York, Bangkok
- Email: info@havoc.digital
- Phone (AU): +61 1300 13 38 13
- Phone (UK): +44 (0)2 031 297 847
- Phone (US): +1 347 408 0155
- Phone (TH): +66 (0)2 107 2830

## Services
- SEO (International, National, Local)
- On-Page & Technical SEO
- Link Building
- Google Ads / PPC
- Social Media Marketing
- Website Auditing
- Content Marketing
- Reputation Management
- LinkedIn Marketing
- Google My Business optimization

## Pricing (monthly, USD)
- Social Media: $199/mo
- Google My Business + Maps: $350/mo
- LinkedIn Growth & Outreach: $450/mo

## Documentation
- Full content: /llms-full.txt
- Sitemap: /sitemap.xml
- Schema: structured data via JSON-LD on every page
```

**Step 2: Commit**
```bash
git add shared-seo/llms.txt
git commit -m "feat(seo): add llms.txt index for AI agents"
```

---

### Task 1.3: Create `shared-seo/llms-full.txt`

**Files:**
- Create: `shared-seo/llms-full.txt`

**Step 1: Write the file** — full markdown of all home-page content + service descriptions + case studies + FAQ. ~1500-2000 words. This is what AI agents ingest for full context.

Sections to include (write in clean markdown):
- About Havoc Digital (full company narrative)
- Services (each service with 50-100 word description)
- Selected case studies (Allstate, Rhino Building, accounting firm 442 calls, etc. — narrate each)
- Pricing tiers with inclusions
- FAQ (6 Q&A pairs)
- Team (Ben Miranda founder bio)
- Contact & locations

**Step 2: Commit**
```bash
git add shared-seo/llms-full.txt
git commit -m "feat(seo): add llms-full.txt with full content for AI ingestion"
```

---

### Task 1.4: Create `shared-seo/schema-snippets.json`

**Files:**
- Create: `shared-seo/schema-snippets.json`

**Step 1: Write the file** — 9 reusable JSON-LD blocks indexed by name.

Structure:
```json
{
  "$schema": "https://schema.org",
  "snippets": {
    "organization": { "@context": "...", "@type": "Organization", ... },
    "localBusiness_sydney": { ... },
    "localBusiness_london": { ... },
    "localBusiness_newyork": { ... },
    "localBusiness_bangkok": { ... },
    "person_benMiranda": { ... },
    "website_searchAction": { ... },
    "faqPage": { ... },
    "offerCatalog_pricing": { ... },
    "service_template": { ... }
  }
}
```

Each snippet must be valid JSON-LD per schema.org. Use real data from design doc §4.

**Step 2: Verify JSON parses**
Run: `python3 -c "import json; json.load(open('shared-seo/schema-snippets.json'))" && echo "OK"`
Expected: `OK`

**Step 3: Commit**
```bash
git add shared-seo/schema-snippets.json
git commit -m "feat(seo): add JSON-LD schema snippet library (9 types)"
```

### Phase 1 verification gate
- All 4 files exist in `shared-seo/`
- JSON-LD validates against schema.org (manual spot-check 2 snippets)
- robots.txt covers 11+ crawler directives
- 4 commits in git log

---

## Phase 2 — Variant A: Editorial Authority

Reference: design doc §2 for visual spec + section structure.

### Task 2.1: Create `mockups/variant-a-editorial/index.html` skeleton

**Files:**
- Create: `mockups/variant-a-editorial/index.html`

**Step 1: Write the HTML skeleton**

Include:
- `<!DOCTYPE html>`, `<html lang="en">` with `dir="ltr"`
- `<head>` with: charset, viewport, title (≤60 chars), meta description (≤155 chars), canonical, Open Graph + Twitter Card tags, favicon link, preconnect to font origin, `<link rel="stylesheet" href="styles.css">`
- Critical CSS inlined in `<style>` for above-fold (will fill after Task 2.2)
- 5 JSON-LD `<script>` blocks: Organization, LocalBusiness×4, Person (Ben Miranda), WebSite, FAQPage
- `<body>` with semantic landmarks: `<header>`, `<main>`, `<footer>`
- 12 empty `<section>` placeholders (one per design doc §2 section list), each with `aria-labelledby` + skip-link target
- Skip-to-content link as first body element

**Step 2: Validate HTML**
Run: `npx -y html-validate mockups/variant-a-editorial/index.html` (or W3C validator)
Expected: No errors. Warnings about empty sections OK at this stage.

**Step 3: Commit**
```bash
git add mockups/variant-a-editorial/index.html
git commit -m "feat(variant-a): add HTML skeleton with semantic structure + schema"
```

---

### Task 2.2: Create `mockups/variant-a-editorial/styles.css` foundation

**Files:**
- Create: `mockups/variant-a-editorial/styles.css`

**Step 1: Write base CSS layers**

Structure using `@layer`:
```css
@layer reset, tokens, base, layout, components, utilities;
```

Fill in:
- **reset** layer: minimal modern reset (box-sizing, margin/padding zero, img max-width)
- **tokens** layer: OKLCH custom properties for palette, typography scale via `clamp()`, spacing scale, radii
- **base** layer: `html`, `body`, headings (Fraunces variable font), body text (Inter), code/mono (JetBrains Mono), `text-wrap: balance` on h1-h3, `text-wrap: pretty` on p
- **layout** layer: container, grid primitives, section spacing
- **components**: empty stubs (will fill in later tasks)
- **utilities**: visually-hidden, focus-visible ring (WCAG 2.2 compliant)

Add `@font-face` for Fraunces, Inter, JetBrains Mono (variable fonts).

Add `prefers-reduced-motion: reduce` block.

Add `@media (prefers-color-scheme: dark)` block using `light-dark()` for tokens.

**Step 2: Open in browser to verify font loading**
Run: `open mockups/variant-a-editorial/index.html`
Expected: Fonts visible, no FOUT/FOIT, basic typography looks right.

**Step 3: Commit**
```bash
git add mockups/variant-a-editorial/styles.css
git commit -m "feat(variant-a): add base CSS (palette, typography, layout primitives)"
```

---

### Task 2.3: Build nav + hero

**Files:**
- Modify: `mockups/variant-a-editorial/index.html` (sections 1-2)
- Modify: `mockups/variant-a-editorial/styles.css` (add nav + hero components)

**Step 1: Write nav** — sticky on scroll, semi-transparent backdrop. Wordmark left, 4 links (Work, Services, About, Thinking), "Book a call" pill right.

**Step 2: Write hero** — single H1 statement *"Marketing that compounds. Strategy that holds up under scrutiny."*, subhead one sentence, primary CTA + ghost CTA. No hero image. Generous whitespace.

**Step 3: Verify in browser** — visually inspect, check responsive at 375px / 768px / 1280px / 1920px.

**Step 4: Commit**
```bash
git add mockups/variant-a-editorial/
git commit -m "feat(variant-a): nav + hero sections"
```

---

### Task 2.4: Build trust strip + services list

**Files:**
- Modify: index.html, styles.css

**Step 1:** Trust strip — 4 cities + phones, "Est. 2012", placeholder cert badges row.
**Step 2:** Services — 3-column editorial *list* (titles + 1-line descriptors). 9 services grouped: Search / Paid / Brand. Use CSS subgrid for alignment.
**Step 3:** Browser verify.
**Step 4:** Commit
```bash
git commit -am "feat(variant-a): trust strip + services list"
```

---

### Task 2.5: Build selected work (case studies)

**Files:** index.html, styles.css

**Step 1:** 3 featured case studies as pull-quote spreads. Each: client name, sector, big metric, 30-word client quote, engagement length. Real data: Allstate Insurance / Rhino Building / Accounting firm (442 calls).
**Step 2:** Browser verify — metric numerals should be ~6-8rem, dominant.
**Step 3:** Commit
```bash
git commit -am "feat(variant-a): selected work case study spreads"
```

---

### Task 2.6: Build approach + founder sections

**Files:** index.html, styles.css

**Step 1:** Approach — short essay (~120 words) with numbered 4-step process (Audit → Strategy → Execute → Measure).
**Step 2:** Founder — Ben Miranda quote pulled large, 3-line bio, photo placeholder, LinkedIn link.
**Step 3:** Browser verify.
**Step 4:** Commit
```bash
git commit -am "feat(variant-a): approach + founder sections"
```

---

### Task 2.7: Build pricing + FAQ

**Files:** index.html, styles.css

**Step 1:** Pricing — 3 clean tiers ($199/$350/$450), 4 inclusions each, annual discount note.
**Step 2:** FAQ — 6 Q&A using `<details>`/`<summary>` (CSS-only). Mark up with FAQPage schema.
**Step 3:** Test keyboard navigation through FAQ (Tab + Enter to expand).
**Step 4:** Commit
```bash
git commit -am "feat(variant-a): pricing + FAQ with schema"
```

---

### Task 2.8: Build blog + contact CTA + footer

**Files:** index.html, styles.css

**Step 1:** Blog — 3 cards with author byline, dated 2026 placeholders.
**Step 2:** Contact CTA — large two-line headline, Calendly link + email, soft accent background.
**Step 3:** Footer — sitemap, schema-rich addresses for 4 cities, social links, ABN line, llms.txt link.
**Step 4:** Commit
```bash
git commit -am "feat(variant-a): blog cards + contact CTA + footer"
```

---

### Task 2.9: Polish

**Files:** styles.css

- Hover states (links, buttons, cards)
- Focus rings (2px, 3:1 contrast — WCAG 2.2)
- Smooth scroll behavior
- View Transitions API for nav links if same-origin
- Container queries for component-level responsiveness
- Final responsive pass at 375 / 414 / 768 / 1024 / 1280 / 1920

**Commit:** `git commit -am "feat(variant-a): polish — hover states, focus, responsive"`

---

### Task 2.10: Lighthouse + validation

**Step 1:** Run `npx -y lighthouse mockups/variant-a-editorial/index.html --view --preset=desktop --quiet` (or open Chrome DevTools Lighthouse).
**Step 2:** Targets — Performance 95+, Accessibility 100, Best Practices 100, SEO 100.
**Step 3:** Fix any sub-target items.
**Step 4:** Validate HTML — `npx -y html-validate mockups/variant-a-editorial/index.html`.
**Step 5:** Commit any fixes.

### Phase 2 verification gate
- `index.html` validates with no errors
- Lighthouse desktop scores: Perf 95+, A11y 100, BP 100, SEO 100
- All 12 sections rendered and visible
- Mobile responsive at 375px without horizontal scroll
- All schema validates at https://validator.schema.org/
- 9-10 commits since start of Phase 2

---

## Phase 3 — Variant B: Quiet Tech / Data-Forward

Reference: design doc §3 for visual spec + section structure.

### Task 3.1: HTML skeleton
Same pattern as Task 2.1, but for Variant B. Different palette tokens, different fonts (Geist + Inter), different page structure (11 sections per design doc §3).
**Commit:** `git commit -am "feat(variant-b): HTML skeleton + schema"`

### Task 3.2: Base CSS
Same pattern as Task 2.2. Tokens differ: crisp white bg, near-black text, indigo accent, Geist headlines, tabular nums everywhere stats appear.
**Commit:** `git commit -am "feat(variant-b): base CSS with quiet-tech tokens"`

### Task 3.3: Nav + hero with stat ticker
Mega-menu services dropdown (CSS-only `:has()` + `popover` attr). H1 *"Digital marketing, measured."* + subhead + animated stat ticker (CSS keyframes, no JS).
**Commit:** `git commit -am "feat(variant-b): nav + hero with stat ticker"`

### Task 3.4: Bento services grid
6 service cards, irregular grid (CSS Grid with `grid-template-areas`). Each: mini-icon SVG inline, name, value prop, "Learn more →".
**Commit:** `git commit -am "feat(variant-b): bento services grid"`

### Task 3.5: Case studies as data tiles
4 metric tiles. Big numeral + label + client + sector.
**Commit:** `git commit -am "feat(variant-b): case study data tiles"`

### Task 3.6: Methodology + stack/certs
Methodology diagram (Audit → Strategy → Execute → Report), monospace step labels, dotted connecting lines (SVG inline). Stack/certs logos row.
**Commit:** `git commit -am "feat(variant-b): methodology + stack & certifications"`

### Task 3.7: Pricing + FAQ accordion
3 tiers as dashboard-style cards with ✓ checklists. Middle tier "Most popular" badge. FAQ as `<details>` accordion, schema-marked.
**Commit:** `git commit -am "feat(variant-b): pricing + FAQ accordion"`

### Task 3.8: Resources + contact + footer
3 blog cards. Split contact: form left (name, email, company, message), Calendly embed iframe right. Minimal technical footer with status indicator.
**Commit:** `git commit -am "feat(variant-b): resources + contact form + footer"`

### Task 3.9: Polish
Hover, focus, responsive, View Transitions, container queries, final responsive pass.
**Commit:** `git commit -am "feat(variant-b): polish — hover, focus, responsive"`

### Task 3.10: Lighthouse + validation
Same targets as Task 2.10.
**Commit:** any fixes.

### Phase 3 verification gate
- Same checklist as Phase 2 gate, applied to Variant B

---

## Phase 4 — README + Presentation Guide

### Task 4.1: Write `mockups/README.md`

**Files:**
- Create: `mockups/README.md`

Sections to include:
1. **What's inside** — quick overview of both variants
2. **How to open** — `open mockups/variant-a-editorial/index.html`, same for B
3. **Variant A pitch (60 seconds)** — talking points for client meeting
4. **Variant B pitch (60 seconds)** — talking points
5. **Side-by-side comparison table** — palette, vibe, best-for, trade-offs
6. **Feedback to gather** — 5-7 specific questions to ask the client (palette preference, layout preference, copy direction, must-have features they noticed are missing, deal-breakers)
7. **Decision matrix** — simple template the client fills out
8. **Next steps after approval** — WordPress conversion outline (out of scope but mentioned)

**Commit:** `git commit -am "docs: add README with presentation guide for client meeting"`

---

## Phase 5 — Final QA pass

### Task 5.1: Cross-variant consistency check
- Both variants render Ben Miranda, 4 cities, real metrics, same pricing
- Both have identical schema coverage (9 types)
- Both have llms.txt link in footer
- No typos (run a quick grep for common ones)

### Task 5.2: HTML validation both variants
Run validator on both. Zero errors.

### Task 5.3: Lighthouse both variants
Confirm targets met.

### Task 5.4: Cross-browser smoke test
Open both in: Chrome, Safari, Firefox (if available). Visually verify no obvious breakage.

### Task 5.5: Final commit + summary message to user
**Commit:** `git commit --allow-empty -m "ship: Havoc Digital mockup phase complete"`

Then summarize for user:
- Files created
- Where to open the mockups
- Lighthouse scores achieved
- Open questions still requiring client input (per design doc § Open Questions)

---

## Skills referenced
- `superpowers:executing-plans` — orchestrate task-by-task execution
- `superpowers:verification-before-completion` — before marking each task complete
- `superpowers:requesting-code-review` — optional, after Phase 2 + Phase 3 if quality concerns

## Risks & mitigations

| Risk | Mitigation |
|---|---|
| Variable fonts fail to load on `file://` | Inline base64 fonts as fallback, OR use system fonts in dev + note CDN URLs in production WordPress phase |
| Lighthouse scores below target | Each phase ends with explicit Lighthouse gate — fix before moving on |
| Schema invalid | Validate via https://validator.schema.org after each schema block |
| Mockup doesn't match design vibe | Reference design doc §2 / §3 vibe descriptions before each major section |
| Browser-specific CSS feature unsupported | `@supports` fallbacks for OKLCH, View Transitions, `:has()` |

## Out of scope reminder

- WordPress conversion (separate phase)
- Real photography (placeholders OK)
- Real testimonial copy (placeholders OK)
- Custom illustrations (text + simple SVGs only)
- Live blog content (placeholders OK)
- Form backend (form is presentational only)
