# Stage 6: Data Analysis

Query, model, and extract insights from ingested geospatial data. This stage produces the analytical outputs that stakeholders will act on.

## Inputs

- Ingested dataset from Stage 5
- Analysis specification (questions to answer, metrics to compute, models to apply)
- Reference or comparison datasets (historical baselines, thresholds, external benchmarks)
- Analysis environment configuration (tools, libraries, compute resources)

## Outputs

- Analysis results in a reproducible, documented form:
  - Computed metrics and statistics
  - Derived layers or features (e.g., change detection polygons, classified zones, interpolated surfaces)
  - Model outputs with accuracy assessments where applicable
- Analysis documentation including:
  - Methods and parameters used
  - Software and version
  - Input dataset versions and query/filter criteria applied
  - Assumptions and limitations
  - Reproducibility notes (queries, scripts, or workflow definitions)
- Intermediate outputs retained if they have standalone value for stakeholders

## QA Criteria

- Results are reproducible: re-running the analysis with the same inputs produces the same outputs (within numerical tolerance)
- Metrics are traceable to the ingested data (no undocumented external data introduced)
- Spatial operations used the correct CRS; results are in the expected CRS
- Derived layers do not contain geometry errors
- Edge cases are handled and documented (null values, empty areas, out-of-range inputs)
- Accuracy assessment is complete for any predictive or classification model
- Results have been sanity-checked against known reference areas or historical values

## Failure Handling

| Failure | Response |
|---------|----------|
| Results fail sanity check | Investigate query logic, CRS handling, and input data quality before delivering |
| Model accuracy below threshold | Document accuracy, adjust methodology, or note limitation explicitly in outputs |
| Analysis is not reproducible | Identify non-deterministic steps; fix or document the source of variance |
| Insufficient data coverage for requested analysis | Document the gap; deliver partial results with explicit coverage caveats |
| Performance too slow for required turnaround | Optimize queries or scale compute; document if results must be delivered incrementally |
