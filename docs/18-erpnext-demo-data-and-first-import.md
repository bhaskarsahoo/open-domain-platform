# ERPNext Demo Data and First Import Plan

## 1. Purpose

This document explains how to approach ERPNext demo data during the discovery phase.

The goal is to quickly feel ERPNext/Frappe, understand the default UI/UX and workflows, and then create a controlled dataset that validates Open Domain Platform lifecycles.

## 2. Does ERPNext come with demo data?

ERPNext may have some demo or test data utilities depending on the version and setup method, but the project should not rely on built-in demo data for serious research.

Built-in demo data, if available, should be treated as a quick exploration aid only.

Reasons:

- Demo utilities may be version-dependent.
- Demo records may be incomplete.
- Demo data may not match our target domains.
- Demo data may not cover full ERP lifecycle flows.
- Demo data may not help validate event-driven module architecture.

## 3. What to do after spinning ERPNext

After starting ERPNext locally, first explore it manually.

Recommended quick-start:

```bash
git clone https://github.com/frappe/frappe_docker
cd frappe_docker
docker compose -f pwd.yml up -d
docker compose -f pwd.yml logs -f create-site
```

Open:

```text
http://localhost:8080
```

Login:

```text
Username: Administrator
Password: admin
```

## 4. Optional: check whether demo utilities exist

After the site is created, enter the backend container:

```bash
docker compose -f pwd.yml exec backend bash
```

List available sites:

```bash
ls sites
```

Depending on the setup, the site name may be something like `frontend` or another generated site name.

If ERPNext demo utilities are available in the installed version, try commands such as:

```bash
bench --site <site-name> execute erpnext.demo.demo.make
bench --site <site-name> execute erpnext.demo.demo.simulate
```

These commands may not work in every version or installation. If they fail, continue with manual exploration and controlled fixtures.

## 5. Manual exploration before import

Before importing data, manually create a small flow in the ERPNext UI.

Create or inspect:

- Company
- Customer
- Supplier
- Item
- Warehouse
- Project
- Task
- Material Request
- Purchase Order
- Purchase Receipt
- Stock Entry
- Sales Invoice
- Payment Entry

This gives the team a feel for:

- Required fields
- Naming patterns
- Status transitions
- Form behavior
- Child tables
- Link fields
- Validation rules
- Reports
- Permissions
- Default workflows

## 6. Why not import public datasets directly?

Most public datasets are not ERP-shaped.

They may not include:

- Valid customer masters
- Valid supplier masters
- Item codes
- Warehouses
- Company setup
- Chart of accounts mapping
- Tax templates
- Project hierarchy
- Document status lifecycle
- Links between procurement, inventory, billing, and finance

Therefore, importing a raw public dataset directly into ERPNext is likely to fail or create confusing records.

## 7. Recommended data flow

Use public datasets as inspiration, then create a normalized demo dataset.

```text
Public dataset
  -> normalized demo model
  -> ERPNext-compatible seed CSVs
  -> ERPNext import
  -> manual validation
  -> event replay later
```

## 8. First controlled dataset

The first controlled dataset should be small and ERP-shaped.

Recommended starting point:

```text
1 company
3 customers
3 suppliers
10 items
3 warehouses
2 projects
10 tasks
3 material requests
3 purchase orders
3 purchase receipts
3 stock entries
3 timesheets
3 sales invoices
3 payment entries
```

This is enough to test ERP basics without overwhelming the team.

## 9. Recommended first domain: construction ERP lifecycle

Construction is a good first import domain because it validates many ERP modules.

Suggested flow:

```text
Lead
  -> Opportunity
  -> Quotation / Estimate
  -> Sales Order / Contract
  -> Project
  -> Tasks / WBS
  -> Material Request
  -> Purchase Order
  -> Purchase Receipt
  -> Stock Entry to Site Warehouse
  -> Timesheet
  -> Sales Invoice / Progress Invoice
  -> Payment Entry
  -> Project profitability review
```

This tests:

- CRM
- Sales
- Projects
- Procurement
- Inventory
- HR/time through timesheets
- Billing
- Finance
- Reporting

## 10. Second domain: smart farming supply-chain flow

After construction, test smart farming and supply chain.

Suggested flow:

```text
Farmer / Supplier
  -> Crop / Item
  -> Collection Center / Warehouse
  -> Harvest Receipt / Purchase Receipt
  -> Batch
  -> Quality Inspection
  -> Stock Entry
  -> Delivery Note
  -> Sales Invoice or POS Invoice
  -> Traceability notes
```

This tests:

- Buying
- Stock
- Batch management
- Quality
- Warehouse movement
- Sales
- POS
- Traceability extension points

## 11. Files to create next

Create:

```text
datasets/demo-model.md
examples/demo-fixtures/construction/customers.csv
examples/demo-fixtures/construction/suppliers.csv
examples/demo-fixtures/construction/items.csv
examples/demo-fixtures/construction/warehouses.csv
examples/demo-fixtures/construction/projects.csv
examples/demo-fixtures/construction/tasks.csv
examples/demo-fixtures/construction/material_requests.csv
examples/demo-fixtures/construction/purchase_orders.csv
examples/demo-fixtures/construction/timesheets.csv
examples/demo-fixtures/construction/sales_invoices.csv
```

These should be small synthetic fixtures shaped for ERPNext import.

## 12. Discovery notes to capture

For every imported or manually created flow, capture:

- What ERPNext supports out of the box
- What requires configuration
- What requires custom fields
- What requires custom DocTypes
- What requires custom Frappe app logic
- What requires external service logic
- What requires custom UI/UX
- Which lifecycle events can be generated
- Which command APIs are needed
- Which reports already exist
- Which reports need to be built

## 13. Design rule

Do not build a custom module until the team has tested whether ERPNext already supports the lifecycle with configuration, custom fields, or standard workflows.

Prefer this order:

```text
ERPNext default behavior
  -> ERPNext configuration
  -> Custom fields
  -> Custom workflows
  -> Custom DocTypes
  -> Custom Frappe app logic
  -> External services
  -> Custom UI/UX
```

## 14. Outcome of this phase

The outcome should be a clear understanding of:

- ERPNext's default behavior
- ERPNext data model constraints
- Which modules are already strong
- Which modules need extensions
- Which data relationships matter
- Which events should be emitted
- Which commands should be exposed
- Which UI/UX areas need focus

This discovery should happen before serious implementation starts.
