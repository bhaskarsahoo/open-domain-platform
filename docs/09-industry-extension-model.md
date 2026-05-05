# Industry Extension Model

## 1. Purpose

The platform should support many industries without turning the core into a collection of hard-coded verticals.

An industry extension is a domain module or set of modules that adds industry-specific entities, workflows, events, commands, reports, and integrations.

## 2. Industry extension structure

```text
domains/<industry>/
  README.md
  domain-model.md
  module.yaml
  events.md
  commands.md
  workflows.md
  analytics.md
  integrations.md
```

## 3. Core rule

The platform core must remain industry-neutral.

Only add something to the core when at least two domains need it or when it represents a reusable platform capability.

## 4. Example: smart farming

Smart farming adds:

- Farm
- Farmer
- Plot
- Crop Plan
- Farm Activity
- Harvest Batch
- Field Inspection
- Farm Advisory

It uses reusable platform concepts:

- Events
- Commands
- Module manifest
- Traceability
- Analytics
- IoT adapter interface
- AI advisor interface

## 5. Example: cement

Cement may add:

- Plant
- Quarry
- Raw Material Batch
- Clinker Batch
- Cement Batch
- Silo
- Packing Line
- Dispatch Order
- Dealer Inventory
- Quality Certificate

It also uses reusable platform concepts:

- Batch traceability
- Quality checkpoints
- Shipment events
- Dispatch workflows
- Analytics
- IoT adapter interface
- AI forecast interface

## 6. Extension process

For every new industry:

1. Create domain model.
2. Map domain entities to ERPNext concepts.
3. Identify gaps requiring custom DocTypes.
4. Define workflows.
5. Define events.
6. Define commands.
7. Define reports.
8. Define optional AI, IoT, traceability, and analytics integrations.
9. Validate the module does not require changes to platform core.
10. If core changes are required, create an ADR.

## 7. Domain-neutral abstractions

Reusable abstractions may include:

- Batch
- Lot
- Quality checkpoint
- Custody transfer
- Shipment
- Traceability proof
- Advisory
- Alert
- Forecast
- Inspection
- Sensor-derived business event
- Workflow task

## 8. Anti-patterns

Avoid:

- Adding farming-specific fields to the core platform.
- Adding cement-specific workflows to the core platform.
- Making AI mandatory for a domain workflow.
- Making IoT mandatory for a domain workflow.
- Making blockchain mandatory for traceability.
- Creating direct dependencies between unrelated domains.

## 9. Validation checklist

A new industry extension is acceptable when:

- It has a domain model.
- It maps to ERPNext concepts where possible.
- It declares events and commands.
- It has a module manifest.
- It can run without optional AI/IoT/blockchain services.
- It does not require an ERPNext fork.
- It does not require platform core changes unless approved by ADR.
