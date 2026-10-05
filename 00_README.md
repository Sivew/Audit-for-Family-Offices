# The Family Office Operational Readiness Audit

**A private 10-minute diagnostic that generates a tailored audit report mapping the respondent's operational posture to SynexumLabs' highest-leverage engagements.**

---

## What this project is

A lead-generation and qualification tool positioned as a **private audit** — not a quiz. The respondent answers 25–30 questions (drawn adaptively from a bank of 55+) and receives a personalised report naming:

1. Their top 3 operational pain areas, scored 0–100
2. Specific findings about their current stack and posture
3. A prioritised matrix of what to fix first (impact × effort)
4. A recommended engagement path with SynexumLabs
5. A booking CTA for a free Discovery session

Everything is designed so the respondent closes the audit thinking *"these people understand my firm better than most of my advisors."*

---

## File map

```
FamilyOffice_Audit_Quiz/
├── 00_README.md                       — this file
├── 01_Project_Config.md               — scoring weights, routing, branding
├── 02_Landing_Page.md                 — pre-audit landing page copy
│
├── Questions/                         — all question definitions
│   ├── Section_A_Qualification.md     — profile the firm (8 Q)
│   ├── Section_B_Pain_Diagnostic.md   — primary pain + adaptive branches (1 + 6)
│   ├── Section_C_Current_Stack.md     — tooling, data, access (8 Q)
│   ├── Section_D_History.md           — prior solution attempts (5 Q)
│   ├── Section_E_Readiness.md         — buy-in, timeline, budget (5 Q)
│   └── Section_F_Capture.md           — contact & consent (2 Q)
│
├── Logic/                             — how the quiz behaves
│   ├── Branching_Rules.md             — if X answer, show Y next
│   ├── Scoring_Model.md               — how pain areas get scored
│   └── Offer_Mapping.md               — pain scores → SynexumLabs offers
│
├── Report/                            — the audit output
│   ├── Report_Template.md             — the layout of the report
│   ├── Finding_Blocks.md              — reusable finding paragraphs
│   └── Priority_Matrix.md             — impact × effort 2×2 definition
│
├── Email_Sequence/
│   ├── Email_01_Report_Delivery.md    — immediate send with the report
│   ├── Email_02_CaseStudy_Day2.md     — case study drop
│   └── Email_03_Followup_Day7.md      — booking push
│
└── Visual_Prompts.md                  — AI image prompts for the quiz UI
```

---

## Question volume

- **~55 question definitions** total across all sections
- **Average respondent sees 25–30 questions** (via branching logic)
- **Completion time:** 8–12 minutes
- **Drop-off checkpoint:** email captured by Question A08 so partial completions still generate leads

---

## How to import into a website builder

The question files use **YAML frontmatter + markdown body**. This format works directly in:

- **Astro, Hugo, Jekyll, Next.js (MDX)** — native parsing
- **Framer, Webflow, Softr** — manual transfer of each question into the builder's form editor using the frontmatter as the source of truth
- **Typeform / Jotform / Tally** — manual import, use the "options" blocks to populate choice fields
- **Custom build** — the YAML schemas are consistent across every question so parsing is straightforward

If your builder expects JSON, every question file converts cleanly — the YAML schema → JSON map is 1:1.

---

## Positioning rules (apply everywhere)

- **Call it an "audit" or "diagnostic." Never "quiz" or "survey."** The tone is institutional.
- **Respondents are "principals" and "family office executives" — not "users."**
- **The report is a "Confidential Audit Report" — not "Your Results."**
- **CTA language: "Request your audit."** Never "Take the quiz."
- **Sovereign/governance language throughout** — mirror the deck and setter script.
- **The three lines from the setter script apply here too**: *"We are selective."* / *"Our founding partners run every discovery call personally."* / *"Not every firm is the right fit."*

---

## Scoring at a glance

Six pain areas scored independently (0–100):

| Pain area | Primary offer that fixes it |
|---|---|
| `data_fragmentation` | Live Data Intelligence Dashboard |
| `reporting_lag` | Live Data Intelligence Dashboard |
| `structural_complexity` | Structure Engine |
| `shadow_ai` | Private Contained AI Workspace |
| `portfolio_blindspots` | Early-Warning System (Portfolio Oversight) |
| `deal_flow_drag` | Deal Flow Triage & Memo Drafting |

Each respondent gets a ranked list, with the top 2–3 driving the report's recommendations.

See `Logic/Scoring_Model.md` for the math.

---

## What to deliver and when

| Touchpoint | When | Deliverable |
|---|---|---|
| **Audit submission** | T+0 | On-screen summary + confirmation that report is on the way |
| **Report email** | T+5 min | `Email_01_Report_Delivery.md` + attached PDF audit report |
| **Case study drop** | T+2 days | `Email_02_CaseStudy_Day2.md` + Family Office case study PDF |
| **Follow-up** | T+7 days | `Email_03_Followup_Day7.md` + calendar link |

Setter script integration: respondents who provide a phone number enter Rena's cadence at Touch 2 (not Touch 1 — the audit email replaces the initial deck send).

---

**Prepared by the AI offer team · For SynexumLabs internal use · Version 1.0**
