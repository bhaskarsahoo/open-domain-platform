# Implementation Roadmap

## 1. Roadmap philosophy

The project should be built in stages. Each stage should produce a usable, locally runnable increment.

Do not start by implementing AI, blockchain, or real IoT infrastructure. Start by building the platform contracts and the event-driven extension foundation.

## 2. Phase 0: Research and architecture

### Goals

- Establish platform vision
- Define architecture principles
- Define licensing strategy
- Define module boundaries
- Define first reference domain
- Define local-first development strategy

### Deliverables

- Platform blueprint
- Architecture document
- Domain modeling guide
- Event-driven architecture guide
- Module system design
- Licensing strategy
- ADR-0001 platform direction

### Exit criteria

- The team can explain what is core vs domain-specific.
- The team agrees ERPNext/Frappe is the initial system of record.
- The team agrees AI, IoT, blockchain, and analytics are optional plug-ins.

## 3. Phase 1: Contracts and schemas

### Goals

Define the contracts before implementation.

### Deliverables

- Event envelope schema
- Command envelope schema
- Module manifest schema
- Example events
- Example commands
- Domain model templates

### Exit criteria

- Schemas can be validated locally.
- Example smart farming and supply-chain events are documented.
- Codex can generate initial validation code from the schemas.

## 4. Phase 2: ERPNext/Frappe event foundation

### Goals

Create the ERPNext/Frappe extension layer that emits events safely.

### Deliverables

- Frappe app skeleton: `open_domain_core`
- Outbox Event DocType
- Event publishing worker
- Basic DocType hook examples
- Local event broker integration
- Event publish retry handling

### Exit criteria

- Submitting a test document writes an outbox event.
- Publisher sends event to local broker.
- Failed publishes can retry.
- No ERPNext core fork is required.

## 5. Phase 3: Command API foundation

### Goals

Allow external modules to request controlled changes in ERPNext.

### Deliverables

- Command API convention
- Command validation
- Example commands
- Command result events
- Service account approach
- Approval-gate pattern for sensitive commands

### Exit criteria

- External service can call a command API.
- ERPNext validates and creates/updates a document.
- Command result is emitted as an event.

## 6. Phase 4: Smart farming reference domain

### Goals

Implement the first domain module.

### Deliverables

- Farm
- Plot
- Crop Plan
- Farm Activity
- Field Inspection
- Harvest Batch
- Farm Advisory
- Traceability Log
- Basic workflows
- Example reports

### Exit criteria

- A crop plan can move through activities to harvest batch.
- Harvest batch can connect to inventory and supply-chain flow.
- Smart farming module does not leak domain assumptions into platform core.

## 7. Phase 5: Local plug-in demos

### Goals

Prove plug-and-play architecture without expensive infrastructure.

### Deliverables

- Mock AI advisor
- IoT simulator
- Local traceability hash-chain service
- Analytics consumer
- Weather adapter mock or public-data adapter

### Exit criteria

- Mock IoT event can trigger a business event.
- Mock AI advisor can create a farm advisory through command API.
- Traceability service can attach a proof hash.
- Analytics consumer can consume platform events.

## 8. Phase 6: Developer runtime

### Goals

Make it easy for developers to run the platform locally.

### Deliverables

- Docker Compose setup
- Environment template
- Seed demo data
- Developer quickstart
- Test scripts
- Local observability notes

### Exit criteria

- New developer can run a demo locally.
- Demo does not require GPUs, blockchain nodes, real sensors, Kubernetes, or cloud services.

## 9. Phase 7: Second domain validation

### Goals

Prove the platform is not only for farming.

### Suggested second domain

Cement supply chain.

### Deliverables

- Cement domain model
- Cement events
- Cement commands
- Example workflow
- Gap analysis against core abstractions

### Exit criteria

- Cement domain can be modeled without changing the platform core significantly.
- Any required core changes are captured as ADRs.

## 10. Phase 8: Production-readiness planning

### Goals

Prepare for pilot customers.

### Deliverables

- Security model
- Tenant model
- Backup and restore plan
- Observability plan
- Upgrade strategy
- Deployment options
- Support model
- Licensing review

### Exit criteria

- A pilot customer deployment plan exists.
- Operational responsibilities are clear.
- Commercial and open-source boundaries are reviewed.

## 11. Initial backlog

### Documentation

- Complete smart farming domain model
- Complete cement domain model
- Add event catalog
- Add command catalog
- Add developer setup guide

### Schemas

- Event envelope schema
- Command envelope schema
- Module manifest schema
- Example event payloads
- Example command payloads

### Platform core

- Frappe app skeleton
- Outbox Event DocType
- Event publisher
- Command API base
- Module registry

### Reference services

- Mock AI advisor
- IoT simulator
- Traceability hash service
- Analytics consumer

### Dev tooling

- Docker Compose
- Schema validation script
- Test fixtures
- Demo data

## 12. What not to build first

Do not build these before the foundation is working:

- Real blockchain network
- Hyperledger Fabric production setup
- Self-hosted GPU inference
- Real device fleet management
- Kafka cluster
- Multi-tenant SaaS control plane
- Large-scale data lake
- Heavy custom ERPNext fork
