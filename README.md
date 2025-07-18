
# 📊 Customer Churn Analysis – Telco Subscription Service

This project analyzes the Telco Customer Churn dataset to uncover key drivers of customer churn and suggest actionable strategies to improve retention. It includes a unique risk scoring heatmap based on tenure and billing patterns, offering deep insights into customer behavior.

---

## 🎯 Objective

- Analyze churn patterns using real-world telecom data
- Identify factors that contribute to customer attrition
- Create visual insights and a unique churn heatmap
- Recommend actionable business strategies to reduce churn

---

## 🗃 Dataset Overview

- **Source**: [Kaggle – Telco Customer Churn](https://www.kaggle.com/datasets/blastchar/telco-customer-churn)
- **Rows**: 7,043 customers
- **Columns**: 21 variables (demographics, service details, billing info, churn status)

---

## 🧰 Tools Used

- **Python** – Pandas, NumPy, Seaborn, Matplotlib
- **Jupyter Notebook**

---

## 🧼 Data Cleaning Summary

- Converted `TotalCharges` to numeric (handling blank values)
- Removed missing values and duplicates
- Replaced encoded binary columns (e.g., `SeniorCitizen` from 0/1 to Yes/No)
- Created grouped bins for tenure and monthly charges

---

## 📊 Exploratory Data Analysis (EDA)

Key insights visualized using bar plots, boxplots, and histograms:
- Churn rate by contract type, tenure, and monthly charges
- Payment method and internet service impact on churn
- Service features (tech support, online security) vs churn likelihood

---

## 🌡️ Unique Feature: Churn Risk Scoring Heatmap

A 2D heatmap showing **churn rates** based on combinations of:
- `TenureGroup`: how long a customer has been with the company
- `ChargeGroup`: the customer’s monthly billing level

### 🔥 Insight:
> Customers with **0–6 months tenure** and **high monthly charges** are most likely to churn.

```python
df['TenureGroup'] = pd.cut(df['tenure'], bins=[0, 6, 12, 24, 48, 72], labels=["0–6", "6–12", "12–24", "24–48", "48–72"])
df['ChargeGroup'] = pd.cut(df['MonthlyCharges'], bins=[0, 35, 70, 105], labels=["Low", "Medium", "High"])

pivot = df.pivot_table(index='TenureGroup', columns='ChargeGroup',
                       values='Churn', aggfunc=lambda x: (x=='Yes').mean(), observed=False)

sns.heatmap(pivot, annot=True, cmap='YlOrRd', fmt=".2f")
```

---

## 💡 Business Insights

- High churn among new users with high monthly charges – likely due to pricing dissatisfaction.
- Loyalty is higher in customers with longer tenure and lower billing.
- Customers on month-to-month contracts churn more than those on longer-term plans.
- Paper billing customers show higher churn – a push toward digital billing may help.
- Upsell and retain mid-tenure, high-charge customers before they churn.

---

## ✅ Recommendations

- Launch retention offers for high-billing customers in their first 6 months.
- Encourage switching to annual contracts with discounts.
- Promote digital payments over paper billing.
- Improve onboarding and support for fiber-optic and tech-heavy users.
