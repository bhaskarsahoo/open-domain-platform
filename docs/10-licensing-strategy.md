# Licensing Strategy

> This document is product and architecture guidance, not legal advice. A qualified lawyer should review the final repository boundaries, licenses, customer contracts, and distribution model before commercial launch.

## 1. Goal

The project should support open-source adoption while allowing commercial support, managed hosting, customer-specific customization, and optional proprietary capability layers.

The platform should be designed so licensing boundaries match technical boundaries.

## 2. Base platform licensing context

The project is designed around ERPNext/Frappe.

Important licensing implications:

- ERPNext is GPLv3.
- Frappe Framework is MIT.
- ERPNext-dependent custom apps should be treated carefully and may need to be GPLv3-compatible if distributed.
- Separate services communicating through APIs or event streams can usually have separate licenses, depending on how they are structured and distributed.
- Some Frappe ecosystem apps may use other licenses such as AGPLv3, so every dependency must be reviewed individually.

## 3. Recommended license layering

```text
ERPNext-dependent Frappe apps
  GPLv3-compatible, safest when distributed

Platform contracts and schemas
  Apache-2.0 or MIT

Reference external services
  Apache-2.0 or MIT

Production enterprise services
  Commercial, proprietary, or source-available

Customer-specific workflow packs
  Customer-specific commercial license

Documentation
  CC-BY or project repository license
```

## 4. Suggested repository boundaries

```text
frappe-apps/
  ERPNext/Frappe extension apps
  Likely GPLv3-compatible if distributed with ERPNext dependency

schemas/
  Event, command, and module manifest contracts
  Prefer Apache-2.0 or MIT

services/
  External AI, IoT, traceability, analytics, or integration services
  Can use Apache-2.0, MIT, or commercial license depending on goal

domains/
  Domain model documentation and reference implementations
  License depends on whether implementation depends on ERPNext internals

enterprise/
  Not part of the open repo unless intentionally open-sourced
```

## 5. Open-source foundation

The open-source foundation should include:

- Platform architecture
- Event envelope
- Command envelope
- Module manifest
- Domain modeling guide
- Event outbox reference design
- Command API reference design
- Local developer runtime
- Smart farming reference domain
- Cement reference domain model
- Mock AI advisor
- IoT simulator
- Local hash-chain traceability service
- Reference analytics consumer

## 6. Commercial opportunities

Commercial offerings can include:

- Managed hosting
- Enterprise support
- SLA-backed deployments
- Upgrade management
- Domain implementation services
- Customer-specific workflow modules
- Premium AI models
- Agronomy models
- Forecasting and optimization engines
- Real IoT integrations
- Blockchain network operations
- Premium analytics dashboards
- Enterprise connectors
- Compliance reports

## 7. Technical separation principles

To keep licensing boundaries clean:

1. Keep ERPNext-coupled functionality in a clearly separated Frappe app.
2. Keep high-value AI, IoT, analytics, and traceability logic in external services where possible.
3. Use stable event and command contracts between ERPNext and external services.
4. Avoid copying ERPNext internals into proprietary services.
5. Avoid direct database writes from external services.
6. Make optional commercial services replaceable by open reference adapters.

## 8. SaaS vs distribution

GPLv3 obligations are generally more distribution-focused than AGPLv3. However, the project should not rely on licensing loopholes as a business strategy.

If software is distributed to customers for on-premise use, source obligations may be triggered for GPL-covered derivative works.

If AGPL components are modified and hosted, network-use source availability obligations may apply.

Every component dependency should be reviewed before inclusion.

## 9. Trademark caution

Do not brand this project as if it is ERPNext itself.

Safer wording:

- Open Domain Platform for ERPNext/Frappe
- ERPNext-compatible event-driven domain platform
- Frappe-based domain extension platform

Avoid names that imply official ownership or endorsement unless permission exists.

## 10. Recommended initial license choice

For this repository, start with a permissive license for documentation, schemas, reference contracts, and external service scaffolds unless GPL-covered code is added.

When ERPNext-dependent Frappe apps are introduced, add explicit licensing notes for those subdirectories.

Recommended initial approach:

- Repository-level license: Apache-2.0 or MIT
- ERPNext-dependent app subdirectory: GPLv3-compatible notice if needed
- Commercial/private modules: keep outside this public repository

## 11. Open question

Before the first release, decide:

- Repository-level license: Apache-2.0 vs MIT
- Whether ERPNext-dependent apps live in this repo or separate repos
- Whether smart farming reference implementation is fully open-source
- Whether premium domain packs live in private repos
- Whether the commercial brand is separate from the open-source project name
