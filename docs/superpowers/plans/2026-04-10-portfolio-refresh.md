# Portfolio Refresh Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Refresh `index.html` with a new featured ML project, a metric-led hero hook, impact-first project descriptions, a reordered featured-projects lineup, and a pruned More Work section — verified locally before pushing to production.

**Architecture:** Single-file edits to `index.html`. No new files except this plan and the previously committed spec. All mockups remain inline SVG/HTML following the existing convention. New CSS classes are added for the Q4 exec brief mockup, the 3-impact-bullet row, and the new ML console mockup. No framework, no build step.

**Tech Stack:** Plain HTML, CSS, vanilla JS, inline SVG. Python `http.server` for local preview. Playwright (already in user's workflow) for desktop + mobile screenshot verification.

**Spec:** `docs/superpowers/specs/2026-04-10-portfolio-refresh-design.md`

---

## File Structure

**Modified:**
- `index.html` — all changes happen here
  - Lines ~569–578: Hero section (Section 1 of spec)
  - Lines ~585–965: Featured Projects section (Sections 2 + 3 of spec)
  - Lines ~967–1024: More Work section (Section 4 of spec)
  - Lines ~108–500: CSS additions for new mockups + 3-bullet row mobile fallback

**Created:** none

**Reference (do not modify):**
- `docs/superpowers/specs/2026-04-10-portfolio-refresh-design.md` — the source of truth for content and layout

---

## Working Conventions

- **No TDD.** This is static HTML/CSS. The "test" is visual verification in a local browser at desktop (1440px) and mobile (393px iPhone 15 Pro). Each task ends with a screenshot check.
- **Local preview server runs throughout.** Started in Task 1, keeps running until Task 11.
- **Commit per task.** Small, focused commits.
- **Do not push** until Task 11 (user approval gate). The user explicitly wants to verify locally before deploy.
- **Use Playwright** for screenshots, not visual inspection alone — the user has Playwright in their workflow per CLAUDE.md.
- **Preserve all existing analytics, Discord webhook, and contact form code.** Do not touch any `<script>` block.

---

## Task 1: Local preview setup + baseline screenshots

**Files:**
- No code changes. Operational setup only.

- [ ] **Step 1: Start local web server in background**

```bash
cd "C:/Users/krysh/OneDrive - MSC Cruises SA/Documents/Work/Portfolio"
python -m http.server 8765
```

Run with `run_in_background: true`. The server stays up for the rest of the session.

- [ ] **Step 2: Take baseline desktop screenshot**

Use Playwright MCP to navigate and screenshot:
- Navigate to `http://localhost:8765/`
- Set viewport to 1440x900
- Take a full-page screenshot, save reference as "baseline-desktop"

- [ ] **Step 3: Take baseline mobile screenshot**

- Resize viewport to 393x852 (iPhone 15 Pro)
- Take a full-page screenshot, save reference as "baseline-mobile"

- [ ] **Step 4: Visual sanity check**

Confirm the baseline screenshots show: 4 featured project cards in current order (NL-to-SQL stacked, Anomaly, Report Pipeline, Ecommerce), 9 More Work cards (4 with `Graduate` badge), current hero with title-led copy. If anything looks broken, stop and investigate before proceeding.

- [ ] **Step 5: No commit** — this task makes no file changes.

---

## Task 2: Hero hook rewrite

**Files:**
- Modify: `index.html` (hero section, lines ~569–578)

- [ ] **Step 1: Read the current hero block**

Read `index.html` lines 565–585 to get the exact text and indentation of the hero block.

- [ ] **Step 2: Replace the hero sub + remove the tagline**

Find this block:

```html
<section class="hero">
  <div class="hero-inner">
    <div class="hero-badge">Miami, FL &middot; AI & Data Science</div>
    <h1 style="color:#fff">Krysh Rajendran</h1>
    <p class="hero-sub">AI & Data Science Engineer</p>
    <p class="hero-tagline">I build intelligent systems that turn data into decisions — from NL-to-SQL agents and real-time anomaly detection to full-stack ecommerce platforms.</p>
```

Replace with:

```html
<section class="hero">
  <div class="hero-inner">
    <div class="hero-badge">Miami, FL &middot; AI & Data Science</div>
    <h1 style="color:#fff">Krysh Rajendran</h1>
    <p class="hero-sub">AI Engineer. Built production ML systems projected to drive <strong style="color:#fff">$15M+</strong> in incremental e-commerce revenue.</p>
```

Note: The `.hero-tagline` `<p>` element is removed entirely. The `<strong>` element bolds and brightens `$15M+` to draw the eye.

- [ ] **Step 3: Adjust .hero-sub CSS to handle the longer two-sentence copy**

Find this CSS rule (around line 120):

```css
.hero-sub { font-size: 18px; color: var(--muted); font-weight: 500; margin-bottom: 12px; letter-spacing: -.3px; }
```

Replace with:

```css
.hero-sub { font-size: 18px; color: var(--muted); font-weight: 500; margin-bottom: 32px; letter-spacing: -.3px; line-height: 1.5; max-width: 560px; margin-left: auto; margin-right: auto; }
```

Changes: `margin-bottom: 12px → 32px` (replaces the gap previously held by `.hero-tagline`), `line-height: 1.5` for two-line readability, `max-width: 560px` and centered margins so the line breaks gracefully.

- [ ] **Step 4: Reload and screenshot at desktop**

Reload `http://localhost:8765/` in Playwright. Viewport 1440x900. Screenshot the hero region (top of page).

Expected: Title "Krysh Rajendran" → metric line below it with `$15M+` bolded white → CTA buttons. No third tagline line.

- [ ] **Step 5: Reload and screenshot at mobile**

Resize viewport to 393x852. Screenshot the hero region.

Expected: Same content, wrapped to fit phone width, CTAs stack vertically (existing mobile rule already handles this).

- [ ] **Step 6: Commit**

```bash
cd "C:/Users/krysh/OneDrive - MSC Cruises SA/Documents/Work/Portfolio"
git add index.html
git commit -m "$(cat <<'EOF'
Replace hero tagline with $15M+ metric hook

Lead with a concrete revenue number instead of a generic job title.
The new sub line bolds the dollar figure to draw the eye on a 5-second
recruiter skim.

Co-Authored-By: Claude Opus 4.6 (1M context) <noreply@anthropic.com>
EOF
)"
```

---

## Task 3: Update Anomaly Detection card (description + impact bullets + tags)

**Files:**
- Modify: `index.html` (Card #2 in current lineup, around lines 723–812)

This task updates content only. The mockup stays as-is.

- [ ] **Step 1: Read the current card**

Read `index.html` lines 723–740 to confirm the exact existing markup of the project-info block.

- [ ] **Step 2: Replace description, impact bullets, and tags**

Find:

```html
<div class="project-info">
  <h3>Real-Time Anomaly Detection Dashboard</h3>
  <p>Production monitoring dashboard tracking hourly e-commerce KPIs with statistical anomaly detection. Uses sigma bands against prior-5-week baselines, 3-tier severity classification, crash detection, and multi-dimensional drill-down. Deployed on Google Cloud Run.</p>
  <div class="impact-row">
    <div class="impact-item"><div class="impact-value accent">1.5hr &rarr; 3min</div><div class="impact-label">Data Refresh Time</div></div>
    <div class="impact-item"><div class="impact-value accent">3-Tier</div><div class="impact-label">Severity System</div></div>
  </div>
  <div class="tags">
    <span class="tag">Python</span><span class="tag">Streamlit</span><span class="tag">BigQuery</span>
    <span class="tag">Cloud Run</span><span class="tag">Plotly</span><span class="tag">Statistical Analysis</span>
  </div>
</div>
```

Replace with:

```html
<div class="project-info">
  <h3>Real-Time Anomaly Detection Dashboard</h3>
  <p>Replaced a 30-minute Power BI refresh and "stare-at-charts" monitoring with a custom hourly anomaly detection dashboard for 5&ndash;10 internal users. Tracks Shoppers, Purchasers, and CVR against statistical baselines using two methods (Prior-5-Week and Rolling-Days), with three severity tiers, automatic crash detection, and a red/amber/green health banner that loads in under a second. A background daemon refreshes data server-side every hour so operators always see fresh numbers.</p>
  <div class="impact-row impact-row-3">
    <div class="impact-item"><div class="impact-value accent">30min &rarr; 1min</div><div class="impact-label">Refresh (30x faster)</div></div>
    <div class="impact-item"><div class="impact-value accent">$54 vs $4,995</div><div class="impact-label">Monthly Cost</div></div>
    <div class="impact-item"><div class="impact-value accent">3-Tier</div><div class="impact-label">Severity System</div></div>
  </div>
  <div class="tags">
    <span class="tag">Python</span><span class="tag">Streamlit</span><span class="tag">BigQuery</span>
    <span class="tag">Cloud Run</span><span class="tag">GCS</span><span class="tag">Plotly</span><span class="tag">Cloud Build</span>
  </div>
</div>
```

Note the new `impact-row-3` modifier class on the impact-row — this is added so we can target 3-bullet rows specifically in CSS later (Task 9). It's harmless if no CSS targets it yet.

- [ ] **Step 3: Reload and screenshot the card at desktop**

Reload `http://localhost:8765/`. Viewport 1440x900. Screenshot the Anomaly Detection card region.

Expected: New description, three impact bullets in a row (refresh, cost, severity), updated tag list including GCS and Cloud Build.

- [ ] **Step 4: Note any wrap issues**

If the three impact bullets visibly overflow or wrap awkwardly at 1440px desktop, note it but don't fix yet — Task 9 handles the 3-bullet row CSS. If they fit fine on desktop, continue.

- [ ] **Step 5: Commit**

```bash
git add index.html
git commit -m "$(cat <<'EOF'
Rewrite Anomaly Detection card with impact-first description

Lead with what was replaced (30-min Power BI refresh) and the cost
delta ($54 vs $4,995/month). Adds GCS and Cloud Build tags. Marks the
impact row with impact-row-3 for the 3-bullet mobile fallback.

Co-Authored-By: Claude Opus 4.6 (1M context) <noreply@anthropic.com>
EOF
)"
```

---

## Task 4: Replace Report Pipeline card with Automated Executive Reporting Engine

**Files:**
- Modify: `index.html` (Card #3 in current lineup, around lines 813–879)
- Modify: `index.html` (CSS section, add new classes for the 5-KPI exec layout)

This task replaces both the project-info content AND the entire mockup. It's the largest single edit in the plan.

- [ ] **Step 1: Add new CSS classes for the executive brief mockup**

Find the existing email mockup CSS block (around line 340, just after `.email-header`):

```css
.email-header {
```

Insert these new classes immediately *before* `.email-header` (so they live in the same visual region of the file):

```css
/* ── Executive Brief Mockup (Q4 Reporting) ── */
.exec-header {
  display: flex; justify-content: space-between; align-items: center;
  padding: 12px 16px; background: linear-gradient(135deg, rgba(59,130,246,.08), rgba(139,92,246,.04));
  border-bottom: 1px solid var(--border);
}
.exec-header strong { color: #fff; font-size: 12px; letter-spacing: -.2px; }
.exec-badge {
  font-size: 9px; color: var(--blue-bright); padding: 3px 8px;
  background: rgba(59,130,246,.1); border: 1px solid rgba(59,130,246,.2);
  border-radius: 100px; font-weight: 600;
}
.exec-body { padding: 14px; }
.exec-kpis { display: grid; grid-template-columns: repeat(5, 1fr); gap: 6px; margin-bottom: 12px; }
.exec-kpi {
  padding: 8px 6px; background: rgba(255,255,255,.03);
  border: 1px solid var(--border); border-radius: 6px; text-align: center;
}
.exec-kpi-label { font-size: 7px; color: #555; text-transform: uppercase; letter-spacing: .5px; }
.exec-kpi-val { font-size: 13px; font-weight: 700; color: #fff; margin: 2px 0; }
.exec-kpi-delta { font-size: 8px; font-weight: 600; }
.exec-section-title { font-size: 9px; color: #555; text-transform: uppercase; letter-spacing: 1px; margin: 10px 0 6px; font-weight: 600; }
.exec-yoy-table { width: 100%; border-collapse: collapse; font-size: 10px; margin-bottom: 10px; }
.exec-yoy-table th { text-align: left; padding: 4px 6px; color: #555; font-weight: 600; font-size: 9px; text-transform: uppercase; letter-spacing: .5px; border-bottom: 1px solid var(--border); }
.exec-yoy-table td { padding: 5px 6px; color: #aaa; border-bottom: 1px solid rgba(255,255,255,.04); }
.exec-yoy-table .delta-up { color: var(--green); font-weight: 600; }
.exec-yoy-table .delta-down { color: var(--red); font-weight: 600; }
.exec-narrative {
  position: relative;
  background: rgba(59,130,246,.04);
  border-left: 3px solid var(--blue);
  border-radius: 0 6px 6px 0;
  padding: 10px 12px 10px 12px;
  font-size: 10px; color: #aaa; line-height: 1.55;
  margin-bottom: 10px;
}
.exec-narrative .auto-tag {
  position: absolute; top: 6px; right: 8px;
  font-size: 8px; color: var(--blue-bright); font-weight: 600;
}
.exec-narrative p { margin: 0 0 6px 0; }
.exec-narrative p:last-child { margin: 0; }
.exec-actions { display: flex; gap: 6px; flex-wrap: wrap; }
.exec-action-chip {
  font-size: 9px; padding: 4px 10px;
  background: rgba(59,130,246,.06);
  border: 1px solid rgba(59,130,246,.15);
  border-radius: 100px; color: var(--blue-bright);
}
```

- [ ] **Step 2: Add a mobile fallback for the 5-KPI grid**

Find the existing mobile breakpoint block (around line 490 or 520, look for `.email-kpis { grid-template-columns: repeat(2, 1fr); }`).

Add this rule inside the same `@media (max-width: 600px)` block (locate the existing one near line 498 or 523 — there are two breakpoints, 900px and 600px; add to both if both have email-kpis overrides):

```css
.exec-kpis { grid-template-columns: repeat(3, 1fr); }
```

This collapses the 5-KPI row to 3-up on tablet/mobile (the 5th and 4th wrap to a second row). On desktop it stays 5-up.

- [ ] **Step 3: Read the current Card #3 (Report Pipeline) markup**

Read `index.html` lines 813–880 to get the exact current markup, including the `<div class="project-card glass reveal">` wrapper.

- [ ] **Step 4: Replace the entire Card #3 markup**

Find the entire `<!-- ═══ 3. Automated Report Pipeline ═══ -->` block from `<!-- ═══ 3. Automated Report Pipeline ═══ -->` through the closing `</div>` of that project-card (should end around line 879, just before `<!-- ═══ 4. Full-Stack Ecommerce Platform ═══ -->`).

Replace with:

```html
    <!-- ═══ 3. Automated Executive Reporting Engine ═══ -->
    <div class="project-card glass reveal">
      <div class="project-layout">
        <div class="project-info">
          <h3>Automated Executive Reporting Engine</h3>
          <p>Replaced days of manual quarterly reporting with an automated pipeline that pulls category-level data from BigQuery, computes YoY deltas across Revenue, Shoppers, Purchasers, CVR, and RPPS, then generates the executive narrative with Claude. Surfaces category-level drivers and action items that would otherwise get missed in a manual scrub &mdash; and the narrative quality stays consistent regardless of who runs it.</p>
          <div class="impact-row impact-row-3">
            <div class="impact-item"><div class="impact-value accent">Days &rarr; Minutes</div><div class="impact-label">Reporting Turnaround</div></div>
            <div class="impact-item"><div class="impact-value accent">AI-Authored</div><div class="impact-label">Executive Narrative</div></div>
            <div class="impact-item"><div class="impact-value accent">5 KPIs &middot; 7 Cats</div><div class="impact-label">YoY Coverage</div></div>
          </div>
          <div class="tags">
            <span class="tag">Python</span><span class="tag">Claude API</span>
            <span class="tag">BigQuery</span><span class="tag">Pandas</span>
            <span class="tag">Parquet</span>
          </div>
        </div>
        <div class="project-mockup">
          <div class="mockup-frame">
            <div class="mockup-bar">
              <span class="dot dot-r"></span><span class="dot dot-y"></span><span class="dot dot-g"></span>
              <span class="mockup-label">Q4 Executive Brief &mdash; generated 2026-04-08</span>
            </div>
            <div class="mockup-body">
              <div class="exec-header">
                <strong>Q4 2025 vs Q4 2024 &mdash; Executive Brief</strong>
                <span class="exec-badge">&#9889; Auto-generated</span>
              </div>
              <div class="exec-body">
                <div class="exec-kpis">
                  <div class="exec-kpi"><div class="exec-kpi-label">Revenue</div><div class="exec-kpi-val">$24.8M</div><div class="exec-kpi-delta" style="color:var(--green)">+18.2%</div></div>
                  <div class="exec-kpi"><div class="exec-kpi-label">Shoppers</div><div class="exec-kpi-val">142K</div><div class="exec-kpi-delta" style="color:var(--green)">+9.4%</div></div>
                  <div class="exec-kpi"><div class="exec-kpi-label">Purchasers</div><div class="exec-kpi-val">28.1K</div><div class="exec-kpi-delta" style="color:var(--green)">+12.7%</div></div>
                  <div class="exec-kpi"><div class="exec-kpi-label">CVR</div><div class="exec-kpi-val">19.8%</div><div class="exec-kpi-delta" style="color:var(--green)">+3.1pp</div></div>
                  <div class="exec-kpi"><div class="exec-kpi-label">RPPS</div><div class="exec-kpi-val">$174</div><div class="exec-kpi-delta" style="color:var(--green)">+5.6%</div></div>
                </div>
                <div class="exec-section-title">Category YoY Highlights</div>
                <table class="exec-yoy-table">
                  <thead>
                    <tr><th>Category</th><th>Metric</th><th>YoY</th><th>Note</th></tr>
                  </thead>
                  <tbody>
                    <tr><td>Beverage Package</td><td>Revenue</td><td class="delta-up">+435%</td><td>Premium pkg breakthrough</td></tr>
                    <tr><td>Premium Drink Pkg</td><td>Revenue</td><td class="delta-up">+212%</td><td>New SKU launched Q3</td></tr>
                    <tr><td>Excursions</td><td>CVR</td><td class="delta-down">&minus;11%</td><td>Product mix shift</td></tr>
                    <tr><td>Internet</td><td>Revenue</td><td class="delta-up">+4.2%</td><td>Stable</td></tr>
                  </tbody>
                </table>
                <div class="exec-narrative">
                  <span class="auto-tag">&#10024; Claude</span>
                  <p><strong>Q4 was driven primarily by Beverage Package growth (+435% YoY)</strong>, with the new Premium Drink package (launched in Q3) accounting for the bulk of the lift. CVR expansion of +3.1pp suggests intent quality is improving, not just volume.</p>
                  <p>The Excursions category warrants attention &mdash; CVR is down 11% YoY, traceable to a product mix shift toward higher-priced shore excursions that convert at a lower rate. Recommend revisiting the excursion landing page to surface mid-tier options.</p>
                </div>
                <div class="exec-section-title">Action Items</div>
                <div class="exec-actions">
                  <span class="exec-action-chip">Double down on Premium Drink promo</span>
                  <span class="exec-action-chip">Re-test Excursion landing mix</span>
                  <span class="exec-action-chip">Brief CRM on Q1 carryover</span>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
```

- [ ] **Step 5: Reload and screenshot the new card at desktop**

Reload `http://localhost:8765/`. Viewport 1440x900. Scroll to and screenshot Card #3 region.

Expected: New title "Automated Executive Reporting Engine", impact-first description, 3 impact bullets, document-style mockup with: header strip, 5 KPI cards in a row, category YoY table with green/red deltas, narrative block with `✨ Claude` tag in the corner, action item chips at the bottom.

- [ ] **Step 6: Reload and screenshot at mobile**

Resize viewport to 393x852. Screenshot the same card.

Expected: KPI grid collapses to 3-up (5th and 4th wrap to row 2), table is readable, narrative block fits, action chips wrap.

If anything overflows or looks broken, fix CSS now (don't defer). Common fixes:
- KPI numbers too large → reduce `.exec-kpi-val` font-size to 11px
- Table column widths uneven → add `table-layout: fixed` to `.exec-yoy-table`

- [ ] **Step 7: Commit**

```bash
git add index.html
git commit -m "$(cat <<'EOF'
Replace Report Pipeline card with Automated Executive Reporting Engine

Drops the daily HTML email mockup and adds a Q4 executive brief layout
with 5 KPI cards, YoY category table, Claude-authored narrative block,
and action item chips. Adds .exec-* CSS classes alongside the existing
.email-* classes (the email classes stay because the same file uses
them in a comment for reference).

Co-Authored-By: Claude Opus 4.6 (1M context) <noreply@anthropic.com>
EOF
)"
```

---

## Task 5: Demote NL-to-SQL Agent — restructure for side-by-side layout + impact-first description

**Files:**
- Modify: `index.html` (Card #1 in current lineup, around lines 591–721)

The NL-to-SQL card currently uses the `agent-card` class (stacked layout). After this task, that class moves to the new ML hero (Task 6), and NL-to-SQL becomes a side-by-side card matching Cards #3 and #4.

Critical: the NL-to-SQL info block currently uses the agent-card-specific structure (`project-info-inner`, `project-info-text`, `project-info-metrics`). When we drop `agent-card`, that nested structure no longer applies — we need to flatten it into the standard `.project-info` shape used by side-by-side cards.

- [ ] **Step 1: Read the current NL-to-SQL project-info block**

Read `index.html` lines 591–610 to confirm the exact existing markup.

- [ ] **Step 2: Replace the project-info block (drop agent-card structure, flatten to side-by-side)**

Find:

```html
    <!-- ═══ 1. NL-to-SQL Agent ═══ -->
    <div class="project-card glass reveal agent-card">
      <div class="project-layout">
        <div class="project-info">
          <div class="project-info-inner">
            <div class="project-info-text">
              <h3>NL-to-SQL AI Agent</h3>
              <p>Conversational analytics agent that translates natural language into BigQuery SQL, renders Plotly charts, and generates written insights. Features a 6-phase deep analysis pipeline with up to 10 autonomous reasoning steps.</p>
              <div class="tags">
                <span class="tag">Python</span><span class="tag">LangChain</span><span class="tag">LangGraph</span>
                <span class="tag">OpenAI</span><span class="tag">Anthropic</span><span class="tag">BigQuery</span>
                <span class="tag">Plotly</span><span class="tag">Streamlit</span>
              </div>
            </div>
            <div class="project-info-metrics">
              <div class="impact-item"><div class="impact-value accent">60%</div><div class="impact-label">Reporting Automated</div></div>
              <div class="impact-item"><div class="impact-value accent">10-step</div><div class="impact-label">Autonomous Reasoning</div></div>
            </div>
          </div>
        </div>
```

Replace with:

```html
    <!-- ═══ 2. NL-to-SQL Agent ═══ -->
    <div class="project-card glass reveal">
      <div class="project-layout">
        <div class="project-info">
          <h3>NL-to-SQL AI Agent</h3>
          <p>Replaced <strong>4 hours</strong> of daily manual reporting with a conversational analytics agent that handles <strong>80%</strong> of ad-hoc data questions across the post-booking e-commerce team. Translates business questions into BigQuery SQL, runs the queries, and writes the insight bullets back. A Deep Analysis mode runs a 6-phase root-cause loop (Decompose &rarr; Temporal &rarr; Segment &rarr; Drill &rarr; Confirm &rarr; Conclude) up to 10 steps deep, tracking hypotheses across iterations and exiting early when the answer is clear.</p>
          <div class="impact-row">
            <div class="impact-item"><div class="impact-value accent">60%</div><div class="impact-label">Reporting Automated</div></div>
            <div class="impact-item"><div class="impact-value accent">10-step</div><div class="impact-label">Autonomous Reasoning</div></div>
          </div>
          <div class="tags">
            <span class="tag">Python</span><span class="tag">Claude Opus 4.6</span><span class="tag">BigQuery</span>
            <span class="tag">Plotly</span><span class="tag">Streamlit</span>
          </div>
        </div>
```

Changes:
- Comment renumbered `1.` → `2.` (it becomes the second card after Task 6 inserts the new hero)
- `agent-card` class removed from the wrapper div
- `<div class="project-info-inner">` removed
- `<div class="project-info-text">` removed
- `<div class="project-info-metrics">` flattened into a regular `<div class="impact-row">` (so the 2 impact items render as a side-by-side row, matching Card #3 and #4)
- `<h3>`, `<p>`, `.impact-row`, `.tags` are now direct children of `.project-info`
- New impact-first description with bolded `4 hours` and `80%`
- Updated tags: drops LangChain, LangGraph, OpenAI, Anthropic — replaces with `Claude Opus 4.6`. Keeps Python, BigQuery, Plotly, Streamlit.

The mockup block (`<div class="project-mockup">...</div>`) below is left untouched.

- [ ] **Step 3: Reload and screenshot at desktop**

Reload `http://localhost:8765/`. Viewport 1440x900. Scroll to and screenshot the NL-to-SQL card region.

Expected: Side-by-side layout (info on left, mockup on right), title "NL-to-SQL AI Agent", new impact-first description with bolded "4 hours" / "80%", 2 impact bullets in a row, updated tag list. The chat mockup on the right should still render correctly — the `chat-layout` class is independent of `agent-card`.

- [ ] **Step 4: Verify mockup still renders**

Visually confirm the chat mockup (sidebar with presets, chat messages, deep stepper, bar chart, insight block, export buttons) still looks correct at the side-by-side narrower width. The mockup may look slightly more compressed than before but should not break.

If the mockup looks visibly broken (text overflow, SVG cropped), do not continue — investigate. Likely fix: the `.chat-layout` `height: 370px` may need to grow slightly. Adjust only if there's a real visible problem.

- [ ] **Step 5: Reload and screenshot at mobile**

Resize viewport to 393x852. Screenshot the same card.

Expected: Card stacks (info above mockup at mobile breakpoint, per existing CSS at line 535+). 2 impact bullets sit side-by-side per existing mobile rule.

- [ ] **Step 6: Commit**

```bash
git add index.html
git commit -m "$(cat <<'EOF'
Demote NL-to-SQL card to side-by-side, rewrite as impact-first

Drops the agent-card stacked layout in preparation for the new ML hero
project to take that slot. Flattens the project-info structure to match
the other side-by-side cards. Description now leads with 4 hours/80%
and tags drop LangChain in favor of Claude Opus 4.6.

Co-Authored-By: Claude Opus 4.6 (1M context) <noreply@anthropic.com>
EOF
)"
```

---

## Task 6: Insert new Card #1 — Predictive Customer Intelligence Engine

**Files:**
- Modify: `index.html` (insert before the NL-to-SQL card, around line 591)
- Modify: `index.html` (CSS section, add new classes for the targeting console mockup)

This is the largest mockup addition in the plan. Split into two commits — first the CSS, then the card.

### Subtask 6a: Add CSS for the targeting console mockup

- [ ] **Step 1: Insert new CSS classes**

Find this CSS block (around line 290, just before `.dash-layout` rule):

```css
/* ── Dashboard Mockup (Anomaly) ── */
.dash-layout {
```

Insert this block immediately *before* it:

```css
/* ── Targeting Console Mockup (Predictive Customer Intelligence) ── */
.tc-layout { display: flex; flex-direction: column; min-height: 420px; }
.tc-top { display: flex; flex: 1; min-height: 0; }
.tc-sidebar {
  width: 160px; min-width: 160px;
  background: rgba(255,255,255,.02);
  border-right: 1px solid var(--border);
  padding: 12px;
  display: flex; flex-direction: column; gap: 2px;
}
.tc-brand {
  font-weight: 700; font-size: 12px; color: #fff; text-align: center;
  padding-bottom: 8px; border-bottom: 1px solid rgba(59,130,246,.2); margin-bottom: 8px;
}
.tc-brand span { color: var(--blue-bright); }
.tc-chips { display: flex; flex-wrap: wrap; gap: 3px; margin-bottom: 4px; }
.tc-chip {
  font-size: 8px; padding: 2px 6px;
  background: rgba(59,130,246,.06);
  border: 1px solid rgba(59,130,246,.15);
  border-radius: 4px; color: var(--blue-bright);
}
.tc-tier-toggle {
  display: flex; border-radius: 5px; overflow: hidden;
  border: 1px solid rgba(59,130,246,.2); margin-bottom: 2px;
}
.tc-tier-toggle div {
  flex: 1; text-align: center; padding: 3px 2px; font-size: 8px; color: #666;
}
.tc-tier-toggle .active { background: rgba(59,130,246,.12); color: var(--blue-bright); font-weight: 600; }
.tc-stat-footer {
  margin-top: auto; padding-top: 8px; border-top: 1px solid var(--border);
  font-size: 9px; color: #888; line-height: 1.5;
}
.tc-stat-footer strong { color: #fff; }

.tc-main { flex: 1; padding: 14px; overflow-y: auto; display: flex; flex-direction: column; gap: 12px; }

.tc-perf-card {
  background: linear-gradient(135deg, rgba(59,130,246,.08), rgba(139,92,246,.04));
  border: 1px solid rgba(59,130,246,.2);
  border-radius: 8px; padding: 12px 14px;
}
.tc-perf-title { font-size: 9px; color: #555; text-transform: uppercase; letter-spacing: 1px; margin-bottom: 4px; font-weight: 600; }
.tc-perf-big { font-size: 24px; font-weight: 800; color: #fff; line-height: 1; margin-bottom: 4px; }
.tc-perf-big .accent-blue { color: var(--blue-bright); }
.tc-perf-sub { font-size: 9px; color: #888; margin-bottom: 8px; }
.tc-perf-pills { display: flex; flex-wrap: wrap; gap: 4px; }
.tc-perf-pill {
  font-size: 8px; padding: 2px 7px;
  background: rgba(255,255,255,.04);
  border: 1px solid var(--border);
  border-radius: 100px; color: #aaa;
}

.tc-funnel-card { padding: 0; }
.tc-funnel-title { font-size: 9px; color: #555; text-transform: uppercase; letter-spacing: 1px; margin-bottom: 6px; font-weight: 600; }
.tc-funnel-row { display: flex; align-items: center; gap: 6px; margin-bottom: 4px; }
.tc-funnel-bar {
  height: 22px;
  background: linear-gradient(90deg, var(--blue), rgba(139,92,246,.6));
  border-radius: 4px;
  display: flex; align-items: center; padding: 0 8px;
  color: #fff; font-size: 10px; font-weight: 700;
}
.tc-funnel-label { font-size: 9px; color: #888; min-width: 80px; }

.tc-tier-table { width: 100%; border-collapse: collapse; font-size: 10px; }
.tc-tier-table th { text-align: left; padding: 4px 6px; color: #555; font-weight: 600; font-size: 9px; text-transform: uppercase; letter-spacing: .5px; border-bottom: 1px solid var(--border); }
.tc-tier-table td { padding: 5px 6px; color: #aaa; border-bottom: 1px solid rgba(255,255,255,.04); }
.tc-tier-table .tier-high { color: var(--green); font-weight: 600; }
.tc-tier-table .tier-med { color: var(--blue-bright); font-weight: 600; }
.tc-tier-table .tier-lowmed { color: var(--gold); font-weight: 600; }
.tc-tier-table .tier-low { color: #555; font-weight: 600; }

.tc-action-bar {
  display: flex; gap: 6px; padding: 8px 12px;
  border-top: 1px solid var(--border); background: rgba(0,0,0,.3);
  justify-content: flex-end;
}
.tc-btn {
  font-size: 9px; padding: 5px 12px; border-radius: 5px;
  background: var(--blue); color: #fff; font-weight: 600;
  border: none; cursor: default;
}
.tc-btn-secondary {
  background: rgba(255,255,255,.05); color: #aaa;
  border: 1px solid var(--border);
}

@media (max-width: 600px) {
  .tc-top { flex-direction: column; }
  .tc-sidebar { width: 100%; min-width: 0; border-right: none; border-bottom: 1px solid var(--border); flex-direction: row; flex-wrap: wrap; gap: 8px; }
  .tc-brand { width: 100%; text-align: left; padding-bottom: 4px; margin-bottom: 4px; }
  .tc-stat-footer { width: 100%; margin-top: 4px; padding-top: 6px; }
}
```

- [ ] **Step 2: Reload to verify CSS parses without breaking other styles**

Reload `http://localhost:8765/`. Viewport 1440x900. Take a quick full-page screenshot.

Expected: Page renders normally. None of the existing cards should look different. If anything regressed, the CSS has a typo — fix before continuing.

- [ ] **Step 3: Commit the CSS only**

```bash
git add index.html
git commit -m "$(cat <<'EOF'
Add targeting console mockup CSS for new ML hero card

Adds .tc-* classes for the upcoming Predictive Customer Intelligence
Engine card. CSS is committed first so the markup commit in the next
task is purely additive HTML.

Co-Authored-By: Claude Opus 4.6 (1M context) <noreply@anthropic.com>
EOF
)"
```

### Subtask 6b: Insert the new hero card markup

- [ ] **Step 4: Locate the insertion point**

Find the start of the (now) NL-to-SQL card:

```html
    <!-- ═══ 2. NL-to-SQL Agent ═══ -->
    <div class="project-card glass reveal">
```

The new card goes immediately *before* this comment.

- [ ] **Step 5: Insert the new hero card**

Insert this block before the `<!-- ═══ 2. NL-to-SQL Agent ═══ -->` line:

```html
    <!-- ═══ 1. Predictive Customer Intelligence Engine ═══ -->
    <div class="project-card glass reveal agent-card">
      <div class="project-layout">
        <div class="project-info">
          <div class="project-info-inner">
            <div class="project-info-text">
              <h3>Predictive Customer Intelligence Engine</h3>
              <p>Identified <strong>$15M+</strong> in projected incremental revenue by replacing blanket post-booking outreach with weekly ML-scored audiences across 7 ancillary product categories. Trained 7 H2O AutoML classifiers on 2.2M historical browsing events, then routed each booking into a tiered marketing action &mdash; high intent gets a reminder, low-medium gets a promotional offer, and the rest fall out. A deterministic 80/20 target/control split lets the team measure true lift.</p>
              <div class="tags">
                <span class="tag">Python</span><span class="tag">H2O AutoML</span><span class="tag">GBM</span>
                <span class="tag">BigQuery</span><span class="tag">scikit-learn</span><span class="tag">Feature Engineering</span>
                <span class="tag">A/B Testing</span>
              </div>
            </div>
            <div class="project-info-metrics">
              <div class="impact-item"><div class="impact-value accent">$15M+</div><div class="impact-label">Projected Annual Incremental Revenue</div></div>
              <div class="impact-item"><div class="impact-value accent">0.89 AUC</div><div class="impact-label">Peak Model Performance</div></div>
              <div class="impact-item"><div class="impact-value accent">12K/wk</div><div class="impact-label">Bookings Scored</div></div>
            </div>
          </div>
        </div>
        <div class="project-mockup">
          <div class="mockup-frame">
            <div class="mockup-bar">
              <span class="dot dot-r"></span><span class="dot dot-y"></span><span class="dot dot-g"></span>
              <span class="mockup-label">Northwind Voyages &mdash; Customer Intelligence Console</span>
            </div>
            <div class="mockup-body">
              <div class="tc-layout">
                <div class="tc-top">
                  <div class="tc-sidebar">
                    <div class="tc-brand">Northwind<span>Voyages</span></div>
                    <div class="cs-label">Week</div>
                    <div class="cs-select">2026-W15</div>
                    <div class="cs-label">Categories</div>
                    <div class="tc-chips">
                      <span class="tc-chip">Photo</span>
                      <span class="tc-chip">Beverage</span>
                      <span class="tc-chip">Spa</span>
                      <span class="tc-chip">Internet</span>
                      <span class="tc-chip">Excursions</span>
                      <span class="tc-chip">Dining</span>
                      <span class="tc-chip">Delights</span>
                    </div>
                    <div class="cs-label">Tier</div>
                    <div class="tc-tier-toggle">
                      <div class="active">High</div>
                      <div>Med</div>
                      <div>Low-Med</div>
                      <div>Low</div>
                    </div>
                    <div class="cs-label">DTD Window</div>
                    <div class="cs-select">4&ndash;30 days</div>
                    <div class="cs-label">T/C Split</div>
                    <div class="cs-select">80 / 20</div>
                    <div class="tc-stat-footer">
                      <strong>12,047</strong> scored<br>
                      <strong>~10,000</strong> targeted
                    </div>
                  </div>
                  <div class="tc-main">
                    <div class="tc-perf-card">
                      <div class="tc-perf-title">Model Performance</div>
                      <div class="tc-perf-big"><span class="accent-blue">0.89</span> AUC</div>
                      <div class="tc-perf-sub">Peak performance &middot; 7 GBM classifiers &middot; H2O AutoML &middot; out-of-time validated</div>
                      <div class="tc-perf-pills">
                        <span class="tc-perf-pill">Photo</span>
                        <span class="tc-perf-pill">Beverage</span>
                        <span class="tc-perf-pill">Spa</span>
                        <span class="tc-perf-pill">Internet</span>
                        <span class="tc-perf-pill">Excursions</span>
                        <span class="tc-perf-pill">Dining</span>
                        <span class="tc-perf-pill">Delights</span>
                      </div>
                    </div>
                    <div>
                      <div class="tc-funnel-title">Weekly Targeting Funnel</div>
                      <div class="tc-funnel-row">
                        <div class="tc-funnel-bar" style="width: 100%;">49,000</div>
                        <div class="tc-funnel-label">Browse Pool</div>
                      </div>
                      <div class="tc-funnel-row">
                        <div class="tc-funnel-bar" style="width: 30%;">12,047</div>
                        <div class="tc-funnel-label">DTD 4&ndash;30</div>
                      </div>
                      <div class="tc-funnel-row">
                        <div class="tc-funnel-bar" style="width: 24%;">~10,000</div>
                        <div class="tc-funnel-label">Eligible (post 80/20)</div>
                      </div>
                    </div>
                    <div>
                      <div class="tc-funnel-title">Tier &rarr; Action Map</div>
                      <table class="tc-tier-table">
                        <thead>
                          <tr><th>Tier</th><th>Action</th></tr>
                        </thead>
                        <tbody>
                          <tr><td><span class="tier-high">High</span></td><td>Evergreen reminder (no discount)</td></tr>
                          <tr><td><span class="tier-med">Medium</span></td><td>Soft nudge</td></tr>
                          <tr><td><span class="tier-lowmed">Low-Medium</span></td><td>Promotional offer (incremental play)</td></tr>
                          <tr><td><span class="tier-low">Low</span></td><td>Suppress (no email)</td></tr>
                        </tbody>
                      </table>
                    </div>
                  </div>
                </div>
                <div class="tc-action-bar">
                  <div class="tc-btn tc-btn-secondary">&#128229; Export CSV</div>
                  <div class="tc-btn">&#9654; Generate Weekly Target List</div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>

```

- [ ] **Step 6: Reload and screenshot at desktop**

Reload `http://localhost:8765/`. Viewport 1440x900. Full-page screenshot.

Expected:
- The Predictive Customer Intelligence Engine card is now the first featured project.
- It uses the stacked layout (info on top, mockup full-width below) — same shape as the old NL-to-SQL hero.
- Title, impact-first description with bold $15M+, 7 tags.
- Three impact bullets stacked vertically on the right side of the info block (this is the agent-card metrics column behavior).
- Mockup shows: sidebar (Northwind brand, Week, Categories chips, Tier toggle, DTD, T/C split, footer stats) + main panel (perf card with 0.89 AUC, funnel, tier table) + bottom action bar.

If anything looks broken, debug now before continuing. Common issues:
- Mockup body too short → increase `.tc-layout min-height` to 460px
- Sidebar too narrow → increase `.tc-sidebar width` to 170px
- Funnel bars don't shrink visibly → check that the inline width % is being applied

- [ ] **Step 7: Reload and screenshot at mobile**

Resize viewport to 393x852. Screenshot the new card.

Expected: Card stacks per existing mobile rules. The targeting console mockup's sidebar collapses to a horizontal row above the main panel (per the `@media (max-width: 600px)` rule added in subtask 6a). All three sections (perf card, funnel, tier table) remain readable.

If the sidebar collapse looks bad, simplify: hide the sidebar entirely on mobile and let the main panel use full width. Add to the mobile breakpoint:
```css
.tc-sidebar { display: none; }
```

Decide based on what you see — only apply if needed.

- [ ] **Step 8: Commit**

```bash
git add index.html
git commit -m "$(cat <<'EOF'
Add Predictive Customer Intelligence Engine as new hero card

New stacked-layout featured project at position #1, replacing NL-to-SQL
in the hero slot. Includes a full targeting-console mockup with model
performance card (0.89 AUC), weekly targeting funnel, and tier-to-action
map. Card description leads with $15M+ projected incremental revenue.

Co-Authored-By: Claude Opus 4.6 (1M context) <noreply@anthropic.com>
EOF
)"
```

---

## Task 7: Move Ecommerce from Featured to More Work

**Files:**
- Modify: `index.html` (delete Card #4 from featured section)
- Modify: `index.html` (insert mini-card into More Work section)

- [ ] **Step 1: Read the current Ecommerce featured card**

Read `index.html` lines 881–965 (the `<!-- ═══ 4. Full-Stack Ecommerce Platform ═══ -->` block) to confirm the exact existing markup.

- [ ] **Step 2: Delete the entire Ecommerce featured card**

Find the block starting at:

```html
    <!-- ═══ 4. Full-Stack Ecommerce Platform ═══ -->
    <div class="project-card glass reveal">
```

Delete the entire block from that comment line through its closing `</div>` (the last `</div>` before `</section>` for the projects section). The block ends just before:

```html
  </div>
</section>
```

After deletion, the featured-projects section should contain exactly 4 cards: new ML hero (#1), NL-to-SQL (#2), Anomaly Detection (#3), Automated Executive Reporting Engine (#4).

- [ ] **Step 3: Insert Ecommerce mini-card into More Work**

Find the More Work `<div class="more-grid">` opening (around line 972). Insert this mini-card as the **first** child of `more-grid`, immediately after the opening `<div class="more-grid">` line:

```html
      <div class="mini-card glass reveal">
        <span class="badge-personal">Personal</span>
        <h4>Full-Stack Ecommerce Platform</h4>
        <p>Production-grade ecommerce stack built from scratch &mdash; dual-market with GeoIP routing, guest checkout, affiliate program with commission tracking, discount codes, store credits, abandoned cart recovery, email campaigns with open tracking, shipping labels via Shippo, and a full admin dashboard. 50+ routes, 13+ database tables.</p>
        <div class="tags"><span class="tag">Python</span><span class="tag">Flask</span><span class="tag">SQLite</span><span class="tag">Vanilla JS</span><span class="tag">Docker</span><span class="tag">Shippo API</span><span class="tag">Playwright</span></div>
      </div>
```

Note: `badge-personal` styling already exists in the CSS (around line 440) — no new CSS needed. The original featured card used `<span class="badge-personal">Personal</span>` inside the `<h3>`, but here we move it above the `<h4>` to match the mini-card pattern (the `badge-grad` cards in the existing More Work follow the same pattern).

- [ ] **Step 4: Verify badge-personal positioning works in mini-card layout**

Check the existing `badge-grad` mini-cards (lines 998–1021 in the current file before our edits) to confirm the badge sits above the `<h4>`. If `badge-grad` and `badge-personal` use compatible styling, the new card should look right. If not, you may need to adjust `.badge-personal` CSS to match `.badge-grad` positioning — but verify visually first before adding CSS.

- [ ] **Step 5: Reload and screenshot at desktop**

Reload `http://localhost:8765/`. Viewport 1440x900.

Screenshot 1: featured projects section. Expected: exactly 4 cards (no Ecommerce).

Screenshot 2: More Work section. Expected: 10 cards visible (the original 9 + the new Ecommerce mini-card at the top), with the Ecommerce card showing the `Personal` badge and 50+ routes / 13+ tables in the description.

(Task 8 will then cut the 4 grad cards, dropping the count to 6.)

- [ ] **Step 6: Reload and screenshot at mobile**

Resize viewport to 393x852. Screenshot both sections. Expected: featured cards stack one-up, More Work mini-cards stack one-up.

- [ ] **Step 7: Commit**

```bash
git add index.html
git commit -m "$(cat <<'EOF'
Move Ecommerce from featured to More Work

Demotes the personal Ecommerce platform to a More Work mini-card so the
featured lineup stays focused on ML/data engineering work. The card
keeps its full description and Personal badge in its new home.

Co-Authored-By: Claude Opus 4.6 (1M context) <noreply@anthropic.com>
EOF
)"
```

---

## Task 8: Cut graduate coursework cards from More Work

**Files:**
- Modify: `index.html` (delete 4 mini-cards from More Work section)

- [ ] **Step 1: Identify the 4 cards to delete**

In the current `more-grid` div, find these four `<div class="mini-card glass reveal">` blocks (each contains a `<span class="badge-grad">` element):

1. NLP Bias Detection (`<h4>NLP Bias Detection</h4>`)
2. Alzheimer's MRI Classification (`<h4>Alzheimer's MRI Classification</h4>`)
3. Flight Delay Prediction (`<h4>Flight Delay Prediction</h4>`)
4. Heart Disease Prediction (`<h4>Heart Disease Prediction</h4>`)

- [ ] **Step 2: Delete each block**

For each of the 4 cards, find the entire `<div class="mini-card glass reveal">...</div>` block (from the opening div through its closing `</div>`) and delete it, including any leading whitespace/blank line if it leaves a visible gap.

Tip: search for `badge-grad` in the file and delete the surrounding `<div class="mini-card ...">...</div>` block 4 times. Each block is approximately 6 lines.

- [ ] **Step 3: Verify the More Work section count**

After deletion, the `more-grid` should contain exactly 6 mini-cards in this order:

1. Full-Stack Ecommerce Platform (Personal badge) — added in Task 7
2. Resume Builder
3. Job Application Automation
4. Promo Calendar ETL
5. SAP BO Booking Pipeline
6. Weekly Tracker Email

- [ ] **Step 4: Reload and screenshot at desktop**

Reload `http://localhost:8765/`. Viewport 1440x900. Scroll to More Work and screenshot.

Expected: Exactly 6 cards. No `Graduate` badges anywhere on the page. The 3-column grid renders cleanly (two rows of 3).

- [ ] **Step 5: Reload and screenshot at mobile**

Resize to 393x852. Screenshot. Expected: 6 cards stacked one-up.

- [ ] **Step 6: Commit**

```bash
git add index.html
git commit -m "$(cat <<'EOF'
Cut graduate coursework cards from More Work

Removes 4 grad-school project cards (NLP Bias, Alzheimer's MRI, Flight
Delay, Heart Disease). Keeps the More Work section focused on
production work and recent personal projects.

Co-Authored-By: Claude Opus 4.6 (1M context) <noreply@anthropic.com>
EOF
)"
```

---

## Task 9: Mobile fallback for the 3-impact-bullet row

**Files:**
- Modify: `index.html` (CSS section, mobile breakpoint)

The new ML hero card and the Anomaly Detection card both use 3 impact bullets in a row (`.impact-row.impact-row-3` for Anomaly, and the agent-card metrics column for the hero). At 393px the existing 2-up row may overflow when there are 3 items.

- [ ] **Step 1: Verify whether there's actually a problem at 393px**

Reload `http://localhost:8765/`. Viewport 393x852. Screenshot Card #1 (new ML hero) and Card #3 (Anomaly Detection) impact rows specifically.

Check:
- Are the impact bullets readable?
- Do they overflow horizontally?
- Do they wrap awkwardly (e.g., one bullet on its own line)?

If everything looks fine, **skip the rest of this task and commit nothing.** Move on to Task 10.

If there are problems, continue.

- [ ] **Step 2: Add mobile rule for 3-bullet rows (only if needed)**

Find the existing mobile breakpoint block at `@media (max-width: 600px)` (around line 522).

Inside that block, find the existing rule:

```css
.impact-row { gap: 6px; }
.impact-item { padding: 7px 11px; flex: 1 1 calc(50% - 3px); min-width: 0; }
.impact-value { font-size: 17px; }
```

(or similar — locate the impact-row mobile rule). Add immediately after it:

```css
.impact-row-3 .impact-item { flex: 1 1 100%; }
.impact-row-3 .impact-value { font-size: 16px; }
.impact-row-3 .impact-label { font-size: 10px; }
```

This forces 3-bullet rows to stack vertically on mobile, with slightly smaller text. Two-bullet rows continue using the 50/50 side-by-side layout.

For the agent-card hero (which uses `.project-info-metrics` not `.impact-row`), find the existing agent-card mobile rule:

```css
.agent-card .project-info-metrics { ... }
```

If it doesn't already exist, add:

```css
.agent-card .project-info-metrics { flex-direction: row; flex-wrap: wrap; gap: 6px; }
.agent-card .project-info-metrics .impact-item { flex: 1 1 calc(50% - 3px); min-width: 0; }
```

Verify visually — the goal is for 3 metrics on the new ML hero to render as 2 bullets on row 1 + 1 bullet on row 2 at mobile.

- [ ] **Step 3: Reload and re-screenshot at 393px**

Verify both cards now render their 3-bullet rows readably.

- [ ] **Step 4: Commit (only if changes were made)**

```bash
git add index.html
git commit -m "$(cat <<'EOF'
Add mobile fallback for 3-impact-bullet rows

Stacks 3-bullet impact rows vertically at 393px so they don't overflow.
Two-bullet rows continue using the existing 50/50 side-by-side layout.

Co-Authored-By: Claude Opus 4.6 (1M context) <noreply@anthropic.com>
EOF
)"
```

If no changes were needed in step 2, no commit. Move to Task 10.

---

## Task 10: Final desktop + mobile screenshot review

**Files:**
- No code changes. Verification only.

- [ ] **Step 1: Take a fresh full-page screenshot at desktop (1440x900)**

Reload `http://localhost:8765/`. Take one full-page screenshot of the entire site.

- [ ] **Step 2: Take a fresh full-page screenshot at mobile (393x852)**

Resize viewport. Take one full-page screenshot.

- [ ] **Step 3: Walk through the spec checklist on the screenshots**

For each item in the spec, verify it's present and correct:

- [ ] Hero: title-led copy is gone, replaced with verb-first metric line, $15M+ is bold/white
- [ ] Featured Card #1: Predictive Customer Intelligence Engine, stacked layout, $15M+ / 0.89 AUC / 12K/wk impact bullets, full targeting console mockup
- [ ] Featured Card #2: NL-to-SQL Agent, side-by-side layout, "4 hours" + "80%" bolded in description, Claude Opus 4.6 in tags (no LangChain)
- [ ] Featured Card #3: Anomaly Detection, three impact bullets (refresh, cost, severity), GCS + Cloud Build in tags
- [ ] Featured Card #4: Automated Executive Reporting Engine, document-style mockup with 5 KPIs + YoY table + Claude narrative + action chips
- [ ] Featured Card 5 (Ecommerce) is GONE from featured
- [ ] More Work: Ecommerce mini-card present at top with Personal badge
- [ ] More Work: zero Graduate badges anywhere
- [ ] More Work: exactly 6 cards
- [ ] Mobile: all cards readable at 393px, no horizontal overflow, impact bullets render correctly

Note any issues. Fix inline if quick (typos, small CSS tweaks). Otherwise list them for the user.

- [ ] **Step 4: No commit unless fixes were made**

If you made fixes in step 3, commit them with a `Polish: ...` message. Otherwise no commit.

---

## Task 11: User approval gate

**Files:**
- No code changes. Hand-off to user.

- [ ] **Step 1: Confirm the local server is still running**

Check that `http://localhost:8765/` still responds. If not, restart it.

- [ ] **Step 2: Hand the URL to the user with a review checklist**

Send the user a message containing:
- The local URL: `http://localhost:8765/`
- A note that they should review on desktop AND on a mobile-sized window (DevTools responsive mode at 393px)
- The list of things to check (matches the Task 10 spec checklist above)
- An explicit "do not push until you tell me to" line

- [ ] **Step 3: Wait for the user**

Do not proceed to Task 12 until the user explicitly approves. If they request changes, loop back to the relevant earlier task, fix, re-screenshot, re-commit, and bring them back to this gate.

---

## Task 12: Push to main

**Files:**
- No code changes. Deploy only.

- [ ] **Step 1: Verify clean working tree on main**

```bash
cd "C:/Users/krysh/OneDrive - MSC Cruises SA/Documents/Work/Portfolio"
git status
git log --oneline -10
```

Expected: Working tree clean. Recent commits include all the task commits from this plan plus the spec commit from earlier.

- [ ] **Step 2: Push to origin/main**

```bash
git push origin main
```

- [ ] **Step 3: Verify GitHub Pages deployment**

```bash
gh run list --repo kryshr/kryshr.github.io --limit 3
```

Wait ~30 seconds, then check the run status. Expected: most recent run shows `completed success`.

- [ ] **Step 4: Live verification**

Use Playwright to navigate to `https://kryshr.github.io` and take a desktop screenshot. Compare against the local final screenshot from Task 10 — they should be visually identical (modulo any 30s delay if Pages hasn't propagated yet).

- [ ] **Step 5: Stop the local web server**

Kill the background `python -m http.server 8765` process started in Task 1.

- [ ] **Step 6: Final confirmation to user**

Tell the user the changes are live at `https://kryshr.github.io`. Provide the LinkedIn Post Inspector link from CLAUDE.md if they want to verify the OpenGraph image still resolves: `https://www.linkedin.com/post-inspector/`.

---

## Self-Review Notes

**Spec coverage check:**
- Section 1 (Hero) → Task 2 ✓
- Section 2 Card #1 (new ML) → Tasks 6a + 6b ✓
- Section 2 Card #2 (NL-to-SQL) → Task 5 ✓
- Section 2 Card #3 (Anomaly) → Task 3 ✓
- Section 2 Card #4 (Q4 Reporting) → Task 4 ✓
- Section 3 Mockup A (targeting console) → Task 6 ✓
- Section 3 Mockup B (exec brief) → Task 4 ✓
- Section 4 (More Work changes) → Tasks 7 + 8 ✓
- Section 5 (Workflow: local preview, user gate, push) → Tasks 1, 10, 11, 12 ✓
- Open risk #1 (mobile 3-bullet layout) → Task 9 ✓
- Open risk #2 (mockup numbers fabricated) → Mockups use Northwind Voyages and the stated illustrative numbers ✓

**Type/naming consistency check:**
- `.impact-row-3` modifier class introduced in Task 3, referenced in Task 9 mobile rule ✓
- `.tc-*` class prefix used consistently in Task 6a CSS and Task 6b markup ✓
- `.exec-*` class prefix used consistently in Task 4 CSS and markup ✓
- Card numbering: spec says new lineup is #1 ML, #2 NL-to-SQL, #3 Anomaly, #4 Q4 Reporting. Plan reorders by editing in place: Task 4 replaces existing #3 (Report Pipeline → Q4 Reporting), Task 5 demotes existing #1 (NL-to-SQL), Task 6 inserts new #1 (ML hero). The HTML comment numbers are renumbered in Tasks 4, 5, and 6. ✓
- `agent-card` class moves: removed from NL-to-SQL in Task 5, added to new ML hero in Task 6 ✓

**Placeholder scan:** No TBDs, TODOs, or "implement later" found. All code blocks contain real content.
