# 🏛️ HYPERCAST: Technical Architecture

Welcome to the technical backbone of **Hypercast** (PS 26077 - Team ARISHEM). This document provides a deep dive into our methodology, data flow, and the technology stack powering our AI-Driven Hyper-Local Early Warning System.

---

## 🌊 1. System Pipeline & Data Flow

Our architecture is designed for speed and precision, processing live satellite imagery and historical weather data through a spatiotemporal transformer to predict multiple hazards simultaneously.

```mermaid
flowchart LR
    %% Theming
    classDef input fill:#e1f5fe,stroke:#0288d1,stroke-width:2px,color:#000;
    classDef process fill:#e8f5e9,stroke:#388e3c,stroke-width:2px,color:#000;
    classDef ai fill:#ede7f6,stroke:#673ab7,stroke-width:3px,color:#000;
    classDef output fill:#fff3e0,stroke:#f57c00,stroke-width:2px,color:#000;

    subgraph INPUT ["📥 1. DATA INPUTS"]
        direction TB
        A["🛰️ INSAT-3D/3DR<br/>(Live Satellite)"]:::input
        B["🌦️ IMDAA Reanalysis<br/>(Moisture & Wind)"]:::input
        C["🌧️ QPE Estimates<br/>(Rainfall)"]:::input
        D["⛰️ CartoDEM<br/>(Terrain & Slopes)"]:::input
    end

    subgraph PROCESSING ["⚙️ 2. PROCESSING & AI CORE"]
        direction TB
        F["🔄 Data Fusion & Alignment<br/>(Grid & Timestamp Sync)"]:::process
        
        subgraph FE ["🔍 Feature Engine (Storm Signs)"]
            direction LR
            G["Moisture"]:::process
            H["Instability"]:::process
            I["Wind Shear"]:::process
            J["Cloud Cooling"]:::process
        end
        
        K{"🧠 Multi-Task Spatiotemporal Transformer<br/>(Predicts: Storm, Cloudburst, Flood)"}:::ai
        
        L["💡 XAI Reasoning<br/>(Names the trigger)"]:::process
        M["🗺️ DEM Terrain Overlay<br/>(Maps ground impact)"]:::process
    end

    subgraph OUTPUT ["📤 3. ACTIONABLE OUTPUTS"]
        direction TB
        N["📍 Hazard Risk Maps<br/>(Grid-level)"]:::output
        O["💻 Web GIS Dashboard<br/>(Live Monitoring)"]:::output
        P["📲 REST API Alerts<br/>(2-6h Warning)"]:::output
    end

    %% Routing
    A & B & C --> F
    F --> FE
    FE --> K
    D --> M
    K --> L & M
    L & M --> N & O & P
```

## 🛠️ 2. Technology Stack

We have selected a robust, scalable, and open-source heavy stack to ensure feasibility and low-cost deployment.

| Category | Technologies Used | Purpose |
| :--- | :--- | :--- |
| **📡 Data Sources** | **INSAT-3D/3DR (MOSDAC)** | Live satellite imagery tracking rapid cloud-top cooling. |
| | **IMDAA Reanalysis** | Historical and current weather metrics (moisture, wind). |
| | **QPE & CartoDEM / SRTM** | Rainfall estimates and terrain elevation mapping. |
| **🧠 AI & ML Core** | **Spatiotemporal Transformer**| The primary backbone model learning linked hazard patterns. |
| | **Tree-based Baseline** | Fallback model for early validation and low-compute edge cases. |
| | **SHAP-style XAI** | Explainable AI reasoning to build trust in generated alerts. |
| **⚙️ Backend System**| **Python / Node.js** | Core data processing pipeline and fast API serving. |
| | **PostgreSQL + PostGIS** | Storing spatial data, risk grids, and geographic JSON (GeoJSON). |
| **💻 Frontend & UX** | **React.js + Leaflet/Mapbox**| Web GIS dashboard for live risk layer visualization. |
| | **REST API & Push Services** | Categorized warning delivery to First Responders & Authorities. |
| **☁️ Deployment** | **Cloud GPU Training** | Training the transformer on historical flood data (e.g., Aug 2023). |
| | **Edge / Cloud Inference** | Real-time, fast predictions based on incoming live data feeds. |

---
*Architected for speed, precision, and explainability.*
