Automated Data Leakage Detection System

This project provides a CLI-based Python module that automatically inspects a dataset to detect potential target leakage using purely statistical relationships. The system assigns a leakage risk score to every feature and produces a ranked report, helping prevent models from learning information they should not have access to at prediction time.

No machine learning models are trained.
No rule-based detection is used.
All outputs are deterministic and reproducible.

 Features

Detects potential target leakage automatically

Identifies proxy variables that strongly map to the target

Works for binary and multi-class targets

Computes a feature-wise leakage risk score

Ranks features by likelihood of leakage

Produces a clean textual report

Saves results to CSV

Runs fully from terminal

 Project Structure
.
├── leakage_detector.py
├── leakage_report.csv   (generated)
├── README.md
└── dataset.csv          (your data)

 How Leakage Is Detected

For each feature, the system computes:

1. Normalized Mutual Information (NMI)

Measures shared information between the feature and target.

2. Correlation Strength

Binary target → Point Biserial correlation

Multi-class → Spearman rank correlation

3. Uniqueness / Stability Penalty

Flags ID-like variables that uniquely encode outcomes.

These components are combined into a 0–1 leakage risk score:

Score Range	Meaning
> 0.75	High leakage risk
0.5–0.75	Moderate risk
< 0.5	Low risk
 Installation

Requires Python 3.8+

pip install pandas numpy scipy scikit-learn

 Usage

Run from terminal:

python leakage_detector.py --data dataset.csv --target target_column


Example:

python leakage_detector.py --data claims.csv --target fraud_flag

 Output
Terminal report example
===== FEATURE LEAKAGE RISK REPORT =====

       feature   risk_score      risk
 discharge_day       0.902      HIGH
 claim_status        0.777  MODERATE
 policy_age          0.422       LOW
 zipcode             0.116       LOW

Saved: leakage_report.csv

CSV report fields
feature	risk_score	risk
column name	0–1 leakage score	HIGH / MODERATE / LOW
 What This Tool Prevents

This system helps flag:

✔ Post-event data
✔ Fields derived from the target
✔ Encoded target labels
✔ Columns uniquely mapping to outcomes
✔ Metadata created after the outcome occurs

Constraints Satisfied

✔ No ML training
✔ No manual rules
✔ Fully statistical
✔ Reproducible
✔ CLI script
✔ Ranked risk report

 Assumptions & Limitations

Correlation does not guarantee leakage

Domain review is recommended

Does not detect temporal leakage automatically

Works best on structured tabular datasets

 Future Enhancements (Optional)

Temporal leakage detection

Drift-aware risk scoring

Feature grouping

HTML risk dashboard

Explainability notes per feature

Automated Data Analytics & ML Assessment Project

If you want, tell me your project or course name and I can tailor the intro and tone to match it.
