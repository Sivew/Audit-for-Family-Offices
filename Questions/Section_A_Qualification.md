---
section: A
title: Firm Profile
subtitle: Eight short questions. We use these to shape every finding in your report against your firm's actual size and complexity.
show_when: always
questions_count: 8
estimated_minutes: 2
---

# Section A — Firm Profile

Every respondent sees all eight questions. These establish the firm's shape and are referenced throughout the audit report. The email capture at A08 ensures partial completions still generate leads.

---

## A01 — Role

```yaml
id: A01_role
type: single_choice
required: true
label: "What is your role in the family office?"
help_text: "This shapes the lens your audit report is written through."
options:
  - value: principal
    label: "Principal / head of family"
    scores:
      principal_voice: 1
  - value: cio
    label: "Chief Investment Officer"
    scores:
      investment_lens: 1
  - value: coo
    label: "Chief Operating Officer / Family Office Executive"
    scores:
      operations_lens: 1
  - value: cfo
    label: "Chief Financial Officer / Controller"
    scores:
      finance_lens: 1
  - value: advisor
    label: "External advisor to a family office"
    scores:
      external_lens: 1
  - value: other
    label: "Other"
    scores:
      external_lens: 1
```

---

## A02 — Firm type

```yaml
id: A02_firm_type
type: single_choice
required: true
label: "Which best describes your firm?"
options:
  - value: sfo
    label: "Single Family Office (one family)"
  - value: mfo
    label: "Multi Family Office (several families)"
  - value: embedded
    label: "Family office embedded inside an operating company"
  - value: virtual
    label: "Virtual / outsourced family office setup"
  - value: forming
    label: "Still being formed — we don't operate as one yet"
```

---

## A03 — AUM range

```yaml
id: A03_aum
type: single_choice
required: true
label: "Approximate assets under management"
help_text: "Across all family-controlled vehicles. A rough band is fine."
options:
  - value: under_25m
    label: "Under $25M"
    disqualify_soft: true
  - value: 25_100m
    label: "$25M – $100M"
  - value: 100_500m
    label: "$100M – $500M"
  - value: 500_1b
    label: "$500M – $1B"
  - value: 1_5b
    label: "$1B – $5B"
  - value: over_5b
    label: "Over $5B"
    scores:
      complexity_tier: 2
```

---

## A04 — Team size

```yaml
id: A04_team_size
type: single_choice
required: true
label: "How many people work in the family office operation?"
help_text: "Full-time equivalents, excluding external advisors."
options:
  - value: 1_3
    label: "1–3"
    scores:
      team_bottleneck_risk: 20
  - value: 4_8
    label: "4–8"
    scores:
      team_bottleneck_risk: 15
  - value: 9_15
    label: "9–15"
    scores:
      team_bottleneck_risk: 10
  - value: 16_30
    label: "16–30"
  - value: over_30
    label: "Over 30"
    scores:
      complexity_tier: 1
```

---

## A05 — Jurisdictions

```yaml
id: A05_jurisdictions
type: single_choice
required: true
label: "In how many jurisdictions are the family's assets held?"
help_text: "Countries or states/provinces where entities, properties, or accounts are domiciled."
options:
  - value: 1_3
    label: "1–3"
  - value: 4_10
    label: "4–10"
    scores:
      structural_complexity: 10
  - value: 11_20
    label: "11–20"
    scores:
      structural_complexity: 20
  - value: over_20
    label: "Over 20"
    scores:
      structural_complexity: 30
  - value: dont_know
    label: "Honestly, I'm not sure"
    scores:
      structural_complexity: 15
      governance_risk: 10
```

---

## A06 — Legal entities

```yaml
id: A06_entities
type: single_choice
required: true
label: "Approximate number of legal entities (trusts, LLCs, holdings, foundations)"
help_text: "Including dormant ones. A rough count is fine."
options:
  - value: under_10
    label: "Fewer than 10"
  - value: 10_30
    label: "10–30"
    scores:
      structural_complexity: 10
  - value: 30_75
    label: "30–75"
    scores:
      structural_complexity: 20
  - value: over_75
    label: "Over 75"
    scores:
      structural_complexity: 30
      counsel_dependency: 20
  - value: dont_know
    label: "I don't have an exact number"
    scores:
      structural_complexity: 15
      counsel_dependency: 15
```

---

## A07 — Portfolio companies

```yaml
id: A07_portfolio_companies
type: single_choice
required: true
label: "How many operating businesses or portfolio companies does the family own, directly or via holdings?"
options:
  - value: zero
    label: "None"
  - value: 1_3
    label: "1–3"
    scores:
      portfolio_blindspots: 10
  - value: 4_10
    label: "4–10"
    scores:
      portfolio_blindspots: 25
  - value: over_10
    label: "More than 10"
    scores:
      portfolio_blindspots: 40
```

---

## A08 — Email capture

```yaml
id: A08_contact_gate
type: contact_form
required: true
label: "Where should we send your audit report?"
help_text: "Delivered within 5 minutes of completion. Confidential and single-recipient."
fields:
  - name: first_name
    label: "First name"
    type: text
    required: true
  - name: last_name
    label: "Last name"
    type: text
    required: true
  - name: email
    label: "Business email"
    type: email
    required: true
  - name: firm_name
    label: "Family office or firm name"
    type: text
    required: true
    privacy_note: "We never publish firm names. Used only to personalise your report."
behavior_on_submit: save_lead_as_partial
```

Note to builder: once A08 is submitted, the lead is captured even if the respondent abandons after. Partial completers trigger `Email_01_Report_Delivery.md` in "partial" mode, which delivers whatever findings are possible from the data gathered so far and invites them to resume.
