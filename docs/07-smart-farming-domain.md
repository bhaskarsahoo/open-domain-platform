# Smart Farming Domain

## 1. Purpose

Smart farming is the first reference domain for Open Domain Platform.

The goal is to model farm operations, harvest batches, quality checks, inventory movement, supply-chain traceability, advisory workflows, and optional AI/IoT integrations.

## 2. Scope

Initial scope:

- Farm registration
- Farmer management
- Plot management
- Crop planning
- Farm activities
- Field inspections
- Harvest batch creation
- Quality grading
- Warehouse movement
- Shipment
- Traceability
- Farm advisory workflow

Out of initial scope:

- Real IoT device fleet management
- Production AI disease model
- Blockchain network deployment
- Satellite imagery processing
- Drone image processing
- Advanced agronomy recommendation engine

## 3. Actors

- Farmer
- Farm manager
- Agronomist
- Field officer
- Aggregator
- Warehouse operator
- Quality inspector
- Distributor
- Retailer
- Consumer

## 4. Core entities

- Farm
- Farmer
- Plot
- Crop
- Crop Season
- Crop Plan
- Farm Activity
- Field Inspection
- Input Application
- Irrigation Log
- Disease Observation
- Harvest Batch
- Quality Grade
- Farm Advisory
- Traceability Log

## 5. ERPNext mapping

| Smart farming concept | ERPNext/Frappe mapping |
|---|---|
| Seed, fertilizer, pesticide | Item |
| Warehouse or cold storage | Warehouse |
| Farmer | Supplier, Customer, or custom Farmer depending on business model |
| Aggregator or buyer | Customer or Supplier depending on role |
| Harvest output | Item + Batch |
| Quality check | Quality Inspection |
| Farm advisory | Custom DocType |
| Shipment | Delivery Note or custom Shipment DocType |
| Retail sale | POS Invoice or Sales Invoice |

## 6. Workflows

### Crop planning workflow

```text
Farm Registered
  -> Plot Created
  -> Crop Plan Created
  -> Sowing Planned
  -> Activities Scheduled
```

### Farm activity workflow

```text
Sowing Completed
  -> Irrigation Logged
  -> Fertilizer Applied
  -> Pest Observation Logged
  -> Field Inspection Completed
```

### Harvest workflow

```text
Harvest Planned
  -> Harvest Completed
  -> Harvest Batch Created
  -> Quality Inspection Completed
  -> Batch Stored
```

### Farm-to-supply-chain workflow

```text
Harvest Batch Created
  -> Warehouse Receipt
  -> Batch Packed
  -> Shipment Dispatched
  -> Shipment Delivered
  -> POS Invoice Submitted
  -> Traceability Lookup
```

## 7. Events

Initial smart farming events:

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
- `FarmAdvisoryCreated`

## 8. Commands

Initial smart farming commands:

- `CreateFarmAdvisory`
- `CreateFieldInspectionTask`
- `CreateHarvestBatch`
- `CreateQualityInspection`
- `PutHarvestBatchOnHold`
- `AttachTraceabilityProof`
- `UpdateCropPlanStatus`

## 9. AI opportunities

- Crop advisory assistant
- Disease risk detection
- Irrigation recommendation
- Yield forecast
- Market price recommendation
- Procurement assistant
- Supply-chain exception copilot

## 10. IoT opportunities

- Soil moisture readings
- Temperature readings
- Humidity readings
- Water level readings
- Pump status
- Cold storage monitoring
- GPS shipment tracking

## 11. Traceability opportunities

- Farm origin
- Plot origin
- Crop plan history
- Input application history
- Harvest batch history
- Quality inspection history
- Warehouse movement
- Shipment movement
- Retail sale reference

## 12. MVP demo flow

The first demo should show:

```text
Farm Registered
  -> Plot Created
  -> Crop Plan Created
  -> Field Inspection Completed
  -> Mock AI Advisor creates Farm Advisory
  -> Harvest Batch Created
  -> Quality Inspection Completed
  -> Batch Moved to Warehouse
  -> Traceability Proof Created
```
