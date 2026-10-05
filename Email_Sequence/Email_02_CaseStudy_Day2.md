---
file: email_02_casestudy_day2
sends: Day 2 after submission (48–72 hours)
purpose: Deliver a case study that mirrors the respondent's top pain, no ask inside
gates:
  - variant must be standard or priority
  - consent_followup must be true
  - no_followup_requested must NOT be set
  - preferred_contact must not be "no_followup"
---

# Email 02 — Case Study Drop (Day 2)

Sent 48–72 hours after submission to respondents who consented to follow-up. The attachment is the Family Office case study PDF already built in your Family Offices folder. No ask inside the email — this is a value drop.

---

## Subject line options (pick one)

1. *A short case scenario that mirrors your audit*
2. *{{first_name}} — one page on how we've done this*
3. *The outcome piece I mentioned*

**Recommended default:** option 1 (ties directly to the audit, reinforces personalisation).

---

## From

Same as Email 01: **Sivakumar Swaminathan · SynexumLabs**

---

## Preheader

> One page. Fifteen minutes. No ask inside.

---

## Body (default)

Hi {{first_name}},

Following your audit two days ago, one quick note.

Your top finding was **{{top_pain_1_label}}** — scored {{top_pain_1_score}}/100.

I'm attaching a one-page case scenario that walks through how we solved exactly that pattern for a family office in a similar position. The structure is simple:

**Problem → Action → Systems → Outcome → Result.**

Fifteen minutes at most. No sales pitch inside.

The reason I'm sending it is pattern-matching. The firm in the case scenario had the same configuration you described — comparable AUM, comparable team size, similar structural complexity. If what we did for them is relevant to what you're thinking about, the parallels will be clear.

I'll follow up briefly in about a week. If anything in the audit or the case scenario raises a question in the meantime, reply directly — we're easy to reach.

Warm regards,
**Sivakumar Swaminathan**
Chief AI Transformation Officer
SynexumLabs · A Coigne Capital company

---

## Body (variant_priority — top finding is critical)

Hi {{first_name}},

A follow-up to the audit from Tuesday.

Attached is a one-page case scenario about the exact pattern we flagged as critical in your report: **{{top_pain_1_label}}**.

The firm in the case had the same configuration you described — comparable AUM, similar operational drag — and the same critical pattern. The scenario walks through what we did, what systems we deployed, and the measurable outcomes.

**Problem → Action → Systems → Outcome → Result.** One page. Fifteen minutes.

I'll follow up briefly in a few days with the calendar link if you'd like to discuss how addressing this one finding would look for your firm specifically. No pressure if the timing isn't right.

Warm regards,
**Sivakumar Swaminathan**
Chief AI Transformation Officer
SynexumLabs · A Coigne Capital company

---

## Attachment selection logic

```
IF top_pain_1 IN ["data_fragmentation", "reporting_lag"]:
    attach: SynexumLabs_CaseStudy_FamilyOffice.pdf  (consolidated intelligence story)
ELSE IF top_pain_1 IN ["structural_complexity"]:
    attach: SynexumLabs_CaseStudy_FamilyOffice.pdf  (structure-engine framing)
ELSE IF top_pain_1 IN ["shadow_ai"]:
    attach: SynexumLabs_CaseStudy_FamilyOffice.pdf  (sovereign workspace framing)
ELSE IF top_pain_1 IN ["portfolio_blindspots"]:
    attach: SynexumLabs_CaseStudy_FamilyOffice.pdf  (early-warning framing)
ELSE IF top_pain_1 IN ["deal_flow_drag"]:
    attach: SynexumLabs_CaseStudy_FamilyOffice.pdf  (deal flow framing)
```

Note: only one case study PDF currently exists in the Family Offices folder. Subject to future expansion — a pain-specific case study library would be an obvious v2 asset.

---

## File naming for the attachment

- `SynexumLabs_FamilyOffice_CaseStudy.pdf` (clean generic name)
- Not personalised in the filename — this is a reusable artefact, not a one-off

---

## Variable reference

```
{{first_name}}            — from A08
{{firm_name}}             — from A08 (not used in default copy; available for the priority variant if desired)
{{top_pain_1_label}}      — top-scored pain, friendly label
{{top_pain_1_score}}      — numeric score 0–100
```

---

## Why no ask inside this email

Email 02 is **deliberately not a selling email**. Three reasons:

1. The audit report (Email 01) already contained the CTA. Repeating it in Email 02 reads as pressure.
2. Giving twice before asking twice builds reciprocity — the next email (Email 03) is where the ask lives.
3. If the respondent decides on their own to reach out before Email 03 arrives, that's a stronger-fit lead than one who responds only to a push.

---

## Suppression rules

Do not send Email 02 if any of the following are true at send-time:

- Respondent replied to Email 01 with "stop," "unsubscribe," "no," or similar
- Respondent replied to Email 01 with a specific objection or question (route to founding partner for personal reply instead)
- Respondent already booked a call via the Email 01 link (route to Email 04 — booking confirmation — instead; see Email_03 for the gating)
- `no_followup_requested` flag is set
- `nurture_only` or `budget_mismatch` flag is set (nurture track skips Email 02 and 03)

---

## Technical notes

- Send window: 48–72 hours after Email 01 was opened (if open-tracking is on) or after submission timestamp (if not)
- Default send time: 9:00 AM in the respondent's timezone (captured in F01)
- Fallback timezone: Eastern Time if not specified
- Subject line A/B eligible: yes (across the three options above, split 34/33/33)
- Attachment delivery: inline attachment, not a download link — inline reads as higher-trust at this stage
