# Divar Real Estate Analytics & Machine Learning

[![Python](https://img.shields.io/badge/Python-3.10%2B-blue)]()
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange)]()
[![Machine Learning](https://img.shields.io/badge/Machine%20Learning-Scikit--Learn-green)]()
[![NLP](https://img.shields.io/badge/Persian%20NLP-Hazm%20%7C%20FastText-purple)]()

## Overview

This repository presents a complete data science workflow on a large-scale Persian real estate advertising dataset from **Divar**.  
The original dataset contains around **1,000,000 real estate ads** with approximately **60 columns**, covering different listing categories such as residential sale, residential rent, commercial properties, temporary rentals, and construction-related listings.

The project combines **data cleaning**, **exploratory data analysis**, **market insight extraction**, **price prediction**, **clustering**, **dimensionality reduction**, and **Persian NLP classification**.

## Why this project matters

Real estate platforms generate high-volume, noisy, and heterogeneous data. Different listing types have different fields, many missing values, inconsistent user-generated text, and mixed numerical/categorical features. This project demonstrates how to transform such raw platform data into useful analytical and predictive outputs.

The repository is designed as a portfolio-ready data science project that shows:

- Practical work with a large real-world dataset
- Data quality analysis and preprocessing
- Feature engineering for structured real estate data
- Regression modeling for property price prediction
- Unsupervised learning for market segmentation
- Persian text preprocessing and NLP-based classification
- Model comparison and evaluation

## Project objectives

1. Analyze the structure and quality of a large real estate dataset.
2. Separate heterogeneous real estate categories into meaningful analytical subsets.
3. Explore property market patterns across Iranian cities and neighborhoods.
4. Predict residential sale prices using machine learning models.
5. Cluster similar real estate ads and reduce feature dimensions with PCA.
6. Classify property type from Persian advertisement text.
7. Classify user type from Persian advertisement text.

## Repository structure

```text
divar-real-estate-analytics-portfolio/
│
├── data/
│   ├── raw/                 # Place original CSV files here
│   └── processed/           # Generated intermediate datasets
│
├── notebooks/
│   ├── 01_eda_data_quality.ipynb
│   ├── 02_market_analysis_iran_real_estate.ipynb
│   ├── 03_sell_residential_price_prediction.ipynb
│   ├── 04_clustering_and_pca.ipynb
│   ├── 05_property_type_prediction_nlp.ipynb
│   └── 06_user_type_prediction_nlp.ipynb
│
├── reports/
│   └── course_final_report.pdf
│
├── models/                 # Trained models, if exported
├── figures/                # Saved charts and visual outputs
├── docs/                   # Extra documentation
├── requirements.txt
├── .gitignore
└── README.md
```

## Notebook guide

| Notebook | Main focus | Key techniques |
|---|---|---|
| `01_eda_data_quality.ipynb` | Data quality and exploratory analysis | Missing values, duplicates, inconsistency checks, outlier review |
| `02_market_analysis_iran_real_estate.ipynb` | Real estate market insight extraction | City/neighborhood analysis, property-type distribution, amenity-based analysis |
| `03_sell_residential_price_prediction.ipynb` | Residential sale price prediction | Regression models, preprocessing pipelines, imputation, encoding, model comparison |
| `04_clustering_and_pca.ipynb` | Segmentation and dimensionality reduction | K-Means, DBSCAN, WCSS, Silhouette, PCA |
| `05_property_type_prediction_nlp.ipynb` | Property category classification from Persian text | Hazm, FastText embeddings, Logistic Regression, Random Forest, Linear SVM, SGD |
| `06_user_type_prediction_nlp.ipynb` | User type classification from Persian text | Persian text cleaning, FastText, supervised classification |

## Dataset notes

The raw dataset is not included in this repository because of its size and possible redistribution limitations.

Expected files:

```text
data/raw/divar_real_estate_ads.csv
data/raw/real_estate_ads.csv
data/raw/Stopwords.csv
```

Depending on the notebook, `divar_real_estate_ads.csv` and `real_estate_ads.csv` may refer to the same original dataset with different naming conventions. If needed, rename your local dataset file or update the path in the first cells of the notebooks.

## Methodology

### 1. Data understanding and quality checks

The first step focuses on understanding the dataset structure and identifying common real-world data issues:

- High missing-value rate caused by mixed listing categories
- Duplicate records
- Inconsistent values in fields such as floor, total floors, balcony, and capacity
- Unrealistic values in price and size fields
- Category-specific columns that are irrelevant for other property types

### 2. Category-aware preprocessing

Because the dataset contains many different real estate ad categories, the project separates the data into meaningful subsets instead of treating all rows as one homogeneous table.

Main groups include:

- Residential sale
- Residential rent
- Commercial sale
- Commercial rent
- Temporary rent
- Construction-related listings

For price prediction, the main focus is on **residential sale listings**.

### 3. Exploratory market analysis

The market analysis notebook investigates patterns such as:

- Cities with the highest number of listings
- Dominant property categories in Tehran
- Neighborhood-level distribution of apartments and villas
- Renovated vs. non-renovated properties
- New-build apartment patterns
- Amenity-based property distribution

### 4. Price prediction

The price prediction module focuses on residential sale listings and compares several regression models.

Models used:

- Linear Regression
- Ridge Regression
- Random Forest Regressor
- K-Nearest Neighbors Regressor
- CatBoost Regressor

Structured preprocessing includes:

- Missing-value imputation
- Numerical scaling
- Categorical encoding
- Feature selection by category
- Separate modeling for apartment and house/villa listings

### 5. Clustering and dimensionality reduction

The unsupervised learning module uses selected numerical and engineered features to identify groups of similar real estate ads.

Techniques used:

- Standardization
- K-Means clustering
- WCSS elbow method
- Silhouette analysis
- DBSCAN
- PCA for dimensionality reduction and visualization

### 6. Persian NLP classification

Two text classification tasks are included:

#### Property type prediction

Predicts detailed property category from advertisement title and description.

Pipeline:

```text
Raw Persian text
→ Normalization
→ Tokenization
→ Lemmatization
→ Stopword removal
→ FastText embeddings
→ Document vector averaging
→ Classification models
```

Best reported model: **Linear SVM** with approximately **76% accuracy**.

#### User type prediction

Predicts whether an ad was posted by a real estate agent or a personal user based on text patterns.

Best reported model: **Linear SVM** with approximately **85.6% accuracy**.

## Selected results

| Task | Best / notable result |
|---|---|
| Apartment sale price prediction | Random Forest and CatBoost performed strongly; CatBoost reached about `R² ≈ 0.91`, while Random Forest achieved the lowest MAE in the reported run |
| House/villa sale price prediction | Random Forest and CatBoost performed best among tested models, with `R² ≈ 0.67` |
| Property type prediction | Linear SVM achieved about `76%` accuracy |
| User type prediction | Linear SVM achieved about `85.6%` accuracy |
| Clustering | K-Means segmentation was tested and visualized; one reported run used 9 clusters on about 69k records |
| PCA | Reduced selected structured features from 19 dimensions to 5 components |

## How to run

### 1. Clone the repository

```bash
git clone https://github.com/<your-username>/divar-real-estate-analytics.git
cd divar-real-estate-analytics
```

### 2. Create a virtual environment

```bash
python -m venv .venv
```

Activate it:

```bash
# Windows
.venv\Scripts\activate

# macOS / Linux
source .venv/bin/activate
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

### 4. Add the dataset

Place the raw dataset files inside:

```text
data/raw/
```

### 5. Run notebooks

Open JupyterLab or Jupyter Notebook:

```bash
jupyter lab
```

Recommended execution order:

1. `01_eda_data_quality.ipynb`
2. `02_market_analysis_iran_real_estate.ipynb`
3. `03_sell_residential_price_prediction.ipynb`
4. `04_clustering_and_pca.ipynb`
5. `05_property_type_prediction_nlp.ipynb`
6. `06_user_type_prediction_nlp.ipynb`

## Skills demonstrated

- Python for data analysis
- Pandas and NumPy
- Data cleaning and preprocessing
- Missing-value handling
- Exploratory data analysis
- Data visualization
- Feature engineering
- Regression modeling
- Model evaluation
- Clustering and PCA
- Persian NLP preprocessing
- FastText embeddings
- Scikit-learn pipelines
- Working with large, noisy real-world datasets

## Limitations and future improvements

This project was originally developed as a course final project. For a production-grade version, the following improvements are recommended:

- Convert repeated notebook logic into reusable Python modules
- Add automated tests for preprocessing functions
- Add configuration files for paths and model parameters
- Save final charts into the `figures/` directory
- Track experiments with MLflow or a similar tool
- Add model serialization and inference scripts
- Add sample anonymized data for reproducibility
- Add more robust hyperparameter tuning
- Improve NLP models using transformer-based Persian language models

## Contributors

This project was completed as a course final project by:

- Parsa Sepehri
- Mahya Shayani
- Saeideh Masjedjamei

## License

This repository is intended for educational and portfolio purposes.  
Before sharing the dataset or trained models, make sure you have the right to redistribute the data.
