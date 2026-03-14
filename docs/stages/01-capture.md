# Stage 1: Capture

Acquire raw imagery and sensor data from drone flights. This is the entry point of the pipeline.

## Inputs

- Flight plan and mission parameters (area of interest, altitude, overlap/sidelap, sensor type, GSD target)
- Drone and sensor configuration record (make, model, firmware version, sensor calibration data)
- Capture metadata template (fields required for downstream stages)

## Outputs

- Raw data files in source-native format (e.g., JPEG/TIFF imagery, raw LiDAR scans, multispectral bands per channel)
- Capture metadata record including:
  - Drone make/model and sensor type
  - Capture timestamp and time zone
  - Coordinate reference system (CRS) as declared by the source
  - Flight parameters (altitude, speed, overlap/sidelap achieved)
  - Coverage extent (bounding box or polygon)
  - File manifest with checksums

## QA Criteria

- All files in the manifest are present and checksums match
- Capture metadata record is complete (no required fields missing)
- Coverage extent matches the requested area of interest within tolerance
- Achieved overlap/sidelap meets the minimums specified in the flight plan
- Timestamps are present and fall within the expected capture window
- No duplicate captures of the same area/time unless intentional

## Failure Handling

| Failure | Response |
|---------|----------|
| Missing files or checksum mismatch | Flag for re-transfer or re-capture; do not advance to Stage 2 |
| Coverage gap in area of interest | Log gap extent; determine whether re-flight is required before proceeding |
| Overlap/sidelap below minimum | Assess whether the processing engine can reconstruct from available data; re-fly affected strips if not |
| Metadata incomplete | Attempt to derive missing fields from EXIF/XMP headers; if unresolvable, halt and request clarification |
| Flight interrupted or aborted mid-mission | Log coverage achieved; determine whether partial dataset is sufficient or re-flight is required |
