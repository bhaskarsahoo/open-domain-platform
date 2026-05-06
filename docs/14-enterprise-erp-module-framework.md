# Enterprise ERP Module Framework

## 1. Purpose

Open Domain Platform should not be designed as a collection of isolated industry demos. It should be aligned with the capability landscape of enterprise ERP systems, then validated through complete industry lifecycles.

The research goal is to understand what a serious enterprise ERP suite supports, map those capabilities to ERPNext/Frappe and platform modules, and then validate selected domains end to end.

## 2. Principle

Do not target every industry separately.

Instead:

1. Define reusable ERP capability modules.
2. Define cross-module workflows.
3. Define domain lifecycle blueprints.
4. Validate each lifecycle using public or synthetic datasets.
5. Implement domain extensions only where generic ERP modules are insufficient.

## 3. Enterprise ERP capability map

The platform should be evaluated against these ERP capability areas:

- Finance
- Controlling and management accounting
- Sales and order management
- CRM
- Procurement and sourcing
- Inventory and warehouse management
- Manufacturing and production planning
- Project management and project costing
- Asset management and maintenance
- Quality management
- Human resources and workforce/time management
- Payroll or payroll integration
- Expense management
- Services management
- Business operations and internal operations
- IT operations and service management
- Supply chain planning and execution
- Transportation and logistics
- Compliance, risk, and audit
- Analytics and reporting
- Master data management
- Workflow and approvals
- Integration and eventing

## 4. Mapping to Open Domain Platform

| Enterprise ERP capability | Open Domain Platform treatment |
|---|---|
| Finance | ERPNext core first |
| Controlling / costing | ERPNext core plus domain costing extensions |
| Sales | ERPNext core plus domain order extensions |
| CRM | ERPNext core first |
| Procurement | ERPNext core plus domain procurement workflows |
| Inventory | ERPNext stock and warehouse core |
| Warehouse management | ERPNext warehouse core plus optional advanced warehouse module |
| Manufacturing | ERPNext manufacturing where applicable; MES integration optional |
| Project management | ERPNext Projects plus domain project lifecycle extensions |
| Asset management | ERPNext assets/maintenance plus optional IoT maintenance events |
| Quality management | ERPNext quality plus domain checklists and certificates |
| HR / workforce | ERPNext HR where available, explicit workforce lifecycle, and integrations where needed |
| Payroll | ERPNext payroll where applicable or external payroll integration |
| Expense management | ERPNext expense claim / purchase workflows plus policy extensions |
| Services | ERPNext Projects/Support plus domain service workflows |
| Business operations | Workflow, approvals, internal requests, assets, procurement, service desk |
| IT operations | Support/issues, asset assignment, subscriptions, vendor management, service requests |
| Supply chain | ERPNext stock/buying/selling plus event-driven supply-chain module |
| Transportation | Optional logistics module; ERPNext delivery/shipment references |
| Compliance | Domain-specific compliance module |
| Analytics | ERPNext reports plus external analytics consumers |
| Master data | ERPNext masters plus domain-specific masters |
| Workflow | Frappe workflows plus event-driven orchestration |
| Integration | Event bus, command APIs, adapters |

## 5. Lifecycle-first research method

For each domain, research the full business lifecycle.

A lifecycle should include:

- Actors
- Master data
- Transaction flow
- Approval flow
- Inventory movement
- Financial impact
- Workforce and HR impact
- Operations impact
- Quality or compliance checkpoints
- Analytics and reporting
- Domain events
- Commands
- Interactions with other modules
- Dataset requirements
- Gaps in ERPNext core

## 6. Workflow template

Every major workflow should be documented using this structure:

```markdown
# Workflow: <Name>

## Purpose

## Actors

## Preconditions

## Steps

## ERPNext modules used

## Domain extensions required

## Events emitted

## Commands called

## Cross-module interactions

## Financial impact

## Inventory impact

## Workforce / HR impact

## Operations impact

## Quality/compliance impact

## Analytics outputs

## Dataset fields needed

## Open questions
```

## 7. Cross-module interaction model

Domain workflows should show how modules interact.

Example: construction project procurement

```text
Project Budget Approved
  -> Material Request Created
  -> Purchase Order Issued
  -> Purchase Receipt Submitted
  -> Stock Entry to Site Warehouse
  -> Supplier Invoice Submitted
  -> Project Cost Updated
  -> Project Profitability Updated
```

Modules involved:

- Project management
- Procurement
- Inventory
- Accounts payable
- Costing
- Analytics

Events:

- `ProjectBudgetApproved`
- `MaterialRequestCreated`
- `PurchaseOrderIssued`
- `PurchaseReceiptSubmitted`
- `MaterialMovedToSite`
- `SupplierInvoiceSubmitted`
- `ProjectCostUpdated`

## 8. Example domain lifecycle: smart farming

```text
Farm Onboarded
  -> Plot Registered
  -> Crop Plan Created
  -> Input Plan Created
  -> Material Request Created
  -> Purchase Order Issued
  -> Farm Activity Logged
  -> Field Inspection Completed
  -> Harvest Batch Created
  -> Quality Inspection Completed
  -> Warehouse Receipt Submitted
  -> Shipment Dispatched
  -> Sales Invoice or POS Invoice Submitted
  -> Traceability View Generated
```

Modules involved:

- Master data
- Procurement
- Inventory
- Quality
- Sales
- POS
- Supply chain
- Analytics
- AI advisory optional
- IoT optional
- Traceability optional

## 9. Example domain lifecycle: construction

```text
Lead Qualified
  -> Estimate Created
  -> Contract Awarded
  -> Project Created
  -> WBS Created
  -> BOQ Imported
  -> Budget Approved
  -> Material Request Created
  -> Purchase Order Issued
  -> Purchase Receipt Submitted
  -> Site Stock Transfer
  -> Timesheet Submitted
  -> Subcontractor Invoice Submitted
  -> Progress Measurement Recorded
  -> Progress Invoice Submitted
  -> Payment Received
  -> Project Profitability Reviewed
  -> Project Closed
```

Modules involved:

- CRM
- Sales
- Project management
- Procurement
- Inventory
- Accounts payable
- Accounts receivable
- HR / workforce and timesheets
- Quality
- Operations
- Analytics

## 10. Example domain lifecycle: cement distribution and production-lite

```text
Dealer Demand Received
  -> Production or Stock Plan Created
  -> Raw Material Requirement Created
  -> Quality Test Completed
  -> Cement Batch Created
  -> Silo Stock Updated
  -> Dispatch Order Created
  -> Truck Loaded
  -> Delivery Note Submitted
  -> Dealer Invoice Submitted
  -> Payment Received
  -> Dealer Stock Updated
```

Modules involved:

- Sales
- Forecasting
- Procurement
- Inventory
- Manufacturing or production-lite
- Quality
- Logistics
- Finance
- Analytics

## 11. Example domain lifecycle: software and services

```text
Lead Created
  -> Opportunity Qualified
  -> Proposal Submitted
  -> Contract Won
  -> Project Created
  -> Resource Plan Created
  -> Employees Assigned
  -> Sprint or Milestone Planned
  -> Timesheets Submitted
  -> Milestone Completed
  -> Customer Invoice Submitted
  -> Payment Received
  -> Support Period Started
  -> Support Tickets Resolved
  -> Project Profitability Reviewed
  -> Contract Renewed or Closed
```

Modules involved:

- CRM
- Sales
- Project management
- HR / workforce
- Timesheets
- Services / support
- Expense management
- Assets and subscriptions
- Accounts receivable
- Analytics

See `docs/15-hr-operations-software-industry.md` for the detailed HR, operations, and software/services lifecycle.

## 12. Dataset research requirements

For each domain dataset, capture:

- Which lifecycle steps it supports
- Which ERP modules it validates
- Which events can be generated
- Which commands can be tested
- Which analytics can be produced
- Which missing fields require synthetic augmentation
- License and commercial-use status

## 13. Domain selection criteria

A domain is useful for validation when it stresses multiple ERP modules.

Good validation domains:

- Smart farming and supply chain
- Construction project lifecycle
- Cement production/distribution
- Software and services operations
- Retail and distribution
- Manufacturing-lite
- Cold chain logistics

Avoid validating only narrow ML datasets that do not test ERP flows.

## 14. Build strategy

The platform should not build all industry solutions fully.

Instead, for each selected domain:

1. Capture the lifecycle.
2. Map lifecycle to ERP modules.
3. Define events and commands.
4. Identify domain extensions.
5. Identify public datasets.
6. Create small demo fixtures.
7. Generate event replay.
8. Validate dashboards and workflows.

Only then should implementation begin.

## 15. Success criteria

The research is successful when we can answer these questions for a domain:

- Can ERPNext cover most of the lifecycle?
- Which gaps require platform or domain extensions?
- Which events represent the lifecycle?
- Which commands are needed for controlled writes?
- Which public datasets can create realistic demos?
- Which analytics prove business value?
- Which optional AI, IoT, and traceability capabilities can plug in later?
