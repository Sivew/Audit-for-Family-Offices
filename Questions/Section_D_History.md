---
section: D
title: What You've Tried
subtitle: "Five questions on prior attempts to solve this. The audit cites them specifically — so we never recommend what you've already ruled out."
show_when: always
questions_count: 5
estimated_minutes: 1.5
---

# Section D — History & Prior Attempts

Shown to all respondents. These answers are referenced in the "Current State" and "Recommended Path" sections of the report to make it feel personalised rather than generic.

---

## D01 — Prior attempts

```yaml
id: D01_prior_attempts
type: single_choice
required: true
label: "Have you previously tried to solve the pain areas you flagged?"
options:
  - value: yes
    label: "Yes — one or more serious attempts"
    triggers: [D02_what_tried, D03_what_failed, D04_budget_spent]
  - value: partial
    label: "Partial attempts — nothing committed"
    triggers: [D02_what_tried]
  - value: no
    label: "No — this is the first serious look"
    skip_to: D05_internal_capability
```

---

## D02 — What was tried

**Shown if:** `D01` ≠ `no`

```yaml
id: D02_what_tried
type: multi_choice
required: true
label: "What approaches have you tried? (select all that apply)"
options:
  - value: consultant
    label: "Hired a management or technology consultant"
    scores: { counsel_dependency: 10 }
  - value: software_vendor
    label: "Bought a software platform or SaaS product"
  - value: in_house_dev
    label: "Built something in-house"
  - value: added_headcount
    label: "Added internal headcount"
    scores: { team_bottleneck_risk: 10 }
  - value: outsourced
    label: "Outsourced the function entirely"
    scores: { counsel_dependency: 15 }
  - value: ai_pilot
    label: "Ran an AI pilot or proof-of-concept"
  - value: nothing_shipped
    label: "Started something but never shipped it"
```

---

## D03 — What didn't work

**Shown if:** `D01` = `yes`

```yaml
id: D03_what_failed
type: multi_choice
required: false
label: "What specifically didn't work? (select up to three)"
help_text: "This is used verbatim in your audit report. We write around these, not into them."
max_selections: 3
options:
  - value: wrong_scope
    label: "Scope was wrong — solved the wrong problem"
  - value: adoption
    label: "Nobody internally adopted it"
  - value: integration
    label: "Integration with existing systems failed"
    scores: { data_fragmentation: 10 }
  - value: compliance_pushback
    label: "Compliance / GC pushback blocked deployment"
    scores: { governance_risk: 10 }
  - value: too_generic
    label: "Too generic — didn't fit our firm's specifics"
  - value: vendor_abandoned
    label: "Vendor abandoned us post-deployment"
  - value: cost_overrun
    label: "Cost overran significantly"
  - value: never_scaled
    label: "Worked for a pilot, never scaled"
  - value: still_running
    label: "Still running, but delivering less than promised"
```

---

## D04 — Prior spend

**Shown if:** `D01` = `yes`

```yaml
id: D04_prior_spend
type: single_choice
required: false
label: "Approximately how much have you invested in prior attempts to solve these problems?"
help_text: "Rough band is fine. Used only to calibrate the investment range in your recommended path."
options:
  - value: under_50k
    label: "Under $50K"
  - value: 50_200k
    label: "$50K – $200K"
  - value: 200_750k
    label: "$200K – $750K"
  - value: 750k_2m
    label: "$750K – $2M"
  - value: over_2m
    label: "Over $2M"
  - value: prefer_not
    label: "Prefer not to say"
```

---

## D05 — Internal technical capability

```yaml
id: D05_internal_capability
type: single_choice
required: true
label: "What is your internal technical capability today?"
options:
  - value: full_team
    label: "A full in-house technology team"
  - value: one_person
    label: "One technologist / IT lead"
  - value: outsourced_it
    label: "Outsourced IT — no internal engineering"
    scores: { team_bottleneck_risk: 15 }
  - value: none
    label: "No formal technology function"
    scores: { team_bottleneck_risk: 25, counsel_dependency: 15 }
  - value: dont_need
    label: "We've never needed one, and still don't think we do"
```
