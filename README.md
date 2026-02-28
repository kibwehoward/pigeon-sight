# PigeonSight

**A process framework for drone data workflows.**

PigeonSight defines a standardized methodology for processing drone data from sensor to stakeholder delivery, built around the FOSS4G stack with WebODM at its core. The framework defines *what* happens at each stage — your tools define *how*.

---

## From Pests to Programs

PigeonSight grew out of a field inspection problem. Working in integrated pest management, the need to conduct site surveys over large or inaccessible areas pointed toward sUAS — small drones capable of capturing the imagery needed for orthomosaics, point clouds, elevation, and 3D models of habitats and structures. The tools to process that imagery existed. The process framework to manage the data reliably, repeatably, and without a proprietary subscription did not.

The available commercial solutions were expensive and opaque. The stack — WebODM, PostGIS, QGIS — could do the work, but nothing defined *how* the workflow should be structured: what the stages were, what constituted done at each stage, how failures should be handled, or how a dataset should be traced from flight to delivery.

PigeonSight is that framework. Seven stages, a formal QA gate, defined inputs and outputs at every step, and a reference implementation built entirely on open-source tools.

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
