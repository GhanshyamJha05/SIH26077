# 🌩️ HYPERCAST

### AI-Driven Hyper-Local Early Warning System for Severe Weather Nowcasting

![SIH 2026](https://img.shields.io/badge/Smart_India_Hackathon-2026-orange?style=for-the-badge)
![PS 26077](https://img.shields.io/badge/Problem_Statement-26077-blue?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Concept_%2F_PoC-lightgrey?style=for-the-badge)
![Theme](https://img.shields.io/badge/Theme-Disaster_Management-green?style=for-the-badge)
![Category](https://img.shields.io/badge/Category-Software-yellow?style=for-the-badge)
![Team](https://img.shields.io/badge/Team-ARISHEM-red?style=for-the-badge)

---

> **Hypercast** is a **proposed** AI-driven early warning system designed to predict cloudbursts, thunderstorms, and flash floods at a **high-resolution regional grid**, **2–6 hours before they strike**, utilizing free satellite data and explainable AI.

---

## 🚨 The Problem

Cloudbursts and flash floods in hilly regions kill hundreds every year. Current systems fail because:

| ❌ Gap | What Goes Wrong |
| :--- | :--- |
| **Too Slow** | Weather models take hours to run — the event is already happening. |
| **Too Broad** | Warnings cover entire districts, lacking specific geographical targeting. |
| **Siloed** | Storms, rain, and floods are predicted separately — the chain is missed. |
| **No Reason Given** | Alerts say "heavy rain likely" with no explanation — authorities hesitate to act. |

## 💡 Our Proposed Solution

Hypercast addresses these gaps through a **planned 5-step pipeline**:

1. **Fusing live data** — Satellite (INSAT-3D), weather (IMDAA), rainfall (QPE), and terrain (CartoDEM) on one grid.
2. **Extracting storm signs** — Moisture, instability, wind shear, cloud-top cooling.
3. **Predicting 3 hazards together** — A multi-task spatiotemporal AI architecture forecasts storm → cloudburst → flood as a chain.
4. **Explaining every alert** — XAI names the exact trigger (e.g., "rapid cloud-top cooling in Sector 4").
5. **Delivering warnings** — GIS dashboard + REST API push alerts to authorities 2–6 hours early.

## ⚡ Key Highlights (Targets)

| Metric | Target Value |
| :---: | :---: |
| 🕐 **Lead Time** | 2–6 hours |
| 🎯 **Resolution** | High-resolution grid (sub-district level) |
| 🔗 **Hazards** | 3-in-1 (storm, cloudburst, flood) |
| 💡 **Explainability** | Every alert shows its meteorological trigger |
| 💰 **Hardware Cost** | ₹0 — uses free public satellite data |

## 🏗️ Proposed Tech Stack

| Layer | Technologies |
| :--- | :--- |
| **Data** | INSAT-3D/3DR, IMDAA, QPE, CartoDEM |
| **AI/ML** | Spatiotemporal Transformer, XGBoost baseline, SHAP XAI |
| **Backend** | Python, Node.js, PostgreSQL + PostGIS |
| **Frontend** | React.js + Leaflet/Mapbox GIS |
| **Alerts** | REST API push to NDMA/SDMA systems |

## 🔬 Validation Strategy

Our **validation strategy** involves **replaying the Aug 2023 Himachal Pradesh floods** (Mandi–Shimla–Solan) through our pipeline and measuring whether the system fires a usable warning within the 2–6 hour window before onset.

## 🚀 Setup & Installation (Coming Soon)

*(Instructions for running the local API and frontend dashboard will be added once the PoC development is completed during the hackathon.)*

## 📂 Repository Structure

```text
SIH26077/
│
├── README.md              ← "Understand HYPERCAST in 2–3 minutes"
│
├── docs/
│   └── report.md          ← "Understand the entire technical proposal"
│
├── assets/                ← Project visuals, mockups, and diagrams
│   ├── architecture/
│   ├── dashboard/
│   └── risk-map/
│
├── frontend/              ← React.js Web GIS Dashboard (Planned)
├── backend/               ← Node.js/Python REST API for alerts (Planned)
├── ai-service/            ← Python inference service (Transformer & XGBoost)
├── data/                  ← Data ingestion scripts (MOSDAC, IMDAA, CartoDEM)
├── models/                ← Saved model weights and definitions
└── tests/                 ← System validation and evaluation
```

## 📖 Documentation

| Document | Description |
| :--- | :--- |
| [**📋 Project Report**](./docs/report.md) | Complete report covering problem, solution, methodology, feasibility, validation, impact, and references. |
| [**🏛️ Architecture**](./ARCHITECTURE.md) | Technical architecture with Mermaid flowchart and detailed technology stack. |

## 🌍 Anticipated Impact

| Category | Benefit |
| :--- | :--- |
| 🟢 **Social** | Saves lives in flood-prone hill areas; builds public trust with explained alerts. |
| 🟡 **Economic** | Avoids blanket evacuations; zero hardware cost; reduces infrastructure damage. |
| 🔵 **Environmental** | Better data for river-basin monitoring and climate-risk planning. |

## 📚 Data Sources

- [MOSDAC — INSAT-3D/3DR Satellite Data](https://www.mosdac.gov.in)
- [IMDAA Reanalysis — NCMRWF / IMD](https://rds.ncmrwf.gov.in)
- [ISRO Bhuvan — CartoDEM Elevation](https://bhuvan.nrsc.gov.in)
- [WMO — Early Warnings for All](https://wmo.int/site/knowledge-hub)

---

<p align="center">Made with ❤️ by <b>Team ARISHEM</b> for Smart India Hackathon 2026</p>
