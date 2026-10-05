---
file: branching_rules
purpose: Deterministic rules the quiz engine applies between questions
---

# Branching Rules

Every rule here is machine-interpretable. The quiz engine evaluates them in order after each answer is submitted. Fire order is top-to-bottom; first matching rule wins unless marked `continue`.

---

## 1 · Section flow (top-level)

The audit always runs sections in this order: **A → B → C → D → E → F**. No skips at the section level.

Within sections, individual questions may be shown, skipped, or routed via the rules below.

---

## 2 · Section A (always-shown)

All 8 questions are mandatory. No branching inside Section A. On submit of **A08**, mark the lead as `captured_partial` and trigger the autosave + resume-link email if the respondent abandons after this point.

---

## 3 · Section B (adaptive)

### Rule B.1 — Branch triggers from B01

```
IF B01_primary_pains CONTAINS "data_fragmentation"      THEN show branch B02 (3 questions)
IF B01_primary_pains CONTAINS "reporting_lag"           THEN show branch B03 (3 questions)
IF B01_primary_pains CONTAINS "structural_complexity"   THEN show branch B04 (3 questions)
IF B01_primary_pains CONTAINS "shadow_ai"               THEN show branch B05 (3 questions)
IF B01_primary_pains CONTAINS "portfolio_blindspots"    THEN show branch B06 (3 questions)
IF B01_primary_pains CONTAINS "deal_flow_drag"          THEN show branch B07 (3 questions)
```

Branches are shown in the order the respondent selected them in B01. (Not in alphabetical/code order — in selection order.)

### Rule B.2 — Branch depth cap

If more than 3 branches would fire, only the first 3 selected (max_selections already enforces this). The engine shows those 3 branches in sequence, then advances to Section C.

### Rule B.3 — Branch skip if no fit

If `A03_aum` = `under_25m` AND `B01_primary_pains` only contains `deal_flow_drag`, skip the B07 branch (deal flow volume is unlikely to be meaningful at that scale) and show a short confirmation screen instead reading: *"Noted. We'll weight this lightly in your report."*

---

## 4 · Section C (always-shown)

All 8 questions mandatory. No branching inside Section C.

---

## 5 · Section D (adaptive)

### Rule D.1 — D01 drives subsequent questions

```
IF D01_prior_attempts = "no"          THEN skip D02, D03, D04 → go directly to D05
IF D01_prior_attempts = "partial"     THEN show D02 only → skip D03, D04 → D05
IF D01_prior_attempts = "yes"         THEN show D02, D03, D04 → D05
```

D05 is always shown.

---

## 6 · Section E (always-shown)

All 5 questions mandatory. E04 and E05 are optional text fields but the screens are always presented.

### Rule E.1 — Qualification flags

```
IF E01_authority = "not_me"                              THEN set flag: not_decision_maker
IF E02_timeline = "no_timeline"                          THEN set flag: nurture_only
IF E03_budget = "under_25k"                              THEN set flag: budget_mismatch
```

Flags cumulate. See `Scoring_Model.md` → "Qualification handling" for how flags affect the report and the CTA.

---

## 7 · Section F

Both questions mandatory. No branching inside.

### Rule F.1 — Phone optional, consent required

If `F02_consent.consent_report` or `F02_consent.consent_privacy` is unchecked, display inline validation and block submission.

### Rule F.2 — Follow-up gating

```
IF F01.preferred_contact = "no_followup"
    THEN uncheck F02.consent_followup
    AND set flag: no_followup_requested
    AND email sequence stops after Email_01
```

---

## 8 · Report routing

After submission, the respondent's answers are scored (see `Scoring_Model.md`) and routed into one of four report variants:

```
IF total_pain_score < 100                              → variant_light (soft recommendations, no CTA)
IF total_pain_score >= 100 AND readiness_score < 20    → variant_nurture (full findings, soft CTA)
IF total_pain_score >= 100 AND readiness_score >= 20   → variant_standard (full findings, hard CTA)
IF total_pain_score >= 200 AND readiness_score >= 25   → variant_priority (flagged for partner review)
```

Variants only affect the report's recommendation strength and CTA language — the findings themselves are generated from the same scoring data for all variants.

---

## 9 · Resume handling

A respondent who abandons mid-audit receives a resume link at the email captured in A08. Clicking the link reopens the quiz at the last unanswered question. Resumed sessions are valid for 14 days.

---

## 10 · Rule override log

For transparency when debugging:

- Every triggered branch logs: `question_id`, `triggering_answer`, `timestamp`
- Every skipped question logs: `question_id`, `skip_reason`, `timestamp`
- Every applied flag logs: `flag_name`, `source_question_id`, `timestamp`

Audit trail retained with the lead record for 24 months.
