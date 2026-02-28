# Methodology

PigeonSight is not just a technical pipeline. It is a process framework — a deliberate application of software development methodology to a domain where ad hoc workflows are the norm.

## Why Gate-Based Stages

Drone data workflows are typically treated as a continuous process: fly, process, deliver. In practice, this produces a recurring problem — errors discovered late are expensive to fix, and without defined checkpoints, there is no consistent standard for when a dataset is "good enough" to act on.

PigeonSight applies a principle from software development: **discrete, gate-based stages with explicit definitions of done**. Each stage has defined inputs, defined outputs, and verifiable QA criteria that must be met before the next stage begins. Data that fails the criteria is routed back — not forward.

This structure enforces quality at the point where it is cheapest to fix, not at the point where it is discovered by a stakeholder.

## The Scrum Parallel

Each pipeline run in PigeonSight is structured like a Scrum sprint:

| Scrum | PigeonSight |
|-------|-------------|
| Sprint backlog | Flight plan and mission parameters |
| Sprint execution | Stages 1–2: capture and processing |
| Sprint review / definition of done | Stage 3: Data Validation gate |
| Sprint retrospective | Pipeline completion checklist (Stage 7) |
| Velocity and capacity | QA metrics: GSD achieved, point cloud density, GCP residuals |

The analogy is not decorative. A sprint without a definition of done produces inconsistent output. A drone data pipeline without a validation gate produces the same. The question "is this done?" needs a verifiable answer in both contexts.

## Stage 3 as a Formal QA Gate

Stage 3 (Data Validation) is the primary checkpoint in the pipeline. It functions as an SDLC-style QA gate:

- **Acceptance criteria** are defined in advance (the validation ruleset), not assessed after the fact
- **Findings are classified** as blocking or advisory — blocking failures halt advancement; advisory issues are documented but do not stop the pipeline
- **A decision record is required** — Pass, Conditional Pass, or Fail with explicit routing — so every gate outcome is auditable
- **Failures route to root cause**, not just to the prior stage — a coverage gap routes back to Stage 1 (re-flight), a processing artifact routes back to Stage 2 (reprocess in WebODM)

This is the same pattern as a QA sign-off in a software release cycle: defined criteria, documented outcome, traceable routing.

## Lineage as an Audit Trail

Every dataset that passes through PigeonSight carries a lineage record from original capture through final delivery. This is the equivalent of a commit history or a change log — a traceable record of what data entered the pipeline, what transformations were applied, and what decisions were made at each gate.

The lineage record closes the loop between the QA checklist (what was verified) and the delivery artifact (what was delivered). Without it, a stakeholder question — "how was this orthomosaic produced?" — has no reliable answer.

## Why This Matters

Most drone data practitioners are highly skilled at operating equipment and processing imagery. Few apply formal process methodology to the workflow. The result is pipelines that are difficult to audit, hard to hand off, and inconsistent across runs.

PigeonSight is an attempt to close that gap: to bring the rigor of gate-based software development — sprint structure, acceptance criteria, formal QA sign-off, audit trail — to a domain that has not typically demanded it.
