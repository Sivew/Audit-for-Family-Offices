---
file: email_01_report_delivery
sends: Within 5 minutes of audit submission
purpose: Deliver the audit report PDF with a short, substantive accompanying note
---

# Email 01 — Audit Report Delivery

Sent automatically within 5 minutes of submission. Attached: the generated audit report PDF.

---

## Subject line options (pick one)

1. *Your Operational Readiness Audit — {{firm_name}}*
2. *Your audit is ready, {{first_name}}*
3. *Confidential: your SynexumLabs audit report*

**Recommended default:** option 1 (most professional, personalised).

---

## From

**Name:** Sivakumar Swaminathan · SynexumLabs
**Email:** [founding-partner-shared-inbox]
**Reply-to:** same as from

---

## Preheader (shown in inbox preview)

> One PDF attached. Three findings. A single highest-leverage change for your quarter.

---

## Body (default — variant_standard)

Hi {{first_name}},

Your audit is attached.

A few things worth saying before you open it.

**It was reviewed by hand.** Every audit that leaves our office is read by one of our founding partners before it's sent. Yours was reviewed by me this morning. The findings reflect what we actually saw in your answers — not a template.

**Three findings. One priority.** Page 3 names three operational areas creating meaningful friction at {{firm_name}} today. Page 4 plots them on a matrix of impact against effort — the single highest-leverage change for your quarter is called out at the bottom.

**No follow-up unless you want one.** You selected {{F01_preferred_contact_label}} as your preference. We'll honour it. {{conditional_followup_sentence}}

If a specific finding doesn't ring true — or if a number we cited looks off — reply directly. We'd rather fix the report than let you form a view based on a wrong read.

Warm regards,
**Sivakumar Swaminathan**
Chief AI Transformation Officer
SynexumLabs · A Coigne Capital company

P.S. — The report is confidential. We retain it for 24 months unless you ask us to delete it sooner. Reply "delete" at any time and we remove every trace within 48 hours.

---

## Body (variant_priority — one finding is critical)

Hi {{first_name}},

Your audit is attached — and one finding in it needs a direct note.

**{{top_pain_1_label}} scored {{top_pain_1_score}}/100 for your firm.** That puts it in the "critical" band. It isn't the only finding in the report, but it's the one I'd want you to read first.

We've seen this exact pattern at firms of your shape before. It is solvable. The reason I'm writing a separate note is that the pattern tends to compound quickly — if nothing changes architecturally in the next 90 days, it typically gets worse, not better.

The full report (pages 3–5) explains the finding in detail and lays out what addressing it would look like.

No pressure on the discovery call. {{conditional_booking_sentence}}

Warm regards,
**Sivakumar Swaminathan**
Chief AI Transformation Officer
SynexumLabs · A Coigne Capital company

P.S. — If you want to walk through this one finding specifically — not a full sales conversation — I'd welcome 15 minutes. Just reply.

---

## Body (variant_light — soft findings only)

Hi {{first_name}},

Your audit is attached.

**Honest read:** your operation is in solid shape. The findings in the report point to incremental improvements, not foundational gaps. {{firm_name}} is running better than most of the family offices we see.

A few things might be worth watching — those are on page 3 — but nothing that calls for immediate action.

I'd suggest re-running the audit in two quarters as a check-in. If anything shifts materially before then, our line is always open.

Warm regards,
**Sivakumar Swaminathan**
Chief AI Transformation Officer
SynexumLabs · A Coigne Capital company

P.S. — The report is yours to keep. We retain our copy for 24 months unless you ask us to delete it.

---

## Body (variant_nurture — timing not right)

Hi {{first_name}},

Your audit is attached.

The pattern we see is familiar — there's real friction in your operation, but your timeline on {{E02_timeline_label}} suggests this isn't the right quarter to act on it. That's completely reasonable.

The report is yours to keep. Nothing in it is time-sensitive — the findings will still be true in two quarters, and the recommendations won't move.

**No calendar push.** When the window opens, you'll know where to find us. Until then, the only email you'll see from me is a brief check-in next quarter.

Warm regards,
**Sivakumar Swaminathan**
Chief AI Transformation Officer
SynexumLabs · A Coigne Capital company

---

## Body (not_decision_maker flag set)

Hi {{first_name}},

Your audit is attached.

You mentioned the final decision would sit with someone other than you. The report is written in a way that forwards cleanly — it's addressed to {{firm_name}} as a whole, not to any individual.

If you'd like to share it, feel free. If you'd like a second copy formatted for your principal specifically (with their name and your context), reply to this email and we'll send one.

The findings themselves are yours as the person who answered — the report is confidential to you and {{firm_name}}.

Warm regards,
**Sivakumar Swaminathan**
Chief AI Transformation Officer
SynexumLabs · A Coigne Capital company

---

## Variable reference

```
{{first_name}}                      — from A08
{{firm_name}}                       — from A08
{{F01_preferred_contact_label}}     — resolved from F01
{{conditional_followup_sentence}}   — generated from variant + preferences
{{conditional_booking_sentence}}    — generated from variant + preferences
{{top_pain_1_label}}                — top-scored pain
{{top_pain_1_score}}                — score 0–100
{{E02_timeline_label}}              — from E02
```

### `conditional_followup_sentence` resolution

```
IF variant = standard/priority AND consent_followup = true:
    "In the next week you'll receive one short email with a case study, and a calendar link if you'd like to book a call. If you'd rather not, reply 'stop' any time."

IF variant = light:
    "If you'd like to pressure-test anything in the report, the calendar link is in the footer below."

IF variant = nurture OR consent_followup = false:
    "No further emails from us this quarter."

IF no_followup_requested:
    "No further emails from us at all — as you requested."
```

### `conditional_booking_sentence` resolution

```
IF variant = priority AND readiness_score >= 25:
    "If you'd like to discuss what addressing it would look like, our founding-partner Discovery call is 30 minutes, no cost. Calendar link in the report footer."

IF variant = priority AND readiness_score < 25:
    "No action required today — the report is yours to use when the timing is right."

Default fallback:
    "The booking link is in the report if you'd like it."
```

---

## Technical notes

- Send-time guarantee: **≤5 minutes** from submission to delivery
- From-domain: synexumlabs.com (DKIM + SPF + DMARC all passing — critical for inbox placement)
- Attachment name: `SynexumLabs_Audit_{{firm_name_slug}}_{{submission_date_short}}.pdf`
- Open tracking: optional, respect regional law (off by default in EU/UK)
- Click tracking: on for the calendar link only, off for everything else
- Unsubscribe footer: present on every email, honoured within 24h
