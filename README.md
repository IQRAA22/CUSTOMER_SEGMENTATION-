# Customer Segmentation — Unsupervised Learning with PCA & K-Means

This project segments retail customers into distinct groups without any labels. It scales the data, reduces 30+ columns with Principal Component Analysis (PCA), uses the Elbow Method and Silhouette Score to choose the number of clusters, applies K-Means, and translates each cluster into a business persona with a marketing action.

---

## 📁 Repository Contents

| File | Description |
|---|---|
| `customer_segmentation.ipynb` | Google Colab notebook with all code and outputs |
| `images/pca_variance.png` | Cumulative explained variance of PCA |
| `images/elbow_silhouette.png` | Elbow Method and Silhouette Score for K = 2 to 10 |
| `images/clusters.png` | Customer clusters in PCA space |
| `images/personas.png` | Income, spending and deal usage by persona |

> The dataset is not included. The notebook downloads it automatically using `kagglehub`.

---

## 📊 Dataset

- **Source:** [Customer Personality Analysis — Kaggle](https://www.kaggle.com/datasets/imakash3011/customer-personality-analysis)
- **Customers:** 2,240
- **Columns:** 29 — demographics (birth year, education, marital status, income, children), spending on 6 product categories, purchases by channel (web, catalog, store, deals), website visits, campaign responses and recency

---

## 🛠️ Project Workflow

### 1. Data Cleaning
- Filled **24 missing `Income`** values with the median.
- Removed **4 invalid rows**: 3 customers with an age above 100 and 1 with an unrealistic income (666,666).
- Dropped columns with no analytical value: `ID`, `Year_Birth`, `Dt_Customer`, `Z_CostContact`, `Z_Revenue`.
- Final clean data: **2,236 customers**.

### 2. Feature Engineering
| Feature | Description |
|---|---|
| `Age` | 2026 − birth year |
| `Children` | Kids + teenagers at home |
| `TotalSpent` | Total spending across all 6 product categories |
| `TotalPurchases` | Web + catalog + store + deal purchases |

### 3. Encoding & Scaling
- One-Hot Encoding for `Education` and `Marital_Status`.
- **StandardScaler** brought every column to mean 0 and standard deviation 1. Without scaling, `Income` (in thousands) would dominate the Euclidean distance used by K-Means.

### 4. Dimensionality Reduction (PCA)
- **27 components** were needed to keep 95% of the variance.
- For clustering and visualization, the data was reduced to **3 components**, which together explain **35.8%** of the variance (PC1: 23.2%, PC2: 7.2%, PC3: 5.4%).

### 5. Choosing K — Elbow Method & Silhouette Score
K-Means was run for K = 2 to 10. Within the practical range for personas (K = 3 to 6), **K = 3** gave the highest Silhouette Score, which also matched the bend in the Elbow curve.

### 6. K-Means Clustering (K = 3)

## 👥 Customer Personas

| | Cluster 0 | Cluster 1 | Cluster 2 |
|---|---|---|---|
| **Persona** | 💎 Affluent Premium Buyers | 🛒 Budget-Conscious Browsers | 👨‍👩‍👧 Deal-Seeking Family Shoppers |
| Customers | 558 (25%) | 1,049 (47%) | 629 (28%) |
| Avg. Age | 57.3 | 54.4 | 61.6 |
| Avg. Income | $76,166 | $35,149 | $58,497 |
| Avg. Children | 0.2 | 1.2 | 1.2 |
| Avg. Total Spent | **$1,398** | $101 | $747 |
| Avg. Total Purchases | 20.8 | 8.0 | 21.1 |
| Avg. Deal Purchases | 1.2 | 2.0 | **3.8** |
| Avg. Web Visits / Month | 2.8 | **6.4** | 5.7 |

### Who they are & what to do

**💎 Affluent Premium Buyers (Cluster 0)**
Highest income, mostly no children, spend the most and rarely use discounts.
*Action:* premium product lines, loyalty and VIP programs, exclusive early access. Discounts are unnecessary for this group.

**🛒 Budget-Conscious Browsers (Cluster 1)**
The largest group. Lowest income and spending, but they visit the website more than anyone else.
*Action:* retargeting ads, small entry-level bundles and first-purchase discounts to convert browsing into buying.

**👨‍👩‍👧 Deal-Seeking Family Shoppers (Cluster 2)**
Middle income with children, buy often and use deals the most.
*Action:* family bundles, coupons and multi-buy offers such as "buy 2, get 1".

---

## 💡 Key Findings

- Income, spending and children were the strongest factors separating the customers.
- `Recency` was almost the same in every cluster (~49 days), so it did not help separate the groups.
- Nearly half of the customers (Cluster 1) browse a lot but spend little — the biggest growth opportunity for the business.
- 3 PCA components keep only 35.8% of the variance. This is a trade-off accepted for clear visualization; using more components could produce more detailed segments.

---

## 🧰 Tools & Libraries

Python · Pandas · NumPy · Scikit-Learn (StandardScaler, PCA, KMeans, Silhouette Score) · Matplotlib · Seaborn · Google Colab · kagglehub

---

## ▶️ How to Run

1. Open `customer_segmentation.ipynb` in [Google Colab](https://colab.research.google.com/).
2. Run the cells one by one from the top. The first cell downloads the dataset automatically.

---
