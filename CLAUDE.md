# CLAUDE.md

This file provides guidance to Claude Code when working with this repository.

## Project Overview

PigeonSight is a **tool-agnostic process framework for drone data workflows**. It defines a standardized methodology for moving drone data from flight to stakeholder delivery, built around gate-based progression and full dataset lineage.

This is an architecture and methodology project, not a code library. The primary deliverables are documentation and process definitions. The framework defines *what* happens at each stage. The tools used to implement each stage may vary by budget, environment, technical requirements, or organizational preference.

## Repository Structure

```
pigeon-sight/
├── README.md
├── CLAUDE.md
├── diagrams/
│   ├── workflow.md
│   └── workflow.svg
├── docs/
│   ├── overview.md
│   ├── methodology.md
│   └── stages/
│       ├── 01-capture.md
│       ├── 02-processing.md
│       ├── 03-validation.md
│       ├── 04-cleaning.md
│       ├── 05-ingestion.md
│       ├── 06-analysis.md
│       └── 07-delivery.md
└── templates/
    ├── qa-checklist.md
    ├── flight-plan-template.md
    ├── capture-metadata-template.md
    ├── validation-ruleset-template.md
    └── delivery-specification-template.md
```

## Stage Document Structure

Each stage doc defines:

- **Inputs** — What enters the stage
- **Outputs** — What the stage produces
- **QA Criteria** — Verifiable conditions that must be met before advancing
- **Failure Handling** — How specific failure modes are routed and resolved

## The Seven Stages

1. **Capture** — Acquire raw imagery and sensor data from drone flights
2. **Processing** — Transform raw inputs into orthomosaics, point clouds, and DEMs
3. **Validation** — QA/QC gate; the primary checkpoint where non-conforming data is rejected
4. **Cleaning** — Normalize schemas, transform coordinates, handle anomalies
5. **Ingestion** — Load validated data into target storage
6. **Analysis** — Query, model, and extract insights
7. **Delivery** — Package and distribute results to stakeholders

## Conventions

- **Tool-agnostic language** — Do not reference specific tools (WebODM, PostGIS, QGIS, GeoServer) in framework documents. Use generic terms: processing engine, target storage, compatible GIS application, web service endpoint.
- **Stage naming** — Use short names without "Data" prefix: Capture, Processing, Validation, Cleaning, Ingestion, Analysis, Delivery.
- **Validation gate** — Stage 3 has two outcomes only: Pass or Fail. There is no Conditional Pass.
- **Mission ID** — The linking key across all pipeline artifacts. All templates and stage reports reference the same Mission ID.
- **Routing labels** — Match the diagram exactly: Re-flight, Reprocess, Schema / geometry errors, Pass, Data issue, Analysis issue.
- **New templates** go in `templates/`
- **Do not over-engineer** — This is a framework document, not a production system.
