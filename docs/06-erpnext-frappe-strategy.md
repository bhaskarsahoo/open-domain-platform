# ERPNext / Frappe Strategy

## 1. Role of ERPNext/Frappe

ERPNext/Frappe is the initial system of record for Open Domain Platform.

It should provide the reusable business foundation instead of rebuilding ERP from scratch.

ERPNext/Frappe should own:

- Master data
- Customers
- Suppliers
- Items
- Warehouses
- Stock
- Buying
- Selling
- CRM
- POS
- Accounting
- Users and roles
- Approval workflows
- Core operational reports

## 2. What the platform adds

Open Domain Platform adds:

- Domain-specific workflows
- Event outbox
- Event publishing
- Command APIs
- Domain module registry
- Module manifest contract
- AI-ready interfaces
- IoT-ready interfaces
- Traceability-ready interfaces
- Analytics integration conventions

## 3. Extension strategy

Prefer ERPNext/Frappe extension points:

- Custom apps
- Custom DocTypes
- Custom fields
- Hooks
- Workflows
- Whitelisted methods
- Background jobs
- Webhooks
- Reports
- Dashboards

Avoid direct changes to ERPNext core.

## 4. What to avoid

Avoid:

- Forking ERPNext early
- Direct database writes to ERPNext tables from external services
- Replacing accounting logic
- Replacing stock ledger logic
- Storing raw IoT telemetry in ERPNext operational tables
- Making AI agents perform irreversible changes without approval

## 5. Recommended ERPNext app boundaries

Initial Frappe apps may include:

```text
open_domain_core
  Event outbox, command API, module registry, shared platform DocTypes

open_domain_smart_farming
  Farm, plot, crop plan, farm activities, harvest batch, farm advisory

open_domain_traceability
  Traceability log, local hash-chain proof, proof attachment APIs
```

These may later be split into separate repositories if licensing or deployment boundaries require it.

## 6. Upgrade-safety rule

Every customization should be designed so ERPNext upgrades remain manageable.

Use an ADR for any proposed ERPNext core modification.

## 7. Integration pattern

ERPNext emits events through hooks into an outbox.

External modules consume events and call ERPNext back through command APIs.

```text
ERPNext DocType change
        |
        v
Outbox Event
        |
        v
Event Bus
        |
        v
External Module
        |
        v
ERPNext Command API
```

## 8. Decision checkpoints

Before implementation, decide:

- Initial ERPNext version target
- Local installation method
- Frappe app naming convention
- Event broker choice
- Whether core Frappe apps live in this repo or separate repos
- License boundary for ERPNext-dependent app code
