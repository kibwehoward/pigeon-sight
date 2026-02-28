# PigeonSight Workflow Diagram

```mermaid
flowchart TD
    CAP["**1. Data Capture**\nAcquire raw drone imagery & sensor data"]
    PRO["**2. Data Processing**\nWebODM → orthomosaic, point cloud, DSM/DTM"]
    VAL{"**3. Data Validation**\nQA/QC Gate"}
    CLN["**4. Data Cleaning**\nVoid fill, noise filter, ground classify"]
    ING["**5. Data Ingestion**\nLoad to PostGIS"]
    ANA["**6. Data Analysis**\nQGIS / Python (GeoPandas, Rasterio, PDAL)"]
    DEL["**7. Stakeholder Delivery**\nGeoServer / QGIS layouts / data exports"]

    CAP --> PRO
    PRO --> VAL

    VAL -->|"✓ Pass"| CLN
    VAL -->|"✗ Coverage gap\n(re-flight needed)"| CAP
    VAL -->|"✗ WebODM artifact\nor CRS error"| PRO
    VAL -->|"✗ Schema / geometry\nerrors"| CLN

    CLN --> ING
    ING --> ANA
    ANA --> DEL

    DEL -->|"Rejected — analysis issue"| ANA
    DEL -->|"Rejected — data issue"| VAL

    style CAP fill:#1a1a2e,color:#fff,stroke:#4a9eff
    style PRO fill:#1a1a2e,color:#fff,stroke:#4a9eff
    style VAL fill:#2d1b00,color:#fff,stroke:#ff9900
    style CLN fill:#1a1a2e,color:#fff,stroke:#4a9eff
    style ING fill:#1a1a2e,color:#fff,stroke:#4a9eff
    style ANA fill:#1a1a2e,color:#fff,stroke:#4a9eff
    style DEL fill:#0d2b0d,color:#fff,stroke:#4caf50
```

## Routing Rules

- Stages advance only when all **blocking** QA criteria are met.
- Failures route back to the **earliest stage** where the root cause can be fixed — not necessarily the prior stage.
- The **Validation gate** (Stage 3) is the primary checkpoint. It can route back to Stage 1 (re-flight) or Stage 2 (reprocess in WebODM) depending on the failure type, or forward to Stage 4 for issues that cleaning can resolve.
- **Advisory** findings are documented but do not block progression.
