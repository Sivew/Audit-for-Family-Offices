---
file: finding_blocks
purpose: Reusable finding templates — one block per pain area, instantiated with respondent data
---

# Finding Blocks

Each pain area has a finding block below. The engine picks the top-3 scoring pains and renders them into the report's "Priority Findings" page.

Variables marked `{{v}}` are substituted from the respondent's answers. Variables marked `[benchmark]` are substituted from the SynexumLabs institutional benchmarks.

---

## Block 01 — Data Fragmentation

**Severity trigger:** `data_fragmentation` ≥ 61

```
TITLE: Your data lives in {{B02a_source_count_label}} places. Your decisions can only live in one.

THE NUMBER:
{{B02c_time_cost_label}} per month spent getting to a consolidated view.
Benchmark: firms of your shape typically spend [benchmark: 20–40 hours].

WHY THIS MATTERS FOR {{firm_name}}:
With {{A05_jurisdictions_label}} jurisdictions and {{A06_entities_label}} entities,
you can't afford a consolidated view that depends on manual reconciliation.
Every day that passes between a source change and the dashboard is a day your
principal is making decisions on stale information.

IF LEFT AS-IS:
Scales directly with growth. If AUM doubles, consolidation effort more than doubles —
reconciliation complexity is exponential, not linear.

IF ADDRESSED:
A unified data layer with hourly refresh. The same team you have today handles
2–3× the complexity, with less friction, not more.
```

---

## Block 02 — Reporting Lag

**Severity trigger:** `reporting_lag` ≥ 61

```
TITLE: {{B03a_lag_days_label}} between quarter-end and consolidated truth.

THE NUMBER:
{{B03a_lag_days_label}} — vs. a [benchmark: under-15-day] standard among firms running
modern consolidation infrastructure.

WHY THIS MATTERS FOR {{firm_name}}:
Reporting lag is only partially a reporting problem. It's a decision-making problem.
By the time your {{A01_role_label}} sees Q3 numbers, Q4 is already two months old
and the market has moved. In the last 12 months, this lag contributed to:
{{B03b_consequences_summary}}.

IF LEFT AS-IS:
The lag compounds pressure on year-end planning, tax structuring, and rebalancing windows.
Material decisions get made on verbal explanations rather than audited numbers.

IF ADDRESSED:
Same-week visibility, with plain-English variance commentary on every material movement.
The quarter closes and you see it the same week — not the next one.
```

---

## Block 03 — Structural Complexity

**Severity trigger:** `structural_complexity` ≥ 61

```
TITLE: {{A06_entities_label}} entities. {{B04b_query_frequency_label}} outside-counsel queries.
       {{B04a_counsel_spend_label}} per year.

THE NUMBER:
{{B04a_counsel_spend_label}} in annual outside-counsel spend on structural questions alone —
not litigation, not transactions.
Benchmark: comparable firms with an in-house structural intelligence layer spend
[benchmark: 60–70% less].

WHY THIS MATTERS FOR {{firm_name}}:
Every structural question routing to outside counsel adds days to the decision cycle
and dollars to the fee bill. {{B04c_holder_knowledge_label}} — which means the
structure's complexity has outgrown the team's ability to hold it in their heads.

IF LEFT AS-IS:
Scale brings more entities, which brings more queries, which brings more counsel spend
and slower decisions. Nothing self-corrects.

IF ADDRESSED:
Routine structural questions answered in seconds inside your tenancy, with source documents
cited. Outside counsel reserved for genuinely novel questions — not routine ones.
```

---

## Block 04 — Shadow AI

**Severity trigger:** `shadow_ai` ≥ 61

```
TITLE: Your team is already using AI. The question is where your data goes when they do.

THE NUMBER:
{{B05a_tools_used_summary}} currently used across the office.
{{B05b_doc_exposure_label}}.

WHY THIS MATTERS FOR {{firm_name}}:
Your General Counsel's current position — {{B05c_gc_position_label}} — doesn't match
the reality of what your team is already doing. The gap between policy and practice
is where governance exposure lives.

IF LEFT AS-IS:
The gap compounds with every new AI tool released. Banning tools shifts usage underground;
not banning them normalises data egress. Neither resolves the underlying issue.

IF ADDRESSED:
Sovereign AI deployment inside your environment. Same productivity your team wants,
with the data posture your principal demands. Not a policy — the architectural
guarantee that sensitive data cannot leave.
```

---

## Block 05 — Portfolio Blindspots

**Severity trigger:** `portfolio_blindspots` ≥ 61

```
TITLE: Your portfolio surprises you {{B06b_surprise_frequency_label}}. Every surprise has a cost.

THE NUMBER:
{{A07_portfolio_companies_label}} portfolio companies reporting on a
{{B06a_report_cadence_label}} cadence.
{{B06b_surprise_frequency_label}} material surprises in the last 24 months.

WHY THIS MATTERS FOR {{firm_name}}:
Portfolio company issues surfaced in a {{B06a_report_cadence_label}} report are, by definition,
weeks old by the time you read them. {{B06c_covenant_tracking_label}} — which means issues
tied to covenants, KPIs, or anomalous movements are not caught at their earliest actionable point.

IF LEFT AS-IS:
Each future surprise carries both direct cost (the issue itself) and indirect cost
(reactive decisions, principal frustration, trust erosion with portfolio-company CFOs).

IF ADDRESSED:
Monthly reports read the day they arrive. Anomalies flagged against trend and peer benchmarks.
Board-ready summaries ready before your morning coffee on report day.
```

---

## Block 06 — Deal Flow Drag

**Severity trigger:** `deal_flow_drag` ≥ 61

```
TITLE: {{B07a_inbound_volume_label}} inbound deals per week. Only {{B07b_real_review_rate_label}} get a real read.

THE NUMBER:
{{B07a_inbound_volume_label}} deals per week.
{{B07b_real_review_rate_label}} receive a genuine first review.
That leaves [calculated_missed_count] opportunities per month going un-reviewed.

WHY THIS MATTERS FOR {{firm_name}}:
Deal flow coverage is directly linked to adverse selection. If you only review the ones
intermediaries push hardest, you select for persistence — not quality. The deals that
would have been most interesting are often the ones that die quietly.

IF LEFT AS-IS:
Coverage ratio stays flat as volume grows. Your single analyst (or you) becomes the bottleneck.
The quality of your deal flow decays slowly and invisibly.

IF ADDRESSED:
Every deck gets a documented first read overnight. Scoring against your thesis.
IC-ready memos drafted for the keepers; one-line declines for the rest. Your team only
touches the ones worth touching.
```

---

## Supplementary findings (shown only if specific flags fire)

### Governance Risk amplifier

**Fires if:** `governance_risk` ≥ 60, regardless of pain band

```
APPENDED TO EACH FINDING AS A FOOTER LINE:

Governance note: your current {{C07_residency_label}} + {{C08_access_control_label}} posture
on the data involved amplifies the exposure described above. Any remediation should be
architected to resolve both — not treat them as separate problems.
```

### Team Bottleneck amplifier

**Fires if:** `team_bottleneck_risk` ≥ 60

```
APPENDED TO EACH FINDING AS A FOOTER LINE:

Key-person note: with a team of {{A04_team_size_label}}, each finding above carries
a secondary risk — the person who knows how to work around the gap is the person
whose departure would surface it. Addressing the finding structurally removes the
key-person dependency.
```

### Principal Frustration signal

**Fires if:** `principal_frustration` ≥ 40

```
APPENDED TO EXECUTIVE SUMMARY AS A SECOND PARAGRAPH:

Based on your answers, your principal has already voiced friction on at least one of these
areas directly. That is unusual for an audit of this type to surface — most principals absorb
operational friction silently. Treat it as a signal that the window to act is open.
```

---

## Rendering rules

- Each finding block takes approximately 1/3 of a page in the final PDF
- Three findings total fill Page 3 cleanly
- Finding titles use H3 (navy, 15pt bold)
- "THE NUMBER" is rendered as oversized cyan text (24pt) with the benchmark line in grey underneath
- "WHY THIS MATTERS FOR {{firm_name}}" and the following paragraphs render in standard body (11pt)
- Each finding has a cyan left accent bar (3pt wide) spanning the block height
- Severity chip (`Significant` / `Critical`) renders top-right of each block, filled with the band colour from `Scoring_Model.md`

---

## Writing principles for findings

If the engine ever generates a finding that reads generically — rewrite it. The entire value of this report is that it reads as if a human founding partner studied the firm. Every finding should reference at least two specific numbers from the respondent's answers, and name {{firm_name}} at least once.

Findings that could apply to any family office are failures. Findings that could only apply to this one are successes.
