# Stage 4: Data Cleaning

Normalize, repair, and transform validated data into a consistent, analysis-ready state. This stage resolves issues identified in Stage 3 and standardizes the dataset for ingestion.

## Inputs

- Processed data files from Stage 2
- Validation report from Stage 3 (identifies specific issues to address)
- Data dictionary / target schema (defines field names, types, domains, and encoding conventions)
- Transformation rules (coordinate conversions, unit normalizations, classification mappings)

## Outputs

- Cleaned data files conforming to the target schema
- Cleaning log documenting every transformation applied:
  - Type of operation (repair, normalize, reclassify, fill, drop)
  - Fields or geometries affected
  - Before/after values or counts where applicable
  - Operator or automated rule that applied the change
- Updated file manifest with checksums
- Flagged records that required manual review or could not be automatically resolved

## QA Criteria

- All geometry errors identified in the validation report are resolved
- Attribute values conform to the target schema (correct types, valid domains, no nulls in required fields)
- No duplicate features (by defined key fields or spatial coincidence threshold)
- Coordinate values are within the valid range for the target CRS
- Cleaning log accounts for every issue flagged in the validation report
- No unintended data loss: record count changes are explained in the cleaning log
- Flagged records that could not be resolved are documented with a disposition (hold, drop, escalate)

## Failure Handling

| Failure | Response |
|---------|----------|
| Geometry cannot be repaired automatically | Flag for manual review; do not drop without approval |
| Required field cannot be derived or filled | Escalate to data owner or return to Stage 1 if source data is absent |
| Duplicate resolution is ambiguous | Flag duplicates; apply documented priority rules or escalate |
| Cleaning introduces new validation failures | Re-run Stage 3 validation rules against cleaned output before advancing |
| Volume of issues exceeds threshold for automated cleaning | Halt and escalate; systematic issues may indicate a Stage 2 processing problem |
