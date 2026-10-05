---
section: F
title: Final Details
subtitle: "Two short questions, then your report is on its way."
show_when: always
questions_count: 2
estimated_minutes: 0.5
---

# Section F — Final Capture

Final section. Confirms contact detail, optional phone, and consent. The email was already captured at A08 — this is where phone, delivery preferences, and consent live.

---

## F01 — Delivery details

```yaml
id: F01_delivery_details
type: contact_form
required: true
label: "Where should we deliver — and when?"
fields:
  - name: role_title
    label: "Your title"
    type: text
    required: true
    prefill_from: A01_role
    editable: true
  - name: phone
    label: "Direct phone (optional)"
    type: tel
    required: false
    help_text: "Only if you'd welcome a brief call from a founding partner — never auto-dialled."
  - name: preferred_contact
    label: "If we follow up, how do you prefer?"
    type: single_choice
    required: true
    options:
      - value: email
        label: "Email only"
      - value: email_then_phone
        label: "Email first, phone if I'd like a call"
      - value: no_followup
        label: "Deliver the report — no follow-up"
        qualification_flag: no_followup_requested
  - name: timezone
    label: "Your timezone"
    type: single_choice
    required: false
    options:
      - value: pt
        label: "Pacific"
      - value: mt
        label: "Mountain"
      - value: ct
        label: "Central"
      - value: et
        label: "Eastern"
      - value: gmt
        label: "GMT / UK"
      - value: cet
        label: "Central Europe"
      - value: me
        label: "Middle East"
      - value: asia
        label: "Asia / Pacific"
      - value: other
        label: "Other"
```

---

## F02 — Consent

```yaml
id: F02_consent
type: consent_checkbox
required: true
label: "Please confirm before we deliver your audit."
checkboxes:
  - id: consent_report
    required: true
    label: "I understand I'll receive one audit report by email within 5 minutes."
  - id: consent_privacy
    required: true
    label: "I've read how my data will be handled and I consent to it being stored for 24 months — or until I request deletion, whichever is sooner."
    privacy_link: "[Privacy policy URL]"
  - id: consent_followup
    required: false
    label: "I'd welcome one case study and a calendar link in the week following delivery. (Optional — unchecks itself if you selected 'no follow-up' above.)"
    default_checked_if:
      F01_delivery_details.preferred_contact: email_then_phone
```

---

## Final submission screen

**Shown immediately on submit, before email arrives:**

### H1 (navy)

> Thank you. Your audit is being prepared.

### Supporting paragraph

> One of our founding partners will review the findings in the next few minutes and release the report to your inbox at **[email]**. If it hasn't arrived in 10 minutes, check spam — or reply to this screen's confirmation email and we'll resend.

### What happens next (small, below)

- **Within 5 minutes:** Confidential audit report in your inbox
- **Day 2:** A one-page case study if your audit shows strong fit
- **Day 7:** An optional calendar link if you'd like a conversation with our founding partners

### Footer line

> Not every firm is the right fit for what we build. Your audit will tell you honestly.
