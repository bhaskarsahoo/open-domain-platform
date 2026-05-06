# Datasets

This directory tracks public dataset sources, mapping notes, and small sample fixtures for validating Open Domain Platform.

Large third-party datasets should not be committed directly to this repository. Instead, store:

- Dataset metadata
- Source URL
- License notes
- Fetch instructions
- Field mappings
- Small synthetic or derived samples
- Event-generation examples

## Initial dataset tracks

1. Smart farming
2. Supply chain
3. Cement / construction materials
4. Cross-domain analytics

## Dataset workflow

```text
public source
  -> raw download outside git
  -> normalized staging format
  -> domain mapping
  -> ERPNext seed data
  -> generated events
  -> analytics / AI / traceability demo
```

## Files

- `sources.yaml` — initial source registry
- `smart-farming/` — farming dataset notes and mappings
- `supply-chain/` — supply-chain dataset notes and mappings
- `cement/` — cement dataset notes and mappings
