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
- [ ] Capture metadata record complete (source, timestamp, CRS, sensor, extent)
- [ ] Coverage extent matches area of interest
- [ ] Capture timestamps fall within expected window
- [ ] No unintended duplicate captures

**Advisory notes:**

---

## Stage 2: Data Processing

- [ ] Output files open without errors
- [ ] Output CRS matches target CRS
- [ ] Spatial extent consistent with Stage 1 capture extent
- [ ] Output resolution / point density meets target
- [ ] Processing report present and references input manifest
- [ ] No data voids in areas with complete input coverage

**Advisory notes:**

---

## Stage 3: Data Validation

- [ ] All validation rules have a recorded result
- [ ] All blocking rules passed (or exceptions formally documented and approved)
- [ ] No geometry errors (self-intersections, null geometries, invalid coordinates)
- [ ] Attribute schema matches expected schema (fields, types, domains)
- [ ] Positional accuracy meets specified tolerance
- [ ] Coverage meets minimum threshold

**Decision:** `[ ] Pass` &nbsp; `[ ] Conditional Pass` &nbsp; `[ ] Fail — route to Stage ___`

**Advisory notes:**

---

## Stage 4: Data Cleaning

- [ ] All geometry errors from Stage 3 report are resolved
- [ ] Attribute values conform to target schema
- [ ] No duplicate features
- [ ] Coordinate values within valid range for target CRS
- [ ] Cleaning log accounts for every issue flagged in Stage 3
- [ ] Record count changes explained in cleaning log
- [ ] Unresolvable records flagged with disposition (hold / drop / escalate)

**Advisory notes:**

---

## Stage 5: Data Ingestion

- [ ] Record count in target matches expected count from manifest
- [ ] Spatial index built and functional
- [ ] Spot-check query returns correct geometry and attributes
- [ ] No attribute truncation or coordinate precision loss
- [ ] Re-run with same manifest does not create duplicates
- [ ] Lineage record complete (references Stage 1 capture metadata)

**Advisory notes:**

---

## Stage 6: Data Analysis

- [ ] Results are reproducible with same inputs
- [ ] All inputs are traceable (no undocumented external data)
- [ ] Spatial operations used correct CRS; results in expected CRS
- [ ] Derived layers have no geometry errors
- [ ] Edge cases handled and documented
- [ ] Results sanity-checked against reference areas or historical values
- [ ] Model accuracy assessment complete (if applicable)

**Advisory notes:**

---

## Stage 7: Stakeholder Delivery

- [ ] All requested artifacts present and match delivery specification
- [ ] Artifacts open correctly in stakeholder tools
- [ ] Spatial exports in stakeholder-specified CRS
- [ ] Access controls applied and verified
- [ ] Metadata and attribution included in all deliverables
- [ ] Known limitations communicated in delivery package
- [ ] Delivery confirmation received from stakeholders
- [ ] All stage outputs and logs archived
- [ ] Complete lineage record filed

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
