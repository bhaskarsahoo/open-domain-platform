# Frappe / ERPNext Discovery Plan

## 1. Purpose

Before building platform modules, the team should understand Frappe and ERPNext deeply enough to avoid unnecessary rework.

The discovery goal is to observe the default ERPNext UI, data model, workflows, permissions, module behavior, and database schema using realistic demo data.

## 2. Key questions

- What should remain in ERPNext core?
- What should be built as Frappe custom apps?
- What should be external services?
- Where does ERPNext already provide good UI/UX?
- Where do domain users need a custom UX?
- Which ERPNext DocTypes should be extended?
- Which domain entities should be new DocTypes?
- Which lifecycle events can be derived from existing DocType hooks?
- Which commands should be custom whitelisted Frappe methods?

## 3. Frappe concepts to study

### DocType

DocType is the core building block in Frappe. It describes the model and view of data. Creating a DocType creates a JSON definition and a database table.

Important details to inspect:

- Fields
- Naming rules
- Permissions
- Controllers
- Child tables
- Links
- Workflows
- Custom fields
- List view and form view

### Database convention

Frappe database tables are generally prefixed with `tab`.

Examples:

- `tabCustomer`
- `tabSupplier`
- `tabItem`
- `tabSales Order`
- `tabPurchase Order`
- `tabProject`

### ERPNext modules

Study at least:

- Accounting
- Selling
- Buying
- Stock
- CRM
- POS
- Projects
- Assets
- Quality
- Manufacturing
- Support
- HR, if enabled

## 4. Local spin-up goal

The first spin-up is not production.

The goal is to feel the default ERPNext product:

- Navigation
- Setup wizard
- Company setup
- Item master
- Customer and supplier flows
- Sales order to invoice
- Purchase order to receipt
- Stock movement
- Project and timesheet flows
- POS flow
- Reports
- Custom fields
- Workflow customization

## 5. Recommended local setup

Use Docker first for exploration.

A simple ERPNext Docker image can be started using the ERPNext repository `pwd.yml` example. The repository notes that after running Docker Compose and waiting for site creation, ERPNext can be opened on port `8080` with username `Administrator` and password `admin`.

For deeper development, use the official Frappe Docker/devcontainer approach or bench-based local setup.

## 6. Discovery dataset approach

Use one domain dataset first to explore default behavior.

Recommended first exploration dataset:

- Construction ERP lifecycle synthetic dataset

Why construction first:

- Tests CRM
- Tests projects
- Tests buying
- Tests stock
- Tests timesheets
- Tests billing
- Tests finance
- Tests reports

Recommended second exploration dataset:

- Smart farming harvest-to-supply-chain dataset

Why farming second:

- Tests custom domain entities
- Tests batch traceability
- Tests supply chain
- Tests advisory workflow
- Tests future AI/IoT hooks

## 7. Discovery tasks

### Task 1: Install and open ERPNext

- Start ERPNext locally.
- Complete setup wizard.
- Create a sample company.
- Explore default modules.

### Task 2: Explore core masters

Create or inspect:

- Company
- Customer
- Supplier
- Item
- Warehouse
- Employee
- Project
- Task
- Asset

### Task 3: Execute default ERP flows

Run these manually:

- Lead to opportunity
- Quotation to sales order
- Sales order to delivery note
- Sales invoice to payment
- Material request to purchase order
- Purchase receipt to purchase invoice
- Stock entry between warehouses
- Project to task to timesheet
- Timesheet to billing, if applicable
- POS invoice flow

### Task 4: Inspect database schema

For each key DocType, inspect:

- Table name
- Fields
- Child tables
- Link fields
- Status fields
- Workflow fields
- Posting fields
- Naming pattern

### Task 5: Map lifecycle events

For each default flow, identify event candidates.

Examples:

- `SalesOrderSubmitted`
- `PurchaseOrderSubmitted`
- `PurchaseReceiptSubmitted`
- `StockEntrySubmitted`
- `ProjectCreated`
- `TaskCompleted`
- `TimesheetSubmitted`
- `SalesInvoiceSubmitted`
- `PaymentEntrySubmitted`

### Task 6: Identify customization points

For each domain lifecycle, decide:

- Use ERPNext as-is
- Add custom field
- Add custom DocType
- Add workflow
- Add report
- Add external service
- Add custom UI
- Add command API
- Add event handler

## 8. Evaluation checklist

For every module reviewed, capture:

- Existing ERPNext behavior
- Data model observations
- UI/UX observations
- Reports available
- Integration points
- Events that can be emitted
- Commands that might be needed
- Gaps for our platform
- Gaps for specific domains

## 9. Output artifacts

Create these after discovery:

```text
docs/frappe-discovery/
  accounting.md
  selling.md
  buying.md
  stock.md
  crm.md
  projects.md
  pos.md
  quality.md
  hr.md
  customization.md
  database-schema-notes.md
```

## 10. SAP/ERP expert feedback

When the SAP/ERP expert reviews, ask for feedback on:

- Missing ERP capabilities
- Incorrect module boundaries
- Weak lifecycle assumptions
- Finance and controlling gaps
- Procurement and inventory gaps
- Project costing gaps
- HR and operations gaps
- Reporting expectations
- Enterprise approval expectations
- Master data governance

## 11. Design rule

Do not implement a custom module until the team has observed whether ERPNext already supports the lifecycle well enough.

Prefer:

1. ERPNext default behavior
2. ERPNext configuration
3. Custom fields and workflows
4. Custom DocTypes
5. Custom Frappe app logic
6. External service
7. Custom UI

Use the later options only when the earlier options are insufficient.
