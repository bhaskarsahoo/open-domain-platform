# Local ERPNext Quickstart

## 1. Purpose

This quickstart is for exploring ERPNext/Frappe before building Open Domain Platform modules.

The goal is not production deployment. The goal is to understand default ERPNext behavior, UI/UX, modules, workflows, DocTypes, and database structure.

## 2. Quick test using Frappe Docker

Use the official Frappe Docker quick-test approach.

```bash
git clone https://github.com/frappe/frappe_docker
cd frappe_docker
docker compose -f pwd.yml up -d
```

Monitor setup:

```bash
docker compose -f pwd.yml logs -f create-site
```

When setup finishes, open:

```text
http://localhost:8080
```

Login:

```text
Username: Administrator
Password: admin
```

Cleanup when finished:

```bash
docker compose -f pwd.yml down -v
```

## 3. What to explore first

### Setup

- Complete setup wizard
- Create company
- Set currency
- Set fiscal year
- Explore workspace navigation

### Master data

- Company
- Customer
- Supplier
- Item
- Warehouse
- Employee
- Project
- Task
- Asset

### Core ERP flows

Run these manually:

- Lead to Opportunity
- Quotation to Sales Order
- Sales Order to Delivery Note
- Sales Invoice to Payment Entry
- Material Request to Purchase Order
- Purchase Order to Purchase Receipt
- Purchase Receipt to Purchase Invoice
- Stock Entry between warehouses
- Project to Task to Timesheet
- POS Invoice flow

## 4. Construction-first exploration path

Construction is the best first ERP validation domain because it stresses CRM, project, procurement, stock, HR/time, billing, and finance.

Suggested manual flow:

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

## 5. Smart farming second exploration path

After construction, test farming and supply-chain behavior:

```text
Supplier / Farmer
  -> Item / Crop
  -> Warehouse / Collection Center
  -> Purchase Receipt / Harvest Receipt
  -> Batch
  -> Quality Inspection
  -> Stock Entry
  -> Delivery Note
  -> Sales Invoice or POS Invoice
  -> Traceability notes
```

## 6. Discovery notes to capture

For each module, capture:

- What ERPNext already supports well
- What requires configuration only
- What requires custom fields
- What requires custom DocTypes
- What requires custom app logic
- What requires an external service
- What needs a custom UI/UX
- Which lifecycle events can be generated
- Which command APIs are needed

## 7. Recommended discovery artifacts

Create notes under:

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

## 8. Development setup later

For actual app development, use a Frappe development setup rather than only the quick-test container.

Options:

- Frappe Docker devcontainer
- Bench-based local development
- Remote development VM

Choose this after the discovery phase.
