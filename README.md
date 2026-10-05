# The Family Office Operational Readiness Audit

**A private 10-minute diagnostic for family office principals. Generates a tailored audit report mapped to SynexumLabs engagements.**

Project files are organised in sorted order — the full project map lives in [`00_README.md`](./00_README.md).

---

## Repository contents

```
.
├── 00_README.md                      — complete project overview
├── 01_Project_Config.md              — brand, scoring, integration config
├── 02_Landing_Page.md                — pre-audit landing page copy
│
├── Questions/                        — all question definitions (55 total)
│   ├── Section_A_Qualification.md    — 8 Q (always shown)
│   ├── Section_B_Pain_Diagnostic.md  — 1 primary + 6 adaptive branches
│   ├── Section_C_Current_Stack.md    — 8 Q
│   ├── Section_D_History.md          — 5 Q
│   ├── Section_E_Readiness.md        — 5 Q
│   └── Section_F_Capture.md          — 2 Q
│
├── Logic/                            — scoring and routing engine
│   ├── Branching_Rules.md
│   ├── Scoring_Model.md
│   └── Offer_Mapping.md
│
├── Report/                           — audit report structure
│   ├── Report_Template.md
│   ├── Finding_Blocks.md
│   └── Priority_Matrix.md
│
├── Email_Sequence/                   — 3-step follow-up
│   ├── Email_01_Report_Delivery.md
│   ├── Email_02_CaseStudy_Day2.md
│   └── Email_03_Followup_Day7.md
│
└── Visual_Prompts.md                 — image generator prompts
```

---

## Quick stats

- **55** question definitions
- **25–30** questions seen on average (via adaptive branching)
- **8–12** minute completion time
- **6** pain areas scored 0–100
- **4** report variants (standard / priority / light / nurture)
- **3-touch** email sequence after submission

---

## For developers / implementers

- All question files use YAML frontmatter — parseable directly in Astro, Hugo, Jekyll, Next.js (MDX), Framer CMS, Webflow CMS
- Scoring model is deterministic — see `Logic/Scoring_Model.md`
- Report template is variable-driven — see `Report/Report_Template.md` for the full variable reference

---

## Positioning rules

- Call it an "audit" or "diagnostic." Never "quiz" or "survey."
- Respondents are "principals" or "family office executives" — not "users."
- The output is a "Confidential Audit Report."
- Primary CTA: "Request your audit."
- Full positioning guidance in `00_README.md`.

---

**Prepared for SynexumLabs · A Coigne Capital company · Governed AI & Automation**
