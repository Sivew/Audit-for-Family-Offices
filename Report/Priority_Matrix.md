---
file: priority_matrix
purpose: Defines the 2x2 impact/effort grid shown on Page 4 of the audit report
---

# Priority Matrix

The matrix is a 2×2 grid plotting the respondent's top-3 findings against **Impact** (vertical) and **Effort** (horizontal). The upper-left quadrant — High Impact + Low Effort — is where the respondent is told to start.

---

## 1 · Grid definition

```
                       HIGH IMPACT
                            │
    [START HERE]            │          [PLAN CAREFULLY]
    high impact,            │          high impact,
    low effort              │          high effort
                            │
LOW EFFORT ─────────────────┼───────────────── HIGH EFFORT
                            │
    [NICE TO HAVE]          │          [DEFER]
    low impact,             │          low impact,
    low effort              │          high effort
                            │
                        LOW IMPACT
```

Only the top-3 findings from the "Priority Findings" page are plotted. The grid is a strategic focusing tool — the respondent should see no more than 3 dots so the single best starting point is unambiguous.

---

## 2 · Scoring each finding on the two axes

### Impact score (vertical axis)

Impact combines the pain's score with its downstream amplifiers.

```
impact_score = pain_score
             + (governance_risk / 2  if governance_risk > 50 and pain is governance-adjacent)
             + (team_bottleneck_risk / 2  if team_bottleneck_risk > 50)
             + (principal_frustration / 2  if principal_frustration > 40 and pain is principal-visible)

Clamp to [0, 100].

HIGH impact  → impact_score ≥ 65
LOW impact   → impact_score < 65
```

Which pains are **governance-adjacent**: `shadow_ai`, `structural_complexity`, `reporting_lag`.
Which pains are **principal-visible**: `reporting_lag`, `portfolio_blindspots`, `structural_complexity`.

### Effort score (horizontal axis)

Effort estimates the implementation lift based on the respondent's current stack posture.

```
effort_score = base_effort_for_pain
             + 15  if C06_integration = "all_manual" or "monthly"
             + 10  if C01_portfolio_platform = "ms_excel" or "none"
             + 10  if D05_internal_capability = "none" or "outsourced_it"
             + 10  if A05_jurisdictions = "over_20"
             - 10  if D05_internal_capability = "full_team"
             - 10  if C06_integration = "fully_automated"

Clamp to [0, 100].

LOW effort   → effort_score < 50
HIGH effort  → effort_score ≥ 50
```

**base_effort_for_pain** values:

| Pain code | Base effort |
|---|---|
| `shadow_ai` | 25 (fastest to deploy) |
| `deal_flow_drag` | 30 |
| `portfolio_blindspots` | 40 |
| `data_fragmentation` | 50 |
| `reporting_lag` | 55 |
| `structural_complexity` | 65 (highest-effort build) |

---

## 3 · Quadrant assignment

```
if impact_score >= 65 and effort_score < 50:
    quadrant = "START HERE"
elif impact_score >= 65 and effort_score >= 50:
    quadrant = "PLAN CAREFULLY"
elif impact_score < 65 and effort_score < 50:
    quadrant = "NICE TO HAVE"
else:
    quadrant = "DEFER"
```

---

## 4 · The "single highest-leverage change" line

Beneath the matrix, the report prints:

> Your single highest-leverage change this quarter: **{{top_impact_low_effort_finding}}**

### Selection logic for the line

```
candidates = all findings in quadrant "START HERE"

if len(candidates) == 1:
    selected = candidates[0]
elif len(candidates) > 1:
    selected = finding with highest (impact_score - effort_score)
elif len(candidates) == 0:  # nothing in "START HERE"
    candidates = all findings in quadrant "PLAN CAREFULLY"
    if candidates:
        selected = finding with highest impact_score
    else:
        selected = finding with highest impact_score across all 3
        line_prefix = "Your highest-impact area, though none are immediately low-effort, is:"
```

Fallback line prefix is only used in the rare case where no finding is both high-impact and low-effort — honesty matters more than forcing a punchy "start here."

---

## 5 · Visual plotting

- Plot each dot inside its quadrant at a position reflecting (effort_score, impact_score), with light jitter if two dots would overlap
- Dot size: fixed 10pt
- Dot colour: cyan (#35D1FF)
- Label beside each dot: the finding's title (truncated to 40 chars + "…")
- Quadrant backgrounds: subtle light-navy tint for "START HERE", neutral for the other three
- Axis labels in grey, uppercase, 8pt

---

## 6 · When fewer than 3 findings exist

If only 2 findings qualify as "Significant" or "Critical" (score ≥ 61), plot only 2 dots. The matrix still renders — it is a strategic tool, not a filler visual. Three empty quadrants with one dot in the "START HERE" square is actually the clearest possible version.

If 0 findings qualify (all pain scores < 61), the matrix is **omitted entirely** and replaced with:

> Your operation does not show any critical pressure points today. The findings above are watch-areas rather than fire alarms. We'd suggest re-running this audit in two quarters.

---

## 7 · Why this matrix is useful (internal note)

Family office principals are shown impact/effort matrices constantly by consultants. What makes this one credible is that it's generated from their own numbers — not from a generic playbook. Every dot has a traceable derivation back to the specific questions they answered.

In the Discovery call, the founding partner will reference exact positioning:

> *"On your audit, the Live Dashboard sat high-impact, low-effort. Your team is already doing most of what makes that build go fast — unified source list, moderate complexity. That's why we're suggesting it first, not because it's our highest-margin offer."*

That's the kind of grounded conversation this matrix enables.
