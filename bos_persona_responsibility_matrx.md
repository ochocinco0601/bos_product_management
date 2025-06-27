# 🧩 BOS Persona-to-Field Responsibility Matrix

This matrix shows who is responsible for completing or validating each section of the BOS Step Template. It reinforces governance by mapping **fields to personas**:
- 🧑‍💼 Product
- 🧑‍💻 Development
- 🧑‍🔧 Platform SRE
- 🤖 BOS (system-generated validation & scaffolding)

| **Template Section / Field**   | 🧑‍💼 Product | 🧑‍💻 Dev | 🧑‍🔧 SRE | 🤖 BOS |
|-------------------------------|--------------|----------|----------|--------|
| Flow Name                     | ✅            |          |          |        |
| Stage Name                    | ✅            |          |          |        |
| Step Name                     | ✅            |          |          |        |
| Description (Business)        | ✅            |          |          |        |
| Business Outcome(s)           | ✅            |          |          | 🔍 validate linkage |
| KPI Definitions               | ✅            |          |          | 🔍 check signal alignment |
| Risk Identification           | ✅            |          |          | 🔍 flag if missing |
| Step Owner(s)                 | ✅            |          |          |        |
| Business Signals                        | ✅            |          |          | 🔍 check completeness |
| Signal → KPI Mapping                    | ✅            |          |          | 🔍 trace signal path |
| Technical Flow Description              |              | ✅        |          | 🔍 check handoffs |
| Observable Unit Mapping                 |              | ✅        |          | 🔍 validate type, tags |
| Observable Unit Tags                    |              | ✅        |          | 🔍 enforce schema |
| Process Signals                         |              | ✅        |          | 🔍 match expected pattern |
| System Signals                          |              |          | ✅        | 🔍 check coverage |
| Platform Tags / Infra Context           |              |          | ✅        | 🔍 check standardization |

> 🔍 BOS is responsible for system-driven validation and automation support.  
> ✅ Each field has one and only one accountable persona.
