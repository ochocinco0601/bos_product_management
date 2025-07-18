# Strategic Capability Map

## Cross-Cutting North Star

**Primary Evaluation Lens:** Can we determine the business impact when there is a production incident?

All tier-based capabilities and ownership expectations should be evaluated against this cornerstone question.

---

## Tier: Strategic

### 1. Business Observability Requirements Authoring System

* **Description:** A structured interface and backend system of record for capturing flows, steps, signals, and associated business impacts.
* **Primary Owners:** Product Teams, Development Teams
* **Responsible Contributors:** Central SRE Team

---

### 2. Service Registry Platform

* **Description:** Enterprise-wide system to standardize, register, and expose metadata for all business and technical services.
* **Primary Owners:** Enterprise Observability Team
* **Fallback Ownership:** Central SRE Team (if enterprise declines)

---

### 3. Business Playbook Composer

* **Description:** Generator that transforms structured observability metadata into consumable business playbooks (e.g., UI card, Markdown, PDF).
* **Primary Owners:** Central SRE Team
* **Supporting Teams:** Product Teams

---

### 4. Alert Specification Translator

* **Description:** Logic engine that converts step-level observability definitions into actionable alert formats (e.g., Splunk, Prometheus rules).
* **Primary Owners:** Central SRE Team
* **Supporting Teams:** Development Teams

---

### 5. Dashboard Blueprint Generator

* **Description:** Component that defines default dashboard structures and widget specifications based on observability requirements.
* **Primary Owners:** Central SRE Team
* **Supporting Teams:** Development Teams

---

### 6. Alert & Dashboard Deployment Engine

* **Description:** Orchestrates implementation of alerts and dashboards in enterprise observability platforms (e.g., Splunk, AppDynamics).
* **Primary Owners:** Development Teams
* **Supporting Teams:** Central SRE Team

---

### 7. Agile Integration Toolkit for Observability

* **Description:** Embedded tooling and practices that integrate observability artifacts into Agile Release Train planning, sprint workflows, and backlogs.
* **Primary Owners:** Product Teams
* **Supporting Teams:** Development Teams

---

### 8. Observability as Code & CICD Integration

* **Description:** Version-controlled observability configuration integrated into automated delivery pipelines.
* **Primary Owners:** Central SRE Team, Development Teams
* **Supporting Teams:** Enterprise Integrated Development Platform Team
* **Note:** Platform SRE teams are **not** expected to contribute here due to current maturity limitations.
