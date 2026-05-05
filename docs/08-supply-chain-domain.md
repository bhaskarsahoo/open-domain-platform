# Supply Chain Domain

## 1. Purpose

The supply-chain domain provides reusable concepts and workflows that can be used across smart farming, cement, manufacturing, retail, cold chain, and other industries.

The goal is to support movement, custody, quality, inventory, shipment, and traceability without making the platform specific to one industry.

## 2. Core concepts

- Batch
- Lot
- Warehouse
- Storage location
- Quality checkpoint
- Shipment
- Custody transfer
- Delivery
- Traceability proof
- Recall risk
- Supplier performance
- Customer delivery

## 3. ERPNext mapping

| Supply-chain concept | ERPNext/Frappe mapping |
|---|---|
| Item | Item |
| Batch or lot | Batch |
| Warehouse | Warehouse |
| Stock movement | Stock Entry |
| Purchase receipt | Purchase Receipt |
| Delivery | Delivery Note |
| Sale | Sales Invoice or POS Invoice |
| Quality checkpoint | Quality Inspection |
| Supplier | Supplier |
| Customer | Customer |
| Shipment | Delivery Note or custom Shipment DocType |

## 4. Reusable workflows

### Receipt workflow

```text
Goods Received
  -> Quality Inspection
  -> Batch Created or Updated
  -> Warehouse Stock Updated
```

### Dispatch workflow

```text
Sales Order Submitted
  -> Stock Reserved
  -> Shipment Created
  -> Delivery Note Submitted
  -> Shipment Dispatched
```

### Custody workflow

```text
Batch Packed
  -> Custody Transferred
  -> Shipment Dispatched
  -> Shipment Arrived
  -> Custody Accepted
```

### Traceability workflow

```text
Batch Created
  -> Quality Checked
  -> Stored
  -> Moved
  -> Dispatched
  -> Delivered
  -> Traceability Lookup
```

## 5. Events

Initial supply-chain events:

- `GoodsReceived`
- `BatchCreated`
- `BatchPacked`
- `BatchMovedToWarehouse`
- `QualityInspectionCompleted`
- `ShipmentCreated`
- `ShipmentDispatched`
- `ShipmentArrived`
- `CustodyTransferred`
- `DeliveryCompleted`
- `POSInvoiceSubmitted`
- `TraceabilityProofCreated`

## 6. Commands

Initial supply-chain commands:

- `CreateQualityInspection`
- `CreateShipment`
- `UpdateShipmentStatus`
- `RecordCustodyTransfer`
- `AttachTraceabilityProof`
- `PutBatchOnHold`
- `ReleaseBatchHold`
- `CreateRecallAlert`

## 7. Smart farming usage

Smart farming uses supply-chain concepts for:

- Harvest batch
- Quality grade
- Warehouse receipt
- Cold storage
- Shipment
- Retail sale
- Farm-to-customer traceability

## 8. Cement usage

Cement can use supply-chain concepts for:

- Raw material batch
- Clinker batch
- Cement batch
- Silo storage
- Packing
- Truck loading
- Dealer dispatch
- Site delivery
- Quality certificate traceability

## 9. IoT opportunities

- Cold storage temperature
- GPS location
- Container opening
- Silo level
- Truck movement
- Machine status

## 10. AI opportunities

- Stockout risk
- Shipment delay prediction
- Quality anomaly detection
- Supplier risk scoring
- Demand forecasting
- Route exception detection

## 11. Traceability opportunities

- Batch provenance
- Custody chain
- Quality certificate proof
- Shipment proof
- Recall support
- Consumer-facing traceability page
