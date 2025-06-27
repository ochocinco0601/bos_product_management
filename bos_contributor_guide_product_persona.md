
# 🧑‍💼 BOS – Product Persona Contributor Guide

This guide defines the responsibilities, expectations, and field-level guidance for contributors acting in the **Product** persona within the BOS Step Template.

As a Product contributor, you are responsible for defining the business purpose, outcomes, KPIs, and risks for this step. Your input ensures that the step is anchored in business value and can be measured consistently at scale.

---

## ✅ Fields You Own (Canonical Mapping)

| **Field Name**         | **Ontology Mapping**              | **Purpose**                                                      |
|------------------------|-----------------------------------|------------------------------------------------------------------|
| Flow Name              | `Flow.name`                       | Name of the overall business process                             |
| Stage Name             | `Stage.name`                      | Logical grouping within the flow                                 |
| Step Name              | `Step.name`                       | Name of the discrete business step                               |
| Description (Business) | `Step.description`                | Narrative description of what the step does and why it matters   |
| Business Outcome(s)    | `Step → Business Outcome`         | Outcomes this step contributes to (e.g., revenue, compliance)    |
| KPI Definitions        | `KPI`                             | Business metrics that measure success at scale                   |
| Risk Identification    | `Step → Risk`                     | Known business or operational risks related to this step         |
| Step Owner(s)          | `Step → Owner` (individual-level) | Name or role of the person accountable for this step             |
| Business Signals       | `Signal.type = business`          | Signals that reflect user intent or business confirmation        |
| Signal → KPI Mapping   | `Signal → KPI`                    | How signals support or inform KPIs                               |

---

## 📘 Field-by-Field Guidance

### 🔹 Flow / Stage / Step Name

- **What to include**: Use consistent, human-readable names that reflect real business terminology.
- **Hierarchy**: A `Flow` contains one or more `Stages`, which contain `Steps`.
- **BOS will check**:
  - That all fields are filled
  - That naming patterns are consistent

---

### 🔹 Description (Business)

- **What to include**: Describe the purpose of the step — what happens, why it matters, and what success looks like.
- **BOS will check**:
  - That the description is non-empty
  - That it includes business intent, not just system details

---

### 🔹 Business Outcome(s)

- **What to include**: Choose or define outcome tags (e.g., customer satisfaction, cycle time reduction, compliance).
- **Format**: Short phrases or tags; e.g., `Faster processing`, `Regulatory compliance`
- **BOS will check**:
  - That at least one outcome is listed
  - That it matches BOS taxonomy, if applicable

---

### 🔹 KPI Definitions

- **What to include**: Business-level performance indicators, not technical stats.
- **Examples**:
  - `Approval Rate`
  - `Funding Cycle Time`
- **BOS will check**:
  - That each KPI includes a formula, description, or threshold
  - That it’s linked to signals below

---

### 🔹 Risk Identification

- **What to include**: Any business, financial, or operational risks associated with this step.
- **Examples**:
  - “Incorrect income validation could lead to underwriting errors”
  - “Delays in document parsing may cause SLA violations”
- **BOS will check**:
  - That risk entries are non-empty for compliance-critical steps

---

### 🔹 Step Owner(s)

- **What to include**: The real name or business role of the accountable owner.
- **Examples**:
  - `Sarah Chen (Loan Ops Product Lead)`
  - `Disbursement Process Owner`
- **BOS will check**:
  - That the field is not empty
  - That it appears to identify a real person or named role

---

### 🔹 Business Signals

- **What to include**: Signals that represent the outcome of a decision or user experience.
- **Examples**:
  - `Income Verified`
  - `Appraisal Completed`
- **BOS will check**:
  - That signals are present
  - That they are distinguishable from process/system signals

---

### 🔹 Signal → KPI Mapping

- **What to include**: For each KPI, indicate which signal(s) inform or support it.
- **Format**:
  - `Approval Rate ← signal: Loan Decision Outcome`
  - `Funding Time ← signal: Disbursement Timestamp`
- **BOS will check**:
  - That all KPIs are mapped to at least one signal

---

## ✅ Reminders

- Use business-first language throughout
- Keep signal names and KPI labels human-readable
- If a step doesn’t support a known business outcome, question its purpose
- BOS will validate linkage but cannot assign meaning — that’s your job

---

## 🔗 Related Resources

- 📄 [Canonical BOS Data Model](#)
- 📄 [Persona-to-Field Responsibility Matrix](#)
- 📄 [KPI Definition Guidelines](#)
- 📄 [Business Outcome Categories](#)
