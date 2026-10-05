---
section: B
title: Where It Hurts
subtitle: "One primary question identifies your top pain areas. The follow-up questions you see depend entirely on what you select."
show_when: always
questions_count: "1 primary + 2–5 adaptive follow-ups"
estimated_minutes: 3
---

# Section B — Pain Diagnostic (adaptive)

This section is the heart of the audit. The respondent picks their top 2–3 pain areas in **B01**, and only the follow-ups matching those selections are shown. Average respondent sees **B01 + 2 branches** (= 1 + 6–10 additional questions). Max exposure: all six branches (~22 questions) for respondents who flag everything as painful.

The six pain branches map 1:1 to SynexumLabs offers — see `Logic/Offer_Mapping.md`.

---

## B01 — Primary pain selection (multi-select, required)

```yaml
id: B01_primary_pains
type: multi_choice
required: true
min_selections: 1
max_selections: 3
label: "Which of the following creates the most friction in your office right now?"
help_text: "Pick up to three. We'll go deeper on the ones you select — no deeper on the ones you don't."
options:
  - value: data_fragmentation
    label: "Our data is scattered across custodians, banks, and operating companies — no single view"
    triggers: [B02_data_fragmentation]
    scores:
      data_fragmentation: 25
  - value: reporting_lag
    label: "Consolidated numbers arrive 30–90 days after quarter-end — too late to act on"
    triggers: [B03_reporting_lag]
    scores:
      reporting_lag: 25
  - value: structural_complexity
    label: "Every structural question routes to outside counsel — slow and expensive"
    triggers: [B04_structural_complexity]
    scores:
      structural_complexity: 25
  - value: shadow_ai
    label: "Our team is using ChatGPT or similar tools with sensitive documents — and we're uncomfortable with it"
    triggers: [B05_shadow_ai]
    scores:
      shadow_ai: 30
      governance_risk: 20
  - value: portfolio_blindspots
    label: "Portfolio company issues surface too late — we read about them in the monthly report"
    triggers: [B06_portfolio_blindspots]
    scores:
      portfolio_blindspots: 25
  - value: deal_flow_drag
    label: "We get too many inbound deals to review properly — good ones are slipping"
    triggers: [B07_deal_flow]
    scores:
      deal_flow_drag: 25
```

---

## B02 — Data fragmentation branch

**Shown if:** `B01` includes `data_fragmentation`

### B02a

```yaml
id: B02a_source_count
type: single_choice
required: true
label: "How many separate data sources feed your consolidated picture?"
help_text: "Custodians, banks, fund administrators, operating company ERPs, insurance carriers, etc."
options:
  - value: 1_5
    label: "1–5"
    scores: { data_fragmentation: 5 }
  - value: 6_15
    label: "6–15"
    scores: { data_fragmentation: 15 }
  - value: 16_30
    label: "16–30"
    scores: { data_fragmentation: 25 }
  - value: over_30
    label: "Over 30"
    scores: { data_fragmentation: 35 }
```

### B02b

```yaml
id: B02b_consolidation_method
type: single_choice
required: true
label: "How is consolidation done today?"
options:
  - value: excel_manual
    label: "Excel, manually, by one or two people"
    scores: { data_fragmentation: 25, team_bottleneck_risk: 15 }
  - value: excel_macros
    label: "Excel with macros / automation we built"
    scores: { data_fragmentation: 15 }
  - value: dedicated_platform
    label: "A dedicated reporting platform (Addepar, Masttro, etc.)"
    scores: { data_fragmentation: 5 }
  - value: outsourced
    label: "Outsourced to our accountant or admin firm"
    scores: { data_fragmentation: 10, counsel_dependency: 10 }
```

### B02c

```yaml
id: B02c_time_cost
type: single_choice
required: true
label: "How many person-hours per month are spent getting to a consolidated view?"
options:
  - value: under_20
    label: "Under 20 hours"
  - value: 20_60
    label: "20–60 hours"
    scores: { data_fragmentation: 10 }
  - value: 60_160
    label: "60–160 hours (effectively one FTE)"
    scores: { data_fragmentation: 20, team_bottleneck_risk: 15 }
  - value: over_160
    label: "Over 160 hours (more than one FTE)"
    scores: { data_fragmentation: 30, team_bottleneck_risk: 25 }
```

---

## B03 — Reporting lag branch

**Shown if:** `B01` includes `reporting_lag`

### B03a

```yaml
id: B03a_lag_days
type: single_choice
required: true
label: "How many days after quarter-end do you see fully consolidated numbers?"
options:
  - value: under_15
    label: "Under 15 days"
    scores: { reporting_lag: 5 }
  - value: 15_30
    label: "15–30 days"
    scores: { reporting_lag: 10 }
  - value: 30_60
    label: "30–60 days"
    scores: { reporting_lag: 20 }
  - value: over_60
    label: "Over 60 days"
    scores: { reporting_lag: 35 }
  - value: dont_know
    label: "Honestly, I don't know how long it takes"
    scores: { reporting_lag: 20, governance_risk: 10 }
```

### B03b

```yaml
id: B03b_consequences
type: multi_choice
label: "Has the reporting lag led to any of the following in the last 12 months? (select all that apply)"
required: false
options:
  - value: missed_rebalance
    label: "Missed rebalancing opportunity"
    scores: { reporting_lag: 10 }
  - value: late_covenant
    label: "Covenant breach noticed too late"
    scores: { reporting_lag: 15, portfolio_blindspots: 10 }
  - value: tax_surprise
    label: "Tax surprise that could have been planned around"
    scores: { reporting_lag: 15, counsel_dependency: 10 }
  - value: principal_frustration
    label: "Principal frustration voiced in a review meeting"
    scores: { reporting_lag: 15, principal_frustration: 20 }
  - value: none
    label: "None of the above"
```

### B03c

```yaml
id: B03c_variance_source
type: single_choice
required: true
label: "When numbers move materially between quarters, how is the variance explained?"
options:
  - value: written_memo
    label: "A written variance memo prepared by our team"
    scores: { reporting_lag: 5 }
  - value: verbal_meeting
    label: "A verbal explanation in the review meeting"
    scores: { reporting_lag: 15 }
  - value: not_explained
    label: "The principal digs into it themselves"
    scores: { reporting_lag: 25, principal_frustration: 20 }
  - value: no_review
    label: "There is no formal variance review"
    scores: { reporting_lag: 20, governance_risk: 15 }
```

---

## B04 — Structural complexity branch

**Shown if:** `B01` includes `structural_complexity`

### B04a

```yaml
id: B04a_counsel_spend
type: single_choice
required: true
label: "Approximate annual spend on outside legal counsel for structural questions"
help_text: "Trust / entity / cross-border structuring questions only — not litigation or transactions."
options:
  - value: under_50k
    label: "Under $50K"
  - value: 50_150k
    label: "$50K – $150K"
    scores: { structural_complexity: 10, counsel_dependency: 15 }
  - value: 150_400k
    label: "$150K – $400K"
    scores: { structural_complexity: 20, counsel_dependency: 25 }
  - value: over_400k
    label: "Over $400K"
    scores: { structural_complexity: 30, counsel_dependency: 35 }
  - value: dont_know
    label: "I don't have an exact number"
    scores: { structural_complexity: 15, counsel_dependency: 15 }
```

### B04b

```yaml
id: B04b_query_frequency
type: single_choice
required: true
label: "How often does your team ask outside counsel a structural question?"
options:
  - value: daily
    label: "Several times a week"
    scores: { structural_complexity: 25, counsel_dependency: 25 }
  - value: weekly
    label: "Weekly"
    scores: { structural_complexity: 15, counsel_dependency: 15 }
  - value: monthly
    label: "Monthly"
    scores: { structural_complexity: 10 }
  - value: rarely
    label: "A few times a year"
```

### B04c

```yaml
id: B04c_holder_knowledge
type: single_choice
required: true
label: "Does anyone on the internal team hold the full structure in their head?"
options:
  - value: yes_one
    label: "Yes — one person"
    scores: { structural_complexity: 15, team_bottleneck_risk: 20 }
  - value: yes_several
    label: "Yes — several people together"
  - value: no
    label: "No — nobody really does"
    scores: { structural_complexity: 25, counsel_dependency: 20 }
  - value: dont_know
    label: "I'm not sure"
    scores: { structural_complexity: 15 }
```

---

## B05 — Shadow AI branch

**Shown if:** `B01` includes `shadow_ai`

### B05a

```yaml
id: B05a_tools_used
type: multi_choice
required: false
label: "Which AI tools has your team used in the last 90 days? (select all that apply)"
options:
  - value: chatgpt
    label: "ChatGPT (public)"
    scores: { shadow_ai: 15, governance_risk: 15 }
  - value: claude
    label: "Claude (public)"
    scores: { shadow_ai: 15, governance_risk: 15 }
  - value: copilot
    label: "Microsoft Copilot / Office AI"
    scores: { shadow_ai: 5 }
  - value: perplexity
    label: "Perplexity"
    scores: { shadow_ai: 5 }
  - value: unknown
    label: "I know they're using something, I don't know what"
    scores: { shadow_ai: 25, governance_risk: 25 }
  - value: none_approved
    label: "None — we've banned them, but I'm not sure the ban is being followed"
    scores: { shadow_ai: 20, governance_risk: 15 }
```

### B05b

```yaml
id: B05b_doc_exposure
type: single_choice
required: true
label: "Have any of the following types of documents been pasted into a public AI tool, to your knowledge?"
options:
  - value: deal_memos
    label: "Deal memos or investment analysis"
    scores: { shadow_ai: 25, governance_risk: 25 }
  - value: tax_filings
    label: "Tax filings or structural documents"
    scores: { shadow_ai: 30, governance_risk: 30 }
  - value: family_comms
    label: "Family communications or sensitive personal information"
    scores: { shadow_ai: 30, governance_risk: 30 }
  - value: general_docs
    label: "Only general documents — nothing sensitive"
    scores: { shadow_ai: 5 }
  - value: nothing
    label: "Nothing has been pasted — I'm confident"
  - value: dont_know
    label: "I honestly don't know"
    scores: { shadow_ai: 20, governance_risk: 25 }
```

### B05c

```yaml
id: B05c_gc_position
type: single_choice
required: true
label: "What is your General Counsel / Chief Compliance Officer's current position on AI use?"
options:
  - value: full_ban
    label: "Full ban — no AI tools permitted"
    scores: { shadow_ai: 10, governance_risk: 10 }
  - value: unclear
    label: "No formal policy — unclear what's permitted"
    scores: { shadow_ai: 20, governance_risk: 25 }
  - value: informal_ok
    label: "Informally OK, no written rules"
    scores: { shadow_ai: 25, governance_risk: 25 }
  - value: approved_tools
    label: "Approved tool list in place and enforced"
    scores: { shadow_ai: 5 }
  - value: no_gc
    label: "We don't have a GC or CCO"
    scores: { governance_risk: 15 }
```

---

## B06 — Portfolio blindspots branch

**Shown if:** `B01` includes `portfolio_blindspots`

### B06a

```yaml
id: B06a_report_cadence
type: single_choice
required: true
label: "How often do you receive management reports from portfolio companies?"
options:
  - value: weekly
    label: "Weekly"
  - value: monthly
    label: "Monthly"
    scores: { portfolio_blindspots: 10 }
  - value: quarterly
    label: "Quarterly"
    scores: { portfolio_blindspots: 25 }
  - value: inconsistent
    label: "Inconsistent — depends on the company"
    scores: { portfolio_blindspots: 30 }
```

### B06b

```yaml
id: B06b_surprise_frequency
type: single_choice
required: true
label: "In the last 24 months, how often has a portfolio company issue surfaced late — meaning you heard about it after it became a crisis?"
options:
  - value: never
    label: "Never"
  - value: once
    label: "Once"
    scores: { portfolio_blindspots: 15 }
  - value: twice
    label: "Twice"
    scores: { portfolio_blindspots: 25 }
  - value: three_plus
    label: "Three or more times"
    scores: { portfolio_blindspots: 35, principal_frustration: 20 }
```

### B06c

```yaml
id: B06c_covenant_tracking
type: single_choice
required: true
label: "How are debt covenants and KPI thresholds tracked across the portfolio?"
options:
  - value: automated
    label: "Automated — alerts fire when thresholds approach"
  - value: manual_spreadsheet
    label: "Manually in a spreadsheet, reviewed periodically"
    scores: { portfolio_blindspots: 15 }
  - value: by_cfo
    label: "The portfolio company CFO is expected to flag it"
    scores: { portfolio_blindspots: 20 }
  - value: not_tracked
    label: "Not tracked at the family office level"
    scores: { portfolio_blindspots: 30, governance_risk: 15 }
```

---

## B07 — Deal flow drag branch

**Shown if:** `B01` includes `deal_flow_drag`

### B07a

```yaml
id: B07a_inbound_volume
type: single_choice
required: true
label: "Approximate inbound deal volume per week (funds + direct + intros)"
options:
  - value: under_10
    label: "Under 10"
  - value: 10_30
    label: "10–30"
    scores: { deal_flow_drag: 15 }
  - value: 30_60
    label: "30–60"
    scores: { deal_flow_drag: 25 }
  - value: over_60
    label: "Over 60"
    scores: { deal_flow_drag: 35, team_bottleneck_risk: 15 }
```

### B07b

```yaml
id: B07b_real_review_rate
type: single_choice
required: true
label: "What portion of inbound deals get a genuine, documented first review?"
options:
  - value: all
    label: "All of them"
  - value: most
    label: "Most — 60-80%"
    scores: { deal_flow_drag: 10 }
  - value: half
    label: "About half"
    scores: { deal_flow_drag: 20 }
  - value: few
    label: "A minority — maybe 20-30%"
    scores: { deal_flow_drag: 30 }
  - value: unknown
    label: "Honestly, I don't know"
    scores: { deal_flow_drag: 25 }
```

### B07c

```yaml
id: B07c_memo_process
type: single_choice
required: true
label: "How does a deal that passes initial screen become an investment committee memo?"
options:
  - value: analyst_writes
    label: "An internal analyst writes it from scratch"
    scores: { deal_flow_drag: 15, team_bottleneck_risk: 10 }
  - value: external
    label: "An external consultant drafts it"
    scores: { deal_flow_drag: 10, counsel_dependency: 10 }
  - value: pdf_summary
    label: "We skim the PDF and summarise verbally"
    scores: { deal_flow_drag: 25 }
  - value: no_memo
    label: "There's no formal memo — decisions are made directly"
    scores: { deal_flow_drag: 30, governance_risk: 15 }
```
