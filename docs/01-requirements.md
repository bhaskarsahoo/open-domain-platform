# Requirements

## 1. Objective

Build an open, event-driven domain platform on ERPNext/Frappe that supports modular industry solutions.

The first reference domain is smart farming and farm-to-supply-chain traceability. The same architecture should later support domains such as cement, manufacturing, retail, cold chain, and logistics.

## 2. Core requirements

The platform should provide:

- ERPNext/Frappe as the system of record
- Domain module support
- Event-driven integration
- Transactional outbox design
- Command API design
- Module manifest design
- Event and command schema validation
- Local developer runtime
- Smart farming reference domain
- Supply-chain reference workflows
- Optional AI, IoT, traceability, blockchain, and analytics modules

## 3. ERP foundation

ERPNext/Frappe should own official business records such as:

- Customers
- Suppliers
- Items
- Warehouses
- Stock
- Buying
- Selling
- CRM
- POS
- Invoices
- Accounting
- Users and roles
- Approval workflows

## 4. Domain module requirements

A domain module should define:

- Domain entities
- Workflows
- Events
- Commands
- Reports
- Configuration
- Permissions
- Integration points

## 5. Smart farming reference requirements

The smart farming domain should cover:

- Farm registration
- Farmer management
- Plot management
- Crop planning
- Farm activities
- Field inspections
- Input application
- Irrigation logs
- Harvest batch creation
- Quality inspection
- Storage and shipment
- Farm-to-customer traceability
- Farm advisory workflow

## 6. Supply-chain requirements

The platform should support:

- Batch creation
- Batch movement
- Warehouse receipt
- Quality checkpoints
- Shipment
- Custody transfer
- Delivery
- POS sale
- Traceability lookup

## 7. Local-first requirement

The first working version should run on a developer machine without requiring:

- GPU infrastructure
- Blockchain nodes
- Real IoT devices
- Kubernetes
- Kafka cluster
- Large-scale data lake

## 8. Initial MVP

The MVP should demonstrate:

1. ERPNext/Frappe running locally.
2. Core platform schemas.
3. Event envelope and command envelope validation.
4. Smart farming reference domain model.
5. Transactional outbox design.
6. Event publisher design or prototype.
7. Mock AI advisor.
8. Mock IoT simulator.
9. Local traceability hash service.
10. Basic farm-to-supply-chain workflow.

## 9. Open questions

- Which repository-level license should be adopted first?
- Should ERPNext-dependent apps live in this repository or separate repositories?
- Which event broker should be used first: NATS, RabbitMQ, or Redis Streams?
- How much ERPNext customization should be DocType-based versus external-service based?
