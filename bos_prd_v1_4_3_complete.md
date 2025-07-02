# Business Observability System Prototype — Product Requirements Document (PRD) v1.4.3

**Date:** 2025-07-01\
**Prototype Version:** v1.4.3\
**LLM-Optimized for Direct Implementation with Complete Dependencies**

---

## 1. Purpose

Deliver a minimal viable product (MVP) for the BOS application that implements stakeholder-first business observability methodology through core CRUD, visualization, and CSV import/export capabilities. This PRD is optimized for LLM-as-developer implementation with explicit technical specifications and methodology-to-code mappings.

## 1.1 Design Principles (Stakeholder-First Methodology Integration)

### Core Problem Statement
**Current approach of discovering business impact during incidents creates communication delays and response prioritization failures.**

Incident responders currently scramble to identify stakeholder impact because no systematic process exists for documenting business dependencies and outcomes.

### Principle
*Identify **WHO** depends first, before defining **WHAT** breaks* — business observability must be stakeholder-first.

### Discovery Sequence (Implementation Required)
1. **WHO depends** → StakeholderCategoriesForm component
2. **WHAT they need/expect** → DependencyMappingForm component  
3. **WHAT breaks on failure** → ImpactAnalysisForm component
4. **WHAT telemetry detects impact** → TelemetryMappingForm component
5. **WHAT signals to instrument** → SignalDefinitionForm component

### Observability Design Chain (Validation Framework)
```
StakeholderCategories → Dependencies → ImpactCategories → TelemetrySignals → ObservableUnits
```

**LLM Implementation Note:** Every UI workflow must enforce this chain through validation logic and form progression.

### Stakeholder Relationship Framework
**Description:** Steps have three types of stakeholder dependencies based on relationship
- **Serves:** People/customers who get value FROM this step
- **Maintains:** Business entities/objects kept current BY this step
- **Integrates With:** Vendors/systems required FOR this step to function
- **Validation Note:** A step may have 1, 2, or all 3 relationship types

### Stakeholder Dependency Principle
**Logic:** Steps have varying dependency patterns - not all steps require all stakeholder types
**Validation:** Minimum 1 stakeholder total, categories are optional based on step nature
**Business Examples:**
- Data validation step may only integrate with vendors
- Customer notification may only serve people
- Complex process may have all three types

### Discovery Sequence Flexibility
**Principle:** Support logical progression while allowing flexible data entry
**Rationale:** Real users have partial information, work collaboratively, think non-linearly
**Implementation:**
- Provide clear methodology guidance for recommended sequence
- Never block access to any discovery step
- Track completion per step without enforcing dependencies
- Support iterative refinement and collaborative population

### Measurable Impact Principle
**Principle:** All business impacts must be measurable via system telemetry or business metrics
**Rationale:** BOS enables real-time business observability - unmeasurable impacts cannot be instrumented
**Requirements:**
- Impact descriptions must include specific measurable signals or metrics
- Qualitative impacts (frustration, reputation, confidence) are excluded
- Focus on quantifiable business consequences detectable by systems
**Examples:**
- **Measurable:** Transaction failure count, processing time delays, cost increases, abandonment rates, API error rates
- **Not Measurable:** Customer frustration, reputation damage, confidence loss, team morale
**Validation:** Step 3 forms must enforce measurability validation

### Impact Categories Specification
**Financial:**
- **Definition:** Money movement, transactions, revenue impact that systems can track
- **Measurable Examples:** Transaction failures, revenue loss, processing cost increases, abandonment rates

**Legal/Compliance:**
- **Definition:** Regulatory violations, compliance check failures, risk thresholds that systems can detect
- **Measurable Examples:** Disclosure deadline violations, regulatory reporting gaps, compliance check failures, audit findings

**Operational:**
- **Definition:** Process performance, throughput, efficiency metrics that systems can measure
- **Measurable Examples:** Processing delays, manual intervention increases, SLA violations, productivity loss

**Customer Experience:**
- **Definition:** Impact on immediate consumers/callers of this stakeholder (not ultimate human customers)
- **Perspective Approach:** immediate_consumer_model
- **Measurable Examples:** Response time degradation, error rates, session abandonment, support call increases
- **Application by Stakeholder:**
  - **People:** Direct user experience of this person
  - **Business Entities:** Impact on systems/processes that consume this entity's data or services
  - **Vendors:** Impact on the direct client/consumer of this vendor's services
- **Rationale:** In complex enterprise system chains, focus on immediate consumers keeps impacts measurable and traceable

### Telemetry Mapping Principle
**Principle:** Every measurable impact must be traceable to observable telemetry
**Rationale:** Step 4 creates the bridge between business impacts and technical instrumentation
**Requirements:**
- Each impact from Step 3 must have corresponding telemetry requirements
- Telemetry must be automatically collectible by systems
- Focus on real-time or near-real-time observable data
**Traceability Chain:** Stakeholder → Impact → Telemetry → Signals (Steps 1-4 complete chain)

### Signal Types Specification
**Business Signals:**
- **Definition:** User intent, behavior, and business outcome measurements
- **Examples:** Login frequency, application abandonment, transaction completion rates

**Process Signals:**
- **Definition:** Workflow execution, business logic, and process performance measurements
- **Examples:** Queue durations, approval rates, process step completion times

**System Signals:**
- **Definition:** Infrastructure health, service performance, and technical system measurements
- **Examples:** API response times, error rates, service availability, resource utilization

### Complete Methodology Chain
**Principle:** Every stakeholder must be traceable through all 5 discovery steps
**Chain:** WHO depends → WHAT expect → WHAT breaks → WHAT telemetry → WHAT signals
**Validation:** Step 5 completion enables full business observability implementation
**Outcome:** Technical teams have specific instrumentation requirements linked to business stakeholder impacts

---

## 2. Goals & Objectives

- Enable cross-functional teams to collaboratively define, visualize, and refine business observability signals using stakeholder-first methodology
- Provide guided discovery workflows that implement the 5-step discovery sequence
- Allow import/export of signal templates via CSV with full methodology compliance
- Validate stakeholder → impact → signal traceability in real-time

---

## 3. Stakeholders & Persona Mapping

| Persona | Primary Responsibility | Discovery Sequence Focus | Implementation Components |
|---------|----------------------|--------------------------|---------------------------|
| **Product Owner** | Business flow, stakeholder identification | Steps 1-3 (WHO, WHAT expect, WHAT breaks) | StakeholderCategoriesForm, DependencyMappingForm, ImpactAnalysisForm |
| **Developer** | Technical implementation, observable units | Steps 4-5 (Telemetry, Signals) | TelemetryMappingForm, SignalDefinitionForm |
| **Platform SRE** | System health, infrastructure context | Step 5 (System signals) | SystemSignalForm, InfrastructureContextForm |
| **BOS System** | Validation, pattern enforcement | All steps (Automated validation) | TraceValidationEngine, CompletenessScoring |

---

## 4. Enhanced Data Schema (Methodology-Integrated)

### Core Entities

```yaml
Flow:
  id: string
  name: string
  description: string
  version: string
  methodology_version: string  # tracks methodology compliance
  stakeholder_mapping_complete: boolean
  validation_score: number  # 0-100 completeness
  stages: [Stage]

Stage:
  id: string
  flowId: string
  name: string
  stakeholder_categories: StakeholderCategoriesMap
  impact_analysis_complete: boolean
  steps: [Step]

Step:
  id: string
  stageId: string
  name: string
  description?: string
  order: number
  # Methodology fields
  stakeholder_dependencies: StakeholderDependencies
  dependency_mapping: DependencyMapping
  impact_categories: ImpactCategoriesMap
  telemetry_signals: TelemetrySignals
  observable_units: ObservableUnits
  validation_status: ValidationStatus

# Methodology-specific schemas
StakeholderDependencies:
  people: [PersonStakeholder]
  business_entities: [BusinessEntityStakeholder]
  vendors: [VendorStakeholder]

# Consistent stakeholder structure across all types
PersonStakeholder:
  type: "People"
  name: string
  role: string
  dependencies: [string]
  impact_if_unavailable: string

BusinessEntityStakeholder:
  type: "BusinessEntities"  
  name: string
  role: string  # Consistent field structure
  dependencies: [string]
  impact_if_unavailable: string  # Added for consistency

VendorStakeholder:
  type: "Vendors"
  name: string
  role: string  # Consistent field structure
  dependencies: [string]
  impact_if_unavailable: string  # Added for consistency

# Step 2: Dependency Mapping
DependencyMapping:
  type: "object"
  description: "Maps stakeholder expectations from Step 2"
  structure:
    stakeholder_id: string
    expectations: string  # What they expect from this step

# Step 3: Impact Analysis
ImpactCategoriesMap:
  financial: FinancialImpact
  legal_compliance: ComplianceImpact
  operational: OperationalImpact
  customer_experience: CustomerExperienceImpact

FinancialImpact:
  category: "Financial"
  measurable_signals: [string]
  business_consequence: string
  estimated_cost_per_hour?: number

ComplianceImpact:
  category: "Legal/Compliance"
  regulatory_requirements: [string]
  violation_signals: [string]
  business_consequence: string

OperationalImpact:
  category: "Operational"
  process_metrics: [string]
  efficiency_signals: [string]
  business_consequence: string

CustomerExperienceImpact:
  category: "Customer Experience"
  user_experience_metrics: [string]
  satisfaction_signals: [string]
  business_consequence: string

# Step 4: Telemetry Mapping
TelemetrySignals:
  type: "object"
  description: "Maps stakeholder impacts to required telemetry and monitoring data"
  structure:
    stakeholder_id: string
    impact_telemetry_mappings: [ImpactTelemetryMapping]

ImpactTelemetryMapping:
  impact_reference: string  # Reference to specific impact from Step 3
  telemetry_required: string  # What monitoring data is needed
  data_sources: [string]  # Systems that provide the telemetry
  observable_signals: [string]  # Specific metrics/events to collect

# Step 5: Signal Instrumentation
ObservableUnits:
  type: "object"
  description: "Maps telemetry requirements to specific technical signal instrumentation"
  structure:
    stakeholder_id: string
    telemetry_signal_mappings: [TelemetrySignalMapping]

TelemetrySignalMapping:
  telemetry_reference: string  # Reference to specific telemetry from Step 4
  observable_unit: string  # Technical component to instrument
  signal_type: enum ["Business Signal", "Process Signal", "System Signal"]
  signal_name: string  # Metric identifier
  instrumentation_details: string  # Technical implementation description
  threshold_conditions?: string  # Alert thresholds (optional)
  implementation_notes?: string  # Additional technical guidance (optional)

ValidationStatus:
  stakeholder_trace_complete: boolean
  dependency_mapping_complete: boolean
  impact_mapping_complete: boolean
  telemetry_mapping_complete: boolean
  signal_definitions_complete: boolean
  overall_score: number
  missing_elements: [string]
```

---

## 5. UI/UX Implementation Requirements

### Discovery Sequence Integration

**Main Editor Layout:**
- Left sidebar: Flow/Stage/Step hierarchy with methodology progress indicators
- Center canvas: Horizontal Stage visualization with stakeholder context
- Right panel: Discovery sequence forms (context-sensitive)

**Methodology Workflow:**
- Step 1 (WHO): StakeholderCategoriesForm with guided prompts
- Step 2 (WHAT expect): DependencyMappingForm linked to stakeholders  
- Step 3 (WHAT breaks): ImpactAnalysisForm with impact categories
- Step 4 (WHAT telemetry): TelemetryMappingForm with signal recommendations
- Step 5 (WHAT signals): SignalDefinitionForm with trace validation

**Visual Indicators:**
- Progress bars showing discovery sequence completion
- Color-coded validation status (red/yellow/green)
- Trace visualization showing stakeholder → impact → signal connections
- Methodology compliance scores per Step/Stage/Flow

### Guided Prompts UI Specification

**Display Location:** Above each form field as visible guidance text
**Visibility:** Always visible - not hidden behind tooltips or help icons
**Styling:** 💡 icon prefix to distinguish from field labels

**Layout Pattern:**
```
💡 Guided prompt text (always visible with 💡 icon)
Include specific guidance for measurability/methodology compliance
Examples: "Specific examples in quotes to guide user input"

[Form field - textarea/input]

✅ Validation feedback (below field when applicable)
```

**Implementation Example:**
```
💡 How does failure cost money, lose revenue, or create measurable financial risk?
Include specific dollar amounts, rates, percentages, or countable financial events
Examples: "Rate lock cost $2000-5000, application abandonment rate 15%"

[Text area for user input]

✅ Measurability: Good - includes specific dollar amounts
```

**Rationale:** Guided prompts must be immediately visible to ensure methodology compliance
**Applies To:** All discovery steps (2, 3, 4, 5) with guided prompt specifications

---

## 6. Functional Requirements (MVP with Methodology Integration)

### 🔖 FS-01 through FS-07 for FR-1: Create Flow (Enhanced)

**🔖 FS-01: User Story**

> **As a** Product Owner\
> **I want** to create a new Flow with stakeholder-first methodology guidance\
> **So that** I can define a business process container that enforces observability design principles.

---

**🔖 FS-02: Acceptance Criteria**

- A "Create Flow" control appears in the BOS Editor sidebar with methodology guidance
- Flow creation wizard includes methodology overview and discovery sequence explanation
- Form validates that name and description align with business process identification
- Created Flow initializes with methodology compliance tracking
- Discovery sequence progress tracker appears for the new Flow

---

**🔖 FS-03: BDD Scenarios**

```gherkin
Scenario: Create Flow with methodology guidance
  Given I am viewing the BOS Editor sidebar
  When I click "Create Flow"
  Then I see a methodology overview modal
  And I see the discovery sequence steps outlined
  When I enter "Customer Loan Application" as name
  And I enter "End-to-end loan application process" as description
  And I click "Create"
  Then a new Flow appears with methodology compliance tracker
  And the discovery sequence shows "Step 1: WHO depends" as next action

Scenario: Methodology compliance initialization
  Given I create a new Flow
  Then the validation_score starts at 0
  And stakeholder_mapping_complete is false
  And methodology_version is set to current version
```

---

**🔖 FS-04: Functional Requirement Declaration**\
**FR-1: Create Flow with Methodology Integration**\
Allow creation of Flows with embedded stakeholder-first methodology guidance and compliance tracking.

---

**🔖 FS-05: Data Model Linkage**

> **Object:** `Flow` (Enhanced)\
> **Schema Impact:** Adds methodology compliance fields

**Required Implementation:**
```typescript
interface Flow {
  id: string;
  name: string;
  description: string;
  version: string;
  methodology_version: string;
  stakeholder_mapping_complete: boolean;
  validation_score: number;
  stages: Stage[];
}
```

---

**🔖 FS-06: UI Integration Context**

> **Location:** BOS Editor sidebar\
> **Components:** CreateFlowWizard, MethodologyOverlay, DiscoverySequenceTracker

**Implementation Requirements:**
- MethodologyOverlay component displays discovery sequence
- CreateFlowWizard enforces business process naming conventions
- DiscoverySequenceTracker shows progress through 5-step sequence

---

**🔖 FS-07: LLM Implementation Instructions**

**Implementation Dependencies:**
- React hooks: useState from 'react'
- ID generation: Simple Math.random() for prototype
- No external libraries required
- Inline validation functions

**Complete Implementation Code:**

```typescript
import React, { useState } from 'react';

// Simple ID generation for prototype
const generateId = () => Math.random().toString(36).substr(2, 9);

// Inline validation - no external dependencies
const validateFlowCreation = (name: string, description: string) => {
  const errors: string[] = [];
  if (!name.trim()) errors.push("Name is required");
  if (!description.trim()) errors.push("Description is required");
  if (name.length < 3) errors.push("Name must be at least 3 characters");
  return errors;
};

interface Flow {
  id: string;
  name: string;
  description: string;
  version: string;
  methodology_version: string;
  stakeholder_mapping_complete: boolean;
  validation_score: number;
  stages: Stage[];
}

const CreateFlowWizard = () => {
  const [name, setName] = useState('');
  const [description, setDescription] = useState('');
  const [errors, setErrors] = useState<string[]>([]);

  const createFlow = (name: string, description: string): Flow => {
    return {
      id: generateId(),
      name,
      description,
      version: "1.0",
      methodology_version: "1.4.3",
      stakeholder_mapping_complete: false,
      validation_score: 0,
      stages: []
    };
  };

  const handleSave = () => {
    const validationErrors = validateFlowCreation(name, description);
    if (validationErrors.length > 0) {
      setErrors(validationErrors);
      return;
    }
    
    const newFlow = createFlow(name, description);
    // Save flow logic here
    setErrors([]);
  };

  return (
    <div>
      <input 
        value={name} 
        onChange={(e) => setName(e.target.value)}
        placeholder="Flow name"
      />
      <textarea 
        value={description} 
        onChange={(e) => setDescription(e.target.value)}
        placeholder="Flow description"
      />
      {errors.map(error => <div key={error} style={{color: 'red'}}>{error}</div>)}
      <button onClick={handleSave}>Create Flow</button>
    </div>
  );
};
```

---

### 🔖 FS-01 through FS-07 for FR-2: Stakeholder Discovery Workflow

**🔖 FS-01: User Story**

> **As a** Product Owner\
> **I want** guided forms for stakeholder identification following the discovery sequence\
> **So that** I can systematically identify WHO depends on each Step before defining impacts.

---

**🔖 FS-02: Acceptance Criteria**

- StakeholderCategoriesForm appears when adding/editing Steps
- Form sections for People, Business Entities, and Vendors stakeholder categories
- Each category includes guided prompts and examples following stakeholder relationship framework
- Form validates that at least one stakeholder is identified across any category (categories not mutually exclusive)
- Categories are not mutually exclusive - steps may have 1, 2, or all 3 types
- Business logic: some steps only serve people, others only integrate with vendors
- Progress tracker shows completion of Discovery Sequence Step 1
- Form data populates Step.stakeholder_dependencies
- Individual stakeholder forms use simple Save/Cancel pattern only
- Save returns user to main stakeholder discovery overview
- Users add multiple stakeholders by repeating "Add [Type]" workflow
- No "Save & Add More" complexity for prototype MVP

---

**🔖 FS-03: BDD Scenarios**

```gherkin
Scenario: Complete stakeholder identification
  Given I am editing a Step in the "Loan Approval" stage
  When I open the stakeholder discovery form
  Then I see three sections: People, Business Entities, Vendors
  When I add "Loan Applicant" as a Person stakeholder
  And I add "Mortgage Application" as a Business Entity
  And I click "Save & Continue to Step 2"
  Then the Step shows stakeholder_dependencies populated
  And discovery sequence progress shows Step 1 complete

Scenario: Enforce minimum stakeholder requirement
  Given the stakeholder form is open
  When I try to continue without identifying any stakeholders
  Then I see validation error "At least one stakeholder required across any category"
  And the continue button remains disabled

Scenario: Single stakeholder category allowed
  Given the stakeholder form is open
  When I add only a Vendor stakeholder
  And I click "Save & Continue to Step 2"
  Then the form successfully advances
  And Step 1 is marked complete
```

---

**🔖 FS-04: Functional Requirement Declaration**\
**FR-2: Stakeholder Discovery Workflow**\
Implement guided stakeholder identification forms that enforce the "WHO depends first" principle.

---

**🔖 FS-05: Data Model Linkage**

> **Object:** `Step.stakeholder_dependencies`\
> **Schema Impact:** Populates StakeholderDependencies with consistent field structure

**Required Structure:**
```typescript
interface StakeholderDependencies {
  people: PersonStakeholder[];
  business_entities: BusinessEntityStakeholder[];
  vendors: VendorStakeholder[];
}

// Consistent structure across all stakeholder types
interface PersonStakeholder {
  type: "People";
  name: string;
  role: string;
  dependencies: string[];
  impact_if_unavailable: string;
}

interface BusinessEntityStakeholder {
  type: "BusinessEntities";
  name: string;
  role: string;  // Consistent with PersonStakeholder
  dependencies: string[];
  impact_if_unavailable: string;  // Added for consistency
}

interface VendorStakeholder {
  type: "Vendors";
  name: string;
  role: string;  // Consistent with PersonStakeholder
  dependencies: string[];
  impact_if_unavailable: string;  // Added for consistency
}
```

---

**🔖 FS-06: UI Integration Context**

> **Location:** Step editing modal/panel\
> **Components:** StakeholderCategoriesForm, StakeholderCategorySection, DiscoveryProgressTracker

**Form Structure:**
- Three expandable sections for each stakeholder category
- Guided prompts with methodology examples using stakeholder relationship framework
- Add/remove functionality for each stakeholder type
- Real-time validation and progress tracking
- Simple Save/Cancel pattern for individual stakeholder forms

**Stakeholder Form Button Pattern:**
- **Save Button:** Save stakeholder data and return to main stakeholder overview
- **Cancel Button:** Discard changes and return to main stakeholder overview
- **No "Save & Add More":** Eliminated for prototype simplicity - users add multiple via repeated "Add [Type]" clicks
- **Consistent Across Forms:** Person, Business Entity, and Vendor stakeholder forms use same pattern

---

**🔖 FS-07: LLM Implementation Instructions**

**Implementation Dependencies:**
- React hooks: useState from 'react'
- No external libraries for validation
- Inline type definitions for prototype simplicity
- Simple object manipulation (no complex state management)

**Complete Implementation Code:**

```typescript
import React, { useState } from 'react';

// Inline type definitions - no external type files needed
interface PersonStakeholder {
  type: "People";
  name: string;
  role: string;
  dependencies: string;
  impact_if_unavailable: string;
}

interface BusinessEntityStakeholder {
  type: "BusinessEntities";
  name: string;
  role: string;
  dependencies: string;
  impact_if_unavailable: string;
}

interface VendorStakeholder {
  type: "Vendors";
  name: string;
  role: string;
  dependencies: string;
  impact_if_unavailable: string;
}

interface StakeholderDependencies {
  people: PersonStakeholder[];
  business_entities: BusinessEntityStakeholder[];
  vendors: VendorStakeholder[];
}

// Simple validation - no external library
const validateStakeholders = (stakeholders: StakeholderDependencies): boolean => {
  const totalStakeholders = 
    stakeholders.people.length + 
    stakeholders.business_entities.length + 
    stakeholders.vendors.length;
  return totalStakeholders >= 1;
};

// Simple form field specification
const getPlaceholderText = (field: string, type: string): string => {
  const placeholders = {
    name: {
      people: "e.g., Loan Applicant",
      business_entities: "e.g., Mortgage Application Record",
      vendors: "e.g., Experian Credit Bureau"
    },
    role: {
      people: "e.g., Primary loan applicant",
      business_entities: "e.g., Mortgage application record", 
      vendors: "e.g., Credit reporting service"
    }
  };
  return placeholders[field]?.[type] || "";
};

const StakeholderCategoriesForm = ({ step, onSave }) => {
  const [stakeholders, setStakeholders] = useState<StakeholderDependencies>({
    people: [],
    business_entities: [],
    vendors: []
  });
  
  const [showAddForm, setShowAddForm] = useState<string | null>(null);

  const addStakeholder = (type: 'people' | 'business_entities' | 'vendors') => {
    const newStakeholder = {
      type: type === 'people' ? 'People' : type === 'business_entities' ? 'BusinessEntities' : 'Vendors',
      name: '',
      role: '',
      dependencies: '',
      impact_if_unavailable: ''
    };
    
    setStakeholders(prev => ({
      ...prev,
      [type]: [...prev[type], newStakeholder]
    }));
  };

  const canContinue = validateStakeholders(stakeholders);

  return (
    <div>
      <div className="methodology-guidance">
        💡 Identify WHO depends on this step using the relationship framework:
        <br />• SERVES: People/customers who get value FROM this step
        <br />• MAINTAINS: Business entities/objects kept current BY this step  
        <br />• INTEGRATES WITH: Vendors/systems required FOR this step
      </div>

      {/* People Section */}
      <div className="stakeholder-section">
        <h3>👤 PEOPLE (Who this step SERVES)</h3>
        <div className="guided-prompt">
          💡 Which customers, users, or employees does this step serve?
        </div>
        {stakeholders.people.map((person, index) => (
          <div key={index}>✅ {person.name} - {person.role}</div>
        ))}
        <button onClick={() => addStakeholder('people')}>
          + Add Person This Step Serves
        </button>
      </div>

      {/* Business Entities Section */}
      <div className="stakeholder-section">
        <h3>🏢 BUSINESS ENTITIES (What this step MAINTAINS)</h3>
        <div className="guided-prompt">
          💡 Which business objects, requirements, or processes does this step maintain?
        </div>
        {stakeholders.business_entities.map((entity, index) => (
          <div key={index}>✅ {entity.name} - {entity.role}</div>
        ))}
        <button onClick={() => addStakeholder('business_entities')}>
          + Add Business Entity This Step Maintains
        </button>
      </div>

      {/* Vendors Section */}
      <div className="stakeholder-section">
        <h3>🔗 VENDORS (What this step INTEGRATES WITH)</h3>
        <div className="guided-prompt">
          💡 Which third-party services or systems does this step require to function?
        </div>
        {stakeholders.vendors.map((vendor, index) => (
          <div key={index}>✅ {vendor.name} - {vendor.role}</div>
        ))}
        <button onClick={() => addStakeholder('vendors')}>
          + Add Vendor This Step Integrates With
        </button>
      </div>

      {/* Progress Indicator */}
      <div className="progress-indicator">
        Progress: {stakeholders.people.length + stakeholders.business_entities.length + stakeholders.vendors.length} stakeholders identified
        <br />✅ Ready to continue (minimum requirement: at least 1 stakeholder total)
      </div>

      <button 
        onClick={() => onSave(stakeholders)}
        disabled={!canContinue}
      >
        Save & Continue to Step 2
      </button>
    </div>
  );
};
```

---

### 🔖 FS-01 through FS-07 for FR-3: Dependency Mapping Workflow

**🔖 FS-01: User Story**

> **As a** Product Owner\
> **I want** to define what each stakeholder expects from this step\
> **So that** I can systematically map stakeholder dependencies before analyzing impacts.

---

**🔖 FS-02: Acceptance Criteria**

- DependencyMappingForm appears for Step 2 of discovery sequence
- Single form with expandable sections per stakeholder from Step 1
- All stakeholders from Step 1 displayed with expectation fields
- Guided prompts provide context-specific guidance for each stakeholder type
- Allow saving with any amount of progress (no blocking)
- All stakeholders from Step 1 must have expectations defined for step completion
- Progress indicator shows "X/Y stakeholders have expectations defined"
- NO restrictions - users can populate any discovery step anytime
- Recommend 1→2→3→4→5 sequence but don't enforce
- All discovery steps always accessible regardless of completion status
- Show logical inconsistencies as guidance, not blocking errors

---

**🔖 FS-03: BDD Scenarios**

```gherkin
Scenario: Map stakeholder expectations
  Given I have identified stakeholders for a Step
  When I open the dependency mapping form (Step 2)
  Then I see each stakeholder with expectation input fields
  And each section shows context-specific guided prompts
  When I define expectations for Loan Applicant
  And I save progress
  Then the expectation data is saved
  And progress shows "1/3 stakeholders have expectations defined"

Scenario: Flexible step access
  Given I am in Step 2 (dependency mapping)
  When I decide to jump to Step 4 (telemetry mapping)
  Then the system allows navigation without blocking
  And shows guidance about recommended sequence
  And preserves any progress made in Step 2
```

---

**🔖 FS-04: Functional Requirement Declaration**\
**FR-3: Dependency Mapping Workflow**\
Implement guided dependency mapping that connects stakeholder identification to specific expectations.

---

**🔖 FS-05: Data Model Linkage**

> **Object:** `Step.dependency_mapping`\
> **Schema Impact:** Stores stakeholder expectations from Step 2

---

**🔖 FS-06: UI Integration Context**

> **Location:** Step editing interface, Step 2 of discovery sequence\
> **Components:** DependencyMappingForm, stakeholder expectation sections

---

**🔖 FS-07: LLM Implementation Instructions**

```typescript
const DependencyMappingForm = ({ step, stakeholders, onSave }) => {
  const [expectations, setExpectations] = useState<DependencyMapping>({});

  const formSpecification = {
    expectation_field: {
      label: "What they expect from this step",
      type: "textarea",
      required: true,
      guided_prompts_by_type: {
        people: "Processing time, communication, outcomes, user experience...",
        business_entities: "Data requirements, compliance needs, status updates...",
        vendors: "Technical requirements, SLA expectations, integration needs..."
      },
      placeholder_examples: {
        people: "Fast processing within 24 hours, accurate verification, clear status updates...",
        business_entities: "Complete income data, verified DTI calculation, compliance flags...",
        vendors: "Proper API authentication, complete request data, response handling..."
      }
    }
  };

  const validateCompletion = () => {
    // All stakeholders from Step 1 must have expectations defined for step completion
    return stakeholders.every(stakeholder => 
      expectations[stakeholder.id] && expectations[stakeholder.id].length > 0
    );
  };

  // Guided prompts display pattern with 💡 icons
  return (
    <div>
      {stakeholders.map(stakeholder => (
        <section key={stakeholder.id}>
          <h3>{stakeholder.name} ({stakeholder.type})</h3>
          <div className="guided-prompt">
            💡 {formSpecification.expectation_field.guided_prompts_by_type[stakeholder.type.toLowerCase()]}
          </div>
          <textarea
            placeholder={formSpecification.expectation_field.placeholder_examples[stakeholder.type.toLowerCase()]}
            onChange={(e) => setExpectations({
              ...expectations,
              [stakeholder.id]: e.target.value
            })}
          />
        </section>
      ))}
    </div>
  );
};
```

---

### 🔖 FS-01 through FS-07 for FR-4: Impact Analysis Workflow

**🔖 FS-01: User Story**

> **As a** Product Owner\
> **I want** to define what breaks when a Step fails, organized by measurable impact categories\
> **So that** I can connect stakeholder dependencies to quantifiable business consequences.

---

**🔖 FS-02: Acceptance Criteria**

- ImpactAnalysisForm appears for Step 3 of discovery sequence
- Stakeholder sections with impact category subsections (Financial, Legal, Operational, Customer Experience)
- Each impact category field includes guided prompts specific to measurability requirements
- All impacts must be measurable via system telemetry or business metrics per BOS principle
- Measurability validation warns if impacts lack measurable components, but doesn't block saving
- At least 1 impact category must be defined per stakeholder for step completion
- Customer Experience Impact uses immediate consumer model for stakeholder perspective
- Allow saving with any amount of progress (no blocking)
- Progress indicator shows "X/Y stakeholders have measurable impacts defined"

---

**🔖 FS-03: BDD Scenarios**

```gherkin
Scenario: Define measurable impacts
  Given I have completed stakeholder identification and dependency mapping
  When I open the impact analysis form (Step 3)
  Then I see each stakeholder with four impact category sections
  And each section shows guided prompts for measurable impacts
  When I define "Rate lock expiration cost: $2,000-5,000" as Financial impact
  And I define "Portal login attempts +300%" as Customer Experience impact
  Then the system validates measurability as Good
  And progress updates to show impacts defined

Scenario: Measurability validation guidance
  Given I am defining impacts for a stakeholder
  When I enter "Customer frustration and disappointment"
  Then the system shows warning "Consider how this impact can be measured by systems"
  But still allows saving the data
  And suggests measurable alternatives
```

---

**🔖 FS-04: Functional Requirement Declaration**\
**FR-4: Impact Analysis Workflow**\
Implement guided impact analysis that enforces measurability principles and connects to stakeholder perspectives.

---

**🔖 FS-05: Data Model Linkage**

> **Object:** `Step.impact_categories`\
> **Schema Impact:** Populates ImpactCategoriesMap with measurable business consequences

---

**🔖 FS-06: UI Integration Context**

> **Location:** Step editing interface, Step 3 of discovery sequence\
> **Components:** ImpactAnalysisForm, ImpactCategorySection, MeasurabilityValidator

---

**🔖 FS-07: LLM Implementation Instructions**

```typescript
const ImpactAnalysisForm = ({ step, stakeholders, onSave }) => {
  const [impacts, setImpacts] = useState<ImpactCategoriesMap>();

  const impactCategoryFields = {
    financial_impact: {
      label: "Financial Impact",
      type: "textarea",
      required: false,
      guided_prompt: "How does failure cost money, lose revenue, or create measurable financial risk?",
      measurability_guidance: "Include specific dollar amounts, rates, percentages, or countable financial events",
      examples: "Rate lock cost $2000-5000, application abandonment rate 15%, processing cost increase $200-500"
    },
    legal_compliance_impact: {
      label: "Legal/Compliance Impact",
      type: "textarea", 
      required: false,
      guided_prompt: "What regulatory, compliance, or legal requirements are violated with measurable consequences?",
      measurability_guidance: "Include timeline violations, compliance percentages, audit findings, binary flags",
      examples: "FCRA deadline violations 2-3 days, QM rule compliance gap (binary), audit finding count"
    },
    operational_impact: {
      label: "Operational Impact",
      type: "textarea",
      required: false,
      guided_prompt: "How does failure disrupt processes with measurable efficiency or performance impacts?",
      measurability_guidance: "Include processing times, manual intervention rates, queue delays, resource counts",
      examples: "Processing time +15 days, manual intervention rate 25%, queue time +48 hours"
    },
    customer_experience_impact: {
      label: "Customer Experience Impact",
      type: "textarea",
      required: false,
      guided_prompt: function(stakeholderType) {
        const prompts = {
          people: "How does failure affect this person's direct user experience?",
          business_entities: "How does failure affect systems/processes that consume this entity's data?",
          vendors: "How does failure affect the direct client/consumer of this vendor service?"
        };
        return prompts[stakeholderType.toLowerCase()] || "How does failure affect measurable user interactions?";
      },
      measurability_guidance: "Include response times, call volumes, portal usage, completion rates",
      examples: "Customer service calls +150%, portal login attempts +300%, status response delay +24 hours"
    }
  };

  const validateMeasurability = (impactText: string) => {
    // Validate that impacts include specific metrics, counts, percentages, durations, or binary flags
    // Warn if qualitative descriptions detected but don't block
    const measurabilityPatterns = [
      /\d+%/,  // percentages
      /\$\d+/, // dollar amounts  
      /\d+\s*(hours?|days?|minutes?)/, // time durations
      /\d+\s*(count|rate|calls?)/, // countable items
      /(increase|decrease|rise|drop)\s*\d+/ // quantified changes
    ];
    
    const hasMeasurableElements = measurabilityPatterns.some(pattern => 
      pattern.test(impactText)
    );
    
    if (!hasMeasurableElements) {
      return {
        warning: "Consider how this impact can be measured by systems or business metrics",
        suggestion: "Add specific measurable outcomes (counts, rates, times, costs)"
      };
    }
    
    return { status: "Good - includes measurable components" };
  };

  // Display guided prompts with immediate consumer model context
  return (
    <div>
      {stakeholders.map(stakeholder => (
        <section key={stakeholder.id}>
          <h3>{stakeholder.name} ({stakeholder.type})</h3>
          {Object.entries(impactCategoryFields).map(([key, field]) => (
            <div key={key} className="impact-category">
              <div className="guided-prompt">
                💡 {typeof field.guided_prompt === 'function' 
                    ? field.guided_prompt(stakeholder.type)
                    : field.guided_prompt}
              </div>
              <div className="measurability-guidance">
                {field.measurability_guidance}
              </div>
              <div className="examples">
                Examples: "{field.examples}"
              </div>
              <textarea
                onChange={(e) => {
                  const validation = validateMeasurability(e.target.value);
                  // Update impacts and show validation feedback
                }}
              />
            </div>
          ))}
        </section>
      ))}
    </div>
  );
};
```

---

### 🔖 FS-01 through FS-07 for FR-5: Telemetry Mapping Workflow

**🔖 FS-01: User Story**

> **As a** Developer\
> **I want** to define what telemetry must exist to detect the impacts identified by Product Owners\
> **So that** I can bridge business impacts to technical monitoring requirements.

---

**🔖 FS-02: Acceptance Criteria**

- TelemetryMappingForm appears for Step 4 of discovery sequence
- Impact-to-telemetry mapping per stakeholder, referencing impacts from Step 3
- Each impact has telemetry mapping fields: telemetry required, data sources, observable signals
- Guided prompts help identify observable data, systems, and specific metrics
- Ensures every Step 3 impact has corresponding Step 4 telemetry mapping
- Allow saving with any amount of progress (no blocking)
- All impacts from Step 3 must have telemetry mapping for step completion
- Progress indicator shows "X/Y impacts have telemetry defined"
- Impact traceability maintained from Step 3 to Step 4

---

**🔖 FS-03: BDD Scenarios**

```gherkin
Scenario: Map impact to telemetry
  Given I have completed impact analysis with measurable impacts
  When I open the telemetry mapping form (Step 4)
  Then I see each stakeholder's impacts listed
  And each impact has telemetry mapping fields
  When I define telemetry for "Portal login +300%" impact
  And I specify "Web server logs, user analytics" as data sources
  And I define "Login frequency per customer ID" as observable signal
  Then the telemetry mapping is saved
  And progress shows telemetry defined for that impact

Scenario: Complete telemetry traceability
  Given I have defined telemetry for all impacts
  When I review the telemetry mapping
  Then I can trace from each stakeholder impact to specific telemetry requirements
  And no impacts are missing telemetry definitions
```

---

**🔖 FS-04: Functional Requirement Declaration**\
**FR-5: Telemetry Mapping Workflow**\
Implement guided telemetry mapping that connects measurable impacts to observable monitoring data.

---

**🔖 FS-05: Data Model Linkage**

> **Object:** `Step.telemetry_signals`\
> **Schema Impact:** Populates TelemetrySignals with impact-to-telemetry mappings

---

**🔖 FS-06: UI Integration Context**

> **Location:** Step editing interface, Step 4 of discovery sequence\
> **Components:** TelemetryMappingForm, ImpactTelemetryMapper

---

**🔖 FS-07: LLM Implementation Instructions**

```typescript
const TelemetryMappingForm = ({ step, impacts, onSave }) => {
  const [telemetryMappings, setTelemetryMappings] = useState<TelemetrySignals>({});

  const telemetryMappingFields = {
    impact_reference: {
      type: "display_only",
      content: "Show specific impact from Step 3",
      example: "Rate lock expiration cost: $2,000-5,000"
    },
    telemetry_required: {
      label: "What telemetry/monitoring data is needed to detect this impact?",
      type: "textarea",
      required: true,
      guided_prompt: "Identify what observable data, logs, metrics, or events are needed",
      measurability_guidance: "Focus on data that systems can automatically collect and analyze",
      examples: "API response time measurements, event logs, user behavior analytics, workflow state tracking"
    },
    data_sources: {
      label: "Which systems/sources provide this telemetry?",
      type: "textarea",
      required: true,
      guided_prompt: "Identify specific systems, databases, services, or monitoring tools",
      examples: "Customer portal web server logs, loan processing workflow engine, API gateway metrics"
    },
    observable_signals: {
      label: "Specific signals/metrics to collect",
      type: "textarea",
      required: true,
      guided_prompt: "Define measurable signals, metrics, events, or KPIs to instrument",
      examples: "Login frequency per customer ID, API error rates, queue time duration, response time percentiles"
    }
  };

  const validateTelemetryTraceability = () => {
    // Ensure every Step 3 impact has corresponding Step 4 telemetry mapping
    return impacts.every(impact => 
      telemetryMappings[impact.id] && 
      telemetryMappings[impact.id].telemetry_required
    );
  };

  // Display with guided prompts following UI specification
  return (
    <div>
      {impacts.map(impact => (
        <section key={impact.id}>
          <div className="impact-reference">
            {impact.description} {/* Show impact from Step 3 */}
          </div>
          
          {Object.entries(telemetryMappingFields).map(([key, field]) => {
            if (field.type === "display_only") return null;
            
            return (
              <div key={key} className="telemetry-field">
                <div className="guided-prompt">
                  💡 {field.guided_prompt}
                </div>
                <div className="guidance">
                  {field.measurability_guidance || field.examples}
                </div>
                <textarea
                  placeholder={field.examples}
                  onChange={(e) => {
                    // Update telemetry mappings
                  }}
                />
              </div>
            );
          })}
        </section>
      ))}
    </div>
  );
};
```

---

### 🔖 FS-01 through FS-07 for FR-6: Signal Instrumentation Workflow

**🔖 FS-01: User Story**

> **As a** Developer\
> **I want** to define specific signals to instrument in Observable Units based on telemetry requirements\
> **So that** I can complete the methodology chain with technical implementation specifications.

---

**🔖 FS-02: Acceptance Criteria**

- SignalDefinitionForm appears for Step 5 of discovery sequence
- Telemetry-to-observable-signal mapping per stakeholder, referencing telemetry from Step 4
- Signal definition fields include: Observable Unit, Signal Type, Signal Name, Instrumentation Details, Thresholds
- Signal Type dropdown with Business Signal, Process Signal, System Signal options
- Guided prompts help identify technical components and implementation approaches
- All telemetry requirements from Step 4 must have signal definitions for step completion
- Allow saving with any amount of progress (no blocking)
- Progress indicator shows "X/Y telemetry requirements have signals defined"
- Complete methodology chain validation: Stakeholder → Impact → Telemetry → Signal

---

**🔖 FS-03: BDD Scenarios**

```gherkin
Scenario: Define signals for telemetry
  Given I have completed telemetry mapping with monitoring requirements
  When I open the signal definition form (Step 5)
  Then I see each telemetry requirement listed
  And each has signal definition fields
  When I define Observable Unit as "Customer Portal Web Application"
  And I select "Business Signal" as Signal Type
  And I specify instrumentation details
  Then the signal definition is saved
  And progress shows signal defined for that telemetry requirement

Scenario: Complete methodology chain
  Given I have defined signals for all telemetry requirements
  When I review the complete discovery sequence
  Then I can trace from stakeholder to signal instrumentation
  And the methodology chain is complete for implementation
```

---

**🔖 FS-04: Functional Requirement Declaration**\
**FR-6: Signal Instrumentation Workflow**\
Implement guided signal definition that completes the stakeholder-to-technical-implementation methodology chain.

---

**🔖 FS-05: Data Model Linkage**

> **Object:** `Step.observable_units`\
> **Schema Impact:** Populates ObservableUnits with telemetry-to-signal mappings

---

**🔖 FS-06: UI Integration Context**

> **Location:** Step editing interface, Step 5 of discovery sequence\
> **Components:** SignalDefinitionForm, TelemetrySignalMapper

---

**🔖 FS-07: LLM Implementation Instructions**

```typescript
const SignalDefinitionForm = ({ step, telemetryRequirements, onSave }) => {
  const [signalMappings, setSignalMappings] = useState<ObservableUnits>({});

  const signalDefinitionFields = {
    telemetry_reference: {
      type: "display_only",
      content: "Show specific telemetry requirement from Step 4",
      example: "Portal login frequency monitoring from web server logs"
    },
    observable_unit: {
      label: "Which technical component/service to instrument?",
      type: "text_input",
      required: true,
      guided_prompt: "Identify the specific system, service, or component to add observability",
      examples: "Customer Portal Web Application, Loan Processing Service, Income Verification API"
    },
    signal_type: {
      label: "Signal Type",
      type: "dropdown",
      required: true,
      options: ["Business Signal", "Process Signal", "System Signal"],
      guided_prompt: "Business = user behavior/outcomes, Process = workflow/business logic, System = infrastructure/performance"
    },
    signal_name: {
      label: "Signal/Metric Name",
      type: "text_input",
      required: true,
      guided_prompt: "Specific metric identifier for monitoring systems",
      examples: "customer_portal_login_frequency, equifax_api_success_rate, loan_queue_duration_pending_income"
    },
    instrumentation_details: {
      label: "How to technically implement this signal",
      type: "textarea",
      required: true,
      guided_prompt: "Describe the technical implementation: metrics type, data collection method, calculation logic",
      examples: "Counter metric tracking login events per customer ID, Response time histogram with 95th percentile, Boolean metric from database query"
    },
    threshold_conditions: {
      label: "Alert/monitoring thresholds",
      type: "textarea",
      required: false,
      guided_prompt: "Define when this signal indicates a problem requiring attention",
      examples: "Alert when daily logins > 3x baseline, Alert when success rate < 90%, Alert when p95 > 2000ms"
    },
    implementation_notes: {
      label: "Technical implementation guidance",
      type: "textarea",
      required: false,
      guided_prompt: "Additional technical details for developers implementing the instrumentation",
      examples: "Add to authentication service, store in time-series DB, HTTP client latency tracking"
    }
  };

  const validateMethodologyChain = () => {
    // Ensure complete trace: Stakeholder → Impact → Telemetry → Signal
    return telemetryRequirements.every(telemetry => 
      signalMappings[telemetry.id] && 
      signalMappings[telemetry.id].observable_unit &&
      signalMappings[telemetry.id].signal_name
    );
  };

  // Signal Type definitions for guidance
  const signalTypeGuidance = {
    "Business Signal": "User intent, behavior, and business outcome measurements (login frequency, abandonment rates)",
    "Process Signal": "Workflow execution, business logic, and process performance (queue durations, approval rates)",
    "System Signal": "Infrastructure health, service performance, technical measurements (API response times, error rates)"
  };

  return (
    <div>
      {telemetryRequirements.map(telemetry => (
        <section key={telemetry.id}>
          <div className="telemetry-reference">
            {telemetry.description} {/* Show telemetry from Step 4 */}
          </div>
          
          {Object.entries(signalDefinitionFields).map(([key, field]) => {
            if (field.type === "display_only") return null;
            
            return (
              <div key={key} className="signal-field">
                <div className="guided-prompt">
                  💡 {field.guided_prompt}
                </div>
                {field.type === "dropdown" && (
                  <select onChange={(e) => {
                    // Update signal mappings
                    // Show signal type guidance
                  }}>
                    {field.options.map(option => (
                      <option key={option} value={option}>{option}</option>
                    ))}
                  </select>
                )}
                {field.type === "text_input" && (
                  <input
                    type="text"
                    placeholder={field.examples}
                    onChange={(e) => {
                      // Update signal mappings
                    }}
                  />
                )}
                {field.type === "textarea" && (
                  <textarea
                    placeholder={field.examples}
                    onChange={(e) => {
                      // Update signal mappings
                    }}
                  />
                )}
              </div>
            );
          })}
        </section>
      ))}
    </div>
  );
};
```

---

### 🔖 FS-01 through FS-07 for FR-7: Enhanced CSV Import/Export

**🔖 FS-01: User Story**

> **As a** user\
> **I want** to import/export Flow definitions with complete methodology data including stakeholders, impacts, telemetry, and signals\
> **So that** I can work with business observability mappings in spreadsheet format while preserving traceability.

---

**🔖 FS-02: Acceptance Criteria**

- Export includes all methodology fields from all 5 discovery steps
- CSV structure preserves stakeholder → impact → telemetry → signal relationships
- Import validates methodology compliance and traceability before processing
- Exported CSV can be re-imported without data loss
- CSV format includes methodology version for compatibility
- Stakeholder relationship types (serves/maintains/integrates) included in export

---

**🔖 FS-03: BDD Scenarios**

```gherkin
Scenario: Export complete methodology data
  Given I have Steps with complete 5-step discovery sequences
  When I export to CSV
  Then the CSV includes all stakeholder data with relationship types
  And all impact analysis data is preserved with measurability indicators
  And telemetry mappings and signal definitions are included
  And methodology chain traceability is maintained

Scenario: Import with methodology validation
  Given I have a CSV with complete methodology data
  When I import the file
  Then stakeholder mappings are restored with relationship framework
  And impact analysis includes measurability validation
  And telemetry and signal mappings are reconstructed
  And methodology chain validation runs on imported data
```

---

**🔖 FS-04: Functional Requirement Declaration**\
**FR-7: Enhanced CSV Import/Export with Complete Methodology**\
Support full methodology data in CSV operations with traceability validation.

---

**🔖 FS-05: Data Model Linkage**

> **Objects:** All entities with methodology fields across 5 discovery steps\
> **Schema Impact:** Requires flattening/expanding of nested methodology data for CSV format

---

**🔖 FS-06: UI Integration Context**

> **Location:** Main toolbar\
> **Components:** Enhanced ImportExportControls with methodology options and validation feedback

---

**🔖 FS-07: LLM Implementation Instructions**

```typescript
class MethodologyCSVHandler {
  static export(flows: Flow[]): string {
    const headers = [
      'flow_name', 'stage_name', 'step_name', 'step_description',
      // Step 1: Stakeholder data
      'people_stakeholders', 'business_entity_stakeholders', 'vendor_stakeholders',
      'stakeholder_relationship_types',
      // Step 2: Dependencies  
      'stakeholder_expectations',
      // Step 3: Impact analysis
      'financial_impacts', 'legal_impacts', 'operational_impacts', 'customer_experience_impacts',
      'measurability_validation_status',
      // Step 4: Telemetry mapping
      'telemetry_requirements', 'data_sources', 'observable_signals_step4',
      // Step 5: Signal instrumentation
      'observable_units', 'signal_types', 'signal_names', 'instrumentation_details',
      'threshold_conditions', 'implementation_notes',
      // Validation and metadata
      'validation_score', 'methodology_version', 'methodology_chain_complete'
    ];

    const rows = [];
    flows.forEach(flow => {
      flow.stages.forEach(stage => {
        stage.steps.forEach(step => {
          rows.push({
            flow_name: flow.name,
            stage_name: stage.name,
            step_name: step.name,
            step_description: step.description || '',
            
            // Step 1 data
            people_stakeholders: JSON.stringify(step.stakeholder_dependencies?.people || []),
            business_entity_stakeholders: JSON.stringify(step.stakeholder_dependencies?.business_entities || []),
            vendor_stakeholders: JSON.stringify(step.stakeholder_dependencies?.vendors || []),
            stakeholder_relationship_types: JSON.stringify({
              serves: step.stakeholder_dependencies?.people?.length || 0,
              maintains: step.stakeholder_dependencies?.business_entities?.length || 0,
              integrates_with: step.stakeholder_dependencies?.vendors?.length || 0
            }),
            
            // Step 2 data
            stakeholder_expectations: JSON.stringify(step.dependency_mapping || {}),
            
            // Step 3 data
            financial_impacts: JSON.stringify(step.impact_categories?.financial || {}),
            legal_impacts: JSON.stringify(step.impact_categories?.legal_compliance || {}),
            operational_impacts: JSON.stringify(step.impact_categories?.operational || {}),
            customer_experience_impacts: JSON.stringify(step.impact_categories?.customer_experience || {}),
            measurability_validation_status: this.validateMeasurability(step.impact_categories),
            
            // Step 4 data
            telemetry_requirements: JSON.stringify(step.telemetry_signals || {}),
            data_sources: this.extractDataSources(step.telemetry_signals),
            observable_signals_step4: this.extractObservableSignals(step.telemetry_signals),
            
            // Step 5 data
            observable_units: JSON.stringify(step.observable_units || {}),
            signal_types: this.extractSignalTypes(step.observable_units),
            signal_names: this.extractSignalNames(step.observable_units),
            instrumentation_details: this.extractInstrumentationDetails(step.observable_units),
            threshold_conditions: this.extractThresholds(step.observable_units),
            implementation_notes: this.extractImplementationNotes(step.observable_units),
            
            // Validation and metadata
            validation_score: step.validation_status?.overall_score || 0,
            methodology_version: flow.methodology_version || '1.4.3',
            methodology_chain_complete: this.validateMethodologyChain(step)
          });
        });
      });
    });

    return this.arrayToCSV(headers, rows);
  }

  static import(csvContent: string): Flow[] {
    // Parse CSV and reconstruct complete methodology data structures
    // Validate methodology compliance during import
    // Run methodology chain validation on imported data
    // Preserve stakeholder relationships and traceability
    // Validate measurability requirements
    // Ensure signal type consistency
    
    const parsedData = this.parseCSV(csvContent);
    const flows = [];
    
    parsedData.forEach(row => {
      // Reconstruct nested methodology structures
      const step = {
        stakeholder_dependencies: {
          people: JSON.parse(row.people_stakeholders || '[]'),
          business_entities: JSON.parse(row.business_entity_stakeholders || '[]'),
          vendors: JSON.parse(row.vendor_stakeholders || '[]')
        },
        dependency_mapping: JSON.parse(row.stakeholder_expectations || '{}'),
        impact_categories: {
          financial: JSON.parse(row.financial_impacts || '{}'),
          legal_compliance: JSON.parse(row.legal_impacts || '{}'),
          operational: JSON.parse(row.operational_impacts || '{}'),
          customer_experience: JSON.parse(row.customer_experience_impacts || '{}')
        },
        telemetry_signals: JSON.parse(row.telemetry_requirements || '{}'),
        observable_units: JSON.parse(row.observable_units || '{}')
      };
      
      // Validate methodology chain on import
      const validation = this.validateImportedStep(step);
      step.validation_status = validation;
      
      // Add to flows structure...
    });
    
    return flows;
  }

  private static validateMethodologyChain(step: Step): boolean {
    // Validate complete chain: Stakeholder → Impact → Telemetry → Signal
    const hasStakeholders = step.stakeholder_dependencies && (
      step.stakeholder_dependencies.people.length > 0 ||
      step.stakeholder_dependencies.business_entities.length > 0 ||
      step.stakeholder_dependencies.vendors.length > 0
    );
    
    const hasImpacts = step.impact_categories && Object.keys(step.impact_categories).length > 0;
    const hasTelemetry = step.telemetry_signals && Object.keys(step.telemetry_signals).length > 0;
    const hasSignals = step.observable_units && Object.keys(step.observable_units).length > 0;
    
    return hasStakeholders && hasImpacts && hasTelemetry && hasSignals;
  }
}
```

---

## 7. Test Data Scenario for Implementation Validation

### Test Scenario Context:
- **Flow:** Home Lending Mortgage
- **Stage:** Pre-Application  
- **Step:** Document Income Verification
- **Description:** "Collect and validate customer income documentation including pay stubs, tax returns, and employment verification to assess loan qualification"

### Complete 5-Step Discovery Data:

#### Step 1: Stakeholders (WHO depends)
**👤 Person Stakeholder:**
```yaml
name: "Loan Applicant"
role: "Primary borrower applying for mortgage"
dependencies: "Current income verification to support loan qualification and ensure loan approval process continues without delays"
impact_if_unavailable: "Cannot proceed with loan application, may lose rate lock, frustrated customer experience"
```

**🏢 Business Entity Stakeholder:**
```yaml
name: "Loan Record"
role: "Mortgage loan moving through origination system"
dependencies: "Current and verified income data to calculate accurate DTI ratios, update loan status, and maintain compliance with underwriting policies"
impact_if_unavailable: "Loan cannot progress to underwriting, DTI calculations become stale, regulatory compliance at risk, loan status stuck in pending"
```

**🔗 Vendor Stakeholder:**
```yaml
name: "Equifax Work Number"
role: "Income verification service provider"
dependencies: "API calls with customer SSN and employer info to retrieve employment history, current income, and pay frequency data for verification"
impact_if_unavailable: "Manual income verification required, process delay of 2-3 days, increased operational costs, customer frustration"
```

#### Step 2: Dependencies (WHAT they expect)
**👤 Loan Applicant Expects:**
- Fast processing: Income verification completed within 24 hours
- Accurate results: Verification matches their actual employment/income 
- Clear communication: Status updates on verification progress
- Privacy protection: Personal income data handled securely
- Next steps clarity: Know what happens after verification completes

**🏢 Loan Record Requires:**
- Complete income data: Gross monthly income, pay frequency, employment status
- Verified DTI calculation: Current debt-to-income ratio based on verified income
- Compliance flags: Any income discrepancies or red flags documented
- Status updates: Loan record status changed from "pending income" to "income verified"
- Audit trail: Documentation trail for regulatory compliance

**🔗 Equifax Work Number Requires:**
- Proper API authentication: Valid credentials and permissions
- Complete request data: Customer SSN, employer info, consent authorization
- Response handling: System can process verification results and error codes
- Rate limiting compliance: API calls within agreed usage limits
- Error recovery: Fallback procedures when service unavailable

#### Step 3: Impact Analysis (WHAT breaks - Measurable Impacts Only)
**👤 Loan Applicant Measurable Impacts:**
- **Financial:** Rate lock expiration cost: $2,000-5,000 additional monthly payment cost, Application abandonment: Binary event trackable in CRM system
- **Legal/Compliance:** FCRA disclosure timeline violations: Days past required disclosure deadline, TILA communication deadline breaches: Hours/days past required timing
- **Operational:** Manual documentation requirement: Count of additional documents needed, Processing time extension: +15 days added to timeline, Additional appointments: Count of extra meetings
- **Customer Experience:** Portal login frequency: +300% increased status check attempts, Customer service call volume: +150% additional calls generated

**🏢 Loan Record Measurable Impacts:**
- **Financial:** Application abandonment rate: 15% of loans lost at this stage, Processing cost increase: $200-500 per loan for manual verification, Pipeline velocity impact: +5-7 days delay affecting quarterly targets
- **Legal/Compliance:** Incomplete file percentage: 25% of loan files missing required income verification, QM rule compliance gap: Binary flag for Qualified Mortgage requirement failure, Audit finding count: +2-3 compliance issues per regulatory examination cycle
- **Operational:** Queue time increase: +48-72 hours loan stuck in pending status, Manual intervention rate: 35% requiring human processing vs 5% standard, DTI recalculation frequency: 2-3 additional calculations per loan
- **Customer Experience:** Status inquiry response time: +24-48 hour delay in providing accurate loan status, Customer portal accuracy: 40% of status updates delayed or inaccurate, Loan status API errors: +15% increase in status query failures

**🔗 Equifax Work Number Measurable Impacts:**
- **Financial:** Failed API transaction cost: Dollar amount of unused API calls, Service credit application: Binary flag for SLA violation compensation
- **Legal/Compliance:** Alternative data source usage: Count of non-standard verification methods used, Data security incident flag: Binary indicator if manual workarounds create exposure
- **Operational:** API failure rate: 15% of verification attempts fail, Retry attempt count: 3-5 additional API calls required, Alternative workflow activation: Binary flag for backup process engagement
- **Customer Experience:** Service delivery SLA breach: Minutes/hours past committed response time to lender client, Verification completion rate: Percentage of successful verifications delivered to Income Verification Service

#### Step 4: Telemetry Mapping (WHAT telemetry detects impact)
**Example Mappings:**
- **Impact:** "Portal login +300%" → **Telemetry:** Web application access logs, user session analytics, customer portal metrics → **Data Sources:** Customer portal web server logs, Google Analytics, authentication system → **Observable Signals:** Login frequency per customer ID, session duration metrics, status page view counts

- **Impact:** "API failure rate 15%" → **Telemetry:** API call success/failure logs, retry attempt counters, service health monitoring → **Data Sources:** Integration middleware logs, API gateway metrics, service mesh telemetry → **Observable Signals:** API response codes, retry count per transaction, service availability metrics

#### Step 5: Signal Instrumentation (WHAT signals to instrument)
**Example Signal Definitions:**
- **Telemetry:** "Portal login frequency monitoring" → **Observable Unit:** Customer Portal Web Application → **Signal Type:** Business Signal → **Signal Name:** `customer_portal_login_frequency` → **Instrumentation:** Counter metric tracking login events per customer ID per day → **Threshold:** Alert when daily logins > 3x baseline → **Implementation:** Add event tracking to authentication service, store in time-series database

- **Telemetry:** "API failure rate monitoring" → **Observable Unit:** Income Verification Integration Service → **Signal Type:** System Signal → **Signal Name:** `equifax_api_success_rate` → **Instrumentation:** Success rate percentage over 5-minute sliding window → **Threshold:** Alert when success rate < 90% → **Implementation:** API response code monitoring, calculate success percentage

**Note:** This complete test scenario validates all methodology specifications and provides realistic data for LLM implementation testing.

---

## 8. Non-Functional Requirements

- **Methodology Compliance:** All features must support the 5-step discovery sequence with stakeholder-first enforcement
- **Validation Performance:** Real-time validation must complete within 200ms
- **Data Integrity:** Complete stakeholder → impact → telemetry → signal traceability required
- **Measurability Enforcement:** Impact analysis must enforce measurable consequences only
- **Accessibility:** WCAG 2.1 AA compliance for all methodology forms
- **LLM Optimization:** All components must have explicit implementation specifications with guided prompts

---

## 9. LLM Implementation Priority

### Phase 1: Core Methodology Infrastructure
1. Enhanced data schemas with complete methodology fields
2. TraceValidationEngine implementation with 5-step chain validation
3. Discovery sequence form components with guided prompts UI and complete implementation dependencies
4. CompletenessScoring algorithm with methodology compliance

**Note:** Key FS-07 blocks (FR-1, FR-2, FR-4) include complete implementation dependencies with:
- Exact import statements
- Inline utility functions (no external dependencies)
- Full TypeScript interfaces
- Complete working examples ready for copy-paste implementation

### Phase 2: Guided Discovery Workflows
1. StakeholderCategoriesForm with relationship framework (serves/maintains/integrates)
2. DependencyMappingForm with stakeholder expectation mapping
3. ImpactAnalysisForm with measurability validation and immediate consumer model
4. TelemetryMappingForm with impact-to-telemetry traceability
5. SignalDefinitionForm with complete methodology chain validation
6. DiscoverySequenceTracker UI component with flexible navigation

### Phase 3: Integration & Validation
1. Enhanced CSV import/export with complete methodology data
2. Methodology chain validation status indicators throughout UI
3. Business consequence narrative generation from complete discovery data
4. Complete stakeholder → impact → telemetry → signal trace visualization

---

## 10. Success Criteria

- **Methodology Adherence:** 100% of Steps can follow complete 5-step stakeholder-first discovery sequence
- **Trace Completeness:** Steps can achieve full stakeholder → impact → telemetry → signal traceability
- **Measurability Compliance:** Impact analysis enforces measurable consequences with validation guidance
- **LLM Implementation:** All components can be built directly from PRD specifications with guided prompts
- **User Experience:** Product Owners can complete stakeholder discovery without technical expertise using guided workflows
- **Business Validation:** Test scenario validates methodology works with realistic enterprise complexity
- **Technical Implementation:** Developers receive specific instrumentation requirements linked to business stakeholder impacts

---

## 11. Validation & Quality Assurance

### Methodology Chain Validation
- Every stakeholder from Step 1 must be traceable through Steps 2-5
- Impact analysis must include only measurable consequences
- Telemetry requirements must map to observable system data
- Signal definitions must provide implementable technical specifications

### Implementation Completeness
- All discovery steps have complete form specifications with guided prompts
- Data schemas support full methodology data with consistent structures
- Validation rules enforce methodology compliance without blocking user progress
- UI patterns support both guided discovery and flexible data entry

### Business Scenario Testing
- Home lending test scenario validates all specifications work in practice
- Stakeholder relationship framework handles realistic enterprise complexity  
- Measurability principle eliminates non-observable impacts
- Complete methodology chain produces actionable technical requirements

**This PRD enables direct LLM implementation of a methodology-compliant business observability system prototype.**
