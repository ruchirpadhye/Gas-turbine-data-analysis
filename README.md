# Gas Turbine Telemetry Analysis: Predictive Maintenance EDA

## Project Overview
This repository contains an Exploratory Data Analysis (EDA) pipeline for gas turbine telemetry. The objective of this project is to process high-frequency sensor data (Temperature, RPM, Torque, Vibrations) to identify operational correlations and isolate mechanical fault signatures. 

This analysis serves as the foundational data-engineering step toward building physics-informed surrogate models and predictive maintenance algorithms for aerospace and heavy mechanical systems.

## Data Handling & Methodology
* **Language:** Python
* **Data Ingestion & Cleaning:** `Pandas` (Handling missing values, boolean filtering, data grouping)
* **Visualization:** `matplotlib` (Time-series mapping, correlation scatter plots, rolling averages)
* **Dataset:** 1,386 telemetry logs containing input parameters (Fuel Flow, Air Pressure) and output monitors (Power Output, Vibrations, Exhaust Temp), labeled with binary fault states (0 = Normal, 1 = Fault).

## Key Findings & Visualizations
<img width="1486" height="889" alt="image" src="https://github.com/user-attachments/assets/1094555a-9d51-4310-84c4-5cbd968a2ad3" />

1. **Thermal Envelope Stability:** Baseline operational limits were successfully mapped by correlating Turbine Inlet Temperature against Power Output.
2. **Fault Signature Overlap:** Initial scatter plot analysis comparing RPM and Torque against Vibrations reveals that fault states (1) and normal states (0) exhibit overlapping clusters in the time domain. 
3. **Trend Deviation:** While absolute magnitudes overlap, trend lines applied to the Torque vs. Vibration distributions suggest the mechanical *operational path* deviates during a fault state.
4. Feature engineering (calculating the discrete time derivative of vibration) successfully isolated mechanical shocks, revealing a massive increase in $\frac{dV}{dt}$ variance during fault states compared to steady-state normal operations.
<img width="844" height="547" alt="image" src="https://github.com/user-attachments/assets/2882b832-02e0-47f3-9313-baf78b534614" />

5. **Frequency Domain Analysis**: Applying a Fast Fourier Transform (FFT) to the vibrations' signals revealed a big spike in frequency at ~220 - 230 Hz during fault states.

<img width="989" height="490" alt="image" src="https://github.com/user-attachments/assets/cb028a99-c45f-42f5-8128-cd3614598d1d" />


## Future Scope
Because mechanical failures often manifest in the *rate of change* rather than absolute magnitude, future iterations of this analysis will feature:
* **Predictive Modeling**: Transition from EDA to supervised learning by training a Random Forest classifier to automate fault detection.
* **Real-time Stream Processing**: Implement a live, sliding FFT pipeline to enable real-time anomaly detection.

---
*Developed as part of an autonomous systems and computational engineering portfolio.*
