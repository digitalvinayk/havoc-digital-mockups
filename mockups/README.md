# Havoc Digital — Mockup Presentation Guide

> Two strategic home page directions for the Havoc Digital rebuild. Built for the client meeting on **2026-05-07**. Pure static HTML/CSS — no build step, no dependencies.

---

## What's inside

| Variant | Direction | Aesthetic | Best for |
|---|---|---|---|
| **A** | Editorial Authority | Pentagram × Stripe Press × NYT opinion | Senior/strategic positioning, premium retainers |
| **B** | Quiet Tech / Data-Forward | Linear × Vercel × modern SaaS | Tech-forward SMBs, transparent reporting story |

Both share identical SEO/GEO/E-E-A-T scaffolding (see `../shared-seo/`). The client picks a *direction*, not a *foundation* — the foundation is the same either way.

---

## How to open

From the project root:

```bash
# Variant A
open mockups/variant-a-editorial/index.html

# Variant B
open mockups/variant-b-quiet-tech/index.html

# Or just double-click either index.html in Finder.
```

Both open in any modern browser via `file://`. Recommended for the meeting: **Chrome on a 1440px+ display, full-width**, so the bento grid and case study spreads breathe.

---

## Variant A — Editorial Authority

**60-second pitch for the client:**

> *"This direction positions Havoc as the most senior, most strategic voice in the room. Think McKinsey-meets-Pentagram. Warm off-white with deep ink and a single muted forest accent. Editorial serif headlines. Magazine-style layout — no carousels, no flashy gradients, generous whitespace. Every page element earns its place. Best fit if Havoc wants to move upmarket, command higher retainer pricing, and attract clients who care about thinking quality, not flashy production."*

**What the client should notice:**
1. The hero — one statement, no image. Confidence through restraint.
2. The case studies as pull-quote spreads (not little card thumbnails). Real numbers in giant numerals.
3. The founder quote. *"We earn renewal each quarter, not at the end of a 12-month contract."* That's positioning.
4. The pricing section — calm, transparent, no urgency tactics.
5. Hover the FAQ items — CSS-only accordion, no JavaScript needed.

**Visual specs:**
- Background: warm off-white `#F7F4EF`
- Foreground: deep ink `#0E1116`
- Accent: muted forest `#2F4A3A`
- Headlines: Fraunces (variable serif)
- Body: Inter (variable sans)
- Stats: JetBrains Mono

---

## Variant B — Quiet Tech / Data-Forward

**60-second pitch for the client:**

> *"This direction positions Havoc as the most transparent, most measurable agency. Think Linear or Vercel — calm, technical, dashboard-feeling. Crisp white with near-black and a muted indigo accent. Geometric sans throughout, tabular numerals everywhere stats appear. Bento grid for services, data-tile case studies, dashboard-style pricing cards. There's even a 'system status' dot in the footer. Best fit if Havoc's audience is data-literate founders, SaaS clients, and modern e-commerce — buyers who want dashboards, not decks."*

**What the client should notice:**
1. The hero — playful italic accent on "measured." Positions the *insight*, not the company.
2. The four data tiles immediately below the hero — instant proof, before you scroll.
3. The bento services grid — irregular, modern, with the SEO card highlighted as a feature.
4. The methodology section with arrows between phases — feels like a product diagram.
5. The split contact — form on one side, channels and city info on the other. SaaS-standard pattern.
6. The footer status indicator — pulses gently. Subtle, but signals "we're alive and operational."

**Visual specs:**
- Background: crisp white `#FCFCFC`
- Foreground: near-black `#0A0A0A`
- Accent: muted indigo `#5B6CFF`
- Headlines: Geist (variable geometric sans)
- Body: Inter
- Stats: JetBrains Mono with tabular numerals

---

## Side-by-side comparison

| Dimension | Variant A — Editorial Authority | Variant B — Quiet Tech |
|---|---|---|
| **Audience signal** | "We're senior strategists" | "We're transparent data-shop" |
| **Closes well with** | Founder-led SMBs, professional services | Tech-forward SMBs, SaaS, DTC |
| **Hero archetype** | Single statement, no image | Statement + animated stat row |
| **Services display** | 3-column editorial list | Bento grid (6 cards, irregular) |
| **Case studies** | Pull-quote spreads (3, full-width) | Data tiles (4, metric-first) |
| **Pricing** | Editorial tier cards with arrow bullets | Dashboard cards with check bullets, "Most popular" |
| **Vibe in two words** | Confident, restrained | Modern, measurable |
| **Risk** | Could feel "boring" to flashy buyers | Could feel "templated" if rendered poorly |
| **Strength** | Highest-quality look on minimal assets | Strong recall, clear data story |

---

## Feedback to gather from the client

Ask these in order. Don't accept "I like both" — force a choice.

1. **Gut reaction (10 seconds each)** — Which one would they want their *competitor* to use? (This often reveals the truer preference faster than asking which they want.)
2. **Audience fit** — Picture a real prospect calling tomorrow. Which version makes them say "these are my people"?
3. **Color** — Forest green (A) or indigo (B) — does either one repel them? (We can substitute the accent if so.)
4. **Typography** — Editorial serif headlines (A) vs geometric sans (B) — opinion?
5. **Case study format** — Pull quotes (A) or data tiles (B) — which feels more like *their* story?
6. **One thing they'd change** — Open question. Listen for vetoes.
7. **One thing they'd keep regardless of which direction wins** — This identifies the few non-negotiables.
8. **Deal-breakers** — Anything missing that they think *must* be there before the WordPress build.

---

## Client decision matrix

Send this with the link to both mockups before the meeting. They fill it out, you have a structured discussion.

| Criterion | Variant A | Variant B | Notes |
|---|---|---|---|
| Reflects how I want to be perceived | ☐ | ☐ |  |
| Speaks to my ideal client | ☐ | ☐ |  |
| Color palette feels right | ☐ | ☐ |  |
| Typography feels right | ☐ | ☐ |  |
| Showcases our work effectively | ☐ | ☐ |  |
| Pricing presentation is clean | ☐ | ☐ |  |
| Founder section gives appropriate weight | ☐ | ☐ |  |
| **Overall preference** | ☐ | ☐ |  |

---

## Open questions the client must answer before WordPress conversion

These are not blockers for the mockups, but they will shape the production build. Capture answers in this meeting if possible:

1. **Real testimonials** — current site has a "Love from Clients" header but no testimonial bodies. Need 5–8 real testimonials with permission.
2. **Certification badges** — Google Partner / Meta Business Partner / GA4 — supply real badge images.
3. **Founder photo** — professional headshot of Ben Miranda required.
4. **Office addresses** — full street addresses for each of the 4 cities (we only have city names + phone numbers right now).
5. **Pricing currency** — which region's $? Or display per-region?
6. **Blog plan** — last current post is July 2024. Commit to content cadence (recommendation: 2 posts/month minimum) or remove blog from main nav?
7. **Hosting / WordPress stack** — managed (Kinsta / WP Engine) vs unmanaged. Affects performance baseline.
8. **Analytics** — GA4 + Google Search Console must be reconfigured. Add Plausible or similar privacy-first secondary?

---

## What's already SEO/GEO-locked in (both variants)

The client doesn't need to ask for these — they're built in:

- ✅ Single `<h1>` per page, semantic H2-H4 hierarchy
- ✅ 6 JSON-LD schema blocks: Organization, WebSite+SearchAction, Person (Ben Miranda), 4× LocalBusiness, FAQPage, OfferCatalog
- ✅ Open Graph + Twitter Card meta for rich link previews
- ✅ Hreflang tags for `en-AU`, `en-GB`, `en-US`, `en` (default)
- ✅ Modern Core Web Vitals discipline: no carousels, lazy-loadable images, system font fallback, `text-wrap: balance`/`pretty`
- ✅ WCAG 2.2 AA: 2.5rem+ target sizes, focus rings with 3:1 contrast, skip-to-content link
- ✅ AI search optimization: definition-style FAQ, first-sentence-optimized sections, FAQ schema, llms.txt + llms-full.txt at site root
- ✅ AI crawler-friendly robots.txt (GPTBot, ClaudeBot, PerplexityBot, Google-Extended, etc. all allowed)
- ✅ View Transitions API for smooth page-to-page nav
- ✅ Container queries for component-level responsiveness
- ✅ Auto dark-mode support via `prefers-color-scheme`
- ✅ `prefers-reduced-motion` respected on all animation

---

## Next steps after the client picks a direction

1. **Capture decisions** — fill in the Open Questions above with real answers.
2. **WordPress conversion** — build a Gutenberg block theme matching the chosen variant. ~2 weeks.
3. **Content production** — testimonials, case study writeups, founder photo, blog refresh (recommend a 2-post-per-month cadence going forward).
4. **Migration plan** — 301 redirect mapping from current site URLs, schema validation, GSC re-verification.
5. **Performance baseline** — Lighthouse audit on the live WordPress site, compare against the static mockup baseline. Targets: Performance 90+, Accessibility 100, Best Practices 100, SEO 100.
6. **Launch checklist** — sitemap submission, GSC re-indexing, analytics validation, schema validation in real environment.

---

## Files in this project

```
HOVC Digital/
├── docs/plans/
│   ├── 2026-05-07-havoc-digital-redesign-design.md    ← strategic design doc
│   └── 2026-05-07-havoc-digital-redesign-plan.md       ← implementation plan
├── mockups/
│   ├── README.md                                        ← this file
│   ├── variant-a-editorial/
│   │   ├── index.html
│   │   ├── styles.css
│   │   └── assets/
│   └── variant-b-quiet-tech/
│       ├── index.html
│       ├── styles.css
│       └── assets/
└── shared-seo/
    ├── llms.txt                  ← AI agent index
    ├── llms-full.txt             ← full content for AI ingestion
    ├── robots.txt                ← AI crawler allow-list
    └── schema-snippets.json      ← reusable JSON-LD library
```

---

*Questions about the mockups? Open the design doc at `docs/plans/2026-05-07-havoc-digital-redesign-design.md` for the full strategic rationale.*
