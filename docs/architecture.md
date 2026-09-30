# 🏛️ HYPERCAST: System Architecture

HYPERCAST is designed to ingest multi-modal, asynchronous weather data, align it into a single spatiotemporal grid, extract thermodynamic features, and run a multi-task AI model to predict Thunderstorms, Cloudbursts, and Flash Floods simultaneously.

---



```mermaid
flowchart TD
    %% Neon Dark Theme Styling with Font Size for Readability
    classDef data fill:#0d1117,stroke:#58a6ff,stroke-width:2px,color:#58a6ff,rx:10,ry:10,font-size:16px;
    classDef engine fill:#0d1117,stroke:#3fb950,stroke-width:2px,color:#3fb950,rx:10,ry:10,font-size:16px;
    classDef ai fill:#1f6feb,stroke:#58a6ff,stroke-width:3px,color:#ffffff,rx:15,ry:15,font-weight:bold,font-size:16px;
    classDef aiFallback fill:#0d1117,stroke:#8957e5,stroke-width:2px,color:#8957e5,rx:15,ry:15,stroke-dasharray: 5 5,font-size:14px;
    classDef hazard fill:#0d1117,stroke:#ff7b72,stroke-width:2px,color:#ff7b72,rx:5,ry:5,font-size:16px;
    classDef context fill:#0d1117,stroke:#d29922,stroke-width:2px,color:#d29922,rx:8,ry:8,font-size:16px;
    classDef action fill:#238636,stroke:#3fb950,stroke-width:3px,color:#ffffff,rx:20,ry:20,font-weight:bold,font-size:16px;
    classDef hub fill:#0d1117,stroke:#8b949e,stroke-width:1px,color:#8b949e,rx:50,ry:50,font-size:14px;

    subgraph S1 ["🛰️ 1. INGESTION"]
        direction LR
        A["INSAT-3D/3DR"]:::data
        B["IMDAA Reanalysis"]:::data
        C["QPE Radar"]:::data
        D["CartoDEM (ISRO)"]:::data
    end

    subgraph S2 ["⚙️ 2. FUSION PIPELINE"]
        direction LR
        E["Ingestion Service"]:::engine
        F["Temporal Sync"]:::engine
        G["Grid Alignment"]:::engine
        E --> F --> G
    end

    subgraph S3 ["🔍 3. METRICS"]
        direction LR
        H["Moisture / IWV"]:::engine
        I["Instability (CAPE)"]:::engine
        J["Lift & Shear"]:::engine
        K["Cloud Cooling"]:::engine
    end

    %% Hub to group features
    FV(("Feature\nVector")):::hub

    subgraph S4 ["🧠 4. AI CORE"]
        direction LR
        M{"Multi-Task\nTransformer"}:::ai
        L{"XGBoost\n(Fallback)"}:::aiFallback
    end

    subgraph S5 ["⚠️ 5. PREDICTION"]
        direction LR
        N["Thunderstorm"]:::hazard
        O["Cloudburst"]:::hazard
        P["Flash Flood"]:::hazard
    end

    %% Hub to group predictions
    PV(("Risk\nOutput")):::hub

    subgraph S6 ["💡 6. CONTEXT"]
        direction LR
        Q["SHAP Trigger"]:::context
        R["Terrain Overlay"]:::context
    end

    subgraph S7 ["🚀 7. DISSEMINATION"]
        direction LR
        S(("REST API\n(Backend)")):::action
        T(("GIS Dashboard\n(Frontend)")):::action
        U(("Alert Signals\n(SDMA/SMS)")):::action
    end

    A & B & C --> E
    G --> H & I & J & K
    
    H & I & J & K --> FV
    
    FV ==> M
    FV -.-> L
    
    M ==> N & O & P
    L -.-> N & O & P
    
    N & O & P --> PV
    
    PV --> Q & R
    D --> R
    
    Q & R --> S
    S --> T & U
```

---

## 3. Component Breakdown

### 3.1 Data Ingestion & Fusion
Because data sources operate on different frequencies (e.g., INSAT images every 15-30 mins, Reanalysis every hour), the **Fusion Pipeline** uses temporal interpolation to normalize data to a single unified timestamp. Geospatial alignment projects this onto a high-resolution Cartesian grid covering the target region (e.g., Himachal Pradesh).

### 3.2 Spatiotemporal AI Core
- **Multi-Task Transformer (Primary):** Designed to handle both temporal sequences (how a cloud cools over time) and spatial relationships (how a storm moves across a grid). It is trained using a multi-task loss function to predict three interconnected hazards simultaneously.
- **XGBoost (Fallback):** A computationally lightweight tree-based ensemble model used to validate features during initial development and serve as a fail-safe in resource-constrained environments.

### 3.3 Explainable AI (XAI) Context Layer
The system employs **SHAP-style explainability** to break the "black box" of AI. When a flash flood alert is triggered, the system explicitly flags the dominant feature (e.g., "Trigger: Rapid Cloud-Top Cooling + Saturated Soil"). This transparency is critical for disaster authorities to trust the system.

### 3.4 Terrain Impact Mapping
While atmospheric models predict *where* it will rain, terrain models dictate *where* it will flood. The **Terrain Overlay** merges atmospheric risk probabilities with CartoDEM topographical data to highlight specific high-risk slopes, valleys, and river channels.

---

## 4. Software Stack

| Layer | Technologies |
| :--- | :--- |
| **Backend & APIs** | Python (FastAPI), Node.js |
| **Data Processing** | Pandas, GeoPandas, Xarray, GDAL |
| **AI / Machine Learning** | PyTorch (Transformer), XGBoost, SHAP |
| **Database** | PostgreSQL with PostGIS extension |
| **Frontend UI** | React.js, Leaflet / Mapbox GL JS |
| **Cloud Infrastructure** | Docker, Kubernetes (Proposed for scale) |
