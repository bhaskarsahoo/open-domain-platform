# HR, Operations, and Software Industry ERP Lifecycle

## 1. Purpose

HR and operations should be treated as first-class enterprise ERP capabilities.

Some HR and operations workflows are partially covered through Projects, Timesheets, Assets, Support, Workflow, and Finance, but a serious enterprise lifecycle needs explicit modeling for people, capacity, utilization, approvals, payroll integration, service operations, internal operations, and delivery governance.

This document focuses especially on software and services companies, where the core lifecycle is people-heavy rather than inventory-heavy.

## 2. Why this matters

A software or services company usually needs ERP coverage for:

- Lead to project or contract
- Resource planning
- Employee onboarding
- Project staffing
- Timesheets
- Utilization
- Delivery milestones
- Customer billing
- Expenses
- Payroll or payroll integration
- Asset allocation
- Support operations
- Internal approvals
- Revenue recognition
- Project profitability
- Customer success

This is different from farming, construction, cement, or retail, but it still validates the platform strongly.

## 3. Capability areas

### HR and workforce

- Employee master
- Department
- Role / designation
- Skills
- Joining and onboarding
- Leave
- Attendance
- Timesheets
- Payroll or payroll integration
- Expenses
- Performance review
- Training
- Offboarding

### Software delivery operations

- Lead
- Opportunity
- Proposal
- Contract
- Project
- Sprint or delivery cycle
- Task
- Timesheet
- Milestone
- Change request
- Bug or issue
- Release
- Support ticket
- SLA
- Customer success review

### Internal operations

- Asset assignment
- Software subscriptions
- Purchase requests
- Vendor bills
- Approvals
- Policy compliance
- Internal helpdesk
- Facilities requests
- IT service requests

## 4. ERPNext mapping

| Capability | ERPNext/Frappe mapping |
|---|---|
| Employee | Employee / HR module if enabled |
| Department | Department |
| Leave | Leave Application / HR module |
| Attendance | Attendance / HR module |
| Timesheet | Timesheet |
| Payroll | Payroll module or external payroll integration |
| Lead and opportunity | CRM Lead / Opportunity |
| Proposal | Quotation |
| Contract | Sales Order / Contract extension |
| Project | Project |
| Task | Task |
| Milestone | Project milestone or custom DocType |
| Support | Issue / Support Ticket |
| Customer billing | Sales Invoice |
| Expense | Expense Claim / Purchase Invoice |
| Asset assignment | Asset / custom assignment workflow |
| Vendor procurement | Material Request / Purchase Order / Purchase Invoice |
| Internal approvals | Frappe Workflow |
| Profitability | Project costing / analytics extension |

## 5. Software company lifecycle

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
  -> Delivery Milestone Completed
  -> Customer Invoice Submitted
  -> Payment Received
  -> Support Period Started
  -> Support Tickets Resolved
  -> Project Profitability Reviewed
  -> Contract Renewed or Closed
```

## 6. HR lifecycle

```text
Hiring Request Created
  -> Candidate Selected
  -> Employee Created
  -> Onboarding Started
  -> Asset Assigned
  -> Project Assigned
  -> Timesheet Submitted
  -> Leave Requested
  -> Expense Claim Submitted
  -> Payroll Processed or Exported
  -> Performance Review Completed
  -> Offboarding Completed
```

## 7. Operations lifecycle

```text
Internal Request Created
  -> Approval Requested
  -> Purchase Request Created
  -> Purchase Order Issued
  -> Asset or Service Received
  -> Asset Assigned or Service Activated
  -> Vendor Invoice Submitted
  -> Payment Made
  -> Renewal or Disposal Scheduled
```

## 8. Domain events

### HR events

- `HiringRequestCreated`
- `EmployeeCreated`
- `EmployeeOnboardingStarted`
- `EmployeeOnboardingCompleted`
- `EmployeeAssignedToProject`
- `LeaveApplicationSubmitted`
- `LeaveApplicationApproved`
- `TimesheetSubmitted`
- `ExpenseClaimSubmitted`
- `PayrollProcessed`
- `PerformanceReviewCompleted`
- `EmployeeOffboardingStarted`
- `EmployeeOffboardingCompleted`

### Software delivery events

- `LeadCreated`
- `OpportunityQualified`
- `ProposalSubmitted`
- `ContractWon`
- `SoftwareProjectCreated`
- `ResourcePlanCreated`
- `SprintPlanned`
- `TaskCompleted`
- `MilestoneCompleted`
- `ChangeRequestCreated`
- `ReleasePublished`
- `SupportTicketCreated`
- `SupportTicketResolved`
- `CustomerInvoiceSubmitted`
- `PaymentReceived`
- `ProjectProfitabilityReviewed`

### Operations events

- `InternalRequestCreated`
- `ApprovalRequested`
- `ApprovalCompleted`
- `PurchaseRequestCreated`
- `PurchaseOrderIssued`
- `AssetReceived`
- `AssetAssigned`
- `VendorInvoiceSubmitted`
- `SubscriptionRenewalDue`
- `AssetRetired`

## 9. Commands

### HR commands

- `CreateHiringRequest`
- `CreateEmployee`
- `StartEmployeeOnboarding`
- `AssignEmployeeToProject`
- `ApproveLeaveApplication`
- `SubmitTimesheet`
- `CreateExpenseClaim`
- `ExportPayrollBatch`
- `StartEmployeeOffboarding`

### Software delivery commands

- `CreateProjectFromContract`
- `CreateResourcePlan`
- `AssignProjectTeam`
- `CreateSprint`
- `CreateMilestone`
- `CreateChangeRequest`
- `CreateCustomerInvoiceDraft`
- `CreateSupportTicket`
- `CloseProject`

### Operations commands

- `CreateInternalRequest`
- `RequestApproval`
- `CreatePurchaseRequest`
- `CreatePurchaseOrderDraft`
- `AssignAsset`
- `CreateVendorInvoiceDraft`
- `ScheduleSubscriptionRenewal`

## 10. Cross-module interactions

### Timesheet to billing

```text
TimesheetSubmitted
  -> ProjectCostUpdated
  -> BillingMilestoneEvaluated
  -> CustomerInvoiceDraftCreated
```

Modules involved:

- HR / workforce
- Project management
- Sales / invoicing
- Finance
- Analytics

### Employee onboarding to asset assignment

```text
EmployeeCreated
  -> EmployeeOnboardingStarted
  -> AssetAssignmentRequested
  -> AssetAssigned
  -> EmployeeOnboardingCompleted
```

Modules involved:

- HR
- Assets
- Procurement
- Operations
- Workflow

### Contract to delivery project

```text
ContractWon
  -> ProjectCreated
  -> ResourcePlanCreated
  -> EmployeesAssigned
  -> MilestonePlanCreated
```

Modules involved:

- CRM
- Sales
- Projects
- HR
- Finance

## 11. Analytics

Useful analytics include:

- Employee utilization
- Billable vs non-billable hours
- Project profitability
- Delivery milestone health
- Revenue by project
- Support SLA performance
- Hiring pipeline
- Attrition risk
- Leave balance
- Expense trends
- Asset allocation
- Subscription renewal exposure

## 12. Dataset opportunities

Potential public datasets:

- Software project management datasets with issues, commits, tasks, or sprints
- Public GitHub issue and pull request data for software delivery workflows
- Public IT service management or helpdesk datasets
- Public HR analytics datasets for attrition, attendance, or performance experiments
- Synthetic timesheet and project billing datasets generated from open issue/task datasets

The first implementation should use small synthetic fixtures derived from public structures rather than importing sensitive HR-like data.

## 13. MVP validation flow

The initial software/services ERP validation should prove:

1. A contract can create a project.
2. A resource plan can assign employees.
3. Timesheets can update project cost.
4. Milestones can trigger billing.
5. Support tickets can link to customer/project.
6. Expenses and assets can be linked to employees and projects.
7. Project profitability can be calculated.

## 14. Design rule

HR and operations should be explicit ERP capabilities, not hidden inside project management.

However, detailed payroll, benefits, statutory compliance, and country-specific HR rules should initially be treated as either ERPNext HR capabilities or external integrations, not custom platform core.
