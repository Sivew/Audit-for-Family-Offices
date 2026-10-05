---
file: email_03_followup_day7
sends: Day 7 after submission
purpose: The booking push — invites a 30-minute founding-partner Discovery call
gates:
  - variant must be standard or priority
  - consent_followup must be true
  - no_followup_requested must NOT be set
  - preferred_contact must not be "no_followup"
  - respondent must not have booked already
  - respondent must not have replied "stop" or similar
---

# Email 03 — Follow-Up & Booking Push (Day 7)

Final automatic email in the sequence. This is where the explicit calendar ask lives.

If the respondent doesn't engage with this email within 14 days, the sequence ends and the lead moves to a 90-day nurture cycle (one touch per quarter).

---

## Subject line options

1. *Was any of this useful, {{first_name}}?*
2. *30 minutes with our founding partners?*
3. *Following up on your {{firm_name}} audit*

**Recommended default:** option 1 — genuine, low-pressure, signals the email is a check-in rather than a sales push.

---

## From

Same as prior emails: **Sivakumar Swaminathan · SynexumLabs**

---

## Preheader

> No pressure — just checking in. Calendar link inside if useful.

---

## Body (default — variant_standard)

Hi {{first_name}},

A week ago we sent your Operational Readiness Audit for {{firm_name}}. A few days after, the case scenario on the pattern we saw.

**I'm writing briefly to ask one thing:** was any of it useful?

I don't need a long reply. A one-liner is fine. The reason I'm asking is pragmatic — the audit and the case scenario cost you ten minutes to receive, and if neither of them resonated, that's useful information for us to know.

If anything in the audit **did** resonate, here's what the next step looks like.

Our founding-partner Discovery call is 30–45 minutes. Both {{partner_1_name}} and {{partner_2_name}} are on it. We walk through our process step by step, ask meaningful questions about your firm, and give you an honest, transparent assessment at the end of the call — is {{firm_name}} the right fit for what we build, or not. No pitch, no obligation.

**[Book 30 minutes · {{calendar_link}}]**

If the audit missed the mark, or the timing isn't right, reply "stop" and you won't hear from us again. That's a legitimate answer, not a problem.

Warm regards,
**Sivakumar Swaminathan**
Chief AI Transformation Officer
SynexumLabs · A Coigne Capital company

P.S. — Our calendar is held open personally by the two founding partners above. If none of the slots work, reply and we'll make space.

---

## Body (variant_priority — critical finding)

Hi {{first_name}},

A week ago your audit flagged **{{top_pain_1_label}}** as a critical pattern — scored {{top_pain_1_score}}/100 for your firm. The case scenario on Monday walked through how we resolved exactly that pattern at a similarly-shaped family office.

**One week in, one question:** does the pattern we flagged match how it actually feels inside {{firm_name}}?

If it does, 30 minutes with our founding partners is the right next step. We'd walk through what addressing it would look like for your firm — specifically your firm, not a generic playbook. By the end of the call, you'd have a direct, transparent assessment of whether we're the right partner for this work.

**[Book 30 minutes · {{calendar_link}}]**

If the critical pattern we flagged doesn't match the reality on the ground, reply to this and tell us — the audit mis-read something, and we'd want to know what. A short note is enough.

Warm regards,
**Sivakumar Swaminathan**
Chief AI Transformation Officer
SynexumLabs · A Coigne Capital company

P.S. — Even if the booking isn't the right next step for you right now, I'd value knowing whether the finding felt accurate. Reply either way.

---

## Body (variant_light — soft findings, no CTA push)

Hi {{first_name}},

A week ago we sent your audit. Just a quick check-in — not a sales email.

Your audit came back clean. {{firm_name}} is running better than most of the family offices we see, and nothing in the findings called for immediate action.

I'll stop emailing here. The report is yours to keep, and we retain our copy for 24 months unless you ask us to delete it.

**If something changes next quarter — a new jurisdiction, a new entity structure, an AI incident, portfolio surprise — the easiest way to re-engage is to re-run the audit. Takes ten minutes and gives you a fresh snapshot.**

Thanks for your time last week.

Warm regards,
**Sivakumar Swaminathan**
Chief AI Transformation Officer
SynexumLabs · A Coigne Capital company

---

## Body (not_decision_maker)

Hi {{first_name}},

A quick follow-up on your audit from a week ago.

The report was written to be forwardable. If you've had a chance to share it with the decision-maker at {{firm_name}}, and they'd welcome a conversation with our founding partners, here's the booking link:

**[Book 30 minutes · {{calendar_link}}]**

Both {{partner_1_name}} and {{partner_2_name}} are on the call. 30–45 minutes. Honest assessment at the end — no pitch.

If the decision-maker would prefer a bespoke version of the report formatted for them specifically, reply with their name and we'll prepare one.

Warm regards,
**Sivakumar Swaminathan**
Chief AI Transformation Officer
SynexumLabs · A Coigne Capital company

---

## CTA button specification

```
label:  "Book 30 minutes with our founding partners"
colour: cyan (#35D1FF) background, navy (#031B4E) text
link:   {{calendar_link}}  — Calendly or equivalent
tracking: on (sole tracked link in this email)
```

In plain-text version of the email, the button becomes:

> → Book 30 minutes: {{calendar_link}}

---

## After-Email-03 behaviour

Once Email 03 is sent, one of the following paths unfolds within 14 days:

```
IF respondent books via the link:
    → Trigger Email 04 (booking confirmation — same copy as Rena's Touch 4 template)
    → Lead status: "booked_discovery_call"
    → Founding partners notified via internal channel with full audit context

IF respondent replies:
    → Route to founding-partner human reply
    → Pause sequence until human has responded
    → Lead status: "live_conversation"

IF respondent clicks the calendar link but doesn't book:
    → Send one gentle nudge at Day 10 ("Did the calendar page not load, or just not right now?")
    → Max 1 nudge, then stop

IF no engagement by Day 14:
    → Move lead to 90-day quarterly nurture
    → Status: "cold_nurture"

IF respondent replies "stop," "unsubscribe," or similar:
    → End sequence immediately
    → Add to suppression list for 12 months
    → Status: "suppressed"
```

---

## Variable reference

```
{{first_name}}            — from A08
{{firm_name}}             — from A08
{{partner_1_name}}        — "Sivakumar Swaminathan" (static for now)
{{partner_2_name}}        — "Sergio Paier" (static for now)
{{calendar_link}}         — from config
{{top_pain_1_label}}      — top-scored pain, friendly label
{{top_pain_1_score}}      — numeric score 0–100
```

---

## Technical notes

- Send window: Day 7 after submission, at 10:00 AM in the respondent's timezone (fallback: Eastern Time)
- Subject line A/B eligible: yes, 34/33/33 split
- Open-tracking on, click-tracking on (only the calendar link)
- Reply-to: live inbox monitored by founding partners (not a no-reply address)
- Suppression list: Email 03 does NOT send to anyone who has replied to Email 01 or Email 02 — those replies trigger human handling and pause the sequence
- Legal: unsubscribe footer present; "reply stop" honoured within 24h

---

## Design/content principle

Email 03 is the only email in the sequence that includes a direct ask. By waiting until the third touch — after a substantive audit report and a value-adding case study have arrived — the ask reads as proportionate to the value already delivered. If it still doesn't land, the respondent leaves the sequence with two useful artefacts and no bad taste.

That's the right trade-off. The audit's job is to open doors to the next 10 family offices via referral, not to force a close on this one.
