# Platform Blueprint

## 1. Purpose

Open Domain Platform is an open, event-driven domain platform for building ERPNext/Frappe-based industry solutions.

The platform should allow a team to build industry-specific workflows without rebuilding ERP, CRM, POS, inventory, accounting, or basic supply-chain capabilities from scratch.

The first reference domain is smart AI farming and farm-to-supply-chain traceability. The architecture must also support other industries such as cement, manufacturing, retail, cold chain, and logistics.

## 2. Problem statement

Many industries need ERP-like systems with deep domain workflows. Rebuilding ERP, CRM, POS, inventory, procurement, accounting, and analytics for every domain is expensive and fragile.

At the same time, generic ERP platforms often do not provide enough flexibility for:

- Smart farming workflows
- IoT-driven operations
- AI advisory and copilots
- Traceability and provenance
- Domain-specific supply-chain optimization
- Industry-specific compliance
- Multi-party coordination
- Advanced analytics

The platform solves this by using ERPNext/Frappe as the system of record and adding a modular event-driven extension layer around it.

## 3. Product thesis

ERPNext/Frappe should own core business records and validated transactions.

Open Domain Platform should own:

- Domain modeling conventions
- Event and command contracts
- Plug-in module architecture
- Workflow extension conventions
- AI-ready interfaces
- IoT-ready interfaces
- Traceability interfaces
- Analytics integration patterns
- Reference domain implementations

## 4. Target users

### Platform users

- System integrators
- ERPNext/Frappe implementers
- Domain solution builders
- Startups building vertical SaaS products
- Enterprises needing domain-specific workflows

### Business users

- Farmers and farmer producer organizations
- Aggregators and cooperatives
- Warehouses and cold storage operators
- Manufacturers
- Cement distributors and plants
- Retail and POS operators
- Logistics teams
- Procurement teams
- Quality teams
- Supply-chain managers

## 5. Core platform layers

```text
ERPNext / Frappe
System of record for customers, suppliers, items, stock, orders, invoices, accounting, users, roles, and workflows
        |
        v
Open Domain Platform Core
Reusable extension layer: events, commands, module registry, domain model registry, workflow conventions, integration contracts
        |
        v
Domain Modules
Smart farming, cement, manufacturing, retail, cold chain, logistics, industry-specific workflows
        |
        v
Optional Capability Modules
AI advisor, IoT gateway, traceability, blockchain adapter, analytics, optimization, external connectors
```

## 6. Core principles

### 6.1 ERPNext remains the system of record

ERPNext/Frappe should be authoritative for:

- Accounting
- Stock ledger
- Item master
- Customer master
- Supplier master
- Sales orders
- Purchase orders
- POS invoices
- Delivery notes
- Purchase receipts
- Warehouse balances
- User permissions
- Workflow approvals

### 6.2 Extend, do not fork

The platform should avoid modifying ERPNext core. Custom behavior should be implemented through:

- Frappe apps
- Custom DocTypes
- Hooks
- Workflows
- Server-side command APIs
- Webhooks
- Background jobs
- External services

### 6.3 Events for side effects

ERPNext should emit business events such as `SalesOrderSubmitted`, `GoodsReceived`, `HarvestBatchCreated`, or `ShipmentDispatched`.

External modules consume events and react asynchronously.

### 6.4 Commands for controlled writes

External modules should not write directly to ERPNext tables. They should call controlled command APIs such as:

- `CreateFarmAdvisory`
- `CreateMaterialRequestDraft`
- `CreateQualityInspection`
- `PutBatchOnHold`
- `AttachTraceabilityProof`
- `UpdateShipmentStatus`

ERPNext validates commands before changing official business state.

### 6.5 Advanced capabilities are optional

The platform must work without:

- Real AI models
- GPUs
- Physical IoT devices
- Blockchain nodes
- Kafka clusters
- Kubernetes
- Data lake infrastructure

The first version should run locally with mocks, simulators, and lightweight services.

## 7. First reference domain: smart farming

The smart farming domain should include:

- Farm
- Farmer
- Plot or field
- Crop
- Crop season
- Crop plan
- Farm activity
- Field inspection
- Input application
- Irrigation activity
- Harvest batch
- Quality grade
- Warehouse movement
- Shipment
- Traceability log
- Farm advisory

## 8. Future domain example: cement

The same platform should support cement industry workflows such as:

- Plant
- Quarry
- Raw material batch
- Production batch
- Silo
- Dispatch order
- Dealer
- Retailer
- Truck movement
- Quality certificate
- Construction site delivery
- Batch traceability
- Dealer inventory
- Demand forecast

This validates that the core platform is domain-neutral.

## 9. Plug-in capability model

Each module declares:

- Events consumed
- Events emitted
- Commands called
- DocTypes owned
- Configuration required
- Permissions required
- External dependencies

Example:

```yaml
module: smart-farming-ai-advisor
version: 0.1.0
consumes:
  - FieldInspectionCompleted
  - WeatherForecastUpdated
  - SoilMoistureReadingReceived
emits:
  - FarmAdvisoryCreated
  - DiseaseRiskDetected
commands:
  - CreateFarmAdvisory
  - CreateFieldInspectionTask
optional_dependencies:
  - weather-adapter
  - iot-gateway
```

## 10. MVP definition

The MVP is not a full AI farming platform.

The MVP is a local, modular platform demonstration where:

1. ERPNext runs locally.
2. A domain core app adds smart farming DocTypes.
3. ERPNext events are written to an outbox.
4. Events are published to a local broker.
5. Mock AI, mock IoT, analytics, and traceability modules consume events.
6. External modules call command APIs back into ERPNext.
7. A farm-to-supply-chain traceability flow can be demonstrated end to end.

## 11. Success criteria

- Runs on a developer machine.
- Does not require ERPNext core edits.
- Supports at least one smart farming workflow.
- Supports an event outbox.
- Supports command APIs.
- Supports at least three mock plug-ins.
- Provides a documented module contract.
- Provides schema validation for events and commands.
- Provides a domain-neutral core that can later support cement or other industries.
