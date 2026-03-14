# QA Checklist

Use this checklist at each pipeline stage gate. Complete all blocking items before advancing. Document any advisory items in the stage report.

---

**Project:**
**Dataset:**
**Run ID / Date:**
**Reviewer:**

---

## Stage 1: Capture

- [ ] All files in manifest are present
- [ ] Checksums verified for all files
- [ ] Capture metadata record complete (drone/sensor, timestamp, CRS, flight parameters, extent)
- [ ] Coverage extent matches area of interest
- [ ] Achieved overlap/sidelap meets minimums specified in flight plan
- [ ] Capture timestamps fall within expected window
- [ ] No unintended duplicate captures

**Advisory notes:**

---

## Stage 2: Processing

- [ ] Processing task completed without errors; task ID recorded
- [ ] Output files open without errors in a compatible GIS application
- [ ] Output CRS matches target CRS
- [ ] Spatial extent consistent with Stage 1 capture extent
- [ ] Orthomosaic GSD meets target resolution
- [ ] Point cloud density meets target for intended analysis
- [ ] Processing report present and references input manifest
- [ ] GCP residuals within acceptable threshold (if GCPs used)
- [ ] No data voids in areas with complete input coverage

**Advisory notes:**

---

## Stage 3: Validation

- [ ] All validation rules have a recorded result
- [ ] All blocking rules passed
- [ ] GSD confirmed against flight plan target
- [ ] Point cloud density confirmed against minimum threshold
- [ ] Output CRS consistent across all products (orthomosaic, DSM/DTM, point cloud)
- [ ] Positional accuracy meets specified tolerance (RMSE vs. check points, if assessed)
- [ ] No data voids in coverage area
- [ ] Coverage meets minimum threshold for area of interest

**Decision:** `[ ] Pass` &nbsp; `[ ] Fail — route to Stage ___`

**Advisory notes:**

---

## Stage 4: Cleaning

- [ ] Orthomosaic voids filled or masked; no artifacts at fill boundaries
- [ ] Point cloud noise filtered; ground classification complete across full extent
- [ ] DSM/DTM values within physically plausible range for surveyed area
- [ ] Coordinate values within valid range for target CRS
- [ ] Cleaning log accounts for every issue flagged in Stage 3
- [ ] Coverage changes explained in cleaning log
- [ ] Unresolvable areas flagged with disposition (hold / mask / escalate)

**Advisory notes:**

---

## Stage 5: Ingestion

- [ ] Record or tile count in target storage matches expected count from manifest
- [ ] Spatial index built and functional (verified with sample query)
- [ ] Spot-check against ingested data returns correct geometry and attributes
- [ ] No attribute truncation or coordinate precision loss
- [ ] Re-run with same manifest does not create duplicates
- [ ] Lineage record complete (references Stage 1 capture metadata and Stage 2 processing task ID)

**Advisory notes:**

---

## Stage 6: Analysis

- [ ] Results are reproducible with same inputs (analysis scripts or project files retained)
- [ ] All inputs are traceable (no undocumented external data)
- [ ] Spatial operations used correct CRS; results in expected CRS
- [ ] Derived layers have no geometry errors
- [ ] Edge cases handled and documented (masked areas, null values, out-of-range raster inputs)
- [ ] Results sanity-checked against ground truth, reference areas, or historical flight values
- [ ] Model accuracy assessment complete (if applicable)
- [ ] Analysis documentation references Stage 3 validation report and carries forward any documented limitations

**Advisory notes:**

---

## Stage 7: Delivery

- [ ] All requested artifacts present and match delivery specification
- [ ] Artifacts open correctly in stakeholder tools
- [ ] Web services return correct data and render without errors (if applicable)
- [ ] Spatial exports in stakeholder-specified CRS
- [ ] Access controls applied and verified
- [ ] Metadata and attribution included in all deliverables
- [ ] Known limitations from Stage 6 communicated in delivery package
- [ ] Delivery confirmation received from stakeholders
- [ ] All stage outputs and logs archived
- [ ] Complete lineage record filed (capture → processing → validation → cleaning → ingestion → analysis → delivery)

**Advisory notes:**

---

## Sign-off

| Stage | Reviewer | Date | Result |
|-------|----------|------|--------|
| 1 — Capture | | | |
| 2 — Processing | | | |
| 3 — Validation | | | |
| 4 — Cleaning | | | |
| 5 — Ingestion | | | |
| 6 — Analysis | | | |
| 7 — Delivery | | | |
