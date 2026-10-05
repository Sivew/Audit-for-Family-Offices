---
file: scoring_model
purpose: Deterministic scoring applied to every submitted audit
version: 1.0
---

# Scoring Model

Each respondent's answers aggregate into **nine named score dimensions**. Six are pain areas; three are contextual modifiers. All dimensions are capped at 100.

---

## 1 · The nine dimensions

| Dimension | Type | What it measures |
|---|---|---|
| `data_fragmentation` | pain | Scattered sources, no single view |
| `reporting_lag` | pain | Delay between quarter-end and consolidated truth |
| `structural_complexity` | pain | Entity sprawl, outside-counsel dependency |
| `shadow_ai` | pain | Unsanctioned public AI use with sensitive data |
| `portfolio_blindspots` | pain | Portfolio company issues surfacing late |
| `deal_flow_drag` | pain | Inbound volume exceeding review capacity |
| `governance_risk` | modifier | Compliance / policy / access-control exposure |
| `team_bottleneck_risk` | modifier | Key-person and capacity risk |
| `counsel_dependency` | modifier | Outside advisor dependence |
| `principal_frustration` | signal | Direct principal-level pain signals |
| `readiness_score` | signal | Buy-in, timeline, budget alignment |
| `complexity_tier` | signal | 0 = small, 1 = large, 2 = institutional |

---

## 2 · How questions contribute

Each option in each question declares a `scores` block in its YAML. On submit:

```
for each answered question:
    for each selected option:
        for each (dimension, value) in option.scores:
            dimension_total[dimension] += value
            dimension_total[dimension] = min(dimension_total[dimension], 100)
```

Multi-select questions sum across all selections. Single-select contributes the chosen option only. Required text fields (E04, E05) contribute nothing to scores — they appear verbatim in the report.

---

## 3 · Pain score banding

Each pain score is interpreted by band:

| Score band | Classification | Report colour | Report tone |
|---|---|---|---|
| 0–30 | Low priority | Grey | *"Not currently a drag."* |
| 31–60 | Watch area | Amber | *"Worth monitoring; not top of list."* |
| 61–80 | Significant | Cyan | *"A clear bottleneck in your current operation."* |
| 81–100 | Critical | Deep navy | *"This is costing you — in time, money, or risk — right now."* |

The three highest-scored pains drive the report's "Priority findings" section (unless the respondent flagged fewer than three in B01, in which case only the ones they named appear).

---

## 4 · Total pain score

```
total_pain_score = sum(all six pain dimensions)
```

Maximum: 600. Typical range from a real respondent: 150–350.

Used for report-variant routing (see `Branching_Rules.md` → "Report routing").

---

## 5 · Modifier amplification

Modifiers do not create findings on their own, but they amplify pain-score narratives in the report:

- If `governance_risk ≥ 60`, every pain finding adds the phrase *"with notable governance exposure."*
- If `team_bottleneck_risk ≥ 60`, every pain finding adds *"with your current team structure, this is a key-person risk."*
- If `counsel_dependency ≥ 60`, every pain finding related to structure or legal workflow adds *"and your outside-counsel spend reflects it."*

Governance risk ≥ 80 overrides routing — the report flags as `variant_priority` regardless of other scores, because unsanctioned AI use with sensitive data is a high-urgency concern we want in front of the founding partners the same day.

---

## 6 · Readiness score

```
readiness_score ∈ [0, 100]
```

Contributing questions: E02 (timeline), E03 (budget), E01 (authority).

Interpretation:

- **0–20** → nurture-only, no CTA
- **21–40** → soft CTA, informational tone
- **41–100** → hard CTA, direct booking link

Readiness score is independent of pain score. A respondent can have high pain and low readiness (they feel the pain but are not yet positioned to act); the report softens the ask without softening the findings.

---

## 7 · Qualification handling

Flags set by Section E and F override scoring in specific ways:

| Flag | Effect |
|---|---|
| `not_decision_maker` | Report CTA switches to *"Share this with your decision-maker"* + a forwardable link |
| `nurture_only` | No CTA; final paragraph invites them to re-run the audit next quarter |
| `budget_mismatch` | Report shows findings but omits the "recommended path" section |
| `no_followup_requested` | Email sequence stops after Email_01; no case study, no booking push |

Flags cumulate but do not conflict — the most restrictive flag wins. `no_followup_requested` is always honoured first.

---

## 8 · Complexity tier

Set by firm-size signals in A03 and A04 and reinforced by A05, A06:

```
IF A03_aum >= $1B AND A04_team_size >= 16         → complexity_tier = 2 (institutional)
IF A03_aum >= $100M AND A04_team_size >= 9         → complexity_tier = 1 (large)
ELSE                                                → complexity_tier = 0 (small-mid)
```

Complexity tier adjusts the pricing shown in the "recommended path" section of the report:

| Tier | Discovery | Dashboard build | Premium ceiling |
|---|---|---|---|
| 0 | $15K–$25K | $75K–$140K | $280K |
| 1 | $25K–$40K | $140K–$220K | $500K |
| 2 | $35K–$60K | $200K–$350K | Priced per scope |

Tier is **never shown explicitly in the report** — it's an internal calibration.

---

## 9 · Score display in report

The audit report displays each of the six pain scores as a horizontal bar (0–100), colour-coded by band, with the one-line descriptor from the band table.

Modifier scores and readiness score are **not displayed to the respondent**. They are used by the internal engine and shown in the lead record for the founding partners' review.

---

## 10 · Audit of the audit

Every submitted score set is reviewed by a founding partner before the report email ships. The partner can override any finding, soften any claim, or escalate the lead for a direct call. Average partner-review time: 90 seconds per submission.

The scoring model exists to make the partner review fast, not to replace it.
