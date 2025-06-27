# Observable Unit Tag Schema

This document defines the recommended tagging schema for Observable Units in the Business Observability System. Tags help classify and group Observable Units for reporting, monitoring, and ownership.

---

## Tag Categories and Examples

|                       | **Tag Name**                                          | **Purpose**                                                   | **Examples** |
| --------------------- | ----------------------------------------------------- | ------------------------------------------------------------- | ------------ |
| `type`                | Classifies the unit by role or technical behavior     | `service`, `function`, `job`, `module`, `process`, `engine`   |              |
| `domain`              | Aligns the unit to a business or technical domain     | `home_lending`, `capital_markets`, `servicing`                |              |
| `deployment`          | Indicates where/how it runs                           | `VM`, `Kubernetes`, `mainframe`, `on_prem`, `cloud`           |              |
| `owner_team`          | Assigns team accountability                           | `app_security`, `loan_ops_platform`, `payments_team`          |              |
| `criticality`         | Flags relative risk or importance                     | `high`, `medium`, `low`                                       |              |
| `language`            | Used for tooling, pipeline routing, or repo structure | `Java`, `Python`, `COBOL`, `Node.js`                          |              |
| `observability_level` | Declares maturity of observability coverage           | `golden_signals`, `metrics_only`, `traces_enabled`, `unknown` |              |

---

## Example Usage

```yaml
observable_unit:
  id: tokenization_module
  name: Tokenization Module
  description: Performs credit card tokenization and PCI compliance checks
  tags:
    type: function
    domain: home_lending
    deployment: VM
    owner_team: app_security
    criticality: high
    language: Java
    observability_level: golden_signals
```

