# Guest_Intelligence_System_Final_Project
Guest Intelligence System (GIS) — A hospitality recommender system  combining Content-Based Filtering and Collaborative Filtering (WBPR)  to deliver personalized activity recommendations with interactive Streamlit dashboard.  
Final Data Science and Machine Learning Project.

<p align="center">
  <img src="https://img.shields.io/badge/Python-3.x-3776AB?logo=python&logoColor=white" alt="Python">
  <img src="https://img.shields.io/badge/Jupyter-Notebook-F37626?logo=jupyter&logoColor=white" alt="Jupyter Notebook">
  <img src="https://img.shields.io/badge/Streamlit-App-FF4B4B?logo=streamlit&logoColor=white" alt="Streamlit">
  <img src="https://img.shields.io/badge/SQLite-Database-003B57?logo=sqlite&logoColor=white" alt="SQLite">
  <img src="https://img.shields.io/badge/Pandas-Data%20Analysis-150458?logo=pandas&logoColor=white" alt="Pandas">
  <img src="https://img.shields.io/badge/Scikit--Learn-ML-F7931E?logo=scikit-learn&logoColor=white" alt="Scikit-learn">
  <img src="https://img.shields.io/badge/Cornac-Recommender-6A0DAD?logoColor=white" alt="Cornac">
  <img src="https://img.shields.io/badge/Plotly-Visualization-3F4F75?logo=plotly&logoColor=white" alt="Plotly">
  <img src="https://img.shields.io/badge/NumPy-Scientific-013243?logo=numpy&logoColor=white" alt="NumPy">
  <img src="https://img.shields.io/badge/Seaborn-Visualization-4C72B0?logoColor=white" alt="Seaborn">
  <img src="https://img.shields.io/badge/Faker-Data%20Generation-00C58E?logoColor=white" alt="Faker">
  <img src="https://img.shields.io/badge/License-MIT-green" alt="MIT License">
</p>

<h1 align="center"> Guest Intelligence System (GIS)</h1>

<p align="center">
  <img src="2.EDA_files/Logo.png" width="200" alt="GIS Logo">
</p>

<p align="center">
  <em>A hospitality recommender system combining Content-Based Filtering and Collaborative Filtering (WBPR) to deliver personalized activity recommendations — Final Data Science & Machine Learning Project</em>
</p>

## 📑 Table of Contents

1. [Project Overview](#-project-overview)
2. [Goal](#-goal)
3. [Repository Structure](#-repository-structure)
4. [Dataset Description](#-dataset-description)
5. [Methodology and Steps](#-methodology-and-steps)
6. [Repository Policy](#-repository-policy)
7. [Reuse in Other Projects](#-reuse-in-other-projects)
8. [Future Development](#-future-development)
9. [Reports](#-reports)
10. [Authors](#-authors)
11. [License](#-license)


---

## 📌 Project Overview

The **Guest Intelligence System (GIS)** is a behavioral KYC and personalized recommender system built for the hospitality industry. It combines structured guest data — bookings, stays, reviews, activity preferences, complaints — to build rich guest profiles and deliver intelligent, personalized activity recommendations through an interactive Streamlit dashboard.

The system was designed to simulate a real-world luxury hotel intelligence platform, **I create a synthetically generated data** that mirrors realistic guest behavior patterns. The complete pipeline covers data generation, exploratory analysis, feature engineering, model development, and a production-ready chatbot interface.

---

## 🎯 Goal

- Build a **Hybrid Recommender System** combining Content-Based Filtering (cosine similarity) and Collaborative Filtering (Weighted Bayesian Personalized Ranking — WBPR) using adaptive weights based on guest interaction history.
- Create a **Behavioral KYC profile** for each guest — capturing spending behavior, satisfaction, mobility needs, dietary restrictions, special occasions, and more.
- Deliver a **Streamlit chatbot** where hotel staff can query any guest and receive personalized activity recommendations with full explainability (scores, radar charts, feature importance).
- Provide **Business Intelligence** insights — guest origins map, market fit analysis, activity demand seasonality, and Pareto analysis of activity performance.

## 🗂 Repository Structure

```
GUEST_INTELLIGENCE_SYSTEM/
│
├── 2.EDA_files/              # EDA visualizations and supporting files
├── Chatboot_Video_u.../      # Demo video of the Streamlit application
├── 2.EDA.md                  # Exploratory Data Analysis report (Markdown)
├── Guest Intelligence ...    # Project documentation
├── LICENSE                   # MIT License
└── README.md                 # This file
```

> ⚠️ **Note:** This public repository contains only a curated subset of the project — EDA reports, visualizations, and a demo video. The full project (datasets, feature engineering, model notebooks, Streamlit app, and trained models) is available in a **private repository upon request**. See [Repository Policy](#-repository-policy) for details.

---

## 📊 Dataset Description

All datasets were synthetically generated using **Faker** and domain-specific logic to simulate realistic hospitality data. The database is stored in **SQLite** (`guest_intelligence.db`) and exported to CSV for processing.

| # | Dataset | Rows | Description |
|---|---------|------|-------------|
| 1 | `GUEST_PROFILE` | 3,500 | Guest demographics, preferences, loyalty, GDPR |
| 2 | `BOOKING_HISTORY` | 5,000 | Reservation details, packages, payment, channel |
| 3 | `STAY_BEHAVIOR` | 3,021 | In-stay spending, complaints, satisfaction |
| 4 | `REVIEWS` | 3,021 | Detailed ratings across 20+ service dimensions |
| 5 | `ACTIVITY_CATALOG` | 81 | Activities across 8 categories with attributes |
| 6 | `COMPLAINTS_LOG` | — | Complaint details, resolution, compensation |
| 7 | `ACTIVITY_PREFERENCES` | 3,021 | Declared interests, attended activities, accessibility needs |

**Activity Categories:** Water & Sea · Wellness · Culture & History · Adventure · Gastronomy · Nature & Land · Entertainment · Family

---

## 🔬 Methodology and Steps

### Step 1 — Data Generation
Synthetic data generated with `Faker`, `random`, `datetime`, `unicodedata` and domain-specific business rules. Stored in SQLite and exported to raw CSV files.

### Step 2 — Exploratory Data Analysis (EDA)
Univariate and bivariate analysis across all datasets. Visualizations with `Matplotlib` and `Seaborn`.

### Step 3 — Feature Engineering
Encoding of categorical variables, aggregation of signals and flags.

### Step 4 — Recommender Dataset
Construction of the unified recommender dataset by merging all feature-engineered tables (`GUEST_PROFILE`, `BOOKING_HISTORY`, `STAY_BEHAVIOR`, `REVIEWS`, `ACTIVITY_PREFERENCES`) and normalizing with `MinMaxScaler`. 
The `ACTIVITY_CATALOG` was normalized separately, as it serves as a bridge between the guest feature space and the activity feature space.

### Step 5 — Display Dataset
Construction of the unified display dataset by merging all tables with their original raw data (`GUEST_PROFILE`, `BOOKING_HISTORY`, `STAY_BEHAVIOR`, `REVIEWS`, `ACTIVITY_PREFERENCES`, `COMPLAINTS_LOG`). 
The `ACTIVITY_CATALOG` was also rebuilt as a display dataset, enriched with a curated image URL for each activity.

### Step 6 — Recommender Model

#### Content-Based Filtering
Cosine similarity between guest and activity feature vectors across 6 dimensions: price range, family, solo, couple, kids, wellness. Hard filters applied for wheelchair accessibility. Affinity bonus (×1.2) for favourite category.

#### Collaborative Filtering — WBPR
Interaction enrichment to reduce sparsity from **95.8% → 61.4%** (7,329 → 66,010 interactions) adding behavioral flags (spa, bar, excursion usage).
Weighted Bayesian Personalized Ranking via `Cornac` library (Python 3.13 compatible). 
Best metrics: **NDCG@10 = 0.8386 · Precision@10 = 0.5239 · Recall@10 = 0.8213**.

#### Hybrid Model — Adaptive Weights
| Guest History | CB Weight | CF Weight |
|---------------|-----------|-----------|
| 0 interactions | 100% | 0% |
| 1–9 interactions | 60% | 40% |
| 10+ interactions | 40% | 60% |

### Step 7 — Streamlit Chatbot
Interactive luxury-themed dashboard with:
- **Sidebar — Guest Controls:** Guest ID input, number of recommendations slider, and filters (category, price range, physical intensity, wheelchair accessibility) — the primary entry point to generate personalized recommendations.
- **Sidebar — Model Performance:** Pop-up dialog displaying the Collaborative Filtering evaluation metrics: NDCG@10, Precision@10, Recall@10, and interaction matrix sparsity.
- **Sidebar — Business Insights:** Pop-up dialog with business-level analytics — guest origins choropleth map, Market Fit radar (supply vs demand), activity demand seasonality by category, and Pareto analysis of activity performance (Stars vs Dogs).
- **Tab 1 — Recommendations:** Activity cards with images, hybrid/content/collaborative scores, recommendation reason pills, and category/price/intensity tags.
- **Tab 2 — Guest Profile:** Full KYC profile with nationality map and 6 subtabs — Guest Info, Booking History, Behavioral Data, Reviews, Activity Preferences, and Complaints Log.
- **Tab 3 — Analytics:** Score breakdown bar chart, recommended categories donut chart, radar charts (guest vs activity match), scatter plot (price vs intensity), sunburst catalog hierarchy, and feature importance (Explainable AI).

---

## 🔒 Repository Policy

This is a **public showcase repository** containing:
- ✅ EDA report and visualizations
- ✅ Application demo video
- ✅ Project presentation slides (exported as PDF)

The following are **not included** in this public repository:
- ❌ Raw and processed datasets (contain synthetic PII)
- ❌ Feature engineering notebooks
- ❌ Model training notebooks and trained model files
- ❌ Full Streamlit application source code

> 📩 **To view the complete project**, please get in touch — contact details are available in the [Authors](#-authors) section below.


## 🔄 Reuse in Other Projects

The GIS architecture is modular and can be adapted for other domains:

- **Retail** — Replace activity catalog with product catalog; guest profile with customer profile
- **Streaming** — Replace activities with content items; stays with viewing sessions
- **Healthcare** — Replace activities with treatment/wellness programs
- **Education** — Replace activities with courses; guest preferences with learning styles

Key components to reuse:
- Interaction enrichment strategy (behavioral flag → implicit feedback)
- Adaptive weight hybrid model (CB + CF based on interaction density)
- WBPR via Cornac (handles high sparsity datasets)
- Streamlit luxury dashboard template

---

## 🚀 Future Development

The following features are planned for future versions of the GIS:

| Feature | Description |
|---------|-------------|
| 🍽️ Restaurant Recommender | Extend recommendations to on-property dining experiences |
| 💳 Guest Financial Profile | Address financial behavior gaps for revenue optimization |
| 🔍 Behavioral KYC for Fraud Detection | Complete fraud detection and risk assessment using behavioral signals |
| 🚨 Real-time Complaint Detection | Implement live complaint detection and automated resolution routing |
| 💬 Sentiment Analysis | Add NLP sentiment analysis for emotional value detection in reviews |
| 🌐 Production Deployment | Deploy with live guest data integration and real-time recommendations |

---

## 📈 Reports

| Report | Description |
|--------|-------------|
| `2.EDA.md` | Full Exploratory Data Analysis with visualizations |
| `Chatboot_Video` | Demo video of the Streamlit application in action |

---

## 👤 Authors

**Janete Barbosa**
- 🎓 Data Science & Machine Learning — Final Project
- 💼 [LinkedIn](https://linkedin.com/in/janete-barbosa)
- 🐙 [GitHub](https://github.com/janeteccbarbosa28-eng)

---

## 📄 License

This project is licensed under the **MIT License** — see the [LICENSE](LICENSE) file for details.

---

<p align="center">
  <em>Built with 💛 for the hospitality industry — GIS © 2026 Janete Barbosa</em>
</p>
