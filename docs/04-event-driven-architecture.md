# Event-Driven Architecture

## 1. Purpose

The platform uses events to connect ERPNext/Frappe, domain modules, AI services, IoT services, traceability services, analytics, and external integrations.

Events allow the system to grow in a plug-and-play way without making ERPNext responsible for every side effect.

## 2. Events vs commands

### Events

Events describe facts that already happened.

Examples:

- `SalesOrderSubmitted`
- `GoodsReceived`
- `HarvestBatchCreated`
- `ShipmentDispatched`
- `TemperatureExcursionDetected`
- `FarmAdvisoryCreated`

Events should be named in past tense.

### Commands

Commands request an action.

Examples:

- `CreateFarmAdvisory`
- `CreateMaterialRequestDraft`
- `CreateQualityInspection`
- `PutBatchOnHold`
- `AttachTraceabilityProof`
- `UpdateShipmentStatus`

Commands should be named in imperative form.

## 3. Event flow

```text
ERPNext document lifecycle event
        |
        v
Frappe hook handler
        |
        v
Outbox Event record
        |
        v
Publisher worker
        |
        v
Event bus
        |
        v
Subscribers: AI, IoT, analytics, traceability, workflows
```

## 4. Command flow

```text
External service consumes event
        |
        v
External service makes decision
        |
        v
External service calls ERPNext command API
        |
        v
ERPNext validates request
        |
        v
ERPNext creates or updates document
        |
        v
ERPNext emits another event
```

## 5. Transactional outbox

ERPNext should not publish events directly to external systems during critical document transactions.

Instead, ERPNext should write events to an outbox table or DocType in the same transaction as the business change.

The event publisher reads from the outbox and publishes events asynchronously.

This improves reliability and avoids slow external calls inside ERPNext transactions.

## 6. Event envelope

All events should use a standard envelope.

```json
{
  "event_id": "uuid",
  "event_type": "HarvestBatchCreated",
  "event_version": "1.0.0",
  "source": "erpnext.smart_farming",
  "tenant_id": "demo_tenant",
  "occurred_at": "2026-05-05T10:30:00Z",
  "correlation_id": "uuid",
  "causation_id": "uuid",
  "actor": {
    "type": "User",
    "id": "user@example.com"
  },
  "subject": {
    "doctype": "Harvest Batch",
    "name": "HB-0001"
  },
  "payload": {},
  "metadata": {}
}
```

## 7. Command envelope

All commands should use a standard envelope.

```json
{
  "command_id": "uuid",
  "command_type": "CreateFarmAdvisory",
  "command_version": "1.0.0",
  "source": "ai_advisor.mock",
  "tenant_id": "demo_tenant",
  "requested_at": "2026-05-05T10:35:00Z",
  "correlation_id": "uuid",
  "actor": {
    "type": "Service",
    "id": "ai-advisor"
  },
  "target": {
    "doctype": "Farm Advisory"
  },
  "payload": {},
  "metadata": {}
}
```

## 8. Idempotency

Every event and command must have a unique ID.

Consumers should be idempotent. If the same event is delivered twice, the result should not create duplicate business records.

Recommended fields:

- `event_id`
- `command_id`
- `correlation_id`
- `causation_id`
- `idempotency_key`

## 9. Event categories

### ERP events

- `SalesOrderSubmitted`
- `PurchaseOrderApproved`
- `PurchaseReceiptSubmitted`
- `StockEntrySubmitted`
- `POSInvoiceSubmitted`
- `DeliveryNoteSubmitted`

### Smart farming events

- `FarmRegistered`
- `PlotCreated`
- `CropPlanCreated`
- `SowingCompleted`
- `IrrigationLogged`
- `FieldInspectionCompleted`
- `DiseaseObserved`
- `HarvestBatchCreated`

### Supply-chain events

- `BatchPacked`
- `BatchMovedToWarehouse`
- `ShipmentCreated`
- `ShipmentDispatched`
- `ShipmentArrived`
- `BatchTransferred`

### IoT events

- `SoilMoistureReadingReceived`
- `TemperatureReadingReceived`
- `ColdStorageTemperatureBreached`
- `DeviceOfflineDetected`
- `GeoFenceExitDetected`

### AI events

- `CropStressRiskDetected`
- `DiseaseRiskDetected`
- `YieldForecastUpdated`
- `IrrigationRecommendationCreated`
- `StockoutRiskDetected`

### Traceability events

- `BatchProvenanceUpdated`
- `CustodyTransferred`
- `CertificateIssued`
- `TraceabilityProofCreated`

## 10. Event bus choice

For local development and early pilots:

- NATS
- RabbitMQ
- Redis Streams

Avoid Kafka initially unless event volume and retention requirements justify it.

## 11. Events that should not be emitted raw

Do not emit every low-level change as a public business event.

Avoid noisy events such as:

- Every field edit
- Every raw IoT sensor reading
- Every internal validation step
- Every temporary draft state

Prefer meaningful business events.

## 12. Event versioning

Events must be versioned.

Breaking changes require a new version.

Compatible changes may add optional fields.

Consumers should be tolerant of unknown fields.

## 13. Failure handling

Event publishing should support:

- Pending state
- Published state
- Failed state
- Retry count
- Last error
- Dead-letter handling

Command processing should support:

- Accepted
- Rejected
- Failed
- Completed
- Duplicate ignored

## 14. Security

Events should not expose unnecessary sensitive data.

Use references to ERPNext documents instead of copying full records whenever possible.

Commands must be authenticated and authorized.

AI agents and external services should have least-privilege service accounts.
