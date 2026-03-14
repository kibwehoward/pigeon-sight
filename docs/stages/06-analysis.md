# Stage 6: Analysis

Query, model, and extract insights from ingested drone data. This stage produces the analytical outputs that stakeholders will act on.

## Inputs

- Ingested datasets from Stage 5
- Analysis specification (questions to answer, metrics to compute, models to apply)
- Reference or comparison datasets (historical flight baselines, threshold surfaces, external benchmarks)
- Analysis environment configuration (software versions, libraries, extensions)

## Outputs

- Analysis results in a reproducible, documented form:
  - Computed metrics and statistics (e.g., volumes, areas, densities, spectral indices)
  - Derived layers (e.g., NDVI from multispectral imagery, canopy height model from DSM minus DTM, change detection polygons between flight epochs, cut/fill volumes)
  - Model outputs with accuracy assessments where applicable
- Analysis documentation including:
  - Methods and parameters used
  - Analysis scripts or project files used to produce results
  - Input dataset versions and query/filter criteria applied
  - Assumptions and limitations
  - Reproducibility notes (SQL queries, processing history, or workflow definitions)
  - Reference to the Stage 3 validation report, so limitations documented at the QA gate are traceable to the final deliverable
- Intermediate outputs retained if they have standalone value for stakeholders

## QA Criteria

- Results are reproducible: re-running the analysis with the same inputs produces the same outputs (within numerical tolerance)
- Metrics are traceable to the ingested data (no undocumented external data introduced)
- Spatial operations used the correct CRS; results are in the expected CRS
- Derived layers do not contain geometry errors
- Edge cases are handled and documented (null values, masked areas, out-of-range raster inputs)
- Accuracy assessment is complete for any predictive or classification model
- Results have been sanity-checked against known reference areas, ground truth, or historical flight values
- Analysis documentation references the Stage 3 validation report and carries forward any limitations or exceptions documented at the QA gate

## Failure Handling

| Failure | Response |
|---------|----------|
| Results fail sanity check | Investigate query logic, CRS handling, and input data quality before delivering |
| Model accuracy below threshold | Document accuracy, adjust methodology, or note limitation explicitly in outputs |
| Analysis is not reproducible | Identify non-deterministic steps; fix or document the source of variance |
| Insufficient data coverage for requested analysis | Document the gap; deliver partial results with explicit coverage caveats |
| Performance too slow for required turnaround | Optimize queries or switch to alternative processing approach; document if results must be delivered incrementally |
