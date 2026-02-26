# Stage 5: Data Ingestion

Load cleaned, validated drone data into the target storage system. This stage transitions data from file-based workflow outputs into queryable, persistent storage. The reference implementation uses **PostGIS** as the spatial database.

## Inputs

- Cleaned data files from Stage 4
- Cleaning log and manifest from Stage 4
- Target storage configuration (PostGIS connection, schema/database, layer or table names, spatial index settings)
- Ingestion rules (upsert vs. append vs. replace, partition keys, indexing strategy)

## Outputs

- Data loaded and accessible in PostGIS (vectors via ogr2ogr/QGIS; rasters via raster2pgsql or file-referenced catalog)
- Ingestion report including:
  - Target schema and table/layer names
  - Record or tile counts: expected vs. loaded
  - Ingestion timestamp
  - Spatial index status
  - Any records or tiles rejected during load with reasons
- Updated lineage record linking the ingested dataset to its source capture and WebODM processing run

## QA Criteria

- Record count in PostGIS matches the expected count from the manifest (accounting for any documented drops)
- Spatial index is built and functional (verify with EXPLAIN ANALYZE on a sample query)
- A sample query in QGIS against the ingested data returns correct results (spot-check geometry and attributes)
- No attributes were silently truncated (field lengths, coordinate precision)
- Ingestion is idempotent: re-running with the same manifest does not create duplicates
- Lineage record is complete and references Stage 1 capture metadata and Stage 2 WebODM task ID

## Failure Handling

| Failure | Response |
|---------|----------|
| Record count mismatch | Identify missing or extra records; do not mark ingestion complete until resolved |
| Load rejected records or tiles | Log rejected items with rejection reason; assess whether they require Stage 4 cleaning |
| PostGIS connection or write failure | Retry with backoff; if persistent, escalate to infrastructure team |
| Coordinate precision loss on load | Verify PostGIS column types and SRID support required precision; correct schema and reload |
| Duplicate records created | Roll back ingestion; review ingestion rules and idempotency mechanism |
| Spatial index build fails | Investigate PostGIS error; do not advance to Stage 6 without a functional spatial index |
