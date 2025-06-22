📊 Sales Performance Dashboard (Power BI Portfolio Project)

    A dynamic Power BI dashboard analyzing sales, profit, and customer trends over a 4-year period. This end-to-end project demonstrates data cleaning, DAX measures, time intelligence, and interactive visual storytelling.

🎯 Objective

To analyze 4 years of sales performance across products, segments, and regions, using advanced Power BI techniques. This dashboard helps in understanding customer behavior, product demand, and overall sales strategy effectiveness.
 Key Business Questions (KPIs)

    What is the total sales, profit, and order volume since 2019?

    How do current-year metrics compare to previous years?

    Which segments, categories, and regions perform best in sales?

    What are the top 10 products sold by year?

    What is the trend of sales across months and quarters?

    Which customers contribute the most to revenue?

    How effective are discounts on driving sales?

    Which shipping method is most commonly used?

 Tools & Technologies

    Power BI Desktop

    Power Query Editor

    DAX (Data Analysis Expressions)

    Bookmarks & Selection Pane

    Slicers, Tooltips, Custom Visuals

🧽 Data Preparation Workflow

    Loaded Excel dataset into Power BI.

    Enabled Column Quality, Distribution, and Profile.

    Removed irrelevant columns & reformatted data types.

    Created Date table with Year, Month, and Quarter.

    Created a centralized Measures table for KPIs.

    Established relationships between Date table and Fact table.

    Applied sorting, filtering, and hierarchies.

    Used slicers for State, City, Year, Month, and Segment.

📊 Visuals & Insights
🧾 Sales, Profit & Orders

    Card visuals show current vs previous year metrics with dynamic DAX comparisons.

    Arrows and color formatting indicate positive/negative growth.

🥇 Top Products & Discounts

    Phones and Chairs dominate sales.

    Phones receive higher discounts, while Chairs sell consistently.

    Funnel charts highlight the top-discounted products.

🚚 Shipment & Category

    Standard Class shipping generates maximum sales.

    Technology is the highest-performing category annually.

📈 Trend Analysis

    Sales peak during March, November, and December (seasonal).

    Sales trends are consistent across states and years.

🧑‍🤝‍🧑 Customer Breakdown

    California leads in customer count and orders.

    Bottom regions like Virginia show scope for marketing focus.

    Multi-row cards highlight top 5 and bottom 5 customers by sales and profit.

🧠 DAX Highlights (Examples)

TotalSales = SUM(Sales[Sales])
salesDrop = [CySales] - [PySales]
salesDiff% = DIVIDE([CySales],[PySales],0) * 100

Arrows = SWITCH(TRUE(),
    [CySales] > [PySales], UNICHAR(9206),
    [CySales] < [PySales], UNICHAR(9207),
    " "
)

📌 Strategic Recommendations

    📉 Focus on improving shipping delays, especially for Same Day Delivery.

    🎯 Increase promotions/discounts for underperforming products.

    📆 Strengthen campaigns during Q2 and Q3 where sales often drop.

    👤 Customer acquisition is strong; now focus on retention and personalized marketing.

✅ Features

    Cleaned & modeled dataset using Power Query

    Custom time intelligence with dynamic date table

    Visual bookmarks for toggling between views

    State-wise and segment-wise analysis with slicers

    Clear storytelling with top metrics and visual hierarchy


👨‍💼 Author
Name: Pinto Leoanrd
Role: Data Analyst
Portfolio: [Your Website]
GitHub: https://github.com/datajutsu-jpl
LinkedIn: www.linkedin.com/in/pintoleonard
