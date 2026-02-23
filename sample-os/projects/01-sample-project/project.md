# Chargeback Prediction Model v2

## Purpose
Build a predictive model that identifies high-risk transactions before chargebacks occur, reducing overall chargeback rate by 15%.

## Status
In progress. Feature engineering phase.

## Links
- Slack: #payments-risk-chargeback
- Google Doc: [Project Brief](https://docs.google.com/d/xxx)
- Google Sheet: [Feature Importance Tracker](https://docs.google.com/spreadsheets/d/xxx)
- Mode Report: [Chargeback Baseline Dashboard](https://app.mode.com/xxx)

## Key Decisions
- 2026-02-18: Using XGBoost over logistic regression based on baseline comparison. Lift was 12% higher.
- 2026-02-14: Scoping to domestic transactions only for v2. International adds complexity without proportional volume.
- 2026-02-10: Aligned with Alex that model refresh cadence will be weekly, not daily.

## Open Questions
- Should we include merchant category code as a feature? Need to check with Compliance on data sensitivity.
- What is the latency budget for real-time scoring?
