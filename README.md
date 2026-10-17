# Customer Churn Analysis: Python & Power BI
An end-to-end analysis of telecom customer churn: data cleaning and exploratory analysis in Python, followed by an interactive two-page Power BI dashboard.

## Business Problem
A telecom company is losing customers. This project answers:

1. What is the overall churn rate?
2. Which customer groups churn the most?
3. When in the customer lifecycle do customers leave?
4. What can the company do to reduce churn?

## Dataset
- **Source:** Telco Customer Churn dataset (add the link where you downloaded it)
- **Size:** 7,043 customers, 21 columns (7,032 rows after cleaning)
- **Columns include:** gender, senior citizen, partner, dependents, tenure, phone and internet services, add-on services (online security, tech support, streaming), contract type, payment method, monthly charges, total charges, and churn

## Tools Used
- **Python:** Pandas, NumPy, Matplotlib, Seaborn (Jupyter Notebook in VS Code)
- **Power BI:** Power Query for data type validation, DAX measures, interactive dashboard

## Project Structure
```
Customer_churn/
├── data/
│   ├── churn.csv                 # original dataset
│   └── churn_clean.csv           # cleaned dataset used in Power BI
├── notebook/
│   └── churn_analysis.ipynb      # full analysis
├── outputs/
│   ├── Churn_Analysis_Dashboard  # Power BI dashboard file
│   └── *.png                     # saved charts and dashboard screenshots
├── requirements.txt
└── README.md
```

## Data Cleaning
- `TotalCharges` was stored as text because of hidden blank values. Converted it to numeric, which exposed 11 missing values.
- Dropped those 11 rows: all had tenure = 0 (new customers not yet billed) and were about 0.16% of the data.
- Checked for duplicate rows and duplicate customer IDs (none found).
- Converted `SeniorCitizen` from 0/1 to No/Yes for consistency.
- Created `ChurnFlag` (1 = churned, 0 = stayed) to calculate churn rates.
- Created `TenureGroup` (0-1 yr, 1-2 yr, 2-4 yr, 4-6 yr) using `pd.cut` to compare customer lifecycle stages.

## Key Findings
**Overall churn rate: 26.58%** (1,869 of 7,032 customers).

| Driver | Highest-risk group | Churn rate | Lowest-risk group | Churn rate |
|---|---|---|---|---|
| Contract | Month-to-month | 42.71% | Two year | 2.85% |
| Payment method | Electronic check | 45.29% | Credit card (automatic) | 15.25% |
| Internet service | Fiber optic | 41.89% | No internet | 7.43% |
| Online security | No | 41.78% | Yes | 14.64% |
| Tech support | No | 41.65% | Yes | 15.20% |
| Tenure group | 0-1 yr | 47.68% | 4-6 yr | 9.51% |
| Senior citizen | Yes | 41.68% | No | 23.65% |
| Dependents | No | 31.28% | Yes | 15.53% |

- **Churn happens early:** 55.5% of all churned customers left within their first year. Churned customers had an average tenure of about 18 months, versus about 38 months for retained customers.
- **Higher bills are associated with churn:** churned customers paid an average of $74.44 per month, versus $61.31 for retained customers.
- **Fiber optic customers** are mostly on month-to-month contracts (68.7%). Fiber customers without tech support churn at 49.4%, versus 22.6% with it.
- **Gender has no meaningful effect** on churn (26.96% vs 26.20%).

## Recommendations
1. **Move customers to longer contracts** with discounts or perks for month-to-month customers who switch to 1- or 2-year plans.
2. **Focus on the first 12 months** with better onboarding and early check-ins.
3. **Promote automatic payments** with a small bill credit for customers paying by electronic check.
4. **Bundle support services:** offer tech support and online security trials, especially to fiber customers.
5. **Prioritize high-risk segments** such as new, single customers without dependents.

## Dashboard
**Page 1: Overview.** KPI cards (total customers, churned customers, churn rate, average monthly charges), slicers (contract, senior citizen, internet service, tenure group), and churn rate charts by contract, payment method, and internet service, plus the share of churned customers by tenure group.

![Dashboard page 1](Outputs/dashboard_page1.png)

**Page 2: Insights.** Churn rate by tenure group and tech support, with a summary of key insights and recommendations.

![Dashboard page 2](Outputs/dashboard_page2.png)

## How to Run
1. Clone this repository.
2. Install the requirements: `pip install -r requirements.txt`
3. Open `notebook/churn_analysis.ipynb` in VS Code or Jupyter and choose **Run All**.
4. Open the dashboard file in Power BI Desktop (free) to explore the dashboard.

## Limitations
- The analysis shows **associations, not proven causes**. For example, customers with tech support may also be more engaged in general.
- The dataset is a single snapshot. It has no data on why customers left, competitor pricing, or service quality.

## Next Steps
- Build a churn prediction model (for example logistic regression or random forest) to flag at-risk customers.
- Add a customer segmentation analysis.

## Author
**Rajalakshmi Manivannan**
LinkedIn: https://www.linkedin.com/in/rajalakshmi8220029137
GitHub: github.com/Rajalakshmi1605