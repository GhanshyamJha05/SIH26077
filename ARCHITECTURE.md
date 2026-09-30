# HYPERCAST: Technical Architecture

This document outlines the technical approach, methodology, and technology stack for Hypercast (PS 26077 - Team ARISHEM).

## Methodology and Process Flow

Our system operates in three main stages: Input, Processing, and Output.

```mermaid
graph TD
    classDef input fill:#e1f5fe,stroke:#0288d1,stroke-width:2px,color:#000;
    classDef process fill:#e8f5e9,stroke:#388e3c,stroke-width:2px,color:#000;
    classDef output fill:#fff3e0,stroke:#f57c00,stroke-width:2px,color:#000;

    subgraph INPUT ["1. INPUT (What we feed in)"]
        A[INSAT-3D/3DR Satellite<br/>Sees storm clouds growing fast]:::input
        B[IMDAA Reanalysis<br/>Air moisture, instability, wind]:::input
        C[QPE Rainfall Estimates<br/>Extreme intensity now]:::input
        D[DEM Terrain CartoDEM<br/>Slopes and river channels]:::input
        E[Past Event Records<br/>Aug 2023 Himachal floods]:::input
    end

    subgraph PROCESSING ["2. PROCESSING (How the system thinks)"]
        F[Align and fuse<br/>All data on one grid and one timestamp]:::process
        
        subgraph FeatureEngine ["Feature Engine: Storm Warning Signs"]
            G[Moisture IWV]:::process
            H[Instability CAPE/CIN]:::process
            I[Lift + wind shear]:::process
            J[Cloud-top cooling]:::process
        end
        
        K{Multi-task spatiotemporal transformer<br/>Thunderstorm | Cloudburst | Flash flood risk}:::process
        
        L[XAI reasoning<br/>Names the trigger]:::process
        M[DEM terrain overlay<br/>Maps ground impact]:::process
        
        F --> G & H & I & J
        G & H & I & J --> K
        K --> L
        K --> M
    end

    subgraph OUTPUT ["3. OUTPUT (What comes out)"]
        N[Hazard risk maps + reasons<br/>On a fine grid]:::output
        O[Web GIS dashboard<br/>Live risk layers, history]:::output
        P[REST API alerts<br/>Warnings 2-6 h before onset]:::output
    end

    A & B & C --> F
    D --> M
    E -.->|Used to train and test| K
    
    L --> N & O & P
    M --> N & O & P
```

## Technologies To Be Used

### DATA
*   **INSAT-3D/3DR (MOSDAC):** For live satellite imagery tracking cloud cooling.
*   **IMDAA reanalysis:** For historical and current weather metrics.
*   **QPE, CartoDEM / SRTM:** For rainfall estimates and terrain elevation.

### AI / ML
*   **Spatiotemporal transformer:** The core model that learns the linked hazards.
*   **Tree-based baseline:** Used for early validation and as a computationally light fallback.
*   **SHAP-style XAI:** Explainable AI reasoning to name the trigger for the alert.

### BACKEND
*   **Python / Node.js pipeline:** For data processing and API serving.
*   **PostgreSQL + GeoJSON:** For storing spatial data and grid information.

### FRONTEND + ALERTS
*   **React.js + GIS map layer:** For the web dashboard visualization.
*   **REST API push alerts:** To categorize and send warnings to end-users (Authorities, First Responders, Communities).

### DEPLOYMENT
*   **Cloud training:** For training the transformer on historical data.
*   **Edge / cloud inference:** For real-time predictions based on live satellite feeds.
