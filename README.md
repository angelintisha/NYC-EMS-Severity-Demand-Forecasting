# Forecasting Severity-Specific EMS Demand for Ambulance Staffing and Deployment in New York City

**AI & BI solution proposal**

📄 [Read the full proposal (PDF)](EMS_Demand_Forecasting_Proposal.pdf)

---

## Overview

New York City's average ambulance response to life-threatening emergencies rose from 9:34 to 11:21 between FY2021 and FY2025, while ambulance in-service hours fell and hospital turnaround times grew. FDNY applies call severity once a call arrives, but staffing and unit positioning are set without a forward-looking estimate of how much demand of each severity to expect, where, and when.

This proposal designs an AI- and BI-enabled demand outlook that converts Computer Aided Dispatch (CAD) incident history into severity-specific forecasts by dispatch area and time window, so capacity can be planned before calls arrive.

## Solution Design

- **Data foundation:** CAD incident records (NYC Open Data, 2005 onward) aggregated into hourly counts by severity segment and dispatch area, using only information available before the forecast origin to prevent leakage
- **Forecasting engine:** Seasonal-naive baseline, statistical count models, and gradient-boosted trees compared under rolling-origin validation, with error reported per severity segment so performance on common low-acuity calls cannot mask weak performance on rare Segment 1 emergencies
- **Outputs:** A seven-day forecast for tour staffing and a same-day forecast with threshold alerts for unit positioning, each issued with a prediction range
- **BI layer:** Descriptive, forecast, equity, and model-health views
- **Design principle:** Runs alongside the 911 dispatch path, never inside it; every operational decision stays with EMS personnel

The proposal includes the solution architecture, a conceptual dashboard mock-up, a before-and-after workflow, and an implementation roadmap.

## Implementation & Governance

- 18-month gated rollout: governance and data readiness, shadow mode, matched-area pilot, and citywide scale-up, each ending in a go/no-go decision
- Governance aligned with the NIST AI Risk Management Framework, including drift-triggered retraining and automatic fallback to the baseline
- Privacy safeguards, small-count suppression, and review under NYC's algorithmic-tool disclosure requirements (Local Law 35 of 2022)

## Evaluation

Five KPIs across three levels:

| Level | KPI |
|---|---|
| Model | Segment-level forecast skill (MAE vs. seasonal-naive baseline) |
| Adoption | Forecast reviewed and decision logged in pilot cycles |
| Outcome | End-to-end response time to life-threatening emergencies |
| Outcome | ALS-capable unit response share |
| Equity | Geographic response-time variation across boroughs |

## Status

This is a design proposal. Forecasting models have not yet been implemented.

## Data Source

[FDNY EMS Incident Dispatch Data — NYC Open Data](https://data.cityofnewyork.us/Public-Safety/EMS-Incident-Dispatch-Data/76xm-jjuj)
