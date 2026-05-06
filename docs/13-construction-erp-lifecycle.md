# Construction ERP Lifecycle Validation

## 1. Purpose

Construction is a strong ERP validation domain for Open Domain Platform because it stresses core ERP behavior without requiring MES.

The goal is to validate the platform around project lifecycle, procurement, inventory, subcontracting, billing, cost control, cash flow, quality, safety, and project profitability.

This domain should focus on ERP and project-business lifecycle first. MES, BIM, equipment telemetry, and advanced IoT can be optional future modules.

## 2. Why construction is useful for ERP validation

Construction companies need strong control over:

- Estimation
- Project budgeting
- Work breakdown structure
- Procurement
- Material requests
- Purchase orders
- Supplier bills
- Site inventory
- Subcontractor work
- Timesheets and labor costing
- Equipment usage
- Progress billing
- Retention
- Variation orders
- Quality and safety issues
- Project profitability
- Cash flow

These map naturally to ERPNext/Frappe concepts and platform event/command flows.

## 3. ERP-first lifecycle

```text
Lead / Opportunity
  -> Estimate / Quotation
  -> Contract / Sales Order
  -> Project Created
  -> Budget and WBS Created
  -> Material Plan
  -> Procurement Plan
  -> Material Request
  -> Purchase Order
  -> Purchase Receipt
  -> Site Stock Transfer
  -> Subcontractor Work Order or Supplier Invoice
  -> Timesheets / Labor Costing
  -> Progress Measurement
  -> Customer Billing
  -> Payment Collection
  -> Project Profitability Review
  -> Project Closure
```

## 4. Core construction entities

- Construction Project
- Site
- Work Breakdown Structure
- Activity or Task
- Bill of Quantities
- Estimate
- Project Budget
- Material Requirement
- Site Warehouse
- Subcontractor
- Subcontract Package
- Progress Measurement
- Variation Order
- Retention
- Quality Checklist
- Safety Issue
- Equipment Usage Log
- Project Cost Report

## 5. ERPNext mapping

| Construction concept | ERPNext/Frappe mapping |
|---|---|
| Lead / client inquiry | Lead / Opportunity |
| Estimate | Quotation or custom Estimate |
| Contract | Sales Order / Project |
| Work breakdown structure | Project + Task hierarchy |
| Project budget | Project budget / Cost Center / custom budget DocTypes |
| Bill of quantities | Item list / custom BOQ DocType |
| Material requirement | Material Request |
| Procurement | Purchase Order |
| Material receipt | Purchase Receipt |
| Site inventory | Warehouse / Stock Entry |
| Labor cost | Timesheet / Activity Cost |
| Subcontractor | Supplier + subcontract package extension |
| Progress billing | Sales Invoice / milestone billing extension |
| Variation order | Change Order custom DocType |
| Retention | Payment terms / custom retention logic |
| Quality issue | Issue / Quality Inspection / custom checklist |
| Safety issue | Issue / custom Safety Observation |
| Project P&L | Project Profitability / custom analytics |

## 6. Initial events

- `OpportunityQualified`
- `ConstructionEstimateCreated`
- `ProjectContractAwarded`
- `ConstructionProjectCreated`
- `ProjectBudgetApproved`
- `BOQImported`
- `MaterialRequestCreated`
- `PurchaseOrderIssued`
- `PurchaseReceiptSubmitted`
- `MaterialMovedToSite`
- `SubcontractPackageCreated`
- `SubcontractorInvoiceSubmitted`
- `TimesheetSubmitted`
- `ProgressMeasurementRecorded`
- `VariationOrderCreated`
- `ProgressInvoiceSubmitted`
- `PaymentReceived`
- `QualityIssueCreated`
- `SafetyIssueCreated`
- `ProjectClosed`

## 7. Initial commands

- `CreateConstructionProject`
- `CreateProjectBudget`
- `CreateBOQ`
- `CreateMaterialRequest`
- `CreatePurchaseOrderDraft`
- `RecordSiteStockTransfer`
- `CreateSubcontractPackage`
- `RecordProgressMeasurement`
- `CreateVariationOrder`
- `CreateProgressInvoiceDraft`
- `CreateQualityIssue`
- `CreateSafetyIssue`
- `CloseProject`

## 8. Public dataset options

Useful public datasets include:

- Construction project management schedule, cost, risk, labor, equipment, material, and constraints datasets.
- Construction resource datasets with labor, equipment, material quantities, project duration, and risk.
- Construction field app datasets with quality, safety, site forms, and task/snag data.
- Bid tabulation datasets for construction procurement and cost-estimation workflows.
- Public construction contract data, such as DoD construction project contract datasets.

These datasets can be used to generate demo estimates, project tasks, material requests, supplier bids, progress events, quality issues, safety issues, and profitability dashboards.

## 9. Suggested demo flow

```text
Opportunity Qualified
  -> Estimate Created
  -> Contract Awarded
  -> Project Created
  -> BOQ Imported
  -> Project Budget Approved
  -> Material Request Created
  -> Purchase Order Issued
  -> Purchase Receipt Submitted
  -> Material Moved to Site
  -> Timesheet Submitted
  -> Progress Measurement Recorded
  -> Progress Invoice Submitted
  -> Payment Received
  -> Project Profitability Reviewed
```

## 10. What to avoid initially

Do not start with:

- Full BIM integration
- MES-like construction site automation
- Equipment telemetry
- Drone progress monitoring
- Complex scheduling optimization
- Full subcontractor portal

These can become optional modules after the ERP lifecycle works.

## 11. MVP validation goal

The construction ERP validation should prove that Open Domain Platform can support a project-based industry lifecycle using ERPNext core modules plus domain extensions.

Success criteria:

- A project can be created from a contract.
- A BOQ or estimate can generate material requirements.
- Procurement can be linked to the project.
- Materials can move into a site warehouse.
- Labor costs can be captured through timesheets.
- Progress can trigger customer billing.
- Project profitability can be analyzed.
- Events can be generated throughout the lifecycle.
