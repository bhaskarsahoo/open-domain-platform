# Public Dataset Strategy

## 1. Purpose

The platform should not start from empty demo data. Public datasets should be used to validate the domain model, event model, analytics, AI-readiness, IoT-readiness, and supply-chain workflows.

The goal is not to find one perfect dataset. The goal is to compose several public datasets into a realistic demo data layer.

## 2. Dataset strategy

Use three dataset categories:

1. Domain datasets for smart farming and supply chain.
2. Cross-domain datasets for inventory, demand, quality, and logistics.
3. Second-domain datasets, such as cement, to validate that the platform is not only for agriculture.

## 3. Smart farming dataset categories

### Crop and farm operations

Needed fields:

- Farm or region
- Crop
- Season
- Yield
- Input variables
- Weather variables
- Soil variables
- Production outcome

Usage:

- Crop planning demo
- Yield forecast demo
- Farm advisory demo
- Analytics dashboards

### Weather data

Needed fields:

- Date
- Latitude and longitude
- Temperature
- Rainfall or precipitation
- Humidity
- Solar radiation
- Wind speed

Usage:

- Weather adapter
- Irrigation advisory
- Disease risk advisory
- Yield forecast features

### Soil data

Needed fields:

- Latitude and longitude
- Soil pH
- Soil organic carbon
- Nitrogen
- Texture
- Bulk density
- Clay, sand, silt

Usage:

- Plot enrichment
- Crop suitability
- Fertilizer advisory

### Plant disease images

Needed fields:

- Crop
- Disease class
- Image
- Label

Usage:

- Optional AI disease detection research
- Advisory workflow demo

## 4. Supply-chain dataset categories

Needed fields:

- Orders
- Products
- Customers
- Warehouses
- Shipments
- Inventory levels
- Delivery dates
- Delays
- Stockouts
- Demand history

Usage:

- Demand forecasting
- Reorder recommendation
- Shipment event generation
- Inventory optimization
- Analytics dashboards

## 5. Cement dataset categories

Needed fields:

- Plant
- Raw materials
- Energy use
- Production type
- Cement product
- Emissions or impact values
- Material flow

Usage:

- Validate second-domain model
- Batch and quality workflows
- Sustainability analytics
- Material-flow analytics

## 6. Recommended initial public dataset bundle

Use the following bundle for early exploration:

1. NASA POWER weather API for weather time series.
2. SoilGrids for soil properties.
3. PlantVillage for disease image classification experiments.
4. Public supply-chain transaction or inventory datasets for demand and shipment flows.
5. Public cement production/LCA dataset for second-domain validation.

## 7. Data ingestion design

Datasets should not be imported directly into ERPNext operational tables.

Instead, build a staging layer:

```text
public dataset
  -> raw files
  -> normalized staging tables
  -> domain fixtures
  -> ERPNext seed data
  -> event replay stream
```

## 8. Repository structure

Suggested future structure:

```text
datasets/
  README.md
  sources.yaml
  smart-farming/
    source-notes.md
    mapping.md
  supply-chain/
    source-notes.md
    mapping.md
  cement/
    source-notes.md
    mapping.md

scripts/
  datasets/
    fetch_weather.py
    fetch_soil.py
    normalize_supply_chain.py
    generate_demo_events.py
```

## 9. Dataset source registry

Every dataset should be recorded with:

- Name
- Source URL
- License
- Domain
- Owner/provider
- Data format
- Refresh method
- Commercial-use suitability
- Fields available
- Mapping to domain model
- Known limitations

## 10. Evaluation criteria

A dataset is useful when it supports at least one of:

- Domain model validation
- ERPNext seed data generation
- Event generation
- Analytics demo
- AI feature engineering
- IoT simulation
- Traceability simulation
- Second-domain validation

## 11. Initial implementation tasks

1. Create `datasets/sources.yaml`.
2. Create source notes for smart farming, supply chain, and cement.
3. Build a small normalized sample dataset.
4. Generate example events from sample data.
5. Use generated events to test mock AI, analytics, and traceability modules.

## 12. Rule

Do not commit large public datasets directly into the repository. Store source metadata, fetch scripts, sample rows, and normalized schemas. Use external storage or documented download steps for larger datasets.
