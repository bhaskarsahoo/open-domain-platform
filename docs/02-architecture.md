# Architecture

## 1. Architectural style

Open Domain Platform uses an ERP-centered, event-driven, modular architecture.

ERPNext/Frappe is the system of record. Domain modules and capability modules extend ERPNext through events, command APIs, workflows, and external services.

The architecture is intentionally designed so that AI, IoT, blockchain, and analytics can be added later without redesigning the core platform.

## 2. High-level architecture

```text
                    +---------------------------+
                    | Branded Web / Desk / UX   |
                    +-------------+-------------+
                                  |
                                  v
                    +---------------------------+
                    | ERPNext / Frappe Core     |
                    | System of Record          |
                    +-------------+-------------+
                                  |
                          DocType hooks
                                  |
                                  v
                    +---------------------------+
                    | Transactional Outbox      |
                    +-------------+-------------+
                                  |
                         Publisher Worker
                                  |
                                  v
+---------------------------------------------------------------+
| Event Bus                                                     |
| NATS / RabbitMQ / Redis Streams locally; Kafka later if needed |
+-------------+-------------------+-------------------+---------+
              |                   |                   |
              v                   v                   v
      +---------------+   +---------------+   +----------------+
      | AI Modules    |   | IoT Modules   |   | Analytics      |
      +-------+-------+   +-------+-------+   +--------+-------+
              |                   |                    |
              v                   v                    v
      +--------------------------------------------------------+
      | ERPNext Command/API Layer                              |
      | Validated Frappe methods and resource APIs              |
      +--------------------------------------------------------+
```

## 3. System responsibilities

### ERPNext/Frappe core

Owns official business state:

- Master data
- Orders
- Invoices
- POS transactions
- Stock ledger
- Purchase receipts
- Delivery notes
- Warehouses
- Accounting
- Roles and permissions
- Approval workflows

### Open Domain Platform core

Owns platform extension mechanisms:

- Event outbox
- Event envelope
- Command envelope
- Module manifest
- Domain model registry
- Workflow conventions
- Integration adapter conventions
- Local developer runtime

### Domain modules

Own industry-specific concepts and workflows:

- Smart farming
- Cement
- Manufacturing
- Retail
- Cold chain
- Logistics

### Capability modules

Own optional advanced capabilities:

- AI advisor and copilots
- IoT gateway
- Traceability and blockchain adapters
- Analytics pipelines
- Forecasting and optimization
- External connectors

## 4. Event-driven design

ERPNext emits business events through DocType hooks and custom workflow transitions.

Events are not published directly from inside critical ERP transactions. Instead, handlers write records into a transactional outbox.

```text
ERPNext transaction
   +-- update official business document
   +-- write outbox event

Publisher worker
   +-- reads pending outbox events
   +-- publishes to event bus
   +-- marks event as published
```

This reduces the chance of lost events and avoids doing heavy external work during ERPNext transactions.

## 5. Command design

External modules call ERPNext through controlled command APIs.

Commands are requests. ERPNext validates permissions, workflow rules, business rules, and document state before making changes.

Example command flow:

```text
DiseaseRiskDetected event
        |
        v
AI advisor module
        |
        v
CreateFarmAdvisory command
        |
        v
ERPNext validates and creates advisory
        |
        v
FarmAdvisoryCreated event
```

## 6. Local-first infrastructure

The local development environment should be able to run with:

- ERPNext/Frappe
- MariaDB
- Redis
- NATS or RabbitMQ
- PostgreSQL
- MinIO if object storage is needed
- FastAPI services
- Mock AI advisor
- IoT simulator
- Local traceability hash service

Avoid mandatory dependencies on:

- GPU infrastructure
- Blockchain nodes
- Kubernetes
- Kafka clusters
- Real IoT devices
- Public cloud services

## 7. Deployment evolution

### Stage 1: Developer machine

Use Docker Compose and lightweight services.

### Stage 2: Pilot deployment

Use a single VM or small managed database setup. Keep event broker lightweight.

### Stage 3: Production deployment

Move to managed databases, managed object storage, observability, backups, and optional Kubernetes.

### Stage 4: Scale deployment

Introduce Kafka, lakehouse, self-hosted AI inference, blockchain networks, or IoT fleet management only when required by real customer needs.

## 8. Module boundaries

Each module must clearly declare:

- What it owns
- What it depends on
- What events it consumes
- What events it emits
- What commands it calls
- What configuration it requires
- Whether it is required or optional

This avoids hidden coupling and keeps the architecture plug-and-play.

## 9. Data boundary rules

### Allowed

- ERPNext APIs
- Frappe whitelisted methods
- Controlled command endpoints
- Events
- Webhooks
- Background jobs
- Read replicas for analytics, when designed carefully

### Not allowed

- External services directly writing to ERPNext database tables
- External services bypassing stock/accounting validations
- Raw IoT telemetry stored directly in ERPNext operational tables
- Blockchain used as the ERP system of record
- AI agents making irreversible ERP changes without approval gates

## 10. Extension points

ERPNext/Frappe extension points:

- Custom apps
- Custom DocTypes
- Custom fields
- Hooks
- Workflows
- Server scripts
- Client scripts
- Whitelisted methods
- REST APIs
- Webhooks
- Background jobs
- Reports and dashboards

Open Domain Platform extension points:

- Event schemas
- Command schemas
- Module manifests
- Domain model definitions
- Capability adapters
- Workflow templates
- Analytics consumers
- AI tools
- IoT adapters
- Traceability adapters

## 11. Architecture risks

| Risk | Mitigation |
|---|---|
| ERPNext customization becomes a fork | Use custom apps and ADR approval for core edits |
| Events become inconsistent | Use transactional outbox and idempotent consumers |
| Modules become tightly coupled | Require module manifests and schema contracts |
| AI agents create bad transactions | Use command APIs, permissions, and approval gates |
| IoT data overwhelms ERPNext | Store raw telemetry outside ERPNext and emit only business events |
| Blockchain adds unnecessary cost | Start with local hash-chain traceability and add blockchain adapters later |
| Analytics hurts ERP performance | Use event streams, replicas, or external warehouses |
