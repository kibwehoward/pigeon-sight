# PigeonSight Framework Overview

PigeonSight is a process framework for geospatial data workflows. It defines a standardized, technology-agnostic methodology for moving geospatial data from capture to stakeholder delivery.

## Design Principles

**Technology-agnostic.** The framework defines *what* happens at each stage. Your tools define *how*. The same seven stages apply whether you're processing drone imagery with Pix4D, ingesting LiDAR to PostGIS, or delivering results through ArcGIS Online.

**Gate-based progression.** Each stage produces defined outputs and must meet QA criteria before the next stage begins. Data that fails validation is routed back — not forward.

**Full lineage.** Every dataset that passes through the pipeline carries a traceable lineage record from original capture through final delivery.

## The Seven Stages

```
[Capture] → [Processing] → [Validation] → [Cleaning] → [Ingestion] → [Analysis] → [Delivery]
                                ↓ fail           ↓ fail
                           (route back)     (route back)
```

| Stage | Purpose | Gate |
|-------|---------|------|
| [1. Data Capture](stages/01-data-capture.md) | Acquire raw data | Manifest complete, checksums match |
| [2. Data Processing](stages/02-data-processing.md) | Transform to usable formats | Output meets target CRS and resolution |
| [3. Data Validation](stages/03-data-validation.md) | QA/QC checkpoint | All blocking rules pass |
| [4. Data Cleaning](stages/04-data-cleaning.md) | Normalize, repair, standardize | Schema conformant, issues resolved |
| [5. Data Ingestion](stages/05-data-ingestion.md) | Load to target storage | Record counts match, index built |
| [6. Data Analysis](stages/06-data-analysis.md) | Query, model, extract insights | Results reproducible, sanity-checked |
| [7. Stakeholder Delivery](stages/07-stakeholder-delivery.md) | Package and distribute | Artifacts delivered, receipt confirmed |

## Stage Document Structure

Each stage document defines:

- **Inputs** — What enters the stage
- **Outputs** — What the stage produces, including required metadata and reports
- **QA Criteria** — Verifiable conditions that must be met before advancing
- **Failure Handling** — How specific failure modes are routed and resolved

## Routing Rules

- A stage advances when all **blocking** QA criteria are met.
- **Advisory** issues are documented but do not block advancement.
- Failures route back to the earliest stage where the root cause can be addressed — not necessarily the immediately preceding stage.
- Any routing decision (advance, hold, route back) should be recorded in the relevant stage report.
