# Flight Plan Template

Complete this template before every mission. This document is a required input for Stage 1 (Capture) and is referenced throughout the pipeline.

---

**Project:**
**Mission ID / Date:**
**Pilot:**
**Reviewer / Approver:**

---

## Area of Interest

| Field | Value |
|-------|-------|
| Site name | |
| Site description | |
| Bounding coordinate — North bound | |
| Bounding coordinate — South bound | |
| Bounding coordinate — East bound | |
| Bounding coordinate — West bound | |
| Area of interest file (KML/GeoJSON) | |
| Known hazards or restricted zones | |

---

## Mission Parameters

| Parameter | Target | Minimum Acceptable |
|-----------|--------|--------------------|
| Flight altitude (AGL) | | |
| Ground sampling distance (GSD) | | |
| Frontal overlap | | |
| Side overlap (sidelap) | | |
| Flight speed | | |
| Capture mode (nadir / oblique / both) | | |

---

## Sensor Configuration

| Field | Value |
|-------|-------|
| Drone make / model | |
| Firmware version | |
| Sensor type (RGB / multispectral / LiDAR / thermal) | |
| Sensor make / model | |
| Calibration date | |
| Calibration record reference | |

---

## Coordinate Reference System

| Field | Value |
|-------|-------|
| Target CRS (EPSG code) | |
| Declared CRS of drone GPS | |
| GCPs used (yes / no) | |
| GCP reference file | |
| Required positional accuracy (RMSE threshold) | |

---

## Capture Metadata Requirements

List all fields required in the capture metadata record for this mission. These fields must be present in the Stage 1 output or the dataset will not advance.

- [ ] Drone make / model and firmware version
- [ ] Sensor type and calibration reference
- [ ] Capture timestamp and time zone
- [ ] Declared CRS
- [ ] Flight altitude achieved (AGL)
- [ ] Overlap / sidelap achieved
- [ ] Coverage extent (bounding box or polygon)
- [ ] File manifest with checksums
- [ ] GCP reference (if applicable)

**Additional required fields for this mission:**

---

## Pre-Flight Checklist

- [ ] Area of interest file loaded and verified in mission planning software
- [ ] Airspace authorization confirmed (FAA LAANC or waiver, if required)
- [ ] Weather conditions within acceptable limits
- [ ] Drone and sensor inspected and calibrated
- [ ] Battery levels confirmed
- [ ] GCPs placed and coordinates recorded (if required)
- [ ] Emergency procedures reviewed

---

## Notes

