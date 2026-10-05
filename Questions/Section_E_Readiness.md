---
section: E
title: Readiness
subtitle: "Five questions on who signs off, when you'd want to start, and what success looks like. These shape the recommended engagement path."
show_when: always
questions_count: 5
estimated_minutes: 1.5
---

# Section E — Readiness

The answers here decide which engagement tier appears in the recommended path section of the audit report, and whether the respondent sees a discovery-call CTA at all.

---

## E01 — Decision authority

```yaml
id: E01_authority
type: single_choice
required: true
label: "Who makes the final decision on an engagement of this type?"
options:
  - value: me
    label: "I do"
  - value: me_and_cfo
    label: "Me, with the CFO or COO"
  - value: principal_only
    label: "The principal — I would recommend"
  - value: committee
    label: "A committee or family council"
  - value: not_me
    label: "Someone else entirely"
    qualification_flag: not_decision_maker
```

---

## E02 — Timeline

```yaml
id: E02_timeline
type: single_choice
required: true
label: "If you found the right partner, when would you want to begin?"
options:
  - value: immediately
    label: "Immediately — within 30 days"
    scores: { readiness_score: 30 }
  - value: 1_3_months
    label: "Within 1–3 months"
    scores: { readiness_score: 25 }
  - value: 3_6_months
    label: "Within 3–6 months"
    scores: { readiness_score: 15 }
  - value: 6_12_months
    label: "Within 6–12 months"
    scores: { readiness_score: 10 }
  - value: no_timeline
    label: "No timeline — just exploring"
    scores: { readiness_score: 5 }
    qualification_flag: nurture_only
```

---

## E03 — Budget range

```yaml
id: E03_budget
type: single_choice
required: true
label: "What budget range are you prepared to consider for the right engagement?"
help_text: "Directional only. Used to recommend the appropriate tier — not a quote."
options:
  - value: under_25k
    label: "Under $25K"
    scores: { readiness_score: 5 }
  - value: 25_100k
    label: "$25K – $100K"
    scores: { readiness_score: 15 }
  - value: 100_300k
    label: "$100K – $300K"
    scores: { readiness_score: 25 }
  - value: 300k_1m
    label: "$300K – $1M"
    scores: { readiness_score: 30 }
  - value: 1m_plus
    label: "Over $1M"
    scores: { readiness_score: 30 }
  - value: unknown
    label: "Haven't scoped it yet"
    scores: { readiness_score: 10 }
```

---

## E04 — Success metric

```yaml
id: E04_success_metric
type: textarea
required: false
max_chars: 300
label: "What would make this a 'clear success' 90 days from now?"
placeholder: "In your own words — a sentence or two is enough."
help_text: "Your answer appears, lightly edited, in the recommended path section of the audit report."
scoring_note: "Not scored — used verbatim in the report."
```

---

## E05 — Failure definition

```yaml
id: E05_failure_definition
type: textarea
required: false
max_chars: 300
label: "What would make this an obvious failure?"
placeholder: "What outcome, 90 days in, would make you say 'this didn't work'?"
help_text: "This is one of the most useful questions in the audit — be concrete if you can."
scoring_note: "Not scored — used verbatim in the report to show we've read it."
```
