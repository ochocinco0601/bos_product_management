# Observable Unit – Summary

This document is part of the **Business Observability System (BOS)**, which introduces structure and traceability between business outcomes and technical system components.

This document summarizes the core concept of the **Observable Unit** in the BOS.

---

## What Is an Observable Unit?

An **Observable Unit** is a foundational concept in our business observability model, designed to reflect the real structure of our systems and enable meaningful alignment between technical components and business outcomes.

It is any technical component that emits signals and contributes to a business-relevant step — even if it's not labeled as a “service.”  
It can be a **REST API**, **batch job**, **microservice**, **data pipeline**, **function**, or **process**.  
If it supports business logic and emits telemetry, it qualifies.

---

## Why We Need a More Flexible Model than “Service”

Traditional terminology like **“service”** breaks down in large-scale systems. Not all critical components are exposed as cleanly deployed services — and many, such as embedded functions or batch jobs, still impact business reliability.

Using **Observable Unit** gives us a flexible, consistent way to model, track, and improve application health — regardless of how code is deployed, owned, or labeled.

It gives precision in:

- Mapping business steps to telemetry  
- Owning signals at the right level  
- Supporting ITIL-aligned operational goals

> If it supports business logic and emits telemetry, it should be observable — even if it’s not called a “service.”

---

## Observable Units vs Traditional Services

This table contrasts traditional service-based observability with the Observable Unit model used in our business observability system:

| **Aspect**         | **Traditional 'Service'**        | **Observable Unit**                                 |
|--------------------|----------------------------------|-----------------------------------------------------|
| **Definition**      | Deployed service or app          | Any component emitting meaningful signals           |
| **Visibility**      | Coarse-grained                   | Fine-grained, step-aligned                          |
| **Ownership**       | Team-based, loosely scoped       | Signal-owner aligned                                |
| **Reusability**     | Not explicitly modeled           | Reused across steps and flows                       |
| **Business Alignment** | Often vague                   | Directly mapped to business activity                |

---

## ITIL and the Role of Observable Units

| **ITIL Function**       | **How Observable Units Support It**                                                   |
|-------------------------|----------------------------------------------------------------------------------------|
| **Event Management**    | Units emit telemetry signals that become events, supporting early detection.           |
| **Incident Management** | Units are mapped to business steps, aiding in pinpointing fault domains.              |
| **Problem Management**  | Fine-grained signal granularity improves RCA and trend detection.                     |
| **Change Enablement**   | Observable Units can be targeted in CAB discussions and post-change analysis.         |
| **Service Configuration** | Units serve as attach points for CI-level signal and dependency mapping.          |

---

## Summary

**Observable Units are the atomic layer of system health.**  
They give us a consistent way to bridge business logic and technical monitoring across ITIL processes.

This abstraction gives us a **scalable foundation** to align operational health with business-critical outcomes, across all architectures.
