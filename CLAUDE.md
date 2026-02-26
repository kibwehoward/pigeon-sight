# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

PigeonSight is a **process framework for geospatial data workflows**. It defines a technology-agnostic, industry-agnostic methodology for processing geospatial data from capture to stakeholder delivery.

This is an architecture/methodology project, not a code library. The primary deliverables are documentation and process definitions, with reference implementations as supporting examples.

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
│       ├── 01-data-capture.md
│       ├── 02-data-processing.md
│       ├── 03-data-validation.md
│       ├── 04-data-cleaning.md
│       ├── 05-data-ingestion.md
│       ├── 06-data-analysis.md
│       └── 07-stakeholder-delivery.md
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

1. **Data Capture** (`01-data-capture.md`) — Acquire raw data from sensors, drones, surveys, or external sources
2. **Data Processing** (`02-data-processing.md`) — Transform raw inputs into usable formats
3. **Data Validation** (`03-data-validation.md`) — QA/QC gate; verify data meets quality standards
4. **Data Cleaning** (`04-data-cleaning.md`) — Normalize schemas, transform coordinates, handle anomalies
5. **Data Ingestion** (`05-data-ingestion.md`) — Load validated data into target storage
6. **Data Analysis** (`06-data-analysis.md`) — Query, model, and extract insights
7. **Stakeholder Delivery** (`07-stakeholder-delivery.md`) — Package and distribute results

## Guidelines for Claude

- This is a **framework/architecture project** — focus on documentation quality, not code complexity
- Maintain technology-agnostic framing throughout (describe *what*, not *how with which tool*)
- Reference implementations should be minimal — just enough to demonstrate a stage works
- Don't over-engineer examples; they exist to illustrate the framework, not to be production systems
- `templates/qa-checklist.md` is a reusable QA template; new templates go in `templates/`
