# ADR-0001: Platform Direction

## Status

Accepted

## Date

2026-05-05

## Context

The project aims to build an open platform for domain-specific business solutions. The first reference domain is smart AI farming and supply chain, but the architecture should also support domains such as cement, manufacturing, retail, cold chain, and logistics.

The platform needs ERP, CRM, POS, inventory, workflows, analytics, and future support for AI, IoT, traceability, and blockchain. Rebuilding ERP from scratch would be expensive and risky.

## Decision

Use ERPNext/Frappe as the initial system of record and build Open Domain Platform as an event-driven, modular extension layer around it.

The core platform will provide:

- Event outbox
- Event schemas
- Command API conventions
- Module manifest
- Domain modeling conventions
- Workflow extension conventions
- AI-ready interface
- IoT-ready interface
- Traceability-ready interface
- Analytics integration conventions

Advanced capabilities such as AI, IoT, blockchain, and analytics will be optional modules rather than required platform dependencies.

## Rationale

ERPNext/Frappe provides a strong open-source foundation for ERP, CRM, POS, stock, buying, selling, accounting, workflows, and customization.

A modular event-driven architecture allows domain workflows and external services to be added without heavily modifying ERPNext core.

A local-first design allows development to begin on a developer machine without expensive infrastructure.

## Consequences

### Positive

- Faster start than rebuilding ERP.
- Strong existing ERP/CRM/POS foundation.
- Clear extension model.
- Supports multiple domains.
- AI, IoT, blockchain, and analytics can be added later.
- Lower initial infrastructure cost.

### Negative

- ERPNext/Frappe expertise is required.
- ERPNext licensing implications must be managed carefully.
- Deep ERPNext changes should be avoided.
- Some advanced workflows may require careful mapping to ERPNext concepts.

### Constraints

- Do not fork ERPNext core without a separate ADR.
- Do not bypass ERPNext validations with direct database writes.
- Keep domain modules separate from platform core.
- Keep optional capability modules replaceable.

## Alternatives considered

### Build from scratch

Rejected because it would require rebuilding ERP, CRM, POS, inventory, workflows, permissions, accounting, and reporting.

### Odoo Community

Considered. Odoo has a strong ecosystem, but the Community/Enterprise boundary may complicate full open-source control for advanced features.

### Apache OFBiz

Considered. It has a permissive license and broad enterprise features, but would likely require more UX and product work.

### Dolibarr or Tryton

Considered. These are useful open-source ERP systems, but ERPNext/Frappe appears to offer a better balance for this project's extensibility, developer experience, and target workflows.

## Follow-up ADRs

- ADR-0002: Repository licensing model
- ADR-0003: Event broker choice for local development
- ADR-0004: ERPNext app boundaries
- ADR-0005: Smart farming domain model
- ADR-0006: Traceability adapter strategy
