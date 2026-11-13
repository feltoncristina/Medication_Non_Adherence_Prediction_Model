# Medicare Part D: Refill Analysis and Simulated Non-Adherence Prediction

## Project Overview

This project demonstrates an end-to-end data science workflow for analyzing Medicare Part D prescription claims and exploring whether historical dispensing patterns can help identify beneficiaries at risk of future medication non-adherence.

Using approximately **5.55 million synthetic prescription drug events** from the Centers for Medicare & Medicaid Services (CMS), I developed a data pipeline to ingest, validate, transform, and analyze prescription records before building and evaluating machine learning models.

During exploratory analysis, I identified limitations in medication identifiers and refill continuity that prevented the construction of a clinically reliable adherence target. To demonstrate the supervised learning process without misrepresenting the data, I developed an explicitly **simulated non-adherence outcome**.

The project emphasizes data quality, feature engineering, model interpretability, and the importance of validating predictive targets before evaluating model performance.

## Technologies Used

- **Python 3.11:** Data processing, analysis, and machine learning
- **PostgreSQL 18.3:** Data storage, SQL transformations, and analytical queries
- **Docker:** Containerized database environment
- **pandas and NumPy:** Data manipulation and feature engineering
- **scikit-learn:** Model development, preprocessing, and evaluation
- **Matplotlib:** Exploratory visualization
- **Jupyter / PyCharm:** Development and documentation

## Methodology

1. **Data Ingestion:** Loaded and validated 5,552,421 synthetic prescription events into PostgreSQL.
2. **Exploratory Data Analysis:** Investigated prescription frequency, medication identifiers (NDC11/NDC9), refill intervals, zero-day supplies, and stockpiling.
3. **Feature Engineering:** Created historical prescription features for 78,720 beneficiaries using a 180-day observation window.
4. **Target Development:** Generated a simulated binary non-adherence outcome because the source data did not support a clinically validated adherence label.
5. **Model Development:** Trained and compared Logistic Regression and Gradient Boosting classifiers.
6. **Model Evaluation:** Applied stratified training, validation, and test splits, selected a classification threshold using validation F1-score, and evaluated the selected model on held-out data.

## Model Results

The selected Logistic Regression model achieved the following results on the held-out simulated test dataset:

| Metric | Result |
|---|---|
| Accuracy | 64.06% |
| Precision | 50.31% |
| Recall | 68.30% |
| F1-Score | 0.5794 |
| ROC-AUC | 0.7141 |
| Average Precision | 0.6135 |
| Classification Threshold | 0.30 |

**Important:** These metrics reflect performance against simulated outcomes, not observed patient medication adherence. They demonstrate the machine learning workflow rather than clinically validated predictive accuracy.

## Key Findings

- Large prescription datasets do not necessarily provide sufficient longitudinal information to measure medication adherence reliably.
- Medication identifier grouping and early-refill stockpiling assumptions can significantly influence calculated refill gaps.
- Historical prescription utilization, patient payment, and prescription recency can be engineered into beneficiary-level predictive features.
- Logistic Regression offered comparable ranking performance to Gradient Boosting while providing greater interpretability.
- Lowering the classification threshold increased recall but also increased false positives, highlighting the importance of considering operational trade-offs.

## Limitations and Future Improvements

This project is a **proof of concept**, not a production-ready clinical prediction system.

Future development would involve incorporating additional beneficiary information, obtaining validated medication mappings and observed adherence outcomes, implementing temporal validation, assessing model calibration, and evaluating performance across patient populations.

The long-term objective would be to develop an evidence-based prediction framework that could support earlier identification of beneficiaries who may benefit from medication adherence interventions.

## Data Source

[CMS Data Entrepreneurs' Synthetic Public Use File (DE-SynPUF), 2008–2010](https://www.cms.gov/data-research/statistics-trends-and-reports/medicare-claims-synthetic-public-use-files/cms-2008-2010-data-entrepreneurs-synthetic-public-use-file-de-synpuf)

*All prescription records used in this project are synthetic. No real patient information was used.*