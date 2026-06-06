# SaaS-revenue-analysis

---

## 📌 Project Objective

The goal of this project is to analyze SaaS revenue data for a 12-month period (June 2022 – May 2023) across three geographic regions and four software products. The analysis focuses on tracking revenue growth, understanding product and regional performance, monitoring key SaaS metrics (MRR, ARPPU), and evaluating customer cohort retention over time.

---

## 📂 Dataset Used

- **Source:** `saas_revenue.csv`
- **Period:** June 2022 – May 2023

| Field | Description |
|---|---|
| `User Id` | Unique customer identifier |
| `Payment Date` | Date of the transaction |
| `Payment Month` / `Payment Month Number` | Month dimension for time-series analysis |
| `Revenue Amount` | Revenue per transaction |
| `Software Name` | Product name (Main App, Customer Success, Marketing Automation, Publishing) |
| `Location` | Region (APAC, EMEA, USA) |
| `Is Enterprise Customer` | Enterprise vs. non-enterprise flag |
| `New User Payment` | Flag indicating first-time payment |
| `ARPPU` | Average Revenue Per Paying User |
| `New MRR` | Monthly Recurring Revenue from new customers |
| `Paid Users` | Count of paying users per month |
| `First Payment Date` / `First Payment Month` | Cohort start date |
| `Total Revenue` | Aggregated revenue metric |

---

## ❓ Questions

1. How did total monthly revenue change over the 12-month period?
2. Which region — APAC, EMEA, or USA — generates the most revenue?
3. Which software product brings in the highest total revenue?
4. How does revenue break down by both region and product simultaneously?
5. How has each product's revenue evolved month over month?
6. How are Paid Users and ARPPU trending over time, and what does this reveal about growth?
7. What is the New MRR trend — is the business acquiring new customers consistently?
8. What does the Revenue Cohort Table reveal about customer retention and revenue decay?

---

## ⚙️ Process

**1. Data Connection & Preparation**
- Connected `saas_revenue.csv` to Tableau
- Verified field types: dates, measures (Revenue Amount, ARPPU, , Paid Users), and dimensions (User ID, Location, Software Name, Is Enterprise Customer)
- Created calculated fields: `Total Revenue`, `ARPPU`, `New MRR`,  `First Paymment Date`, `First Paymment Month`, `Payment Month Number` for cohort logic

**2. Worksheet Development**
Built 10 individual worksheets covering different analytical angles — time series, geographic breakdown, product comparison, user metrics, and cohort analysis

**3. Dashboard Assembly**
Combined worksheets into 2 interactive dashboards with filters for Period (date range slider), Location, and Product

**4. Cohort Analysis**
Built a cohort table tracking revenue from each monthly acquisition cohort across up to 11 subsequent months to measure retention and revenue decay

---

## 📊 Dashboard

🔗 **[View Interactive Dashboard on Tableau Public](https://public.tableau.com/app/profile/kateryna.kiktenko/viz/SaaSRevenue_17799756851350/Dashboard2)**
<img width="668" height="536" alt="image" src="https://github.com/user-attachments/assets/6e84aab6-c436-46b8-81cc-e634848ab9ca" />

### Worksheets

| Sheet | Chart Type | Description |
|---|---|---|
| **Monthly Revenue** | Line chart | Total revenue by month, June 2022 – May 2023 |
| **Monthly Regional Revenue Trends** | Stacked area chart | Revenue split by APAC, EMEA, USA over time |
| **Product Revenue** | Horizontal bar chart | Total revenue per product across the full period |
| **Revenue by Geo & Product** | Highlight table | Revenue matrix: 3 regions × 4 products |
| **Revenue by Location** | Bar chart | Total revenue per region |
| **Product Revenue Dynamics** | Multi-line chart | Month-over-month revenue per product |
| **Monthly ARPPU & Users** | Combo chart (bar + line) | Paid Users (bars) vs. ARPPU (line) by month |
| **New MRR** | Line chart | New Monthly Recurring Revenue from new customers |
| **Total Revenue Dynamics** | Combo chart (bar + line) | Total revenue (line) + % month-over-month change (bars) |
| **Revenue Cohort Table** | Cohort heatmap | Revenue retention by acquisition cohort (months 0–11) |

### Dashboards

| Dashboard | Sheets Included |
|---|---|
| **SaaS Revenue & Analytics Dashboard** | Product Revenue, Revenue by Geo & Product, Revenue by Location, Product Revenue Dynamics, Monthly ARPPU & Users |
| **SaaS Revenue & Cohort Performance** | New MRR, Total Revenue Dynamics, Revenue Cohort Table |
<img width="666" height="534" alt="image" src="https://github.com/user-attachments/assets/e41bc59a-de44-43db-a501-6c18eaaab8c4" />

---

## 💡 Project Insights

- **Steady revenue growth overall:** Total monthly revenue grew from $44,085 in June 2022 to a peak of $162,260 in March 2023 — nearly a 3.7× increase — before declining slightly to $136,945 in May 2023.

- **USA is the top revenue region:** The USA generated approximately $644,000 in total, significantly outperforming APAC (~$449,000) and EMEA (~$240,000). However, APAC shows the strongest growth trajectory.

- **Main App and Customer Success lead by product:** Main App and Customer Success are the two highest-revenue products, each exceeding $380,000+ for the period. Marketing Automation ranks third, while Publishing contributes the least.

- **APAC dominates in Customer Success:** The Revenue by Geo & Product highlight table shows APAC generated $292,860 from Customer Success alone — the single highest product-region combination — while USA leads in Marketing Automation ($297,390).

- **Paid Users are growing but ARPPU is declining:** Paid Users increased from ~750 in June 2022 to ~3,500+ by May 2023, yet ARPPU dropped from ~$60 to ~$38. This suggests the business is acquiring lower-value customers or offering more discounts at scale.

- **New MRR is volatile and declining from its peak:** New MRR started high at $44,085 in June 2022 (launch effect), dropped sharply to $11,515 in July, then recovered inconsistently. By May 2023 it settled at $17,750, indicating the new customer acquisition rate is not keeping pace with user base growth.

- **Cohort table reveals rapid revenue decay:** The Revenue Cohort Table shows that in most cohorts, revenue drops significantly after month 0–1. For example, the June 2022 cohort went from $44,085 (month 0) to $9,400 by month 11. This signals potential churn or contraction issues in existing accounts.

---

## ✅ Final Conclusion

The SaaS business demonstrated strong top-line revenue growth over the analyzed period, driven primarily by the USA market and the Main App and Customer Success products. However, the underlying metrics tell a more nuanced story: while Paid Users are growing, ARPPU is declining, New MRR is inconsistent, and cohort data reveals significant revenue erosion after the first month of acquisition.

To sustain and improve performance, the business should focus on:
- **Improving cohort retention** — investigate why revenue decays so quickly after month 0–1 and invest in onboarding and customer success
- **Stabilizing New MRR** — build a more consistent new customer acquisition pipeline
- **Protecting ARPPU** — review pricing and discount strategies to avoid devaluing the product as the user base scales
- **Expanding EMEA** — EMEA is the weakest region and likely represents the largest untapped opportunity

