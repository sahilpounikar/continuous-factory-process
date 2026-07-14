[README.md](https://github.com/user-attachments/files/30015672/README.md)
# Continuous Factory Process — Defect Prediction & Root Cause Analysis

Predicting quality defects on a real continuous manufacturing line using sensor data, and tracing each prediction back to the machine readings most responsible for it.

**Live site:** https://YOUR-USERNAME.github.io/continuous-factory-process/

---

## Overview

A continuous production line logs machine speed, temperature, pressure, and amperage across multiple stages — far more signals than an operator can watch by hand. This project builds a classifier that flags high-defect-risk output from those sensor readings, then uses feature importance to point at *which* signals are driving that risk, so engineers know what to check on the floor.

## Dataset

- **14,088** process records after cleaning
- **116** numeric sensor / machine features
- Source column renamed for clarity: `Speed`, `Temp`, `Amps`, and the output measurement used as the prediction target

## Approach

1. **Cleaning** — dropped the raw timestamp column, removed rows with missing target values
2. **Labeling** — converted the continuous output measurement into a binary label: top 20% (80th percentile) flagged as high defect risk
3. **Feature engineering** — added a `Thermal_Load` feature (`Temp × Amps`) as a physically meaningful stress signal
4. **Split** — 80/20 train-test split
5. **Modeling** — trained and compared a Decision Tree and a Random Forest classifier
6. **Root cause analysis** — ranked all 116 features by Random Forest importance to identify the top drivers of defect risk

## Results

| Model | Accuracy |
|---|---|
| Decision Tree | 94.6% |
| Random Forest | 95.9% |

**Top 5 root-cause features (by importance):**

1. `Stage1.Output.Measurement14.U.Actual`
2. `Stage1.Output.Measurement2.U.Actual`
3. `FirstStage.CombinerOperation.Temperature2.U.Actual`
4. `Machine3.MaterialPressure.U.Actual`
5. `FirstStage.CombinerOperation.Temperature1.U.Actual`

Full confusion matrix and top-10 feature ranking are in the notebook and on the [live site](https://YOUR-USERNAME.github.io/continuous-factory-process/).

## Root Cause Dashboard

An interactive Tableau dashboard (`Root_cause_analysis_dashboard.twbx`) lets you explore defect risk by stage, machine, and measurement. Published version linked on the live site.

## Repository contents

```
continuous-factory-process/
├── index.html                          # project website
├── assets/
│   └── confusion_matrix.png            # model evaluation plot
├── continuous_factory_process.ipynb    # full analysis notebook
└── README.md
```

## Tech stack

Python · pandas · NumPy · scikit-learn (Decision Tree, Random Forest) · matplotlib · seaborn · Tableau · Jupyter

## How to run the notebook

```bash
pip install pandas numpy matplotlib seaborn scikit-learn
jupyter notebook continuous_factory_process.ipynb
```

## Author

**Your Name**
[LinkedIn](https://www.linkedin.com/in/YOUR-LINKEDIN) · [GitHub](https://github.com/YOUR-USERNAME) · YOUR-EMAIL@example.com
