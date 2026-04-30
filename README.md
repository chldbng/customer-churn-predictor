# 📉 Telco Customer Churn Predictor
*A machine learning project to predict customer churn in the telecom industry and deploy the best model as an interactive web app.*

## 📌 Problem Statement
Customer churn is one of the costlies challenges in the telecom industry. Acquiring a new customer costs **5-7 times** more than retaining an existing one, yet most telecom companies operate with an annual churn rate of **15-25%**.

Without a data-driven tool, customer success teams have no scalable way to identify at-risk customers before they leave, making retention efforts reactive rather than proactive.

**This project aims to:**
  1. Predict which customers are likely to churn using machine learning models: Linear Regression (baseline model) and Neural Networks (advanced model)
  2. Provide interpretable, actionable insights for business teams
  3. Deploy the best model as an interactive app for real-time churn risk scoring

## 🗂️ Dataset
This project uses the hypothetical 'IBM Telco Customer Churn Dataset' including 7,043 customers with 21 features of demographics, services, billing, and target variable of **Churn** (Yes/No).

## 🔬 Methodology
Data Exploration -> Model Training -> Evaluation -> App Deployment.
  1. Data: Load, clean, and explore the Telco customer dataset
  2. Model Training: Train and compare Logistic Regression (baseline) and Neural Network model
  3. Evaluation: Measure Accuracy, Precision, Recall, F-1 Score, and AUC-ROC
  4. App Deployment: Build an interactive app for real-time churn risk predictions

## 🗺️ Roadmap
* Problem definition and project setup
* Exploratory Data Analysis (EDA) 
* Feature engineering
* Train Logistic Regression baseline *(current progress)*
* Train Neural Network
* Model comparison & selection
* Build and deploy churn prediction app

## 📊 Exploratory Data Analysis
The EDA notebook covers:
* **Data cleaning** - fixing TotalCharges type issues, handling missing values
* **Target distribution** - churn rate and class imbalance analysis
* **Univariate analysis** - distributions of all numeric and categorical features
* **Bivariate analysis** - churn rate by contract type, internet service, payment method, and more
* **Correlation analysis** - heatmap and feature correlation with churn

## ⚙️ Preprocessing and Feature Engineering
### Data Cleaning
| Issue | Solution |
|-------|---------|
| `TotalCharges` stored as string | Converted to numeric, filled 11 empty strings with 0 |
| `customerID` column | Dropped — unique identifier with no predictive value |
| Class imbalance (~26% churn) | Handled via `class_weight='balanced'` in models |

### Encoding
Categorical variables were encoded so machine learning models can 
process them mathematically:
* **Binary encoding** — Yes/No columns mapped to 1/0 
  (e.g. `Partner`, `Dependents`, `PaperlessBilling`)
* **One-hot encoding** — Multi-category columns expanded into binary columns 
  (e.g. `Contract`, `InternetService`, `PaymentMethod`)
* `"No phone service"` and `"No internet service"` consolidated to `"No"` 
  to reduce unnecessary dimensionality

### Outlier Detection
Numerical features were inspected using the **IQR method**:
- No extreme outliers were found in `tenure` or `MonthlyCharges`
- `TotalCharges` outliers are expected — they reflect genuine 
  high-value long-term customers and were retained

### Feature Engineering
7 new features were engineered to improve model performance:

| Feature | Description | Rationale |
|---------|-------------|-----------|
| `charges_per_tenure` | MonthlyCharges / (tenure + 1) | High early charges = churn risk |
| `tenure_group` | Tenure binned into 4 groups | Captures non-linear loyalty effect |
| `is_new_customer` | 1 if tenure ≤ 12 months | New customers churn at higher rates |
| `is_long_term_customer` | 1 if tenure ≥ 48 months | Long-term customers are most loyal |
| `total_services` | Sum of all active services | More services = higher switching cost |
| `avg_charge_per_service` | MonthlyCharges / (total_services + 1) | Value perception per service |
| `has_no_support` | No TechSupport AND No OnlineSecurity | Lack of support = churn risk |
| `is_high_value` | 1 if MonthlyCharges > 75th percentile | High-value customers at risk |

## 📈 Results
### Baseline Model - Logistic Regression
| Metric | No Churn | Churn |
|--------|----------|-------|
| **Precision** | 0.90 | 0.51 |
| **Recall** | 0.73 | 0.77 |
| **F1 Score** | 0.81 | 0.61 |
| **Accuracy** | | 0.74 |
| **ROC-AUC** | | **0.8472** |

### Model Comparison
| Model | ROC-AUC | F1 (Churn) | Precision (Churn) | Recall (Churn) |
|-------|---------|------------|-------------------|----------------|
| Logistic Regression (Baseline) | **0.8472** | 0.61 | 0.51 | 0.78 |
| Random Forest | TBD | TBD | TBD | TBD |

> 🎯 ** Priority Metric: Recal** - catching actual churners matters
> more than false alarms in a business context

## 👤 Author
Ngan (Chloe) Doan
*Personal Project with Assistance of Claude AI*
* Data Science @ Washington University in St Louis
* ngan.chloe.doan@gmail.com | c.b.doan@wustl.edu
* LinkedIn: https://www.linkedin.com/in/ngan-doan/
