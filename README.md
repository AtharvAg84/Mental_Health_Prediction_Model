# Mental Health Risk Profiling and Treatment-Gap Identification Using K-Means Clustering

## 1. Project Overview

Mental health concerns are influenced by psychological, behavioral, social, and personal factors. Identifying patterns in these factors can help researchers understand different respondent profiles and explore potential gaps in treatment engagement.

This project applies **unsupervised machine learning using K-Means clustering** to survey-based mental health data. It constructs composite indicators for mental health risk and social isolation, groups respondents into interpretable profiles, and examines differences in treatment engagement across the resulting clusters.

The project is intended for **exploratory data analysis and academic research**. Its clusters are not clinical diagnoses and should not be used as a substitute for professional mental health assessment.

## 2. Objectives

- Explore patterns in mental health survey responses.
- Construct composite indicators for mental health risk and social isolation.
- Apply K-Means clustering to identify distinct respondent profiles.
- Examine treatment engagement and identify groups reporting elevated risk indicators without current treatment.
- Evaluate clustering quality using the silhouette coefficient and visualize clusters using Principal Component Analysis (PCA).
- Explore the potential use of cluster centroids to assign new observations to existing profiles.

## 3. Dataset

**Source:** [Mental Health Dataset — Kaggle](https://www.kaggle.com/datasets/bhavikjikadara/mental-health-dataset)

The project uses survey data containing demographic, behavioral, mental health history, and treatment-related information.

The dataset has been reported to contain **292,364 records and 17 columns**. These figures and the final number of usable records should be verified against the downloaded dataset and the executed preprocessing code.

### Main variables

| Category | Example variables |
|---|---|
| Demographic information | Gender, Occupation, Country |
| Personal and family history | family_history, Mental_Health_History |
| Behavioral indicators | Days_Indoors, Changes_Habits, Growing_Stress |
| Social and coping indicators | Social_Weakness, Coping_Struggles |
| Treatment engagement | treatment, care_options |
| Additional survey information | Work_Interest, Mood_Swings, self_employed |

The exact column names depend on the source dataset and should be checked before execution.

## 4. Methodology

The project follows the workflow below:

1. **Data loading and inspection:** Load the dataset and examine its structure, data types, missing values, duplicate records, and categorical values.
2. **Data preprocessing:** Handle missing or inconsistent values and prepare the variables required for analysis.
3. **Feature engineering:** Construct composite indicators representing mental health risk and social isolation.
4. **Feature selection:** Use the engineered indicators and selected binary variables for clustering.
5. **Feature scaling:** Standardize the selected features before applying K-Means.
6. **Model selection:** Examine candidate cluster counts using the elbow method and silhouette coefficient.
7. **K-Means clustering:** Apply K-Means with four clusters to the 100,000-record sample used in the reported analysis.
8. **Cluster interpretation:** Compare cluster sizes, risk scores, treatment engagement, family history, and mental health history.
9. **Visualization and evaluation:** Use PCA projections and clustering metrics to examine the resulting structure.
10. **New-observation assignment:** Where implemented, assign new observations to existing clusters using the fitted preprocessing procedure and cluster centroids.

### 4.1 Composite indicators

**Mental Health Risk Score:** A score from 0 to 5 constructed from five binary indicators:

- Growing stress
- Changes in habits
- Mental health history
- Coping struggles
- Social weakness

The score represents the number of selected indicators present. It is a project-defined exploratory measure, not a clinically validated risk instrument.

**Social Isolation Score:** A score from 0 to 3 constructed from the reported duration spent indoors and the Social Weakness response. The implementation's exact category mappings should be documented in the code.

### 4.2 Clustering features

The reported five-feature configuration uses:

- Mental_Health_Risk_Score
- Isolation_Score
- has_treatment
- has_family_history
- has_mental_health_history

These features are scaled before clustering. Because treatment engagement is itself a clustering feature, the resulting groups are partly influenced by treatment status. A sensitivity analysis excluding treatment status is therefore important when assessing whether the profiles reveal patterns beyond the treatment variable.

## 5. Reported Results

The existing analysis reports four clusters based on a sample of 100,000 records.

| Cluster | Profile label | Respondents | Percentage | Mean risk score | Treatment engagement |
|---|---|---:|---:|---:|---:|
| 1 | High-Risk Chronic | 16,063 | 16.1% | 2.53 | 100% |
| 2 | Healthy Resilient | 33,709 | 33.7% | 1.49 | 0% |
| 3 | High-Risk Untreated | 15,791 | 15.8% | 2.50 | 0% |
| 4 | Early Intervention | 34,437 | 34.4% | 1.50 | 100% |
| **Total** | | **100,000** | **100%** | | |

The reported silhouette coefficient is approximately **0.30**, while the first two PCA dimensions explain approximately **56.5%** of the variance in the scaled features.

These are previously reported results and should be reproduced from the uploaded code before being treated as final results. The cluster labels are descriptive interpretations of the observed profiles.

### Interpretation

- **High-Risk Chronic:** Respondents with higher average risk scores, reported mental health history, and treatment engagement.
- **Healthy Resilient:** Respondents with lower average risk scores and no reported treatment engagement in the clustering sample.
- **High-Risk Untreated:** Respondents with higher average risk scores, reported mental health history, and no reported treatment engagement.
- **Early Intervention:** Respondents with lower average risk scores and treatment engagement.

The High-Risk Untreated cluster represents a potential treatment-engagement gap for further investigation. Its membership alone does not establish an unmet clinical need or explain why respondents are not receiving treatment.

## 6. Technology Stack

The implementation should be documented according to the actual uploaded code. The reported workflow uses:

- **R** — data processing, feature engineering, and statistical analysis
- **K-Means** — unsupervised clustering
- **Feature standardization** — to place clustering variables on comparable scales
- **Elbow method and silhouette coefficient** — cluster evaluation
- **Principal Component Analysis (PCA)** — dimensionality reduction and visualization
- **Data visualization tools in R** — exploratory analysis and cluster plots

## 7. Repository Structure

A suggested repository structure is:

```text
mental-health-risk-clustering/
├── README.md
├── mental_health_clustering.R
├── data/
│   └── README.md
├── outputs/
│   └── README.md
└── LICENSE
```

- `README.md`: Project overview, methodology, setup, and results.
- `mental_health_clustering.R`: Main analysis script. Replace this filename with the actual uploaded code filename.
- `data/README.md`: Instructions for obtaining and preparing the dataset. Do not upload sensitive or restricted data.
- `outputs/README.md`: Description of generated plots, tables, and other results.
- `LICENSE`: Include a license only after choosing one appropriate for the code and confirming that it does not conflict with the dataset's terms.

The folders shown above are a recommended structure; create only the files and folders that you actually use.

## 8. Installation and Execution

### Prerequisites

- R installed on your system.
- Access to the dataset from the Kaggle source linked above.
- The R packages required by the uploaded script.

### Steps

1. Clone or download this repository.
2. Download the dataset from Kaggle and place it in the location expected by the script.
3. Open the R script in RStudio or another R environment.
4. Install any missing packages specified in the script.
5. Update the dataset path if necessary.
6. Run the script from beginning to end.

Example commands:

```bash
git clone <YOUR_GITHUB_REPOSITORY_URL>
cd mental-health-risk-clustering
```

Then open the R script and execute it in RStudio.

**Important:** The repository URL, script filename, package installation commands, input filename, and output locations must be updated to match the final repository and code. Do not assume the script runs without modification until it has been tested from a clean environment.

## 9. Evaluation

The project uses unsupervised clustering evaluation rather than conventional supervised classification metrics.

- **Elbow method:** Helps assess how within-cluster variation changes with the number of clusters.
- **Silhouette coefficient:** Evaluates how well observations fit their assigned clusters relative to neighboring clusters.
- **PCA visualization:** Projects the scaled features into fewer dimensions for visual exploration.
- **Cluster profiling:** Compares the size and characteristics of the resulting groups.
- **Sensitivity analysis:** Repeats clustering with alternative feature configurations, particularly excluding treatment status.

A silhouette coefficient of approximately 0.30 indicates limited-to-moderate separation under common interpretations; it does not establish clinical validity. Classification metrics such as AUROC, AUPRC, sensitivity, specificity, and calibration are not directly applicable unless a separate supervised prediction task with a clearly defined outcome is implemented.

## 10. Limitations

- The analysis relies on survey responses and may be affected by self-reporting, missing data, and sampling bias.
- The composite mental health risk and isolation scores are project-defined and have not been established as clinically validated measures.
- K-Means is sensitive to feature scaling, feature selection, initialization, and the choice of cluster count.
- The reported silhouette coefficient suggests that cluster separation is not strong.
- Including treatment status among the clustering features influences the observed treatment-engagement profiles.
- The dataset does not, by itself, establish clinical diagnoses, treatment eligibility, causal relationships, or reasons for non-treatment.
- External validation and sensitivity analyses are needed before drawing stronger conclusions.

## 11. Ethical Considerations

This project uses survey data for academic analysis. The findings should be interpreted as exploratory patterns rather than individual-level clinical assessments.

Users should review the dataset's terms of use, source documentation, and any applicable ethical requirements before redistributing data or derived records. Do not publish personal or sensitive information. Any claims about ethics approval, informed consent, anonymization, or regulatory compliance must be supported by the relevant documentation.

## 12. Reproducibility and Data Availability

- **Dataset:** [Mental Health Dataset on Kaggle](https://www.kaggle.com/datasets/bhavikjikadara/mental-health-dataset)
- **Source code:** Available in this repository once uploaded.
- **Random seed:** The existing analysis reports seed `123`; verify that the final script sets and uses it consistently.
- **Sampling:** The reported clustering analysis uses 100,000 records. Document the sampling method and seed in the final code.
- **Software and packages:** Record the R version and package versions used to generate the final results.

For reproducibility, the final code should document missing-value handling, category mappings, feature definitions, sampling, scaling, K-Means initialization, and output generation.

## 13. Future Improvements

- Test cluster stability across different random samples and initializations.
- Perform sensitivity analysis without treatment status as a clustering feature.
- Investigate demographic and occupational differences while accounting for small subgroup sizes and sampling bias.
- Validate the composite indicators against suitable external measures, if available.
- Add confidence intervals for cluster proportions and other appropriate descriptive estimates.
- Improve documentation and automated execution so that the analysis can be reproduced from a clean R environment.

## 14. Disclaimer

This project is an academic data analytics study. It does not diagnose mental health conditions, recommend treatment, or replace consultation with qualified healthcare professionals. Cluster labels describe patterns in the selected survey features and should not be interpreted as clinical categories.

---

**Project:** Mental Health Risk Profiling and Treatment-Gap Identification Using K-Means Clustering  
**Course:** BCSE335L — Healthcare Data Analytics  
**Author(s):** Atharv Agarwal
**Academic Year:** 2026–2027
