# cloud-posture-dashboard

# Cloud Posture Dashboard — Product Management Assignment

## Overview
A multi-account **Cloud Posture Dashboard** designed to help security and platform engineers view, filter, prioritize, and resolve cloud misconfigurations across accounts in one place.

* **Figma Prototype Link:** https://www.figma.com/proto/cE4XrVycwgukhDsk25a4Zk/Cloud-Posture?node-id=0-1&t=uLLNf9J9lOFaBdqP-1
* **Figma Dev Mode Link:** https://www.figma.com/design/cE4XrVycwgukhDsk25a4Zk/Cloud-Posture?node-id=0-1&m=dev&t=uLLNf9J9lOFaBdqP-1

---

## 1. Problem Statement & User Persona

### Problem Statement
Misconfiguration data is often fragmented across multiple cloud accounts, regions, and environments, while high volumes of lower-risk findings obscure urgent exposures. Security engineers spend unnecessary time switching contexts, checking resource sensitivity/owners, and deciding what to fix first.

### User Persona: Rohan, Cloud Security & Platform Engineer
* **Goal:** Quickly identify high-severity misconfigurations across cloud accounts, understand risk impact, and route remediation to the right owner.
* **Pain Points:** Scattered account views, noisy low-priority findings, and unclear ownership or blast radius during triage.
* **Key Needs:** Unified filters, grouped findings, clear remediation steps, and status/ownership tracking.

---

## 2. Wireframes & Annotations

### Screen 1: Cloud Posture Overview & Filter Table
![Cloud Posture Overview](wireframes/screen-1-overview.png)

* **Filter Bar (`Account`, `Severity`, `Env`, `Resource`, `Owner`):** Allows filtering across accounts and environments from a single top bar with a quick reset option.
* **KPI Summary Cards (`Posture Score`, `Critical`, `High`, `Open Issues`):** Surfaces overall posture health (`74/100`) and immediate action counts upfront.
* **Prioritized Issues Table:** Groups recurring misconfigurations by affected resource count (e.g., `8x`, `3x`, `2x`) with owner, last-seen timestamp, bulk selection, and direct `Inspect` actions.

### Screen 2: Misconfiguration Detail & Remediation View
![Misconfiguration Detail View](wireframes/screen-2-detail.png)

* **Risk & Context Card:** Explains the misconfiguration (`Public Storage Bucket w/ Sensitive Tag`, `Policy: CSPM-STR-014`) and highlights data sensitivity (`sensitivity=high`) and potential impact in plain language.
* **Affected Resources Checklist:** Lists impacted resources (e.g., `customer-kyc-exports-prod`) so engineers can select specific or all affected assets.
* **How to Remediate & Ownership Card:** Provides clear step-by-step remediation instructions alongside owner details (`@data-platform`), status updates, and `Assign to Owner` / `Mark Resolved` actions.

### Screen 3: Account Posture & Trend View
![Account Posture and Trend View](wireframes/screen-3-trends.png)

* **Cross-Account Comparison Table:** Compares posture scores, critical/high issue counts, top risk areas, and 30-day score changes across accounts (`prod-data`, `prod-core`, `prod-app`).
* **Time Window Selector (`Last 30 Days`):** Lets users track whether security posture is improving or regressing over time.
* **Export & Risk Threshold Actions:** Supports summary CSV export and account-level risk threshold configuration.

---

## 3. Proposed Features, Prioritization & Success Metrics

### Proposed Features
1. **Multi-Account Filter & Summary View:** Unified posture score, key risk counts, and multi-attribute filters.
2. **Grouped Misconfigurations & Detail View:** Resource roll-ups, risk context, affected resource selection, and step-by-step remediation guidance.
3. **Ownership & Status Workflow:** Clear resource owners, status updates, and owner assignment actions.
4. **Account Comparison & Trend View:** Account-level posture comparison, 30-day trend indicators, CSV export, and threshold controls.

### Prioritization Rationale
* **P0 (MVP) — Filters + Summary Cards + Detail View:** Delivers immediate visibility across accounts and helps engineers understand and fix critical risks first.
* **P1 (Fast Follow) — Resource Grouping + Owner Assignment + Trend View:** Reduces list clutter at scale, speeds up ownership handoffs, and tracks posture progress over time.
* **P2 (Later) — CSV Export + Custom Risk Thresholds:** Adds reporting and policy tuning once core investigation and resolution flows are established.

### Success Metrics
* **Time to Locate Critical Issues:** Median time from finding detection to filtering and opening a critical misconfiguration.
* **Filter-to-Action Rate:** Percentage of filtered critical/high issues assigned to an owner or updated in status.
* **Critical Misconfiguration MTTR:** Median time taken to resolve critical misconfigurations.
* **Repeat Weekly Usage:** Weekly active usage among security and platform engineers.

---

## 4. Bonus: Development Action Items
* **Unified Posture Ingestion API:** Normalize findings across cloud accounts and scanners into a consistent schema (`account_id`, `environment`, `resource_id`, `policy_id`, `severity`, `owner`, `status`).
* **Indexed Filtering & Grouping Query Layer:** Optimize filtering, search, and resource grouping across large multi-account datasets.
* **Tag & Ownership Enrichment Sync:** Pull resource tags, environment labels, and service owner metadata from cloud inventories or catalogs.
* **Status & Audit Log Endpoint:** Record status transitions, owner assignments, timestamps, and user actions for auditability.
