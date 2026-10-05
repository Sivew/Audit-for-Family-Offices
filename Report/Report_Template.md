---
file: report_template
purpose: Structure and copy template for the generated audit report PDF
format: 4–6 pages, portrait, SynexumLabs branding
---

# Audit Report Template

Every respondent receives a bespoke PDF built from this template. Variables are inserted from the respondent's answers at the points marked `{{variable}}`. Everything else is static copy.

The PDF uses the same navy-and-cyan visual system as the deck and case studies.

---

## Page 1 — Cover

**Header bar (navy, full width):**
> SYNEXUM LABS · OPERATIONAL READINESS AUDIT

**Centred vertical block:**

Eyebrow (small cyan, uppercase):
> CONFIDENTIAL — PREPARED FOR {{first_name}} {{last_name}}

H1 (navy, 36pt):
> {{firm_name}}
> Operational Readiness Audit

Subhead (grey, 14pt italic):
> Prepared by SynexumLabs founding partners  ·  {{submission_date}}

Footer line (small, grey):
> This document is confidential. Not for redistribution. Retained for 24 months unless deletion is requested.

---

## Page 2 — Executive summary

**Section eyebrow:** EXECUTIVE SUMMARY

**H1:** What we found

**Three short paragraphs (one each):**

1. **{{firm_name}} is a {{A02_firm_type_label}} managing {{A03_aum_label}} across {{A05_jurisdictions_label}} jurisdictions, with a team of {{A04_team_size_label}}.** *(Firm profile sentence — assembled from Section A answers.)*

2. **The three areas creating the most operational drag today are {{top_pain_1_label}}, {{top_pain_2_label}}, and {{top_pain_3_label}}.** *(Named verbatim from top-3 pain scores.)*

3. **{{variant_sentence}}** *(Routing-dependent — one of:)*
   - *variant_light:* "Your current operation is in solid shape. The findings below point to incremental improvements rather than foundational gaps."
   - *variant_nurture:* "The pattern we see is familiar — serious friction, no clear window to act on it yet. The findings below are for when the window opens."
   - *variant_standard:* "The pattern we see is familiar — and solvable. The findings below map to specific engagements we've delivered for firms of your shape."
   - *variant_priority:* "One finding below needs attention this quarter, not next. We've flagged it for your attention and our founding partners'."

**Visual element:** a horizontal "pain score bar" showing all 6 dimensions with their 0–100 values, colour-banded.

---

## Page 3 — Priority findings

**Section eyebrow:** PRIORITY FINDINGS

**H1:** Three findings for your firm

Three blocks, one for each of the top-3 pain scores. Each block is built from `Finding_Blocks.md` and contains:

- **Finding title** (dynamic from pain code)
- **The number that tells the story** (one score, one metric, one benchmark — pulled from their answers)
- **Why this matters for {{firm_name}}** (two sentences, context-specific)
- **If left as-is** (one sentence consequence)
- **If addressed** (one sentence outcome)

Each block has a cyan accent bar on the left and a small "severity" chip in the top-right (`Significant` / `Critical`).

---

## Page 4 — Priority matrix

**Section eyebrow:** PRIORITY MATRIX

**H1:** Where to focus first

**Intro paragraph:**
> The priority matrix below plots the findings against impact (how much they're costing you now) and effort (how hard they are to resolve). The upper-right quadrant is where to start.

**Visual element:** 2×2 grid with four quadrants:

```
                    HIGH IMPACT
                        │
      [Nice to have]    │   [START HERE]
                        │
LOW EFFORT ─────────────┼───────────── HIGH EFFORT
                        │
      [Defer]           │   [Plan carefully]
                        │
                    LOW IMPACT
```

Each top-3 finding is plotted as a cyan dot with a label. Placement is scripted — see `Priority_Matrix.md` for the plotting logic.

**Below the grid:**
> Your single highest-leverage change this quarter: **{{top_impact_low_effort_finding}}**

---

## Page 5 — Recommended path

**Section eyebrow:** RECOMMENDED PATH

**H1:** If (and only if) we're the right partner

**Opening paragraph:**
> Based on your top findings, here is the engagement path we'd propose for {{firm_name}}. Nothing here is a quote — ranges are directional. The actual scope would be set in a Discovery conversation.

**Path block (routing-dependent):**

### If `variant_standard` or `variant_priority`:

A sequenced visual showing:

```
Step 1  →  Free Discovery Engagement
           Needs + structural analysis. 45–60 minutes. No cost.

Step 2  →  Paid Discovery Engagement
           {{discovery_price}} · 2–3 weeks · Architecture blueprint, integration map, prioritised roadmap

Step 3  →  {{primary_offer.tagline}}
           {{primary_offer.build_range}} · {{primary_offer.duration}} · {{primary_offer.one_line}}

Step 4  →  (If applicable) {{secondary_offer.tagline}}
           {{secondary_offer.build_range}} · {{secondary_offer.duration}}

Ongoing  →  Sustainment
           {{sustainment_range}} per month · System monitoring, performance optimisation, continuous improvement
```

### If `variant_light`:
> Your current operation is in solid shape. We don't believe a build engagement is the right next step. If you want a pressure-test conversation to make sure, our calendar is below.

### If `variant_nurture` or `budget_mismatch`:
> No path recommended at this stage. We'd rather tell you honestly than scope an engagement that doesn't fit.

---

## Page 6 — The call (CTA)

**Section eyebrow:** NEXT STEP

**Centred H1 (navy, 32pt):**

Routing-dependent:

- *variant_standard, variant_priority:* "A 30-minute conversation with our founding partners"
- *variant_light, variant_nurture, budget_mismatch:* "If something here changes next quarter"
- *not_decision_maker:* "Share this report with your decision-maker"

**CTA block (cyan button):**

- *variant_standard, variant_priority:* "Book your Free Discovery call"
- *variant_light:* "Request a pressure-test call"
- *variant_nurture:* "Keep this report; we'll check in next quarter"
- *not_decision_maker:* "Forward this report"

**Beneath the button, small grey:**
> Not every firm is the right fit for what we build. The 30 minutes tells us honestly — either way, you leave with clarity.

**Named founding partners block:**

> **Sivakumar Swaminathan** · Chief AI Transformation Officer
> **Sergio Paier** · Founding Partner, Strategic Consulting · Coigne Capital
>
> One of us (or both) will be on your Discovery call. Our founding partners run every one personally.

**Footer:**
> SynexumLabs · A Coigne Capital company · Governed AI & Automation
> Confidential — Prepared for {{first_name}} {{last_name}}, {{firm_name}}
> Audit submitted {{submission_date}} · Report delivered {{delivery_date}}

---

## Variable reference

All variables used in this template:

```
{{first_name}}              — from A08
{{last_name}}               — from A08
{{firm_name}}               — from A08
{{submission_date}}         — captured on submit
{{delivery_date}}           — set when report is dispatched

{{A02_firm_type_label}}     — resolved from A02 selection
{{A03_aum_label}}           — resolved from A03 selection
{{A04_team_size_label}}     — resolved from A04 selection
{{A05_jurisdictions_label}} — resolved from A05 selection

{{top_pain_1_label}}        — 1st-highest-scored pain, friendly label
{{top_pain_2_label}}        — 2nd
{{top_pain_3_label}}        — 3rd

{{variant_sentence}}        — resolved from variant routing

{{top_impact_low_effort_finding}}  — single finding plotted in top-left quadrant

{{discovery_price}}         — from complexity_tier
{{primary_offer.*}}         — from offer_mapping
{{secondary_offer.*}}       — from offer_mapping
{{sustainment_range}}       — from offer_mapping
```

---

## Rendering notes

- Font: Inter or Helvetica Neue
- Body size: 11pt / 15pt line height
- Primary colour: #031B4E (navy)
- Accent: #35D1FF (cyan)
- Background panels: #ECF5FB (light cyan tint)
- Page size: US Letter, portrait
- Margins: 0.6" all sides
- Headers / footers on every page except cover
- Watermark on bottom-right of every content page (small grey): "Confidential — {{first_name}} {{last_name}}"
