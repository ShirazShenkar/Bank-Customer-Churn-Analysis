Bank Customer Churn Analysis & Retention Strategies
Project Overview
This project focuses on analyzing historical customer churn patterns to identify proactive retention opportunities. By leveraging data analysis and generative AI techniques, we aim to understand why customers leave, identify high-risk segments, and recommend actionable strategies to mitigate revenue loss.

Final Project – Data Analysis & Generative AI | The Hebrew University

Business Challenge
Customer churn significantly impacts bank revenue, customer relationships, and long-term growth. The primary objective is to analyze historical data (10,000 customer records) to prioritize higher-risk segments and implement data-driven retention actions.

Methodology & Tools
Analytical Focus
Understand: Identify churn patterns and key customer characteristics.
Analyze: Explore churn trends, exit reasons, and financial impact.
Act: Prioritize high-risk segments and recommend retention actions.
Technical Stack
Python (Pandas, NumPy, Matplotlib, Plotly): Used for data cleaning, enrichment, EDA, and statistical visualization.
Power BI (DAX): Used for building interactive dashboards and KPI tracking.
Data Enrichment
Synthetic data was added to support deep-dive analysis:

Account Activation Date: Generated based on customer tenure.
Exit Date: Assigned to churned customers for 2023 trend analysis.
Exit Reason: Assigned from five predefined categories (Better Offers, Digital Banking, High Fees, Personal Reasons, Poor Experience).
Key Performance Indicators (KPIs)
Overall Churn Rate: 20.37%
Total Customers: 10,000
Estimated Annual Revenue Loss: ~$7.42M (based on a 4% annual revenue assumption on customer balances).
High-Risk Segment Exposure: 496 high-risk customers representing ~$2.04M in revenue at risk.
Key Findings
Churn Overview
Geography: Germany has the highest churn rate (32.4%) and accounts for 53% of the estimated annual revenue loss.
Demographics: The highest churn rate (56%) is observed among customers aged 51-60.
Product Ownership: Customers with 3-4 products show exceptionally high churn rates (83-100%).
Activity: Inactive customers churn at nearly twice the rate of active customers (27% vs. 14%).
Leading Exit Reasons
Better Offers (27%): The primary driver, especially in Germany and among customers aged 41-50.
Digital Banking & Personal Reasons: Significant secondary factors across various segments.
Retention Strategies & Recommendations
Priority Focus Groups
Rank	Group	Profile	Recommendation
#1	P13	41-50, Inactive, Single Product (France)	ACT NOW: Retention calls from relationship managers and digital service improvements.
#2	P16	31-40, Inactive, Single Product (Germany)	PROTECT VALUE: App onboarding with digital perks and loyalty rates before exit.
#3	P8	41-50, Inactive, Single Product (Germany)	FIX EXPERIENCE: Competitive/loyalty offers, prioritizing balances >100K.
General Recommendations
Product Adoption: Test if introducing a second product reduces churn for single-product holders.
Customer Engagement: Launch targeted re-engagement campaigns for inactive users.
Experience Optimization: Explore digital improvements for younger cohorts (18-40) and service enhancements for older cohorts (51+).
