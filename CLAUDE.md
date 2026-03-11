# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

PigeonSight is a **process framework for drone data workflows**. It defines a standardized methodology for processing drone data from flight to stakeholder delivery, built around the FOSS4G stack with WebODM at its core.

This is an architecture/methodology project, not a code library. The primary deliverables are documentation and process definitions, with reference implementations as supporting examples. The reference stack is WebODM → PostGIS → QGIS/GeoServer.

## Repository Structure

```
pigeon-sight/
├── README.md
├── CLAUDE.md
├── diagrams/
│   ├── workflow.md        # Mermaid diagram (renders on GitHub)
│   └── workflow.svg       # Standalone SVG for embedding
├── docs/
│   ├── overview.md        # Framework overview and routing rules
│   └── stages/
│       ├── 01-capture.md
│       ├── 02-processing.md
│       ├── 03-validation.md
│       ├── 04-cleaning.md
│       ├── 05-ingestion.md
│       ├── 06-analysis.md
│       └── 07-delivery.md
└── templates/
    └── qa-checklist.md    # Per-run QA checklist covering all seven stages
```

## Stage Document Structure

Each stage doc at `docs/stages/NN-stage-name.md` defines:

- **Inputs** — What enters the stage (format, source, schema expectations)
- **Outputs** — What the stage produces (format, destination, artifacts)
- **QA Criteria** — Verifiable conditions that confirm the stage completed correctly
- **Failure Handling** — What happens when validation fails (retry, rollback, escalate)

## The Seven Stages

1. **Capture** (`01-capture.md`) — Acquire raw imagery and sensor data from drone flights
2. **Processing** (`02-processing.md`) — Transform raw inputs into orthomosaics, point clouds, and DEMs (reference: WebODM)
3. **Validation** (`03-validation.md`) — QA/QC gate; verify data meets quality standards
4. **Cleaning** (`04-cleaning.md`) — Normalize schemas, transform coordinates, handle anomalies
5. **Ingestion** (`05-ingestion.md`) — Load validated data into target storage
6. **Analysis** (`06-analysis.md`) — Query, model, and extract insights
7. **Delivery** (`07-delivery.md`) — Package and distribute results

## Guidelines for Claude

- This is a **framework/architecture project** — focus on documentation quality, not code complexity
- The framework is drone-specific but industry-agnostic; stage descriptions should reflect drone data (imagery, point clouds, DEMs, orthomosaics)
- The reference stack is WebODM → PostGIS → QGIS/GeoServer — use these in examples, not proprietary alternatives
- Stage structure defines *what* happens; reference implementations show *how* with the FOSS4G stack
- Reference implementations should be minimal — just enough to demonstrate a stage works
- Don't over-engineer examples; they exist to illustrate the framework, not to be production systems
- `templates/qa-checklist.md` is a reusable QA template; new templates go in `templates/`
