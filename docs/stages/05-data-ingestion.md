# Stage 5: Data Ingestion

Load cleaned, validated data into the target storage system. This stage transitions data from file-based workflow outputs into queryable, persistent storage.

## Inputs

- Cleaned data files from Stage 4
- Cleaning log and manifest from Stage 4
- Target storage configuration (connection, schema/database, layer or table names, spatial index settings)
- Ingestion rules (upsert vs. append vs. replace, partition keys, indexing strategy)

## Outputs

- Data loaded and accessible in the target storage system
- Ingestion report including:
  - Target system and layer/table names
  - Record counts: expected vs. loaded
  - Ingestion timestamp
  - Spatial index status
  - Any records rejected during load with reasons
- Updated lineage record linking the ingested dataset to its source capture and processing run

## QA Criteria

- Record count in target matches the expected count from the manifest (accounting for any documented drops)
- Spatial index is built and functional
- A sample query against the ingested data returns correct results (spot-check geometry and attributes)
- No records were silently truncated (attribute values, coordinate precision)
- Ingestion is idempotent: re-running with the same manifest does not create duplicates
- Lineage record is complete and references Stage 1 capture metadata

## Failure Handling

| Failure | Response |
|---------|----------|
| Record count mismatch | Identify missing or extra records; do not mark ingestion complete until resolved |
| Load rejected records | Log rejected records with rejection reason; assess whether they require Stage 4 cleaning |
| Connection or write failure | Retry with backoff; if persistent, escalate to infrastructure team |
| Coordinate precision loss on load | Verify target column types support required precision; correct schema and reload |
| Duplicate records created | Roll back ingestion; review ingestion rules and idempotency mechanism |
| Spatial index build fails | Investigate storage system error; do not advance to Stage 6 without a functional index |
