
# 🧑‍🔧 BOS – Platform SRE Persona Contributor Guide

This guide defines the responsibilities, expectations, and field-level guidance for contributors acting in the **Platform SRE** persona within the BOS Step Template.

As a Platform SRE contributor, you are responsible for declaring the system-level telemetry and infrastructure context that proves this step can run reliably. Your work ensures that foundational systems—containers, queues, APIs, databases—are healthy and observable.

---

## ✅ Fields You Own (Canonical Mapping)

| **Field Name**               | **Ontology Mapping**             | **Purpose**                                                      |
|------------------------------|----------------------------------|------------------------------------------------------------------|
| System Signals               | `Signal.type = system`           | Prove that systems are up, stable, and performant                |
| Platform Deployment Tags     | `Observable Unit → Platform`     | Identify where the component runs and how it's deployed          |

---

## 📘 Field-by-Field Guidance

### 🔹 System Signals

- **What to include**: Signals that reflect health of system infrastructure supporting the business step.
- **Examples**:
  - `OCR Container Liveness`
  - `Kafka Consumer Lag`
  - `Rules API 5xx Rate`
  - `Income Verification Latency`
- **Signal type**: `system`
- **BOS will check**:
  - That at least one signal is present for each Observable Unit
  - That signals use meaningful names (aligned with platform terminology)
  - That they cover critical components: APIs, queues, storage, compute

---

### 🔹 Platform Deployment Tags

- **What to include**: Tags that describe how the Observable Unit is deployed and where it runs.
- **Required Tags**:
  - `deployment`: `VM`, `Kubernetes`, `mainframe`, etc.
  - `data_center`: e.g., `us-central`, `east-prod`
- **Optional Tags**:
  - `region`, `cluster`, `infra_tier` if your org supports them
- **BOS will check**:
  - That required tags are not empty
  - That values conform to known standards or vocabulary
  - That each Observable Unit has a deployment context

---

## ✅ Reminders

- You don’t need to know the business logic — focus on proving the platform works
- If a service is “invisible” from a telemetry standpoint, the step is untrustworthy
- Your signals are critical for real-time alerting and long-term platform analytics
- BOS will validate that coverage exists, but it’s up to you to ensure quality

---

## 🔗 Related Resources

- 📄 [Canonical BOS Data Model](#)
- 📄 [Persona-to-Field Responsibility Matrix](#)
- 📄 [System Signal Examples](#)
- 📄 [Deployment Tag Standards](#)
