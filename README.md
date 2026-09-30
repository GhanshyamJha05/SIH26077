# HYPERCAST: MULTI-HAZARD NOWCASTING

**AI-Driven Hyper-Local Early Warning System for Severe Weather Nowcasting**

![SIH 2026](https://img.shields.io/badge/Smart_India_Hackathon-2026-orange)
![PS 26077](https://img.shields.io/badge/Problem_Statement-26077-blue)
![Theme](https://img.shields.io/badge/Theme-Disaster_Management-green)
![Category](https://img.shields.io/badge/Category-Software-yellow)
![Team](https://img.shields.io/badge/Team-ARISHEM-red)

## 🚨 The Problem

Cloudbursts, thunderstorms, and flash floods can form in just a few hours over hills. Currently:
- Forecasts arrive too late (models take too long to run).
- Warnings are too broad to say exactly which village is at risk.
- Hazards are predicted separately.
- Alerts give no reason, leading to a lack of trust.

People get little time and little reason to trust the alert before disaster strikes.

## 💡 The Proposed Solution

Hypercast is a software-first solution that solves this by providing:
1. **Collect and align data:** Places satellite images (INSAT), weather history (IMDAA), rainfall estimates (QPE), and terrain (DEM) on one common map grid.
2. **Spot the warning signs:** The system measures storm signals like moisture in the air, instability, wind lift, and cloud tops that cool fast.
3. **Predict three hazards:** One AI model (a transformer) learns from past storms and forecasts thunderstorm, cloudburst, and flash-flood risk together.
4. **Explain and pinpoint:** Shows which signal triggered the alert, then uses terrain height to show which slopes and valleys will be hit.
5. **Send alerts:** A dashboard and API send categorized warnings to authorities and communities 2–6 hours before the event.

## ✨ Why It Works

*   **Fast:** Learns patterns straight from live satellite data; doesn't wait for slow weather-model runs.
*   **Precise:** Risk is shown on a fine grid and adjusted for terrain, for village or ward-level action.
*   **Unified:** Storm, heavy rain, and flood are linked. One model predicts all three.
*   **Trusted:** Every alert comes with its reason (Explainable AI), so officials can check and act with confidence.
*   **Scalable:** Uses free public data, covers remote hills without dense sensor networks, and plugs into NDMA / SDMA systems via API.

## 🌍 Impact and Benefits

*   **2–6 h lead time** before onset.
*   **3 in 1 hazard prediction** (storm, cloudburst, flash flood).
*   **Grid-level risk** for village/ward action.
*   **Explainable:** every alert shows its trigger.

### Benefits
*   **Social:** Saves lives in flood-prone hill areas; builds public trust through clear, explained alerts.
*   **Economic:** Less damage to homes and infrastructure; targeted alerts avoid costly blanket evacuations; cheap to deploy (free public data).
*   **Environmental:** Supports river-basin monitoring; better data for long-term climate-risk planning.

## 🔬 Validation Plan

How we will prove it works:
*   **Region:** Himachal Pradesh monsoon belt (hilly and flood-prone).
*   **Replay:** Aug 2023 Mandi–Shimla–Solan events (re-run past floods as if they were live).
*   **Target:** Usable lead time in the 2–6 h window.

## 📚 Data Sources & References
*   [MOSDAC: INSAT-3D/3DR data products](https://www.mosdac.gov.in)
*   [IMDAA reanalysis (NCMRWF / IMD / UK Met Office)](https://rds.ncmrwf.gov.in)
*   [ISRO Bhuvan: CartoDEM / elevation data](https://bhuvan.nrsc.gov.in)
*   [WMO: Early Warnings for All initiative](https://wmo.int/site/knowledge-hub)

---
*Created by Team ARISHEM for Smart India Hackathon 2026*
