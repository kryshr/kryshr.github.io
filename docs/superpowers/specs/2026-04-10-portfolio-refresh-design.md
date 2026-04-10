# Portfolio Refresh — April 2026

**Date:** 2026-04-10
**Scope:** Single-pass refresh of `index.html`. Adds a new featured project, rewrites the hero, restructures the featured-projects lineup, rewrites all featured project descriptions in an impact-first style, and prunes the More Work section.
**Driver:** Lead recruiters with concrete numbers and senior-level impact, not generic titles or feature lists.

---

## Goals

1. Lead the page with a defensible revenue number, not a job title.
2. Add the strongest piece of work (Predictive Customer Intelligence Engine) as the new hero project.
3. Rewrite all featured project descriptions to lead with what each system *replaced* and the *measurable outcome*, not architecture.
4. Reorder featured projects so they progress from highest-impact ML work down to supporting tooling.
5. Demote the personal Ecommerce project from Featured to More Work — it dilutes the AI/data-engineering signal.
6. Cut graduate coursework from More Work for the same reason.
7. No real employer data appears in mockups (existing constraint preserved).

---

## Non-Goals

- No new pages, sections, or files beyond editing `index.html`.
- No framework introduction. The site stays plain HTML/CSS/JS.
- No changes to analytics, Discord webhook, contact form, or Cloudflare worker.
- No changes to the Anomaly Detection mockup, the NL-to-SQL mockup, or the Ecommerce mockup. Only the new ML card and the Q4 Reporting card need new mockups.

---

## Section 1 — Hero rewrite

### Current

```
Badge:   Miami, FL · AI & Data Science
H1:      Krysh Rajendran
Sub:     AI & Data Science Engineer
Tagline: I build intelligent systems that turn data into decisions —
         from NL-to-SQL agents and real-time anomaly detection
         to full-stack ecommerce platforms.
```

The current hero leads with a job title, not a hook. A recruiter scanning for 5 seconds gets a generic descriptor, not a reason to keep reading.

### New

```
Badge:   Miami, FL · AI & Data Science    (unchanged)
H1:      Krysh Rajendran                  (unchanged)
Sub:     AI Engineer. Built production ML systems projected to drive
         $15M+ in incremental e-commerce revenue.
Tagline: (removed)
```

### Decisions

- The metric hook lives in `.hero-sub`. The existing `.hero-tagline` element is removed entirely.
- The `$15M+` figure is not anchored to a named employer. Per user instruction, no employer name appears in the hero, even though the underlying work is real.
- Number is bold and styled to draw the eye. Surrounding text is muted to highlight the metric.
- CTAs (`View Projects`, LinkedIn link) are unchanged.

---

## Section 2 — Featured Projects (new lineup)

The featured-projects section keeps four cards. The lineup, in order, is:

1. **Predictive Customer Intelligence Engine** (NEW — stacked hero layout)
2. **NL-to-SQL AI Agent** (existing — demoted from #1, becomes side-by-side)
3. **Real-Time Anomaly Detection Dashboard** (existing — stays at #3, side-by-side, mockup unchanged)
4. **Automated Executive Reporting Engine** (REPLACES the existing "Automated Report Pipeline" card — side-by-side, new mockup)

The Full-Stack Ecommerce Platform is removed from Featured and added to More Work as a mini-card.

### Card #1 — Predictive Customer Intelligence Engine *(NEW HERO)*

**Layout:** Stacked (`agent-card` class — full-width mockup below info), matching the current NL-to-SQL hero structure.

**Title:** Predictive Customer Intelligence Engine

**Description:**

> Identified $15M+ in projected incremental revenue by replacing blanket post-booking outreach with weekly ML-scored audiences across 7 ancillary product categories. Trained 7 H2O AutoML classifiers on 2.2M historical browsing events, then routed each booking into a tiered marketing action — high intent gets a reminder, low-medium gets a promotional offer, and the rest fall out. A deterministic 80/20 target/control split lets the team measure true lift.

**Impact bullets (3):**

| Value | Label |
|---|---|
| `$15M+` | Projected Annual Incremental Revenue |
| `0.89 AUC` | Peak Model Performance |
| `12K/wk` | Bookings Scored |

**Tags:** Python · H2O AutoML · GBM · BigQuery · scikit-learn · Feature Engineering · A/B Testing

### Card #2 — NL-to-SQL AI Agent *(existing — demoted from #1)*

**Layout:** Side-by-side. The `agent-card` class moves off this card and onto Card #1.

**Title:** NL-to-SQL AI Agent (unchanged)

**Description (NEW):**

> Replaced **4 hours** of daily manual reporting with a conversational analytics agent that handles **80%** of ad-hoc data questions across the post-booking e-commerce team. Translates business questions into BigQuery SQL, runs the queries, and writes the insight bullets back. A Deep Analysis mode runs a 6-phase root-cause loop (Decompose → Temporal → Segment → Drill → Confirm → Conclude) up to 10 steps deep, tracking hypotheses across iterations and exiting early when the answer is clear.

**Impact bullets:** `60%` Reporting Automated · `10-step` Autonomous Reasoning *(unchanged)*

**Tags (UPDATED):** Python · Claude Opus 4.6 · BigQuery · Plotly · Streamlit

**Mockup:** unchanged.

### Card #3 — Real-Time Anomaly Detection Dashboard *(existing — stays at #3)*

**Layout:** Side-by-side (unchanged).

**Title:** Real-Time Anomaly Detection Dashboard (unchanged)

**Description (NEW):**

> Replaced a 30-minute Power BI refresh and "stare-at-charts" monitoring with a custom hourly anomaly detection dashboard for 5–10 internal users. Tracks Shoppers, Purchasers, and CVR against statistical baselines using two methods (Prior-5-Week and Rolling-Days), with three severity tiers, automatic crash detection, and a red/amber/green health banner that loads in under a second. A background daemon refreshes data server-side every hour so operators always see fresh numbers.

**Impact bullets (UPDATED):**

| Value | Label |
|---|---|
| `30min → 1min` | Refresh Time (30x faster) |
| `$54 vs $4,995` | Monthly Cost (vs Power BI Premium) |
| `3-Tier` | Severity System |

**Tags (UPDATED):** Python · Streamlit · BigQuery · Cloud Run · GCS · Plotly · Cloud Build

**Mockup:** unchanged.

### Card #4 — Automated Executive Reporting Engine *(REPLACES old Report Pipeline)*

**Layout:** Side-by-side. Replaces the existing "Automated Report Pipeline" card content and mockup entirely.

**Title:** Automated Executive Reporting Engine

**Description:**

> Replaced days of manual quarterly reporting with an automated pipeline that pulls category-level data from BigQuery, computes YoY deltas across Revenue, Shoppers, Purchasers, CVR, and RPPS, then generates the executive narrative with Claude. Surfaces category-level drivers and action items that would otherwise get missed in a manual scrub — and the narrative quality stays consistent regardless of who runs it.

**Impact bullets (3):**

| Value | Label |
|---|---|
| `Days → Minutes` | Reporting Turnaround |
| `AI-Authored` | Executive Narrative |
| `5 KPIs · 7 Categories` | YoY Coverage |

**Tags:** Python · Claude API · BigQuery · Pandas · Parquet

**Mockup:** new — see Section 3.

---

## Section 3 — Mockup designs

Two new mockups are required: Card #1 (new ML project) and Card #4 (Q4 Reporting). All other mockups stay as-is.

### Mockup A — Predictive Customer Intelligence Engine *(Card #1, stacked hero)*

**Browser frame label:** `Northwind Voyages — Customer Intelligence Console`

Northwind Voyages is a fabricated cruise-line brand. No real employer numbers or terms appear in the mockup; the cruise context provides domain texture only.

**Layout:** Sidebar + main panel inside `mockup-frame`, mirroring the current NL-to-SQL hero's `chat-top` structure for visual consistency.

**Left sidebar (~22% width)**

- Brand wordmark: `NorthwindVoyages`
- `Week` label → select showing `2026-W15`
- `Categories` label → 7 small chips: Photo, Beverage, Spa, Internet, Excursions, Dining, Delights
- `Tier` label → toggle: **High** / Medium / Low-Med / Low (High active)
- `DTD Window` label → `4–30 days`
- `T/C Split` label → `80 / 20`
- Footer stats: `12,047 scored` · `~10,000 targeted`

**Main panel — three sections**

1. **Model Performance card** (top)
   - Big number: `0.89 AUC`
   - Subtitle: `Peak performance · 7 GBM classifiers · H2O AutoML · out-of-time validated`
   - Chip row underneath: 7 small category pills (Photo, Beverage, Spa, Internet, Excursions, Dining, Delights)
   - Single hero stat instead of a per-category leaderboard — keeps the focus on the headline number.

2. **Weekly Targeting Funnel** (middle)
   - Header: *Weekly Targeting Funnel*
   - Three horizontal stage blocks shrinking left-to-right:
     - `49,000` Browse Pool (full width)
     - `12,047` In DTD Window (4–30 days) (~25% width)
     - `~10,000` Eligible Targets (after 80/20 holdout) (~20% width)
   - Each stage has its count and label; arrows or chevrons connect them.

3. **Tier → Action Map** (bottom)
   - Compact 4-row table:

| Tier | Action |
|---|---|
| High | Evergreen reminder (no discount) |
| Medium | Soft nudge |
| Low-Medium | Promotional offer *(incremental play)* |
| Low | Suppress (no email) |

**Bottom action bar:** `▶ Generate Weekly Target List` button + `📥 Export CSV` button (right-aligned).

**Color treatment:** blue for primary chrome and bars, green for positive deltas, subtle purple tint on the funnel only (matches existing data-viz convention). All chrome uses existing `mockup-frame` / glass-card styling and CSS variables.

### Mockup B — Automated Executive Reporting Engine *(Card #4)*

**Browser frame label:** `Q4 Executive Brief — generated 2026-04-08`

**Layout:** A document/email-style mockup, distinct from the existing daily-report mockup it replaces. Different shape, different content density.

**Sections inside the mockup body:**

1. **Header strip**
   - Title: `Q4 2025 vs Q4 2024 — Executive Brief`
   - Right side: small badge `✨ Auto-generated by Q4 Reporting Pipeline`

2. **KPI row** — 5 small cards across the top:
   - Revenue, Shoppers, Purchasers, CVR, RPPS
   - Each with a YoY delta (up/down) in green or red
   - Specific numbers are illustrative and use the fabricated Northwind/Acme convention

3. **Category YoY table** — 4 visible rows, drawn from real findings in the source material:

| Category | Metric | YoY |
|---|---|---|
| Beverage Package | Revenue | **+435%** *(green)* |
| Premium Extra Drink Pkg | Revenue | *breakthrough — large green delta* |
| Excursions | CVR | **−11%** *(red, footnote: "product mix shift")* |
| Internet | Revenue | *neutral* |

4. **Narrative block** — styled to look LLM-generated, with a small `✨ Auto-generated` badge in the corner. Two short paragraphs of executive summary text drawn from the real findings (Beverage growth driver, premium drink pkg breakthrough, excursion mix shift).

5. **Footer:** `Action Items` chip row with 3 short bullet items.

**Color treatment:** matches existing email/document mockups (Card #4 was navy + gold; the new one drops navy/gold and uses the site's neutral blue scheme since this is a new project unrelated to the old MSC reporting work).

---

## Section 4 — More Work changes

### Cut (4 grad cards)

These dilute the senior-level signal. Recruiters scanning the More Work section see "Graduate" badges and downgrade the whole page.

- NLP Bias Detection
- Alzheimer's MRI Classification
- Flight Delay Prediction
- Heart Disease Prediction

### Add (1 card, demoted from Featured)

- **Full-Stack Ecommerce Platform** — moves from Featured to More Work as a mini-card. Keeps the existing description text and the `Personal` badge.

### Result

More Work goes from 9 cards to 6:

1. Resume Builder
2. Job Application Automation
3. Promo Calendar ETL
4. SAP BO Booking Pipeline
5. Weekly Tracker Email
6. Full-Stack Ecommerce Platform *(moved in, with `Personal` badge)*

---

## Section 5 — Implementation notes

### Files touched

- `index.html` — single-file edit, all changes in one pass.
- `docs/superpowers/specs/2026-04-10-portfolio-refresh-design.md` — this spec.

No other files are created, modified, or deleted.

### CSS considerations

- The new 3-impact-bullet rows (Cards #1 and #3) need to render correctly at 393px (iPhone 15 Pro). The current `.impact-row` is 2-up. A 3-up row may need `flex-wrap`, smaller font, or a stacked-on-mobile fallback. Verify with Playwright at 393px before committing.
- Hero `.hero-tagline` element is removed entirely. `.hero-sub` styling may need a slight adjustment to handle the longer two-sentence metric hook.
- The `agent-card` class moves from the NL-to-SQL card onto the new ML card. NL-to-SQL must look correct as a side-by-side card after the demotion.

### Workflow — review before deploy

The user wants to verify in a local browser before anything is pushed.

1. Edit `index.html` locally — all changes in one pass.
2. Start a local web server: `python -m http.server 8000` from the project root. Hand the URL to the user.
3. Run Playwright screenshots at desktop and 393px for a quick visual check before handing back.
4. **User approves in the browser.** Until then: no commit, no push, no deploy.
5. After approval: commit to `main` and push. GitHub Pages auto-deploys (~30s).
6. Final live verification on `https://kryshr.github.io`.

### Rollback

Git history is the rollback. No `versions/pre-refresh-*.html` snapshot is created — `versions/` is for design alternatives, not safety nets.

---

## Open risks

1. **Mobile 3-impact-bullet layout.** Three impact bullets on a 393px screen may be tight. Mitigation: verify with Playwright before committing; fall back to 2-bullet rows or stacked layout if needed.
2. **Mockup numbers are illustrative.** The Northwind Voyages cruise frame and the Executive Brief mockup both use fabricated company names and illustrative numbers, matching the existing convention across all other mockups on the site. No real employer data appears anywhere.
