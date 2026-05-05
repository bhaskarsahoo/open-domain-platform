# Open Domain Platform

Open Domain Platform is an open, event-driven platform for building modular industry solutions on ERPNext/Frappe, with plug-in support for workflows, AI, IoT, traceability, and analytics.

The goal is to create a reusable foundation that can support multiple domains such as smart farming, supply chain, cement, manufacturing, retail, cold chain, and other industry-specific business workflows without rebuilding the ERP core.

## Vision

Build a domain-extensible business operating platform where:

- ERPNext/Frappe acts as the business system of record.
- Domain modules add industry-specific workflows.
- Events connect ERP, AI, IoT, analytics, traceability, and external services.
- Advanced capabilities are plug-and-play rather than mandatory.
- The platform can run first on a developer machine before moving to production infrastructure.

## First reference domain

The first reference domain is **smart AI farming and farm-to-supply-chain traceability**.

This includes farms, plots, crops, farm activities, harvest batches, quality checks, inventory, warehouses, shipments, POS, analytics, optional IoT telemetry, optional AI advisory, and optional blockchain-style traceability.

## Future domains

The architecture should support additional domains, including:

- Cement industry workflows
- Manufacturing
- Retail distribution
- Cold chain logistics
- Food processing
- Construction materials
- Healthcare supply chain
- General B2B supply chain

## Core architecture

```text
ERPNext / Frappe Core
        |
        v
Open Domain Platform Core
        |
        +-- Event Outbox
        +-- Command API
        +-- Module Registry
        +-- Domain Model Registry
        +-- Workflow Extension Layer
        +-- Integration Adapters
        |
        v
Plug-in Modules
        |
        +-- Smart Farming
        +-- Supply Chain
        +-- AI Advisor
        +-- IoT Gateway
        +-- Traceability
        +-- Analytics
        +-- Industry-specific workflows
```

## Design principles

1. **Extend, do not fork ERPNext.**
2. **ERPNext remains the system of record.**
3. **Use events for side effects and integrations.**
4. **Use commands for controlled writes back to ERPNext.**
5. **Keep AI, IoT, blockchain, and analytics optional.**
6. **Run locally first; scale infrastructure later.**
7. **Separate reusable platform core from domain-specific workflows.**
8. **Design for open-source adoption and commercial support/customization.**

## Repository status

This repository is currently in the research, architecture, and planning phase. Implementation should begin only after the core design documents, domain model, and module contracts are stable enough to guide development.

## Documentation

Start here:

- [Platform Blueprint](docs/00-platform-blueprint.md)
- [Architecture](docs/02-architecture.md)
- [Module System](docs/05-module-system.md)
- [Implementation Roadmap](docs/11-implementation-roadmap.md)
- [ADR-0001: Platform Direction](decisions/ADR-0001-platform-direction.md)

## Development approach

Use ChatGPT for research, architecture, requirement refinement, and design review. Use Codex for implementation, scaffolding, tests, refactoring, and pull requests once the architecture is ready.
