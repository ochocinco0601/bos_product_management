
# 🧑‍💻 BOS – Development Persona Contributor Guide

This guide defines the responsibilities, expectations, and field-level guidance for contributors acting in the **Development** persona within the BOS Step Template.

As a Development contributor, you are responsible for capturing how the business step is implemented technically. Your input connects business intent to code, telemetry, and execution logic.

---

## ✅ Fields You Own (Canonical Mapping)

| **Field Name**               | **Ontology Mapping**             | **Purpose**                                                  |
|------------------------------|----------------------------------|--------------------------------------------------------------|
| Observable Unit Mapping      | `Step → Observable Unit`         | Identify the system components that implement this step      |
| Observable Unit Tags         | `Observable Unit.tags`           | Classify each unit for pattern scaffolding and governance    |
| Process Signals              | `Signal.type = process`          | Confirm execution of internal logic or control paths         |
| Technical Flow Description   | `Observable Unit → Flow Description` | Describe the system-to-system flow powering the step     |

---

## 📘 Field-by-Field Guidance

### 🔹 Observable Unit Mapping

- **What to include**: List the system components responsible for performing the step.
- **How to identify them**: Think in terms of components that emit telemetry — APIs, batch jobs, embedded functions, etc.
- **BOS will check**:
  - That every Step maps to at least one Observable Unit
  - That the Unit is valid (i.e., includes tags, emits signals)

> *Examples:*
> - `ocr_parser_service`
> - `income_verification_function`

---

### 🔹 Observable Unit Tags

- **What to include**: Fill in at least these fields:
  - `type`: `service`, `function`, `job`, `module`, `process`, etc.
  - `deployment`: e.g., `VM`, `Kubernetes`, `mainframe`
  - `criticality`: `high`, `medium`, `low`
  - `owner_team`: e.g., `doc_ops`, `loan_platform`
- **Why it matters**: BOS uses tags to:
  - Scaffold signal expectations
  - Validate unit-level completeness
  - Enable reporting and filtering
- **BOS will check**:
  - That all required tags are present and correctly formatted

---

### 🔹 Process Signals

- **What to include**: List telemetry signals that confirm the system logic worked as expected — even before any business outcome is known.
- **Signal type**: `process`
- **Examples**:
  - `Income Parsed`
  - `Validation Rule Fired`
  - `Missing Income Flag`
- **BOS will check**:
  - That the signal names are plausible and non-empty
  - That at least one process signal is present for each Observable Unit (based on type)

---

### 🔹 Technical Flow Description

- **What to include**: A short, readable summary of the system flow — who calls who, how data moves.
- **Format**: Feel free to include plain text or structured syntax like:
  ```plaintext
  Web App → (POST: PDF) → OCR Service → (Kafka: JSON) → Rules Engine
  ```
- **BOS will check**:
  - That the field is not empty
  - That the syntax appears parsable or followable

---

## ✅ Reminders

- Use real component names from your environment
- Use tags to drive monitoring scaffolds — not just for reporting
- If a unit doesn't emit telemetry, question whether it belongs in the model
- BOS will not stop you from entering data — but it will flag inconsistencies for review

---

## 🔗 Related Resources

- 📄 [Canonical BOS Data Model](#)
- 📄 [Persona-to-Field Responsibility Matrix](#)
- 📄 [Observable Unit Tag Schema](#)
- 📄 [Signal Pattern Expectations by Unit Type](#)
