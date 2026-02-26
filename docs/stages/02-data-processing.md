# Stage 2: Data Processing

Transform raw captured data into analysis-ready formats. This stage handles reconstruction, projection, tiling, and format conversion.

## Inputs

- Raw data files from Stage 1
- Capture metadata record from Stage 1
- Processing configuration (target CRS, output resolution, format, tiling scheme if applicable)
- Ground control points (GCPs) or reference data if georeferencing is required

## Outputs

- Processed geospatial files in target format (e.g., orthomosaic, classified point cloud, reprojected raster, normalized vector layer)
- Processing report including:
  - Software and version used
  - Processing parameters applied
  - Output CRS and resolution
  - Processing timestamp
  - Warnings or anomalies logged during processing
- Updated file manifest with checksums

## QA Criteria

- Output files open without errors in at least one standard GIS tool
- Output CRS matches the target CRS specified in the configuration
- Spatial extent of outputs is consistent with the capture extent from Stage 1
- Resolution or density meets the specified target (within acceptable tolerance)
- Processing report is present and references the input manifest
- No data voids in areas where input coverage was complete

## Failure Handling

| Failure | Response |
|---------|----------|
| Processing job fails or crashes | Capture full error log; retry with diagnostics enabled; escalate if persistent |
| Output resolution below target | Check input data quality; determine if re-capture or adjusted parameters can resolve |
| CRS mismatch in output | Reproject to target CRS; log the discrepancy and resolution |
| Data voids in output | Identify whether void originates from capture gap (return to Stage 1) or processing artifact (reprocess) |
| GCP accuracy insufficient | Review GCP placement and accuracy; reprocess with corrected GCPs |
