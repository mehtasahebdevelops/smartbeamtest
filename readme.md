# Water Pump Sensor Failure Analysis

### Overview

This repository contains an end-to-end data science analysis aimed at understanding and predicting failures in a water pump system using multivariate sensor data.

The goal is to identify failure patterns, determine the most informative sensors, and evaluate machine learning models for early failure detection.

\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

### Dataset

* Rows: 31,817 time-stamped observations
* Sensors: 52 raw sensor readings (sensor\_00 – sensor\_51)
* Target: machine\_status (NORMAL, RECOVERING, BROKEN)

Failures are extremely rare, with only 2 recorded breakdown events, making this a highly imbalanced dataset.

\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

### Data Preprocessing

* Dropped sensor\_15 due to 100% missing values.
* Remaining missing values were forward- and backward-filled to preserve time-series continuity.
* Converted the problem into binary classification:
* BROKEN → 1
* All other states → 0

\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

### Exploratory Analysis

#### Time Series Analysis

* sensor\_00 was plotted over time with failure points overlaid.
* Failures are preceded by increased volatility and abnormal sensor behavior rather than sudden drops.

#### Correlation Analysis

* A full correlation heatmap revealed strong inter-sensor correlations, indicating redundancy.
* Top three sensors most correlated with failure:

1. sensor\_00
2. sensor\_34
3. sensor\_04

\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

### Modeling

Three models were evaluated:

1. Logistic Regression (baseline)
2. Random Forest
3. XGBoost (primary model)

Due to severe class imbalance, ROC-AUC was used as the main evaluation metric instead of accuracy.

#### Key Modeling Insights

* Linear models struggle to capture failure patterns.
* Tree-based models capture non-linear sensor interactions more effectively.
* XGBoost identified a different set of influential sensors, suggesting failures are driven by complex interactions rather than single-sensor thresholds.

\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

### Key Observations

* Failure events are too sparse for reliable supervised learning.
* High accuracy is misleading; recall for failures is limited by data scarcity.
* Sensor instability appears before failures, indicating potential early-warning signals.
* Many sensors provide overlapping information.

\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

### Hypotheses \& Recommendations

* Failures are preceded by degradation patterns rather than instantaneous events.
* Anomaly detection or semi-supervised approaches may outperform pure classification.
* Preventive maintenance windows likely exist before breakdowns.
* Sensor instrumentation can potentially be optimized by removing redundant sensors.

\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_



