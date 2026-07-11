# PigeonSight Workflow Diagram

```mermaid
flowchart TD
    CAP["**1. Capture**
    Acquire raw drone imagery and sensor data"]
    PRO["**2. Processing**
    Transform raw inputs into orthomosaics,
    point clouds, and digital elevation models (DEMs)"]
    VAL{"**3. Validation**
    QA/QC Gate"}
    CLN["**4. Cleaning**
    Handle anomalies, normalize schemas,
    transform coordinates"]
    ING["**5. Ingestion**
    Load validated data into target storage systems"]
    ANA["**6. Analysis**
    Query, model, and extract insights"]
    DEL["**7. Delivery**
    Package and distribute results
    to stakeholders and end users"]

    P0["Pass"]
    R1["Re-flight"]
    R2["Reprocess"]
    R3["Schema / geometry errors"]
    R4["Data issue"]
    R5["Analysis issue"]

    CAP --> PRO
    PRO --> VAL
    VAL --> P0 --> CLN
    VAL --> R1 --> CAP
    VAL --> R2 --> PRO
    VAL --> R3 --> CLN
    CLN --> ING
    ING --> ANA
    ANA --> DEL
    DEL --> R4 --> VAL
    DEL --> R5 --> ANA

    style CAP fill:#1a1a2e,color:#fff,stroke:#4a9eff
    style PRO fill:#1a1a2e,color:#fff,stroke:#4a9eff
    style VAL fill:#2d1b00,color:#fff,stroke:#ff9900
    style CLN fill:#1a1a2e,color:#fff,stroke:#4a9eff
    style ING fill:#1a1a2e,color:#fff,stroke:#4a9eff
    style ANA fill:#1a1a2e,color:#fff,stroke:#4a9eff
    style DEL fill:#1a1a2e,color:#fff,stroke:#4a9eff
    style P0 fill:#0d2b0d,color:#fff,stroke:#4caf50
    style R1 fill:#2d2200,color:#fff,stroke:#ffcc00
    style R2 fill:#2d2200,color:#fff,stroke:#ffcc00
    style R3 fill:#2d2200,color:#fff,stroke:#ffcc00
    style R4 fill:#2d2200,color:#fff,stroke:#ffcc00
    style R5 fill:#2d2200,color:#fff,stroke:#ffcc00
```

## Routing Rules

- Stages advance only when all **blocking** QA criteria are met.
- Failures route back to the **earliest stage** where the root cause can be fixed — not necessarily the prior stage.
- **Pass** — All blocking QA criteria met; workflow advances to Cleaning
- **Re-flight** — Coverage gap detected; dataset is incomplete and requires a new flight
- **Reprocess** — Processing artifact or CRS error; raw imagery is valid but processing must be repeated
- **Schema / geometry errors** — Data can be corrected without reprocessing; routes to Cleaning
- **Data issue** — Delivery rejected due to upstream data quality; returns to Validation
- **Analysis issue** — Delivery rejected due to analytical error; returns to Analysis
- **Advisory** findings are documented but do not block progression
