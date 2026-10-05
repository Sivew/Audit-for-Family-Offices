---
file: offer_mapping
purpose: Maps pain scores to SynexumLabs engagements for the "Recommended path" section of the audit report
---

# Pain → Offer Mapping

Each of the six pain areas has a primary recommended offer and optional supporting offers. The audit report's "Recommended path" section is assembled from this map.

---

## 1 · Primary mappings

| Pain area | Primary offer | Secondary offer (if score ≥ 60) |
|---|---|---|
| `data_fragmentation` | Live Data Intelligence Dashboard | Early-Warning System (if `portfolio_blindspots` ≥ 40) |
| `reporting_lag` | Live Data Intelligence Dashboard | — |
| `structural_complexity` | Structure Engine | — |
| `shadow_ai` | Contained AI Workspace | — |
| `portfolio_blindspots` | Early-Warning System (Portfolio Oversight) | Live Data Intelligence Dashboard (if `data_fragmentation` ≥ 40) |
| `deal_flow_drag` | Deal Flow Triage & Memo Drafting | — |

---

## 2 · Offer descriptions (for insertion into the report)

Each description is written in principal-facing language and sized to one short paragraph. Pulled from the Team Playbook / Finance deck v3.

### Offer 01 — Private Contained AI Workspace

```
code: contained_workspace
tagline: Your AI. Your data. Your hardware.
one_line: A private AI workspace that reads everything your office handles — deal memos, contracts, tax filings, board materials — and works inside your walls. Nothing leaves.
scope_default: Core workspace + document retrieval + redaction + audit logging
build_range:
  tier_0: $75K – $140K
  tier_1: $140K – $220K
  tier_2: $220K – $320K
sustainment: $2.5K – $7.5K per month
duration: 10–16 weeks
```

### Offer 02 — Deal Flow Triage & Memo Drafting

```
code: deal_flow
tagline: Every deck. Every night. Ready by morning.
one_line: An always-on system that reads every inbound pitch deck, scores it against your thesis, drafts the IC memo for the keepers, and shelves the rest with a one-liner.
scope_default: Scoring rubric + memo drafting + routing + one quarter of operation
build_range:
  tier_0: $60K – $110K
  tier_1: $110K – $170K
  tier_2: $170K – $250K
sustainment: $2.5K – $6K per month
duration: 8–14 weeks
```

### Offer 03 — Live Data Intelligence Dashboard

```
code: live_dashboard
tagline: Hours, not months.
one_line: A live, unified intelligence layer that sits above every custodian, bank, fund administrator and operating company — one place to see, ask, and act.
scope_default: Data ingestion + unified data model + dashboard + natural-language query layer
build_range:
  tier_0: $85K – $160K
  tier_1: $160K – $260K
  tier_2: $260K – $400K
sustainment: $3K – $9K per month
duration: 12–20 weeks
```

### Offer 04 — Early-Warning System (Portfolio Oversight)

```
code: early_warning
tagline: Hear about the problem before the CFO does.
one_line: An intelligence layer that reads every portfolio company's monthly report, flags anomalies against trend and peer benchmarks, and produces a board-ready summary the day reports arrive.
scope_default: Report ingestion + anomaly detection + covenant tracking + weekly digest
build_range:
  tier_0: $70K – $130K
  tier_1: $130K – $200K
  tier_2: $200K – $300K
sustainment: $3K – $7K per month
duration: 10–16 weeks
```

### Offer 05 — Structure Engine

```
code: structure_engine
tagline: Every structural question, answered without a call to counsel.
one_line: A contained AI loaded with your family's full legal structure — trusts, LLCs, holdings, agreements — that answers "if we sell asset X out of trust Y, what flows where?" in seconds.
scope_default: Entity graph + document ingestion + query layer + confidence thresholding
build_range:
  tier_0: $110K – $200K
  tier_1: $200K – $320K
  tier_2: $320K – $500K
sustainment: $4K – $10K per month
duration: 14–22 weeks
```

---

## 3 · Recommendation generation

The report's "Recommended path" section is assembled from the top-scoring pains, in the following structure:

```
IF only 1 pain in critical/significant band:
    show: 1 primary offer, 2–3 line recommendation + "where to start" paragraph

IF 2 pains in critical/significant band:
    show: 2 primary offers as a sequenced path
    narrative: "Start with [first offer], add [second offer] within 90 days of go-live"

IF 3 pains in critical/significant band:
    show: all 3 primary offers as a 12-month roadmap
    narrative: "Discovery → first offer (quarter 1) → second (quarter 2) → third (quarter 3)"

IF only modifier scores are high (no pains in critical band):
    show: "No single engagement recommended. We suggest a 30-minute conversation to pressure-test what you've built."
```

---

## 4 · Sequencing logic

When two or more offers are recommended, sequence them in this fixed priority order:

1. **Contained AI Workspace** — always first if recommended. (It unlocks every other sovereign-AI workload.)
2. **Live Data Intelligence Dashboard** — second priority. (Shared data layer feeds other workloads.)
3. **Structure Engine** — third. (Depends on the Workspace being in place.)
4. **Early-Warning System** — fourth. (Depends on the Dashboard for input data.)
5. **Deal Flow Triage** — can run in parallel; sequence by principal preference.

This order is not shown to the respondent as a hierarchy — it's used by the engine to construct the "sequenced path" narrative.

---

## 5 · When no offer is recommended

Three scenarios where the report omits the "Recommended path" section entirely:

- `total_pain_score < 100` → report says *"Your current operation is in good shape. We'd suggest re-running this audit in 6 months as a check-in."*
- `budget_mismatch` flag set → report shows findings only, replaces path with *"We don't believe we're the right fit for your firm at this stage. We'd rather tell you honestly than scope an engagement we can't deliver well."*
- `nurture_only` flag set → report shows findings only, replaces path with *"Nothing to decide today — this report is yours to keep. We'll check in next quarter."*

---

## 6 · Discovery engagement always precedes a build

Every recommended path, regardless of tier, begins with the **Free Discovery Engagement** followed by a **Paid Discovery Engagement** before any build offer:

```
Free Discovery (needs + structural analysis, 45–60 minutes)
    ↓
Paid Discovery Engagement ($10K–$20K, 2–3 weeks)
    ↓
Build offer(s) as mapped above
```

The audit report always frames the first step as the Free Discovery — never as a build.

---

## 7 · Cross-reference

The six pain areas and five offers map 1:1 to:

- The deck's **Section 2 — The Product** (Slides 5–10)
- The Team Playbook's **four strongest offers** (01, 02, 04, 05 in the Playbook numbering)
- The setter calling script's **Section 9 segment-specific pain scripts**

Any change to offer definitions, pricing, or positioning in those documents must be mirrored here to keep the audit report in sync.
