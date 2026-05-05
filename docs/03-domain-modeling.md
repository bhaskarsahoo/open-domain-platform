# Domain Modeling

## 1. Goal

The platform must support multiple business domains without rewriting the core architecture.

Domain modeling is the process of identifying the business concepts, workflows, events, commands, and integrations that are unique to an industry while keeping the platform core reusable.

The first reference domain is smart farming and supply chain. A future domain could be cement, manufacturing, retail, cold chain, or another vertical.

## 2. Core vs domain-specific

### Platform core

The platform core should be generic and reusable:

- Event envelope
- Command envelope
- Module manifest
- Outbox pattern
- Command API conventions
- Domain registry
- Workflow template conventions
- Traceability abstraction
- AI tool interface
- IoT adapter interface
- Analytics adapter interface

### Domain-specific layer

The domain-specific layer owns industry concepts:

- Smart farming: farm, plot, crop plan, harvest batch, irrigation, pest observation
- Cement: plant, quarry, clinker batch, cement batch, silo, dispatch, dealer, truck
- Retail: store, POS shift, promotion, stock replenishment, customer loyalty
- Cold chain: temperature zone, sensor reading, cold room, excursion, custody event

## 3. Domain modeling workflow

For every new domain, follow these steps.

### Step 1: Identify domain actors

Examples for smart farming:

- Farmer
- Farm manager
- Agronomist
- Aggregator
- Warehouse operator
- Quality inspector
- Distributor
- Retailer
- Consumer

Examples for cement:

- Plant operator
- Quality engineer
- Dispatch planner
- Dealer
- Distributor
- Truck driver
- Construction site buyer
- Sales manager

### Step 2: Identify domain entities

Examples for smart farming:

- Farm
- Plot
- Crop
- Crop season
- Crop plan
- Farm activity
- Input material
- Field inspection
- Harvest batch
- Quality grade
- Warehouse receipt
- Shipment
- Traceability log

Examples for cement:

- Plant
- Quarry
- Raw material batch
- Clinker batch
- Cement batch
- Silo
- Packing line
- Dispatch order
- Truck
- Dealer
- Retailer
- Quality certificate

### Step 3: Map entities to ERPNext concepts

Do not create new entities if ERPNext already has an appropriate concept.

Examples:

| Domain concept | ERPNext/Frappe concept |
|---|---|
| Seed, fertilizer, pesticide | Item |
| Warehouse, cold storage | Warehouse |
| Farmer, buyer, dealer | Customer or Supplier depending on role |
| Procurement | Purchase Order / Purchase Receipt |
| Sale | Sales Order / Sales Invoice / POS Invoice |
| Shipment | Delivery Note or custom Shipment DocType |
| Harvest batch | Batch plus domain extension |
| Quality check | Quality Inspection |

### Step 4: Identify workflows

Examples for smart farming:

- Farm onboarding
- Crop planning
- Sowing
- Input application
- Irrigation
- Field inspection
- Harvest
- Grading
- Warehouse receipt
- Shipment
- Retail sale
- Traceability lookup

Examples for cement:

- Raw material receipt
- Production batch
- Quality testing
- Silo storage
- Packing
- Dispatch planning
- Truck loading
- Dealer delivery
- Site delivery
- Complaint/quality traceability

### Step 5: Identify domain events

Events describe things that happened.

Smart farming examples:

- `FarmRegistered`
- `PlotCreated`
- `CropPlanCreated`
- `SowingCompleted`
- `IrrigationLogged`
- `FertilizerApplied`
- `PesticideApplied`
- `FieldInspectionCompleted`
- `DiseaseObserved`
- `HarvestCompleted`
- `HarvestBatchCreated`
- `QualityInspectionCompleted`
- `BatchMovedToWarehouse`
- `ShipmentDispatched`

Cement examples:

- `RawMaterialReceived`
- `ProductionBatchCreated`
- `QualityCertificateIssued`
- `CementBatchPacked`
- `SiloStockUpdated`
- `DispatchOrderCreated`
- `TruckLoaded`
- `DealerDeliveryCompleted`

### Step 6: Identify commands

Commands request the system to do something.

Smart farming examples:

- `CreateFarmAdvisory`
- `CreateFieldInspectionTask`
- `CreateHarvestBatch`
- `CreateQualityInspection`
- `PutBatchOnHold`
- `UpdateCropPlanStatus`
- `AttachTraceabilityProof`

Cement examples:

- `CreateQualityCertificate`
- `CreateDispatchOrder`
- `ReserveDealerStock`
- `CreateTruckLoadingTask`
- `AttachBatchTestReport`

### Step 7: Identify optional capability integrations

For every domain, decide which optional capabilities may apply.

| Capability | Smart farming | Cement |
|---|---|---|
| AI | crop advisory, disease risk, yield forecast | demand forecast, quality anomaly detection |
| IoT | soil moisture, weather, cold storage, GPS | plant sensors, silo levels, truck GPS |
| Traceability | farm-to-consumer batch provenance | raw material-to-site batch provenance |
| Analytics | yield, quality, input cost, sales | production, dispatch, dealer stock, quality |
| Blockchain | provenance proof where required | quality certificate or custody proof where required |

## 4. Domain model template

Every domain should have a file under `domains/<domain-name>/domain-model.md` using this structure:

```markdown
# Domain Model: <Domain Name>

## Scope

## Actors

## Core entities

## ERPNext mapping

## Workflows

## Events

## Commands

## Reports and analytics

## AI opportunities

## IoT opportunities

## Traceability opportunities

## Out of scope

## Open questions
```

## 5. Design rule

A domain module should not change the platform core unless the new capability is reusable across multiple domains.

If a smart farming workflow requires a new concept that could also apply to cement, manufacturing, or retail, consider placing the abstraction in the platform core.

If it only applies to farming, keep it in the smart farming domain module.
