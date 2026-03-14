# Stage 3: Validation

Quality gate. Verify that processed drone data meets defined standards before it proceeds to cleaning and ingestion. This is the primary checkpoint where non-conforming data is rejected.

## Inputs

- Processed data files and manifest from Stage 2
- Processing report from Stage 2
- Validation ruleset (format, CRS, resolution/GSD, coverage thresholds, point cloud density)
- Reference data for accuracy assessment (if positional accuracy validation is required, e.g., check points surveyed independently)

## Outputs

- Validation report including:
  - Pass/fail result for each rule
  - Summary of failures with severity (blocking vs. advisory)
  - Positional accuracy metrics (RMSE from check points, if assessed)
  - GSD and point cloud density measurements
  - Attribute completeness statistics
  - Validation timestamp and ruleset version
- Annotated data files (if issues are flagged inline)
- Decision record: **Pass** (advance to Stage 4) or **Fail** (return to earlier stage with documented routing — Re-flight, Reprocess, or Schema / geometry errors)

## QA Criteria

- Every rule in the validation ruleset has a recorded result
- All blocking rules have passed
- Positional accuracy meets the specified tolerance (e.g., RMSE ≤ threshold relative to check points)
- GSD of the orthomosaic meets the target specified in the flight plan
- Point cloud density meets the minimum threshold for the intended analysis
- Output CRS is correct and consistent across all products (orthomosaic, DSM/DTM, point cloud)
- No data voids in areas where coverage was confirmed complete in Stage 1
- Coverage meets the minimum threshold for the area of interest

## Failure Handling

| Failure | Severity | Response |
|---------|----------|----------|
| GSD below target | Blocking | Assess root cause (altitude, overlap, processing parameters); return to Stage 2 or Stage 1 |
| Point cloud density insufficient | Blocking | Return to Stage 2 for reprocessing; if insufficient input overlap, return to Stage 1 |
| CRS mismatch | Blocking | Return to Stage 2 for reprocessing |
| Positional accuracy below threshold | Blocking | Assess GCP placement and accuracy; return to Stage 2 or Stage 1 |
| Data voids in coverage area | Blocking | Return to Stage 1 if gap is in source imagery; return to Stage 2 if processing artifact |
| Coverage below minimum | Blocking | Return to Stage 1 for additional flight coverage |
| Advisory issues only | Advisory | Document in validation report; advance with notation |
