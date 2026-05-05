# Module System

## 1. Purpose

The module system allows new domains and capabilities to be added without changing the platform core.

A module can represent:

- A domain, such as smart farming or cement
- A capability, such as AI advisory or IoT ingestion
- An integration, such as weather, market prices, or logistics provider sync
- A workflow pack, such as cold-chain monitoring or quality compliance

## 2. Module types

### Core modules

Required platform modules.

Examples:

- Event outbox
- Command API
- Module registry
- Domain registry

### Domain modules

Industry-specific modules.

Examples:

- Smart farming
- Cement
- Retail distribution
- Cold chain

### Capability modules

Optional advanced modules.

Examples:

- AI advisor
- IoT gateway
- Traceability service
- Blockchain adapter
- Analytics consumer
- Forecasting service

### Integration modules

Connectors to external services.

Examples:

- Weather API adapter
- Market price adapter
- Logistics tracking adapter
- Payment provider adapter
- GIS/map adapter

## 3. Module manifest

Every module must declare its contract using a module manifest.

Example:

```yaml
module_id: smart-farming-core
name: Smart Farming Core
version: 0.1.0
module_type: domain
status: experimental

owns_doctypes:
  - Farm
  - Plot
  - Crop Plan
  - Farm Activity
  - Harvest Batch

consumes_events:
  - FieldInspectionCompleted
  - WeatherForecastUpdated

emits_events:
  - FarmRegistered
  - PlotCreated
  - CropPlanCreated
  - HarvestBatchCreated

commands:
  provides:
    - CreateFarmAdvisory
    - CreateHarvestBatch
  calls:
    - CreateQualityInspection
    - AttachTraceabilityProof

optional_dependencies:
  - ai-advisor
  - weather-adapter
  - iot-gateway
  - traceability-service

required_permissions:
  - smart_farming_user
  - smart_farming_manager

configuration:
  - key: default_crop_season
    required: false
  - key: enable_traceability
    required: false
```

## 4. Module lifecycle

A module can be:

- `experimental`
- `active`
- `deprecated`
- `retired`

Experimental modules can change rapidly.

Active modules should maintain schema compatibility.

Deprecated modules should continue working during a transition period.

Retired modules should no longer be used.

## 5. Module boundaries

A module should own its own:

- Domain entities
- Workflows
- Reports
- Events
- Commands
- Configuration
- Documentation
- Tests

A module should not directly mutate another module's internal state. It should communicate through events and commands.

## 6. Required module documentation

Every module should include:

```text
README.md
module.yaml
domain-model.md
events.md
commands.md
workflows.md
configuration.md
```

## 7. Plug-and-play rule

A module should be removable without breaking the core platform.

For example:

- If AI advisor is removed, farm workflows should still work.
- If IoT gateway is removed, manual observations should still work.
- If blockchain adapter is removed, local hash-chain traceability should still work.
- If analytics is removed, ERPNext operational workflows should still work.

## 8. Dependency rules

Allowed dependencies:

- Domain module depends on platform core.
- Capability module depends on platform core.
- Capability module may optionally depend on a domain module.
- Integration module depends on platform core and external API.

Avoid:

- Platform core depending on a specific domain.
- Smart farming core depending on blockchain.
- Smart farming core depending on a specific AI model.
- Cement module depending on smart farming module.

## 9. Example module split for smart farming

```text
smart-farming-core
  Owns farm, plot, crop plan, activities, harvest batch

smart-farming-ai-advisor
  Consumes farm events and creates advisories

smart-farming-iot-adapter
  Converts sensor readings into business events

smart-farming-traceability
  Tracks batch provenance and custody

smart-farming-analytics
  Builds dashboards and metrics
```

## 10. Example module split for cement

```text
cement-core
  Owns plant, raw material batch, cement batch, silo, dispatch domain extensions

cement-quality
  Owns quality certificates and test reports

cement-logistics
  Owns truck dispatch and dealer delivery workflows

cement-analytics
  Owns production, dispatch, dealer stock, and quality dashboards
```

## 11. Adapter design

Adapters should hide external provider details behind stable interfaces.

Examples:

```text
weather-adapter
  open-meteo provider
  paid weather provider later

traceability-adapter
  local hash-chain provider
  public-chain anchor provider later
  Hyperledger Fabric provider later

ai-advisor-adapter
  mock rule engine provider
  hosted LLM provider later
  self-hosted model provider later
```

## 12. Testing expectations

Each module should include tests for:

- Manifest validity
- Event schema compatibility
- Command schema compatibility
- Idempotency behavior
- Local configuration
- Optional dependency behavior

## 13. Module review checklist

Before accepting a new module, check:

- Is it domain-specific or reusable core?
- Does it declare consumed and emitted events?
- Does it call ERPNext only through approved commands/APIs?
- Can it run locally?
- Does it introduce mandatory external infrastructure?
- Does it document configuration and permissions?
- Does it have tests or examples?
