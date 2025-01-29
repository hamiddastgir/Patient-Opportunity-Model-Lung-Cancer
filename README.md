# Building a Patient Opportunity Model for Lung Cancer Treatments
Leveraging Synthetic & ChatGPT-Generated Data for Predictive Insights

---

## Table of Contents
1. [Overview](#overview)  
2. [Project Objectives](#project-objectives)  
3. [Why Synthetic Data?](#why-synthetic-data)  
4. [Data Files](#data-files)  
5. [Notebooks & Workflow](#notebooks--workflow)  
6. [Methodology](#methodology)  
7. [Key Insights for Sales & Marketing](#key-insights-for-sales--marketing)  
8. [Limitations & Future Work](#limitations--future-work)  
9. [References](#references)  
10. [License](#license)  

---

## Overview
In the dynamic realm of **precision medicine**, one of the biggest challenges for **pharmaceutical companies** is determining how best to **identify and reach the right patients**—especially in conditions like **Non-Small Cell Lung Cancer (NSCLC)** where treatment pathways are increasingly complex. Real-world data (RWD) can be prohibitively **expensive** or simply **inaccessible**, particularly for smaller-scale projects, leading us to explore the use of **synthetic** and **ChatGPT-generated** data as a cost-effective and privacy-preserving alternative.

This repository outlines our data preparation, feature engineering, and exploratory approaches for building a **Patient Opportunity Model** designed to:

- Predict which **patients** are likely to initiate therapy with our company’s Product A  
- Identify **potential switchers** from a competitor’s Product B  

---

## Project Objectives
1. **Model the Patient Journey**: Understand how NSCLC patients progress through different lines of therapy (LOTs).  
2. **Predict Initiation & Switching**: Pinpoint the key inflection points that indicate a patient might start or switch therapies.  
3. **Empower Sales & Marketing (S&M)**: Equip teams with timely insights (e.g., which physicians are prime for outreach).  
4. **Validate Synthetic Data Approaches**: Compare **Synthetic Data Vault** outputs and **ChatGPT-generated** data for realism and usability in ML modeling.  

---

## Why Synthetic Data?
- **Cost-Effective**: Large real-world datasets can be extremely expensive.  
- **Privacy-Compliant**: Synthetic data circumvents many personal health data (PHI) restrictions.  
- **Quick Prototyping**: Ideal for testing feature engineering techniques and ML workflows without extensive compliance hurdles.  

> **Decision**: We ultimately leaned toward **ChatGPT-generated data** because it presented fewer data anomalies and required less cleaning compared to our initial synthetic dataset generated via **Synthetic Data Vault**.

---

## Data Files
Below are the **CSV files** that form the backbone of our analysis. Each file is **synthetic** or **ChatGPT-generated** and carefully designed to replicate real-world scenarios (prescription patterns, patient timelines, HCP details).

1. **Synthetic Dataset.csv**  
2. **Synthetic Features.csv**  
3. **Synthetic hcp_level_final_data.csv**  
4. **Synthetic HCP_level_final_features.csv**  
5. **Synthetic HCP_universe_table_final.csv**  
6. **Synthetic mNSCLC Patients.csv**  
7. **Synthetic Patient_LOT_data.csv**  
8. **Synthetic patientXLOT_feature.csv**  
9. **Synthetic_Prescription_Data.csv**  

Each file contains attributes like **prescribing volume, treatment lines, biomarker statuses,** and **demographics** that collectively enable robust **feature engineering**.

---

## Notebooks & Workflow
This project comprises **three main Jupyter notebooks**, each focusing on a different aspect of the **Patient Opportunity Model** pipeline:

1. **Patient Cohort Analysis_08302024-Synthetic.ipynb**  
   - Explores patient demographics and high-level prescribing behaviors.  
   - Conducts initial data cleaning & merges from various CSVs.  

2. **LOT and Regimen creation_08302024-Synthetic.ipynb**  
   - Defines **Lines of Therapy (LOT)** rules and identifies patient transitions (e.g., from 1st-Line to 2nd-Line therapy).  
   - Creates **regimen-level features** to capture complexities in treatment pathways.  

3. **Feature Creation-GPT copy.ipynb**  
   - Focuses on **feature engineering** for ML modeling.  
   - Aggregates data by **HCP** and **Patient** over a 12-month lookback window.  
   - Creates features around **prescription counts**, **biomarker status**, **LOT durations**, and more.  

**Recommended Order**:  
1. **LOT and Regimen creation** -> 2. **Patient Cohort Analysis** -> 3. **Feature Creation**  

*(Feel free to adapt based on your specific data needs.)*

---

## Methodology
### 1. Data Integration
- **Merge multiple CSV files** to unify patient details, prescription records, and HCP-level data.  
- **Resolve conflicts & duplicates** arising from synthetic data generation.  

### 2. Data Cleaning & Preprocessing
- **Handle missing values** in critical fields (e.g., biomarker status, prescription dates).  
- **Filter out anomalies** like zero-day therapy durations or contradictory LOT progressions.  

### 3. Feature Engineering
- **LOT-Based Features**: Duration in each line of therapy, frequency of switching.  
- **Prescription Counts**: Monthly prescribing volumes (our Product A vs. competitor Product B).  
- **Growth Trends**: Month-over-month changes in prescription volume.  
- **Patient Demographics**: Age, EGFR status, comorbidities (if available).  
- **HCP-Level Insights**: Volume of NSCLC patients treated, prescribing patterns, brand loyalty scores, etc.  

### 4. Model-ready Dataset
- **Anchor Date**: For each patient, define a reference date and take a 1-year lookback to compute recent prescribing behavior.  
- **Outlier Removal**: Exclude extreme outliers (e.g., 1000+ days in 1L therapy).  
- **Feature Matrix**: Combine patient-level and HCP-level features into a single table for modeling.  

---

## Key Insights for Sales & Marketing
- **Identifying High-Value HCPs**: Pinpoint which physicians are heavy prescribers of competitor products, representing top targets for outreach.  
- **Predicting Switchers**: Highlight patients most likely to transition from Product B to our Product A based on side-effect profiles, tolerability, and historical patterns.  
- **Spotting Emerging Treatment Trends**: Early signals of a spike in 1L or 2L usage can guide **demand forecasting** and **resource allocation**.  

> **Value**: These insights empower **Sales & Marketing** teams to focus their energy, time, and budget on the **right accounts** at the **right time**, improving both **patient outcomes** and **commercial performance**.

---

## Limitations & Future Work
1. **Synthetic ≠ Real**: While we strived for realism, synthetic and ChatGPT-generated data lack certain nuances of actual patient behavior.  
2. **Extended Feature Engineering**: Incorporating additional real-world signals (e.g., lab results, insurance claims detail, ICD codes) could deepen insights.  
3. **Modeling & Evaluation**: This repository focuses primarily on data prep. Predictive modeling and performance metrics will be showcased in **Part 2**.  
4. **Regulatory Context**: In real scenarios, consult compliance experts regarding patient data handling and HIPAA/GDPR standards.  

---

## References

- **Synthetic Data Vault**: [SDV GitHub](https://github.com/sdv-dev/SDV)  
- **ChatGPT**: [OpenAI](https://openai.com)

---

## License
This project is released under the **MIT License** and the general usage terms of **OpenAI's ChatGPT model**. Feel free to adapt or expand upon this work for your own research, educational, or commercial purposes, provided you adhere to the terms of the license.
