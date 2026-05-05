# AGENTS.md

This repository is in the architecture-first phase. Agents and automated coding tools should prioritize design stability, modularity, and minimal coupling to ERPNext core.

## Primary goal

Build an open, event-driven domain platform on ERPNext/Frappe that can support multiple industries through plug-in domain modules.

The first reference domain is smart farming and supply chain, but the core must remain reusable for other domains such as cement, manufacturing, retail, logistics, and cold chain.

## Non-negotiable architecture rules

1. Do not fork ERPNext unless explicitly approved by an ADR.
2. Do not write directly to ERPNext database tables from external services.
3. External modules must call ERPNext through approved command APIs or Frappe APIs.
4. ERPNext document lifecycle hooks should write events to an outbox, not perform heavy side effects inline.
5. AI, IoT, blockchain, and analytics are optional plug-ins, not mandatory dependencies.
6. All domain modules must declare the events they consume, events they emit, commands they call, DocTypes they own, and configuration they require.
7. The local developer setup must work without GPUs, blockchain nodes, physical IoT devices, Kafka clusters, or Kubernetes.

## Preferred local stack

- ERPNext/Frappe
- MariaDB
- Redis
- NATS or RabbitMQ
- PostgreSQL for platform services and analytics experiments
- MinIO or local object storage where needed
- FastAPI for external services
- JSON Schema for events and commands
- Docker Compose for local orchestration

## Implementation style

- Start with documentation, schemas, and contracts before writing runtime code.
- Keep the platform core domain-neutral.
- Put smart farming under a separate domain module.
- Avoid hidden coupling between smart farming and the core platform.
- Prefer small, testable services and explicit interfaces.
- Add tests for event schemas, command schemas, and module manifests.

## Suggested first implementation milestones

1. Create the Frappe app skeleton for the event outbox and command API.
2. Add JSON Schema validation for event and command envelopes.
3. Add a local event broker and publisher worker.
4. Add a smart farming reference domain module.
5. Add a mock AI advisor, mock IoT simulator, analytics consumer, and local traceability hash service.

## Coding constraints

- Use clear names and simple abstractions.
- Do not introduce infrastructure that cannot run locally unless isolated behind an optional adapter.
- Do not implement blockchain before the local hash-chain traceability adapter exists.
- Do not implement self-hosted LLM inference before the AI service interface exists.
- Do not implement real device integrations before the IoT simulator exists.

## Pull request expectations

Every PR should explain:

- What layer it changes: core, domain module, service, schema, documentation, or deployment.
- Whether it introduces coupling to ERPNext, AI, IoT, blockchain, or analytics.
- Whether it affects the event or command contract.
- How it can be tested locally.
