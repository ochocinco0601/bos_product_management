# 🧑‍💼 BOS Step Template – Product View

This view contains only the fields for which the **Product** persona is accountable. Each field includes its BOS ontology mapping for traceability.

---

## 🔹 Business Process Context

| **Field**        | **Ontology Mapping** | **Description / Guidance**              |
|------------------|----------------------|------------------------------------------|
| Flow Name        | `Flow.name`          | Name of the overall business flow       |
| Stage Name       | `Stage.name`         | Logical grouping within the flow        |
| Step Name        | `Step.name`          | Specific step within the stage          |
| Description      | `Step.description`   | Describe the intent and purpose of the step |

---

## 🔹 Business Alignment

| **Field**                | **Ontology Mapping**            | **Description / Guidance**                         |
|--------------------------|----------------------------------|----------------------------------------------------|
| Business Outcome(s)      | `Step → Business Outcome`        | What outcome(s) does this step help deliver?       |
| KPI Definitions          | `KPI`                            | What metrics indicate success at scale?            |
| Risk Identification      | `Step → Risk`                    | Any known business, operational, or regulatory risks |
| Step Owner(s)       | `Step → Owner`       | Name or title of the individual accountable for this step's business success (e.g., John Smith, Product Lead for Disbursements) |

---

## 🔹 Signal Alignment

| **Field**                | **Ontology Mapping**             | **Description / Guidance**                         |
|--------------------------|----------------------------------|----------------------------------------------------|
| Business Signals         | `Signal.type = business`         | Real-time signals that reflect user/business intent |
| Signal → KPI Mapping     | `Signal → KPI`                   | Which signals directly inform the KPIs above?      |

> BOS validates signal completeness and KPI traceability (🔍).
