# PigeonSight

**A process framework for geospatial data workflows.**

PigeonSight defines a standardized methodology for processing geospatial data from capture to stakeholder delivery. It's technology-agnostic and industry-agnostic — the framework adapts to your existing tools and domain.

---

## Why the Name

- **Pi** — Precision, measurement, mathematical rigor
- **Geo** — Geospatial analysis, location-based intelligence
- **nSight** — Insight from raw data
- **Pigeon** — NYC's most ubiquitous, overlooked, resilient creature

---

## The Framework

PigeonSight defines seven stages for geospatial data workflows:

| Stage | Purpose |
|-------|---------|
| **Data Capture** | Acquire raw data from sensors, drones, surveys, or external sources |
| **Data Processing** | Transform raw inputs into usable formats |
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

---

## Technology Agnostic

PigeonSight works with your existing stack. The framework defines *what* happens at each stage — your tools define *how*.

**Data Capture**
- Drones: DJI, senseFly, custom builds
- Processing: WebODM, Pix4D, DroneDeploy, Metashape
- Sensors: LiDAR, multispectral, RGB
- External: APIs, open data portals, file transfers

**Data Storage**
- Open source: PostgreSQL/PostGIS, GeoPackage, SpatiaLite
- Enterprise: Esri Enterprise Geodatabase, SQL Server, Oracle Spatial
- Cloud: Snowflake, BigQuery, AWS RDS

**Analysis & Delivery**
- Desktop: QGIS, ArcGIS Pro, Global Mapper
- Web: ArcGIS Online, GeoServer, MapBox
- Code: Python, R, SQL

---

## When to Use PigeonSight

PigeonSight applies wherever geospatial data flows from collection to decision-making:

- **Agriculture** — Crop health monitoring, yield analysis
- **Construction** — Site surveys, progress tracking, as-builts
- **Disaster Response** — Damage assessment, resource allocation
- **Energy** — Infrastructure inspection, environmental compliance
- **Government** — Land management, urban planning, census analysis
- **Environmental** — Habitat mapping, change detection

---

## Repository Structure

```
pigeonsight/
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
│   └── workflow.png
└── templates/
    └── qa-checklist.md
```

---

## License

MIT
