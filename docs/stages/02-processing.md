# Stage 2: Processing

Transform raw drone imagery into analysis-ready geospatial products. This stage handles photogrammetric reconstruction, georeferencing, and output generation.

## Inputs

- Raw imagery and sensor data from Stage 1
- Capture metadata record from Stage 1
- Processing configuration:
  - Target CRS and output resolution
  - Processing engine task parameters (point cloud quality, mesh octree depth, orthomosaic resolution, feature extraction settings)
- Ground control points (GCPs) if enhanced positional accuracy is required

## Outputs

- Processed geospatial products in target format:
  - Orthomosaic (GeoTIFF)
  - Dense point cloud (LAS/LAZ)
  - Digital surface model / digital terrain model (DSM/DTM, GeoTIFF)
  - 3D mesh (optional, OBJ/PLY)
- Processing report including:
  - Processing task ID, software version, and parameters applied
  - Output CRS and resolution
  - Processing timestamp
  - GCP residuals (if GCPs were used)
  - Warnings or anomalies logged during processing
- Updated file manifest with checksums

## QA Criteria

- Output files open without errors in a compatible GIS application
- Output CRS matches the target CRS specified in the configuration
- Spatial extent of outputs is consistent with the capture extent from Stage 1
- Orthomosaic resolution (GSD) meets the specified target within acceptable tolerance
- Point cloud density meets expectations for the flight altitude and overlap achieved
- Processing report is present and references the input manifest
- No data voids in areas where input coverage was complete
- GCP residuals are within the acceptable accuracy threshold (if GCPs were used)

## Failure Handling

| Failure | Response |
|---------|----------|
| Processing task fails or crashes | Capture full task log; retry with diagnostics enabled; adjust processing parameters if systematic |
| Output resolution (GSD) below target | Check input overlap and altitude; determine if re-flight or adjusted parameters can resolve |
| CRS mismatch in output | Reproject to target CRS using available reprojection tools; log the discrepancy and resolution |
| Data voids in orthomosaic or point cloud | Identify whether void originates from coverage gap (return to Stage 1) or processing artifact (reprocess) |
| GCP accuracy insufficient | Review GCP placement and coordinate accuracy; reprocess with corrected GCPs |
