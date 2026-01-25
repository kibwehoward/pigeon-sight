# CLAUDE.md

This file provides guidance to Claude Code when working in this repository.

## Project Overview

PigeonSight is a **process framework for geospatial data workflows**. It defines a technology-agnostic, industry-agnostic methodology for processing geospatial data from capture to stakeholder delivery.

This is an architecture/methodology project, not a code library. The primary deliverables are documentation and process definitions, with reference implementations as supporting examples.

## Repository Structure

```
pigeonsight/
├── README.md              # Framework overview
├── docs/                  # Framework documentation
│   ├── overview.md
│   └── stages/            # Stage definitions (inputs, outputs, QA criteria)
├── diagrams/              # Workflow and architecture diagrams
└── templates/             # Reusable templates (QA checklists, etc.)
```

## The Seven Stages

1. **Data Capture** — Acquire raw data
2. **Data Processing** — Transform to usable formats
3. **Data Validation** — QA/QC gate
4. **Data Cleaning** — Normalize, transform, handle anomalies
5. **Data Ingestion** — Load to target storage
6. **Data Analysis** — Query and model
7. **Stakeholder Delivery** — Package and distribute results

## Guidelines for Claude

- This is a **framework/architecture project** — focus on documentation quality, not code complexity
- Reference implementations should be minimal — just enough to demonstrate the stage works
- When adding content, maintain technology-agnostic framing
- Stage documentation should define inputs, outputs, QA criteria, and failure handling
- Don't over-engineer examples; they exist to illustrate the framework, not to be production systems
