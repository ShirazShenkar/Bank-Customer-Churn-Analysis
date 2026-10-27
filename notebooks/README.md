# Bank Customer Churn Analysis — Python Notebook

This folder contains the Python notebook for the Bank Customer Churn Analysis project.

**Notebook:** [`bank_churn_pro.ipynb`](bank_churn_pro.ipynb)

The notebook studies which customers leave the bank, why they leave, and where financial risk is concentrated. It turns the customer table into a clear story: overall churn, the main drivers (products, age, country, activity, reasons), and a shortlist of remaining customers to protect.

---

## What the notebook does

1. Loads `../data/Bank_Churn_Data.csv` and inspects shape, types, missing values, and unique counts.
2. Calculates headline KPIs: customer count, churn rate, departed balance, and estimated profit loss.
3. Charts churn over time, by products, age, country, and activity.
4. Breaks down **why** customers left, using the `Churn_Reason` field.
5. Scores remaining customers by segment risk and ranks retention priority groups.

**Libraries used:** Pandas, NumPy, Matplotlib.

---

## How to run

1. Open `bank_churn_pro.ipynb` in Jupyter or VS Code / Cursor.
2. Run the first code cell to install packages, or install them yourself:

```python
%pip install pandas numpy matplotlib
```

3. Run all remaining cells from top to bottom.

The data path in the notebook is relative to this folder:

```python
db_bank_churn = pd.read_csv("../data/Bank_Churn_Data.csv")
```

---

## Notebook structure

| Section | Content |
| :--- | :--- |
| **1. Setup and data overview** | Load the CSV and inspect structure, missing values, and unique counts. |
| **2. Business snapshot** | Headline KPIs: customers, churn rate, lost balance, and 4% profit assumption. |
| **3. Churn over time** | Quarterly exits in 2023 and the balance that left with them. |
| **4. Products and churn** | Churn rate and headcount by number of products. |
| **5. Age and churn** | Churn rate and headcount by age range. |
| **6. Financial loss by age** | Estimated loss per age group as 4% of departed balance. |
| **7. Geography, age, and loss** | Country–age combinations with high volume and high financial impact. |
| **8. Why customers leave** | Reason mix overall, then by products, age, country, and activity. |
| **9. Retention priority** | Segment risk scoring and a shortlist of remaining-customer groups to protect. |

---

## Dataset used by the notebook

The notebook reads **10,000 rows** and **16 columns**.

| Column | Role in the analysis |
| :--- | :--- |
| `O` | Row identifier |
| `CreditScore` | Credit score |
| `Geography` | Country: France, Germany, or Spain |
| `Gender` | Male or Female |
| `Age` | Customer age |
| `EstimatedSalary` | Estimated salary |
| `Balance` | Account balance; used for financial-loss estimates |
| `NumOfProducts` | Number of bank products (1–4) |
| `HasCrCard` | Credit-card flag (1 / 0) |
| `IsActiveMember` | Activity flag (1 = Active, 0 = Inactive) |
| `Exited` | Churn flag (1 = left, 0 = retained) |
| `Tenure` | Years with the bank |
| `Account_Open_Date` | Account open date |
| `Exit_Date` | Exit date for churned customers; empty for retained customers |
| `Churn_Reason` | Exit reason, or `Retained` for customers who stayed |
| `Customer_Segment` | Segment label used in the source table |

**Missing values in the notebook check:** `Exit_Date` is missing for **7,963** retained customers. That is expected, not a data-quality error. All other columns are complete.

---

## Assumptions used in the notebook

These are stated in the notebook and are **not** observed bank P&L figures:

- Estimated profit / revenue loss = **4% of customer balance**.
- For customers who already left: `lost profit = departed balance × 0.04`.
- For remaining high-risk customers: `estimated annual revenue at risk = remaining high-risk balances × 0.04`.
- For priority groups: `est. annual revenue loss = remaining balance × 4% × historical churn rate`.

`Churn_Reason`, `Account_Open_Date`, and `Exit_Date` are fields in the CSV the notebook loads. They support the reason and time analyses. Treat them as analysis inputs from the prepared table, not as independently verified survey results.

---

## Key results from the notebook

### Headline KPIs

| KPI | Result |
| :--- | :--- |
| Total customers | **10,000** |
| Customers who left | **2,037** |
| Overall churn rate | **20.37%** |
| Departed balance | **185,588,094.63** |
| Estimated lost profit (4% of departed balance) | **7,423,523.79** |
| Remaining customers | **7,963** |
| High-risk remaining customers | **496 (6.2%)** |
| High-risk remaining balance | **51.37M** |
| Estimated annual revenue at risk (4% of high-risk balances) | **2.05M** |

Risk mix among remaining customers: **Low 82.0% | Medium 11.8% | High 6.2%**. Medium + High = **18.0%** (1,433 of 7,963).

### Churn over time (2023)

Share of all churned customers by quarter:

| Quarter | Share of churned customers |
| :--- | :--- |
| 2023 Q1 | 23.07% |
| 2023 Q2 | 23.56% |
| 2023 Q3 | 25.43% |
| 2023 Q4 | 27.93% |

Later quarters carry a larger share of exits.

### Who leaves

| Split | Finding from the notebook |
| :--- | :--- |
| **Country** | Germany **32.44%** churn vs France **16.15%** and Spain **16.67%**. |
| **Age** | Highest rate is ages **51–60 (56.21%)**. Ages 41–50: 33.97%. Ages 18–30: 7.52%. |
| **Products** | 1 product: **27.7%**. 2 products: **7.6%**. 3 products: **82.7%**. 4 products: **100%**. |
| **Activity** | Inactive customers **26.85%** vs active customers **14.27%**. |

### Why they leave

Among the 2,037 customers who left:

| Churn reason | Share |
| :--- | :--- |
| Better Rates or Competitor Offer | **27.00%** |
| Relocation / Personal Circumstances | 21.26% |
| Poor Customer Service Experience | 17.53% |
| Switched to Digital / Mobile Bank | 17.53% |
| High Account & Maintenance Fees | 16.69% |

Selected patterns from the reason splits:

- **Germany:** 46.4% of exits are competitor offers.
- **Ages 41–50:** 35.9% competitor offers.
- **Ages 18–30 / 31–40:** digital switching is the main reason (55.4% and 40.1%).
- **Ages 51–60:** 41.5% cite poor customer service.
- **3–4 products:** most exits are high fees (66.8% and 60.0%).

---

## Retention priority (Section 9)

The notebook scores **remaining** customers by segment: age range × products × activity × country.

| Rule | Definition in the notebook |
| :--- | :--- |
| Historical churn | Churned ÷ all customers in the segment |
| High risk | Segment n ≥ 12 and historical churn ≥ 40% |
| Medium risk | Historical churn ≥ 20% |
| Low risk | Everything else |
| Focus list | Remaining customers ≥ 50, remaining balance ≥ 5,000,000, High or Medium risk; top 9 by estimated loss |

### Priority groups

| Rank | Group | Age | Products | Status | Country | Remaining customers | Historical churn | Est. annual rev. loss |
| :---: | :---: | :---: | :---: | :---: | :--- | ---: | ---: | ---: |
| 1 | P13 | 41–50 | 1 | Inactive | France | 166 | 44.9% | 291.0K |
| 2 | P16 | 31–40 | 1 | Inactive | Germany | 176 | 32.3% | 269.0K |
| 3 | P8 | 41–50 | 1 | Inactive | Germany | 72 | 69.1% | 236.8K |
| 4 | P20 | 31–40 | 1 | Active | Germany | 182 | 24.8% | 215.8K |
| 5 | P18 | 41–50 | 1 | Active | France | 184 | 27.8% | 190.8K |
| 6 | P11 | 41–50 | 1 | Active | Germany | 74 | 51.9% | 187.3K |
| 7 | P12 | 41–50 | 1 | Inactive | Spain | 84 | 48.1% | 150.9K |
| 8 | P19 | 18–30 | 1 | Inactive | Germany | 84 | 27.0% | 111.1K |
| 9 | P14 | 51–60 | 1 | Active | France | 75 | 38.5% | 105.6K |

The notebook also flags **3-product customers: 82.7% historical churn; only 46 remain.** That segment needs further investigation.

The priority chart labels four action zones: **ACT NOW**, **PROTECT VALUE**, **FIX EXPERIENCE**, and **MONITOR**. The notebook then shows historical reason mix for the top three groups: **P13**, **P16**, and **P8**.
