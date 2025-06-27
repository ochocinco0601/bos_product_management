# 📘 Canonical BOS Step Template – Data Model

| **Field Name**                   | **Ontology Mapping**                                | **Responsible Persona** |
|----------------------------------|------------------------------------------------------|--------------------------|
| Flow Name                        | `Flow.name`                                          | Product                 |
| Stage Name                       | `Stage.name`                                         | Product                 |
| Step Name                        | `Step.name`                                          | Product                 |
| Description (Business)           | `Step.description`                                   | Product                 |
| Business Outcome(s)              | `Step → Business Outcome`                            | Product                 |
| KPI Definitions                  | `KPI` (informed by signals, tied to outcome)         | Product                 |
| Risk Identification              | `Step → Risk`                                        | Product                 |
| Step Owner(s) | `Step → Owner` (individual-level) | Product |
| Business Signals                 | `Signal.type = business`                             | Product                 |
| Signal → KPI Mapping             | `Signal → KPI`                                       | Product                 |
| Technical Flow Description       | `Observable Unit → Flow Description` (narrative)     | Development             |
| Observable Unit Mapping          | `Step → Observable Unit`                             | Development             |
| Observable Unit Tags             | `Observable Unit.tags` (type, domain, criticality)   | Development             |
| Process Signals                  | `Signal.type = process`                              | Development             |
| System Signals                   | `Signal.type = system`                               | Platform SRE            |
| Platform Deployment Tags         | `Observable Unit → Platform`                         | Platform SRE            |

