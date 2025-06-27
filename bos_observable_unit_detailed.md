# Observable Unit – Detailed Design Reference

This document is part of the Business Observability System (BOS), which introduces structure and traceability between business outcomes and technical system components.

This document expands on the core concept of the **Observable Unit** in the Business Observability System (BOS), capturing the rationale, context, supporting logic, and implementation implications discussed during the design process.

---

## 1. Definition
An **Observable Unit** is any technical component that emits signals and contributes to a business-relevant step, regardless of how it is deployed, organized, or labeled. It is the foundational abstraction for aligning technical system behavior with business outcome measurement.

Observable Units include but are not limited to:
- Traditional services (APIs, microservices)
- Internal functions (e.g., tokenization modules, rule evaluators)
- Scheduled jobs or ETL processes
- Code modules within monoliths
- OS-level processes or integration daemons

If it can be measured, and it matters to the business, it qualifies as an Observable Unit.

---

## 2. Motivation for Introducing "Observable Unit"

### Why Not Just Use "Service"?
- The term **"service" is overloaded** and inconsistently applied in enterprise environments
  - It can mean an ITIL service, a REST API, a shared platform, or a deployment unit
- Many business-critical components are **not exposed as services**
  - Example: shared functions embedded in monoliths
  - Example: batch jobs without direct user interaction
- For large systems (e.g., Home Loan Origination), business steps often span **multiple codebases and ownership teams**, making a pure service boundary misleading

### What Observable Unit Solves
- **Clarity and inclusiveness**: All meaningful components are first-class citizens
- **Traceability**: Steps and flows can point to real supporting logic, regardless of implementation
- **Ownership and reliability**: Every unit can be tagged, measured, and governed
- **Pattern-aligned modeling**: Tags allow each Observable Unit to be classified by type (e.g., service, job, function), which enables us to apply consistent, repeatable observability patterns. For example, all `job`-type units can be expected to report `completion_status`, `duration`, and `success_rate`. This approach supports observability standardization across diverse architectures.

---

## 3. Example: Tokenization Module

| **Aspect**            | **Value**                                              |
|-----------------------|---------------------------------------------------------|
| Type (tag)            | `function`                                              |
| Emits Signals         | `tokenization_latency`, `failure_rate`                 |
| Used in Step          | `Collect Appraisal Fee`                                |
| Part of Flow          | `Mortgage Origination`                                 |
| Deployed As           | Java component running in VM within a monolithic app   |
| Owned By              | `app_security`                                          |
| Observability Level   | `golden_signals`                                        |

This example illustrates why a service-only model fails: there's no standalone deployment, but the component is **critical** to loan processing and **must** be observable.

---

## 4. Tag Schema (Condensed)
Tags enable consistent classification and filtering of Observable Units across views, dashboards, and governance processes.

Observable Units are classified using tags for filtering, reporting, and governance.

- `type`: `service`, `function`, `job`, `module`, `process`
- `domain`: business/technical domain (e.g., `home_lending`)
- `deployment`: where/how it runs (e.g., `VM`, `Kubernetes`, `mainframe`)
- `owner_team`: accountable team
- `criticality`: `high`, `medium`, `low`
- `language`: implementation language (optional)
- `observability_level`: `golden_signals`, `metrics_only`, `unknown`

---

## 5. Role in the Semantic Model
*SLI = Service Level Indicator (a measurable signal like latency or error rate); SLO = Service Level Objective (a reliability target, such as 99.9% success over 30 days).*

Observable Units serve as the **linking layer** between:
- **Steps** (business-defined actions)
- **Signals** (emitted data from systems)
- **SLIs and SLOs** (reliability contracts)

They enable **both forward and reverse traceability**, such as:
- From business flow → step → observable unit → signals
- From a component → what business steps it supports → what flows it impacts

---

## 6. Observability Patterns by Type
These patterns guide teams on which signals and SLIs are expected based on the observable unit type, supporting consistent onboarding and review practices.

This aligns with the principle that there are a **finite number of base monitoring patterns**, which can be systematized by Observable Unit type:

| **Type**    | **Pattern Description**                                   | **Typical SLIs / Signals**                                |
|-------------|------------------------------------------------------------|------------------------------------------------------------|
| `service`   | Request/response APIs or user-facing services              | `latency`, `availability`, `error_rate`, `traffic`         |
| `job`       | Batch or scheduled tasks                                   | `success_rate`, `run_time`, `record_count`, `delay`        |
| `function`  | Shared internal logic called by other units                | `execution_time`, `error_rate`, `invocation_rate`          |
| `module`    | Subsystem in monoliths or multi-repo distributed monoliths | Composite of signals from internal sub-functions           |
| `process`   | Long-running background workers or OS-level integrations   | `uptime`, `heartbeat`, `message_rate`, `queue_depth`       |

---

## 7. Summary
The Observable Unit is a foundational shift in observability modeling. It reflects the true shape of enterprise systems and allows us to:
- Standardize monitoring across heterogeneous architectures
- Enable composable and reusable observability metadata
- Align technical components with business outcomes
- Lead the industry forward with a model that honors both reliability and complexity

