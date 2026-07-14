# **Enhanced Network Management and Planning (Slovenian Pilot)**

## **Overview**
The Enhanced Network Management and Planning service is a core machine learning component developed for the Slovenian Pilot. Its primary goal is to provide deep visibility, anomaly detection, and forecasting capabilities within secondary distribution networks (specifically focusing on the aggregated MV/LV interface at the transformer station level).

By integrating with the PowerCIM platform, the service securely accesses DSO-owned grid data formatted in the Common Information Model (CIM) standard, transforming raw grid measurements into actionable operational insights.

## **Core Features & ML Modules**
The service implements three distinct Machine Learning (ML) pipelines:

  **Anomaly Detection & Mitigation:** Continuously monitors secondary distribution grids using power quality parameters to identify operational irregularities, and automatically reconstructs/replaces corrupted or anomalous data points to maintain high data quality.
  
  **Demand Forecast:** Predicts active and reactive power consumption trends at the MV/LV interface to assist in local grid planning and flexibility management.
  
  **PV Capacity Estimation:** Provides aggregated solar (photovoltaic) generation estimates specifically mapped to the MV/LV interface, allowing operators to understand net vs. gross load profile behaviors.

## **Data Architecture & Integration**
The service relies on a multi-source data ingestion strategy, unified through the PowerCIM layer:
### Data Inputs: 
**Power Quality (PQ) Measurements:** High-resolution data from the substation meters, including Current (I), Voltage (V), Active Power (P), and Reactive Power (Q)

**Meteorological Data:** Local weather observations and forecasts used as primary drivers for both the PV Estimation and Demand Forecast models

**Geospatial Data:** Location and topological data of the secondary transformer stations

**Dynamic Thermal Rating (DTR) Calculations:** Inputs/insights regarding transformer thermal limits and ampacity (aligned with the pilot's thermal assessment modules).

### **Data Flow & Ownership**
[ DSO Data Domain ] ──> [ PowerCIM Platform (CIM Data) ] ──> [ Enhanced Network Management Service ] ──> [ ML Inference Engine ]

**Data Privacy Note:** All operational grid data remains under the strict ownership and control of the DSO. The service connects via the PowerCIM platform to ensure compliance with the pilot's data space security protocols.

## **Testing and Validation**
To ensure high accuracy and resilience before deployment, the ML models underwent a strict two-stage validation process:

**Synthetic Data Validation:** Initial benchmarking, framework debugging, and edge-case testing were performed using high-fidelity synthetically generated grid data.

**Historical Data Validation:** Final training, calibration, and performance verification were executed utilizing real, anonymized historical historical data provided directly by the DSO.

## **Service Outputs & Results**
The service runs periodic inferences and exposes the following structured results for each secondary transformer station:

**Anomaly Detection Results**

Anomaly Score / Flag: Binary or continuous metric indicating whether the current grid state is operating outside normal parameters.

Timestamp & Phase Identification: Exact time and specific phase(s) where the anomaly or power quality issue was detected.

Reconstructed / Replacement Values: Automatic replacement of the detected anomalous data points with estimated, clean values (e.g., reconstructed P, Q, U, or I profiles) to ensure data continuity and robustness for downstream processes.

**Demand Forecast Results**

Load Forecast Profiles: Time-series predictions of Active Power (P) and Reactive Power (Q) demand at the MV/LV interface.Horizon: Short-term and mid-term intra-day predictions (e.g., 15-minute or hourly intervals).

**PV Generation Estimation Results**

Aggregated PV Generation: Estimated actual solar power production (kW) currently active behind the MV/LV interface.

