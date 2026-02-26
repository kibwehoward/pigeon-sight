# Stage 3: Data Validation

Quality gate. Verify that processed data meets defined standards before it proceeds to cleaning and ingestion. This is the primary checkpoint where non-conforming data is rejected.

## Inputs

- Processed data files and manifest from Stage 2
- Processing report from Stage 2
- Validation ruleset (format, CRS, resolution, attribute schema, coverage thresholds)
- Reference data for accuracy assessment (if positional accuracy validation is required)

## Outputs

- Validation report including:
  - Pass/fail result for each rule
  - Summary of failures with severity (blocking vs. advisory)
  - Positional accuracy metrics (if assessed)
  - Attribute completeness statistics
  - Validation timestamp and ruleset version
- Annotated data files (if issues are flagged inline, e.g., feature-level error flags)
- Decision record: **Pass** (advance to Stage 4), **Conditional Pass** (advance with documented exceptions), or **Fail** (return to earlier stage)

## QA Criteria

- Every rule in the validation ruleset has a recorded result
- All blocking rules have passed (or exceptions are formally documented and approved)
- Positional accuracy meets the specified tolerance (e.g., RMSE ≤ threshold)
- Attribute schema matches the expected schema: required fields present, correct data types, values within defined domains
- No geometry errors (e.g., self-intersections, null geometries, invalid coordinate values)
- Coverage meets the minimum threshold for the area of interest

## Failure Handling

| Failure | Severity | Response |
|---------|----------|----------|
| Geometry errors | Blocking | Return to Stage 4 (Data Cleaning) for repair, or Stage 2 if errors are systematic |
| CRS mismatch | Blocking | Return to Stage 2 for reprocessing |
| Required attribute missing | Blocking | Return to Stage 4 for enrichment or Stage 1 if source data is absent |
| Positional accuracy below threshold | Blocking | Assess root cause (GCPs, processing); return to Stage 2 or Stage 1 |
| Advisory issues only | Advisory | Document in validation report; advance with notation |
| Coverage below minimum | Blocking | Return to Stage 1 for additional capture |
