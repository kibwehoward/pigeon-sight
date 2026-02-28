# QA Checklist

Use this checklist at each pipeline stage gate. Complete all blocking items before advancing. Document any advisory items in the stage report.

---

**Project:**
**Dataset:**
**Run ID / Date:**
**Reviewer:**

---

## Stage 1: Data Capture

- [ ] All files in manifest are present
- [ ] Checksums verified for all files
- [ ] Capture metadata record complete (drone/sensor, timestamp, CRS, flight parameters, extent)
- [ ] Coverage extent matches area of interest
- [ ] Achieved overlap/sidelap meets minimums specified in flight plan
- [ ] Capture timestamps fall within expected window
- [ ] No unintended duplicate captures

**Advisory notes:**

---

## Stage 2: Data Processing (WebODM)

- [ ] WebODM task completed without errors; task ID recorded
- [ ] Orthomosaic opens without errors in QGIS
- [ ] Output CRS matches target CRS
- [ ] Spatial extent consistent with Stage 1 capture extent
- [ ] Orthomosaic GSD meets target resolution
- [ ] Point cloud density meets target for intended analysis
- [ ] Processing report present and references input manifest
- [ ] GCP residuals within acceptable threshold (if GCPs used)
- [ ] No data voids in areas with complete input coverage

**Advisory notes:**

---

## Stage 3: Data Validation

- [ ] All validation rules have a recorded result
- [ ] All blocking rules passed (or exceptions formally documented and approved)
- [ ] GSD confirmed against flight plan target
- [ ] Point cloud density confirmed against minimum threshold
- [ ] Output CRS consistent across all products (orthomosaic, DSM/DTM, point cloud)
- [ ] Positional accuracy meets specified tolerance (RMSE vs. check points, if assessed)
- [ ] No data voids in coverage area
- [ ] Coverage meets minimum threshold for area of interest

**Decision:** `[ ] Pass` &nbsp; `[ ] Conditional Pass` &nbsp; `[ ] Fail — route to Stage ___`

**Advisory notes:**

---

## Stage 4: Data Cleaning

- [ ] Orthomosaic voids filled or masked; no artifacts at fill boundaries
- [ ] Point cloud noise filtered; ground classification complete across full extent
- [ ] DSM/DTM values within physically plausible range for surveyed area
- [ ] Coordinate values within valid range for target CRS
- [ ] Cleaning log accounts for every issue flagged in Stage 3
- [ ] Coverage changes explained in cleaning log
- [ ] Unresolvable areas flagged with disposition (hold / mask / escalate)

**Advisory notes:**

---

## Stage 5: Data Ingestion (PostGIS)

- [ ] Record or tile count in PostGIS matches expected count from manifest
- [ ] Spatial index built and functional (verified with sample query)
- [ ] Spot-check in QGIS returns correct geometry and attributes
- [ ] No attribute truncation or coordinate precision loss
- [ ] Re-run with same manifest does not create duplicates
- [ ] Lineage record complete (references Stage 1 capture metadata and Stage 2 WebODM task ID)

**Advisory notes:**

---

## Stage 6: Data Analysis (QGIS / Python)

- [ ] Results are reproducible with same inputs (SQL, QGIS project, or Python script retained)
- [ ] All inputs are traceable (no undocumented external data)
- [ ] Spatial operations used correct CRS; results in expected CRS
- [ ] Derived layers have no geometry errors
- [ ] Edge cases handled and documented (masked areas, null values, out-of-range raster inputs)
- [ ] Results sanity-checked against ground truth, reference areas, or historical flight values
- [ ] Model accuracy assessment complete (if applicable)

**Advisory notes:**

---

## Stage 7: Stakeholder Delivery (GeoServer / QGIS)

- [ ] All requested artifacts present and match delivery specification
- [ ] Artifacts open correctly in stakeholder tools
- [ ] GeoServer services return correct data and render without errors (if applicable)
- [ ] Spatial exports in stakeholder-specified CRS
- [ ] Access controls applied and verified
- [ ] Metadata and attribution included in all deliverables
- [ ] Known limitations from Stage 6 communicated in delivery package
- [ ] Delivery confirmation received from stakeholders
- [ ] All stage outputs and logs archived
- [ ] Complete lineage record filed (capture → WebODM → PostGIS → analysis → delivery)

**Advisory notes:**

---

## Sign-off

| Stage | Reviewer | Date | Result |
|-------|----------|------|--------|
| 1 — Data Capture | | | |
| 2 — Data Processing | | | |
| 3 — Data Validation | | | |
| 4 — Data Cleaning | | | |
| 5 — Data Ingestion | | | |
| 6 — Data Analysis | | | |
| 7 — Stakeholder Delivery | | | |
