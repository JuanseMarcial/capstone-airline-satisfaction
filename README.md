# Airline Passenger Satisfaction: An Integrated Psychometric and Machine Learning Framework

**Author:** Juan Sebastian Marcial Piedra
**Institution:** IE University, Bachelor in Data and Business Analytics
**Course:** Capstone Project, 4th Year
**Date:** March 2026

## Abstract

This thesis develops an integrated analytical framework that combines psychometric measurement theory with machine learning to diagnose and prioritise airline service quality improvements. The pipeline applies Item Response Theory (via single-factor Exploratory Factor Analysis as a proxy for the Graded Response Model) to extract a continuous latent satisfaction score from 14 Likert-scale survey items. K-Means clustering (k=4, PCA-validated) segments passengers into interpretable archetypes along three dimensions: latent satisfaction, departure delay, and flight distance. A Random Forest classifier (91.58% test accuracy, 5-fold CV: 91.46%) predicts binary satisfaction, and SHAP (TreeExplainer) decomposes feature-level driver importance. The central methodological contribution is the **Strategic Priority Matrix**, a novel two-dimensional diagnostic tool that plots each service dimension according to its psychometric sensor quality (factor loading) on the horizontal axis and its predictive driver impact (mean absolute SHAP value) on the vertical axis, producing four actionable quadrants: Critical Priority, Hidden Drivers, Hygiene Factors, and Low Priority.

## Repository Structure

```
.
├── README.md
├── requirements.txt
├── notebooks/
│   └── JuanseMarcial_FinalThesis_Code_v2.ipynb    # Full analysis pipeline
├── thesis/
│   └── FinalSubmission_JuanseMarcial_Draft8.docx   # Final thesis document
├── data/
│   └── airline_passenger_satisfaction.csv           # Dataset (130K rows)
├── figures/
│   ├── cell_9_img_0.png     # Figure 1: Likert distributions + correlation heatmap
│   ├── cell_10_img_1.png    # Figure 2: Departure delay + flight distance distributions
│   ├── cell_13_img_2.png    # Figure 4: Factor loadings + Item Information Functions
│   ├── cell_16_img_3.png    # Figure 3: Elbow + Silhouette for k=4
│   ├── cell_18_img_4.png    # Figure 5: PCA projection + segment heatmap
│   ├── cell_21_img_5.png    # Figure 6: Confusion matrix (91.58% accuracy)
│   ├── cell_24_img_6.png    # Figure 7: SHAP summary plot
│   ├── cell_25_img_7.png    # Figure 8: SHAP dependence plots
│   └── cell_28_img_8.png    # Figure 9: Strategic Priority Matrix
└── .gitignore
```

## Methodology Pipeline

The analysis follows a five-stage pipeline:

1. **Latent Trait Estimation (IRT Proxy):** Single-factor EFA extracts a continuous satisfaction score from 14 Likert items, with factor loadings interpreted as IRT discrimination parameters.

2. **Customer Segmentation (K-Means):** Passengers are clustered on latent satisfaction, departure delay, and flight distance, producing four interpretable archetypes validated via PCA projection and silhouette analysis (s = 0.406).

3. **Predictive Modelling (Random Forest):** A 100-tree ensemble (max_depth=12) predicts binary satisfaction with 91.58% accuracy on a held-out test set (N=5,000), confirmed by 5-fold cross-validation (91.46% +/- 0.34%).

4. **Feature Attribution (SHAP):** TreeExplainer decomposes predictions into per-feature contributions, identifying online boarding, inflight wifi, and leg room as the top three satisfaction drivers.

5. **Strategic Priority Matrix:** A novel synthesis plotting sensor quality (factor loading) against driver impact (SHAP value) to classify service dimensions into four strategic quadrants.

## Dataset

The [Airline Passenger Satisfaction dataset](https://raw.githubusercontent.com/akmand/datasets/main/airline_passenger_satisfaction.csv) from Kaggle contains approximately 130,000 passenger records with 14 Likert-scale service quality items, operational variables, and a binary satisfaction outcome. The analysis uses a stratified subsample of N=25,000 (seed=42).

## Key Results

| Stage | Result |
|-------|--------|
| Factor Analysis | Factor 1 explains 22.9% of variance (unidimensionality supported) |
| Top Discriminating Items | Inflight Entertainment (1.170), Cleanliness (1.053), Seat Comfort (0.966) |
| K-Means (k=4) | 4 segments: short-haul dissatisfied, long-haul dissatisfied, satisfied, delay-resilient |
| Random Forest | 91.58% accuracy, macro F1 = 0.91 |
| Top SHAP Drivers | Online Boarding (0.145), Inflight Wifi (0.093), Leg Room (0.061) |
| Critical Priority | Inflight Entertainment, Seat Comfort, Online Boarding, Onboard Service |

## How to Run

```bash
# Clone the repository
git clone https://github.com/JuanseMarcial/capstone-airline-satisfaction.git
cd capstone-airline-satisfaction

# Install dependencies
pip install -r requirements.txt

# Run the notebook
jupyter notebook notebooks/JuanseMarcial_FinalThesis_Code_v2.ipynb
```

The notebook downloads the dataset automatically and produces all figures and results in sequence.

## Technologies

- Python 3.9+
- scikit-learn (Factor Analysis, K-Means, Random Forest)
- SHAP (TreeExplainer)
- pandas, NumPy, Matplotlib, Seaborn
- python-docx (thesis document generation)

## License

This project is submitted as part of the IE University Capstone Project requirements. All rights reserved.
