---
section: C
title: Current Stack
subtitle: "Eight questions on the tools, data, and controls already in place. Shapes what we can and cannot build without displacing something."
show_when: always
questions_count: 8
estimated_minutes: 2
---

# Section C — Current Stack

Every respondent sees Section C. The answers inform the "Current State" page of the audit report and reveal integration surface area that matters when scoping Discovery.

---

## C01 — Primary portfolio / reporting platform

```yaml
id: C01_portfolio_platform
type: single_choice
required: true
label: "What is your primary portfolio reporting platform?"
options:
  - value: addepar
    label: "Addepar"
  - value: masttro
    label: "Masttro"
  - value: eton_solutions
    label: "Eton Solutions / AtlasFive"
  - value: archway
    label: "Archway Technology Partners"
  - value: ssandc
    label: "SS&C / Advent"
  - value: ms_excel
    label: "Microsoft Excel / Google Sheets (custom)"
    scores: { data_fragmentation: 15, reporting_lag: 10 }
  - value: in_house
    label: "An internal system we built"
  - value: none
    label: "No single platform — multiple tools"
    scores: { data_fragmentation: 20 }
  - value: other
    label: "Other / combination"
```

---

## C02 — CRM or client system

```yaml
id: C02_crm
type: single_choice
required: true
label: "What do you use for CRM, contacts, and interaction tracking?"
options:
  - value: salesforce
    label: "Salesforce"
  - value: hubspot
    label: "HubSpot"
  - value: dynamics
    label: "Microsoft Dynamics"
  - value: pipedrive
    label: "Pipedrive"
  - value: email_contacts
    label: "Outlook / Gmail contacts"
    scores: { data_fragmentation: 15 }
  - value: none
    label: "No formal CRM"
    scores: { data_fragmentation: 20, governance_risk: 10 }
  - value: other
    label: "Other"
```

---

## C03 — Document management

```yaml
id: C03_doc_management
type: single_choice
required: true
label: "Where do you store deal memos, contracts, and sensitive family documents?"
options:
  - value: sharepoint
    label: "SharePoint / OneDrive"
  - value: google_drive
    label: "Google Drive / Workspace"
  - value: box
    label: "Box"
  - value: dropbox
    label: "Dropbox"
  - value: ironclad
    label: "Dedicated DMS (iManage, NetDocuments, Ironclad)"
  - value: email_attachments
    label: "Mostly email attachments and local drives"
    scores: { shadow_ai: 15, governance_risk: 20 }
  - value: physical
    label: "Physical files + some digital"
    scores: { data_fragmentation: 15, governance_risk: 20 }
  - value: other
    label: "Other"
```

---

## C04 — AI tools currently used

```yaml
id: C04_ai_tools
type: multi_choice
required: false
label: "Which AI tools are in active use across the office? (select all that apply)"
help_text: "Honest answer — this shapes which risks we flag."
options:
  - value: chatgpt_free
    label: "ChatGPT (free or plus)"
    scores: { shadow_ai: 15, governance_risk: 15 }
  - value: chatgpt_team
    label: "ChatGPT Team / Enterprise"
    scores: { shadow_ai: 10 }
  - value: claude_free
    label: "Claude (free or pro)"
    scores: { shadow_ai: 15, governance_risk: 15 }
  - value: claude_team
    label: "Claude Team / Enterprise"
    scores: { shadow_ai: 5 }
  - value: copilot
    label: "Microsoft Copilot"
  - value: gemini
    label: "Google Gemini"
  - value: perplexity
    label: "Perplexity"
  - value: in_house
    label: "An internal / self-hosted model"
  - value: none_officially
    label: "None officially — but we suspect some use"
    scores: { shadow_ai: 25, governance_risk: 25 }
  - value: none_actually
    label: "None at all"
```

---

## C05 — Reporting cadence to the principal

```yaml
id: C05_reporting_cadence
type: single_choice
required: true
label: "How often does the principal receive consolidated reports?"
options:
  - value: daily
    label: "Daily"
  - value: weekly
    label: "Weekly"
  - value: monthly
    label: "Monthly"
    scores: { reporting_lag: 10 }
  - value: quarterly
    label: "Quarterly"
    scores: { reporting_lag: 20 }
  - value: ad_hoc
    label: "Ad hoc / when requested"
    scores: { reporting_lag: 25, principal_frustration: 15 }
```

---

## C06 — Data integration posture

```yaml
id: C06_integration
type: single_choice
required: true
label: "How are your data sources currently connected to your reporting?"
options:
  - value: fully_automated
    label: "Fully automated feeds, hourly or better"
  - value: nightly
    label: "Nightly automated feeds"
  - value: weekly
    label: "Weekly batch imports"
    scores: { data_fragmentation: 10 }
  - value: monthly
    label: "Monthly manual imports"
    scores: { data_fragmentation: 20, reporting_lag: 15 }
  - value: all_manual
    label: "Manual re-keying throughout the month"
    scores: { data_fragmentation: 30, team_bottleneck_risk: 20 }
```

---

## C07 — Data residency

```yaml
id: C07_residency
type: single_choice
required: true
label: "Where does sensitive family data physically reside?"
options:
  - value: on_prem
    label: "On-premises — hardware we control"
  - value: private_cloud
    label: "Private cloud (dedicated tenancy)"
  - value: public_cloud_our_tenant
    label: "Public cloud (AWS/Azure/GCP), our own tenant"
  - value: vendor_cloud
    label: "Our vendors' cloud (SaaS platforms)"
    scores: { governance_risk: 10 }
  - value: mixed
    label: "A mix — different data in different places"
    scores: { data_fragmentation: 10 }
  - value: dont_know
    label: "I'm not sure"
    scores: { governance_risk: 20 }
```

---

## C08 — Access controls on sensitive data

```yaml
id: C08_access_control
type: single_choice
required: true
label: "How is access to sensitive family data controlled?"
options:
  - value: role_based_mfa
    label: "Role-based access with MFA, audited"
  - value: role_based
    label: "Role-based access, no MFA"
    scores: { governance_risk: 10 }
  - value: shared_logins
    label: "Shared logins or passwords"
    scores: { governance_risk: 25 }
  - value: everyone_everything
    label: "Everyone has access to everything"
    scores: { governance_risk: 30 }
  - value: dont_know
    label: "I'm not entirely sure"
    scores: { governance_risk: 20 }
```
