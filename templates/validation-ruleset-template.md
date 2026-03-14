# Validation Ruleset Template

Define project-specific thresholds and acceptance criteria before the mission begins. This document is a required input for Stage 3 (Validation). Thresholds should be established based on the intended analysis, stakeholder requirements, and applicable standards.

---

**Project:**
**Mission ID / Date:**
**Prepared by:**
**Approved by:**
**Ruleset version:**

---

## Orthomosaic Rules

| Rule | Threshold | Severity | Notes |
|------|-----------|----------|-------|
| Ground sampling distance (GSD) | ≤ ___ cm/px | Blocking | |
| No data voids in coverage area | 0% void in AOI | Blocking | |
| Output CRS | EPSG: ___ | Blocking | |
| Radiometric consistency (no visible seam artifacts) | Pass / Fail | Advisory | |

---

## Point Cloud Rules

| Rule | Threshold | Severity | Notes |
|------|-----------|----------|-------|
| Minimum point density | ≥ ___ pts/m² | Blocking | |
| Ground classification coverage | ≥ ___% of extent | Blocking | |
| Noise point percentage | ≤ ___% | Advisory | |
| Output CRS | EPSG: ___ | Blocking | |

---

## Digital Elevation Model (DSM/DTM) Rules

| Rule | Threshold | Severity | Notes |
|------|-----------|----------|-------|
| No data voids in coverage area | 0% void in AOI | Blocking | |
| Elevation value range (plausible for site) | ___ m to ___ m | Blocking | |
| Output CRS | EPSG: ___ | Blocking | |
| Vertical datum | | Blocking | |

---

## Positional Accuracy Rules

| Rule | Threshold | Severity | Notes |
|------|-----------|----------|-------|
| Horizontal RMSE (vs. check points) | ≤ ___ m | Blocking | Required if check points surveyed |
| Vertical RMSE (vs. check points) | ≤ ___ m | Blocking | Required if check points surveyed |
| GCP residuals | ≤ ___ m | Blocking | Required if GCPs used |
| Minimum number of check points | ≥ ___ | Blocking | |

---

## Coverage Rules

| Rule | Threshold | Severity | Notes |
|------|-----------|----------|-------|
| Coverage of area of interest | ≥ ___% | Blocking | |
| Maximum allowable gap size | ≤ ___ m² | Blocking | |
| Overlap/sidelap achieved | ≥ ___% / ___% | Blocking | |

---

## Metadata and Lineage Rules

| Rule | Threshold | Severity | Notes |
|------|-----------|----------|-------|
| Capture metadata record complete | All required fields present | Blocking | |
| Processing report present | Yes | Blocking | |
| File manifest with checksums present | Yes | Blocking | |
| Processing task ID recorded | Yes | Blocking | |

---

## Project-Specific Rules

Add any rules specific to this project, client, or regulatory requirement.

| Rule | Threshold | Severity | Notes |
|------|-----------|----------|-------|
| | | | |
| | | | |
| | | | |

---

## Ruleset Sign-off

| Field | Value |
|-------|-------|
| Prepared by | |
| Date | |
| Approved by | |
| Approval date | |
| Ruleset version | |

---

## Change Log

| Version | Date | Changed by | Summary of changes |
|---------|------|------------|--------------------|
| 1.0 | | | Initial version |
| | | | |
