# Cyclone System Analysis

## Project Overview
This project performs a comprehensive analysis of the Cyclone system using operational data. The workflow includes:

1. **Feature Engineering & Clustering**
   - Creation of lag features, deltas, and rolling statistics.
   - Multivariate clustering (KMeans/DBSCAN/HDBSCAN) to identify operational states such as Normal, High Load, Degraded, and Startup/Shutdown.

2. **Contextual Anomaly Detection & Root Cause Analysis**
   - Cluster-specific anomaly detection using Isolation Forest.
   - Grouping consecutive anomalies into events and identifying most implicated variables.
   - Root cause hypotheses based on deviations relative to cluster behavior.

3. **Short-Horizon Forecasting**
   - Forecasting `Cyclone_Inlet_Gas_Temp` for the next 1 hour (12 steps) using:
     - Persistence baseline
     - ARIMA model
   - Evaluation using RMSE and MAE.

4. **Insights & Storytelling**
   - Analysis connecting clusters, anomalies, shutdowns, and forecast performance.
   - Actionable recommendations for monitoring and operator alerts.

## Deliverables

### 1. `anomalous_periods.csv`
- **Description:** Consolidated list of anomalous events.
- **Columns:**
  - `start_time`: Start of anomaly period
  - `end_time`: End of anomaly period
  - `duration`: Duration in hours/minutes
  - `state_label`: Cluster/state during the anomaly
  - `most_implicated_var`: Feature most responsible for anomaly
  - `hypothesis`: Root cause explanation based on feature deviations

### 2. `clusters_summary.csv`
- **Description:** Summary statistics of all operational states/clusters.
- **Columns:**
  - `state_label`: Cluster/operational state
  - `<feature>_mean, <feature>_std, <feature>_min, <feature>_max, <feature>_median`: Feature statistics for each cluster
  - `num_occurrences`: Number of times the state appeared
  - `avg_duration_min`: Average duration of the state
  - `std_duration_min, min_duration_min, max_duration_min, median_duration_min`: Duration statistics

### 3. `forecasts.csv`
- **Description:** Comparison of true vs predicted values for forecasting tasks.
- **Columns:**
  - `time`: Timestamp of observation
  - `true_value`: Actual `Cyclone_Inlet_Gas_Temp`
  - `persistence_pred`: Forecast from persistence baseline
  - `arima_pred`: Forecast from ARIMA model

## Usage
1. Load the CSV files into Python, R, or Excel for further analysis or visualization.
2. The CSVs can be used to:
   - Analyze cluster behavior (`clusters_summary.csv`)
   - Identify operational anomalies and root causes (`anomalous_periods.csv`)
   - Compare forecasting performance (`forecasts.csv`)

## Insights & Recommendations
- **Anomalies often precede shutdowns**, especially in the *Degraded* state.
- Cluster-specific anomalies and forecasting performance highlight **regime shifts** as a key challenge.
- Recommendations include:
  - Implement **state-aware anomaly alerts**
  - Train **cluster-specific forecasting models**
  - Monitor key variables jointly for **early warning of operational issues**

## Notes
- Ensure that `timestamp` or `date` columns in the CSVs are parsed as datetime for analysis.
- All numeric features are included in `clusters_summary.csv` automatically.
- Forecasting models assume **regular time intervals**; resampling may be needed if data is irregular.

---

*This README provides an overview of the analysis workflow, datasets, and usage instructions for the Cyclone system analysis project.*