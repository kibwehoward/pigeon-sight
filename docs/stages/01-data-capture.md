# Stage 1: Data Capture

Acquire raw geospatial data from the source. This is the entry point of the pipeline.

## Inputs

- Mission parameters or data request specification (area of interest, resolution, sensor type, timing)
- Access credentials or permissions for external sources (APIs, portals, file transfers)
- Capture metadata template (fields required for downstream stages)

## Outputs

- Raw data files in source-native format (e.g., images, point clouds, vector files, raster tiles)
- Capture metadata record including:
  - Source identifier and type
  - Capture timestamp and time zone
  - Coordinate reference system (CRS) as declared by the source
  - Sensor/instrument type and configuration
  - Coverage extent (bounding box or polygon)
  - File manifest with checksums

## QA Criteria

- All files in the manifest are present and checksums match
- Capture metadata record is complete (no required fields missing)
- Coverage extent matches the requested area of interest within tolerance
- Timestamps are present and fall within the expected capture window
- No duplicate captures of the same area/time unless intentional

## Failure Handling

| Failure | Response |
|---------|----------|
| Missing files or checksum mismatch | Flag for re-transfer or re-capture; do not advance to Stage 2 |
| Coverage gap in area of interest | Log gap extent; determine whether re-capture is required before proceeding |
| Metadata incomplete | Attempt to derive missing fields from file headers; if unresolvable, halt and request clarification |
| External source unavailable | Log outage, retry per source SLA; escalate if delay exceeds threshold |
