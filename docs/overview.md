# PigeonSight Framework Overview

PigeonSight is a process framework for drone data workflows. It defines a standardized methodology for moving drone data from flight to stakeholder delivery, built around gate-based progression and full dataset lineage.

## Design Principles

**Tool-agnostic by design.** The framework defines *what* happens at each stage; the tools used to implement each stage may vary by budget, environment, technical requirements, or organizational preference. Any platform that meets the stage's input and output requirements fits the framework.

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
| [1. Capture](stages/01-capture.md) | Acquire raw imagery and sensor data from drone flights | Manifest complete, checksums match, overlap verified |
| [2. Processing](stages/02-processing.md) | Generate orthomosaic, point cloud, DSM/DTM | Output meets target CRS, GSD, and point cloud density |
| [3. Validation](stages/03-validation.md) | QA/QC checkpoint | All blocking rules pass |
| [4. Cleaning](stages/04-cleaning.md) | Normalize, repair, standardize | Schema conformant, issues resolved |
| [5. Ingestion](stages/05-ingestion.md) | Load to target storage | Record counts match, spatial index built |
| [6. Analysis](stages/06-analysis.md) | Query, model, extract insights | Results reproducible, sanity-checked |
| [7. Delivery](stages/07-delivery.md) | Distribute results to stakeholders | Artifacts delivered, receipt confirmed |

## Stage Document Structure

Each stage document defines:

- **Inputs** — What enters the stage
- **Outputs** — What the stage produces, including required metadata and reports
- **QA Criteria** — Verifiable conditions that must be met before advancing
- **Failure Handling** — How specific failure modes are routed and resolved

## Further Reading

- [Methodology](methodology.md) — The process thinking behind the framework: gate-based stages, the Scrum parallel, and Stage 3 as a formal QA gate

## Routing Rules

- A stage advances when all **blocking** QA criteria are met.
- **Advisory** issues are documented but do not block advancement.
- Failures route back to the earliest stage where the root cause can be addressed — not necessarily the immediately preceding stage.
- Any routing decision (advance, hold, route back) should be recorded in the relevant stage report.

See the [workflow diagram](../diagrams/workflow.md) for the full set of routing labels and their definitions.
