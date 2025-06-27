# 📘 BOS Step Template – Onboarding Guide

This guide introduces the structure, purpose, and usage expectations for the BOS Step Template. It is intended for all contributors—Product, Development, Platform SRE, and system automation—to understand their roles in documenting and aligning business-critical steps.

---

## 🧭 What Is This Template?

The BOS Step Template is part of the **Business Observability System (BOS)**. It defines and captures how a single business step is:

- Mapped to its technical implementation
- Connected to real-time signals
- Measured using KPIs
- Aligned with business outcomes and accountability

Each completed template becomes a **system of record** for that step.

---

## 👥 Personas and Responsibilities

There are **four personas** in the BOS model:

| Persona         | Description |
|-----------------|-------------|
| 🧑‍💼 **Product**       | Owns business flow, step intent, KPIs, and outcome alignment |
| 🧑‍💻 **Development**   | Owns technical implementation, process logic, and unit-level signals |
| 🧑‍🔧 **Platform SRE**  | Owns system health, infra tags, and system signals |
| 🤖 **BOS**             | Validates structure, prompts for missing elements, scaffolds pattern expectations |

Each field in the template is owned by exactly **one persona**, defined in the [Persona-to-Field Responsibility Matrix](#).

---

## 🧱 Template Structure

The full template is built from a **canonical data model** and divided into four persona-specific views:

| Template View   | Includes Fields For...                           |
|-----------------|--------------------------------------------------|
| Product         | Business flow, step name, KPIs, outcomes, risks  |
| Development     | Observable Units, process signals, flow logic    |
| Platform SRE    | System signals, platform tags, alert readiness   |
| BOS             | Validation scaffolds and structural enforcement  |

Each view is tailored to the fields that **you** are responsible for completing. The system will assemble the full BOS Step once all persona views are populated.

---

## 📌 Contributor Expectations

- **Be precise**: Use plain language and real signal names or KPIs where possible
- **Stay within scope**: Only fill the fields assigned to your persona
- **Name real people**: Where applicable (e.g., Step Owner), include an actual person or accountable role
- **Use tags correctly**: BOS uses tags to assign patterns and validate completeness
- **Ask BOS for help**: If you're unsure, BOS will highlight structural gaps

---

## ✅ Getting Started

1. Review your **persona view template**
2. Gather any existing documentation or system diagrams
3. Fill in your assigned fields
4. Submit or upload your completed view

When all views are complete, BOS will:
- Validate signal coverage
- Generate missing scaffolds
- Link the step to its flow, stage, and surrounding KPIs

---

## 📎 References

- 📄 [Canonical Data Model](#)
- 📄 [Persona-to-Field Responsibility Matrix](#)
- 📄 [Product View Template](#)
- 📄 [Development View Template](#)
- 📄 [Platform SRE Template](#)

