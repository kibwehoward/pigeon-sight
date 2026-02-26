# Stage 7: Stakeholder Delivery

Package and distribute analysis results to end users in a form they can act on. This is the final stage of the pipeline.

## Inputs

- Analysis outputs from Stage 6
- Delivery specification:
  - Target audience and their technical capabilities
  - Required formats (interactive map, static report, data export, API, dashboard)
  - Access control requirements
  - Delivery deadline and method (portal, email, shared drive, API endpoint)
- Branding or formatting requirements

## Outputs

- Delivered artifacts in the stakeholder-specified format, which may include:
  - Interactive web map or dashboard
  - Static map products (PDF, PNG, printed layout)
  - Data exports (GeoPackage, Shapefile, CSV, GeoJSON, KML)
  - Written report with embedded maps and charts
  - API endpoint or data service
- Delivery confirmation record including:
  - Recipient(s) and delivery method
  - Artifact list with versions and checksums
  - Delivery timestamp
  - Access instructions provided to recipients
- Feedback record (if stakeholder review is part of the workflow)

## QA Criteria

- All requested artifacts are present and match the delivery specification
- Artifacts open correctly in the tools stakeholders are expected to use
- Spatial data exports are in the CRS specified by the stakeholder
- Access controls are applied correctly (correct users can access; unauthorized users cannot)
- Delivery confirmation record is complete
- Metadata and attribution are included in all deliverable files
- Any known limitations or caveats from Stage 6 are communicated clearly in the delivery package

## Failure Handling

| Failure | Response |
|---------|----------|
| Artifact fails to open or render correctly | Identify format compatibility issue; regenerate in compatible format before delivery |
| Access control misconfiguration | Revoke access, correct permissions, re-deliver; log the incident |
| Stakeholder rejects results (quality concern) | Determine whether issue is in the delivery presentation or in the underlying analysis; route back to Stage 6 or earlier as appropriate |
| Delivery deadline missed | Communicate proactively; deliver available artifacts with clear notation of what is pending |
| Stakeholder requests format not in original specification | Assess effort; deliver if minor, negotiate timeline if significant |

## Pipeline Completion

Delivery marks the end of a pipeline run. Before closing:

1. Confirm delivery receipt from stakeholders
2. Archive all stage outputs and logs with consistent naming and versioning
3. Record the complete lineage: capture → processing → validation → cleaning → ingestion → analysis → delivery
4. Document lessons learned or process improvement notes for future runs
