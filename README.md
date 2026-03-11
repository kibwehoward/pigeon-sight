# PigeonSight

**PigeonSight is a modular operational framework for drone-data workflows. It defines how imagery moves from capture to delivery — through intake, processing, QA, orchestration, and handoff — in a repeatable system that adapts across tools, platforms, and industries.**

---

## From Pests to Programs

PigeonSight grew out of a field inspection problem. Working in integrated pest management, the need to conduct site surveys over large or inaccessible areas pointed toward sUAS — small drones capable of capturing the imagery needed for orthomosaics, point clouds, elevation models, and 3D reconstructions of habitats and structures. The tools to process that imagery existed. What did not exist was a process framework for managing that data reliably, repeatably, and without requiring either a proprietary subscription or deep systems-administration expertise.

Commercial and open-source offerings could process imagery, but they were often expensive, opaque, or tightly bound to vendor-specific workflows. The larger gap was methodological: nothing clearly defined how a drone-data workflow should be structured, what the stages were, what constituted done at each stage, how failures should be handled, or how a dataset should be traced from flight to delivery across tools and domains.

PigeonSight is that framework. It defines seven stages, a formal QA gate, clear inputs and outputs at every step, and a repeatable definition of done from capture through stakeholder delivery. The reference implementation demonstrates the framework in practice, but the framework itself is designed to adapt across tools, platforms, and industries.

---

## Why the Name

- **Pi** — Precision, measurement, mathematical rigor
- **Geo** — Geospatial analysis, location-based intelligence
- **nSight** — Insight from raw data
- **Pigeon** — Nature's most ubiquitous, overlooked, resilient creature

---

## The Framework

PigeonSight defines seven stages for drone data workflows:

| Stage | Purpose |
|-------|---------|
| **Data Capture** | Acquire raw imagery and sensor data from drone flights |
| **Data Processing** | Transform raw inputs into orthomosaics, point clouds, and DEMs |
| **Data Validation** | QA/QC gate — verify data meets quality standards |
| **Data Cleaning** | Handle anomalies, normalize schemas, transform coordinates |
| **Data Ingestion** | Load validated data into target storage systems |
| **Data Analysis** | Query, model, and extract insights |
| **Stakeholder Delivery** | Package and distribute results to end users |

Each stage has defined:
- **Inputs** — What enters the stage
- **Outputs** — What the stage produces
- **QA Criteria** — How to verify the stage completed successfully
- **Failure Handling** — What happens when validation fails

See the [workflow diagram](diagrams/workflow.md) for the full pipeline with routing logic, or embed [workflow.svg](diagrams/workflow.svg) in reports and presentations.

---

## Reference Stack

PigeonSight is designed around open-source tools. These are the reference implementations for each stage — other tools fit the same stages, but this is the stack the framework is built to demonstrate.

| Stage | Reference Tool |
|-------|---------------|
| Data Capture | DJI / senseFly / custom builds |
| Data Processing | **WebODM** (NodeODM engine) |
| Data Storage | **PostGIS** (PostgreSQL + spatial extension) |
| Data Analysis | **QGIS** / Python (GeoPandas, Rasterio) |
| Data Delivery | **GeoServer** / QGIS Server |

WebODM is the vanguard of this stack — it handles the most compute-intensive transformation (raw imagery → orthomosaic/point cloud/DEM) and its output format defines the schema expectations for downstream stages.

---

## When to Use PigeonSight

Any domain where drone imagery drives decision-making:

- **Agriculture** — Crop health monitoring, yield analysis, irrigation planning
- **Construction** — Site surveys, progress tracking, as-builts
- **Disaster Response** — Damage assessment, search and rescue support
- **Energy** — Infrastructure inspection, environmental compliance
- **Government** — Land management, urban planning, parcel analysis
- **Environmental** — Habitat mapping, change detection, erosion monitoring

---

## Repository Structure

```
pigeon-sight/
├── README.md
├── docs/
│   ├── overview.md
│   └── stages/
│       ├── 01-data-capture.md
│       ├── 02-data-processing.md
│       ├── 03-data-validation.md
│       ├── 04-data-cleaning.md
│       ├── 05-data-ingestion.md
│       ├── 06-data-analysis.md
│       └── 07-stakeholder-delivery.md
├── diagrams/
│   ├── workflow.md        # Mermaid diagram (renders on GitHub)
│   └── workflow.svg       # Standalone SVG for embedding
└── templates/
    └── qa-checklist.md
```

---

## License

MIT
