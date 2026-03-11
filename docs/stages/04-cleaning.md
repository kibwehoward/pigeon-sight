# Stage 4: Data Cleaning

Normalize, repair, and transform validated drone data into a consistent, analysis-ready state. This stage resolves issues identified in Stage 3 and standardizes the dataset for ingestion.

## Inputs

- Processed data files from Stage 2
- Validation report from Stage 3 (identifies specific issues to address)
- Data dictionary / target schema (defines field names, types, domains, and encoding conventions)
- Transformation rules (coordinate conversions, unit normalizations, classification mappings)

## Outputs

- Cleaned data files conforming to the target schema:
  - Orthomosaic with voids filled or masked
  - Point cloud with noise filtered and ground points classified
  - DSM/DTM with artifacts removed and voids interpolated
  - Vector layers derived from raster products (if applicable)
- Cleaning log documenting every transformation applied:
  - Type of operation (void fill, noise filter, ground classification, reproject, reclassify, mask)
  - Files or areas affected
  - Parameters used (e.g., filter radius, classification thresholds)
  - Operator or automated rule that applied the change
- Updated file manifest with checksums
- Flagged areas that required manual review or could not be automatically resolved

## QA Criteria

- All issues identified in the validation report are resolved or formally documented as accepted exceptions
- Orthomosaic voids are filled or masked with no unintended artifacts introduced at fill boundaries
- Point cloud noise is filtered; ground classification covers the full extent
- DSM/DTM values are within physically plausible range for the surveyed area
- Coordinate values are within the valid range for the target CRS
- Cleaning log accounts for every issue flagged in the validation report
- No unintended data loss: coverage changes are explained in the cleaning log
- Flagged areas that could not be resolved are documented with a disposition (hold, mask, escalate)

## Failure Handling

| Failure | Response |
|---------|----------|
| Orthomosaic void cannot be filled acceptably | Mask the void and document extent; flag for re-flight if area is critical to the analysis |
| Point cloud noise or artifacts are systematic, not isolated | Escalate to Stage 2; systematic artifacts indicate a processing problem rather than a cleaning task |
| Ground classification fails over complex terrain | Adjust PDAL/CloudCompare classification parameters; document parameter choices in cleaning log |
| Cleaning introduces new validation failures | Re-run Stage 3 validation rules against cleaned output before advancing |
| Volume of issues exceeds threshold for automated cleaning | Halt and escalate; systematic issues may indicate a Stage 2 processing problem |
