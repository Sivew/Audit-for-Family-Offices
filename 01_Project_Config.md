---
project: family_office_operational_audit
version: 1.0
brand: SynexumLabs
parent_company: Coigne Capital Inc.
positioning: "A private, 10-minute diagnostic of your family office's operational posture."
runtime_minutes: 10
total_questions_bank: 55
average_questions_shown: 28
languages: [en]
---

# Project Configuration

The settings in this file govern the overall behaviour of the audit. Change here first, then propagate to any builder.

---

## Brand

| Property | Value |
|---|---|
| Brand name | SynexumLabs |
| Parent | Coigne Capital Inc. |
| Audit name | The Family Office Operational Readiness Audit |
| Short name | Operational Readiness Audit |
| Primary colour (navy) | #031B4E |
| Accent colour (cyan) | #35D1FF |
| Secondary accent (deep cyan) | #00BDE0 |
| Light tint background | #ECF5FB |
| Grey text | #64748B |
| Body text | #1F2937 |
| Primary typeface | Inter, Helvetica, Arial (fallback stack) |

## Progress

- Show progress bar: **yes**
- Progress calibration: **"adaptive"** — the bar should reflect ~28 questions, not the full bank
- Show section labels at top of each question: **yes** (e.g. "Section A · Firm Profile · Question 3 of 8")
- Allow back navigation: **yes**
- Autosave answers to local storage: **yes**

## Email capture

- Capture email at question **A08** (before pain diagnostic)
- Partial completers (any respondent who answered A08) receive the Email 01 sequence based on partial data with a prompt to resume
- Full completers receive the full report

## Scoring thresholds

Each of the six pain areas scores 0–100.

| Score band | Classification | Report colour band |
|---|---|---|
| 0–30 | Low priority | Grey |
| 31–60 | Watch area | Amber |
| 61–80 | Significant | Cyan |
| 81–100 | Critical | Deep navy — flagged for principal attention |

Report shows top 3 pain areas by score — if top score < 40, the respondent is flagged internally as "low urgency / nurture only" and the report softens recommendations accordingly.

## Qualification gates

Respondents who score as follows are **not** offered a discovery-call CTA — they receive a nurture email instead:

- AUM range below $25M (likely too small)
- Timeline = "Just curious" AND no identified pain over 50
- Decision authority = "Other" AND they explicitly indicate they are not the decision-maker

All other respondents receive the full discovery-call CTA.

## Branding voice checklist

Before any copy ships, confirm it:

- Uses "principal," "family office executive," not "user"
- Calls the output an "audit report," not "results"
- Says "sovereign," "governed," "institutional-grade" where appropriate
- Avoids "AI-powered," "cutting-edge," "revolutionary"
- Ends with the discovery-call ask, not a product push

## Integration endpoints

Placeholders for the builder — fill in during implementation:

- `audit_submission_webhook`: `[your CRM endpoint]`
- `email_sequence_provider`: `[Klaviyo / Mailchimp / HubSpot / SendGrid]`
- `calendar_link_sergio_shiva`: `[Calendly or similar]`
- `report_pdf_generator`: `[Make.com / PDFShift / Puppeteer backend]`
- `analytics`: `[GA4, Plausible, Mixpanel]`

## Legal

- GDPR / PIPEDA notice at Section F (consent)
- Data retention: 24 months on completed audits unless respondent requests deletion
- Audit report explicitly marked "Confidential — Prepared for [Respondent Name]"
- Internal note: never redistribute audit reports; each is bespoke
