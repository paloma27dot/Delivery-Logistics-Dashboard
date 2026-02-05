
# Delivery-Logistics-Dashboard
Data analysis and Power BI dashboard project analyzing delivery costs, delays, and service performance using CSV data and Excel KPI validation.
This repository contains a data analysis and visualization project focused on logistics performance, specifically delivery costs, delays, and service quality. The project was developed as a practical portfolio exercise for data analytics and BI interviews.

The main objective of the dashboard is to identify operational patterns and inefficiencies related to delivery delays, costs, and customer satisfaction across different dimensions such as region, distance, weather conditions, package type, and delivery partners.

Project Structure
1. Raw Dataset

File: Delivery_Logistics.csv

Description: Raw dataset containing delivery order information, including costs, delivery status, region, distance category, weather conditions, package type, delivery partner, and customer ratings.

Purpose: Primary data source used for data cleaning, transformation, and modeling.

2. Excel Analysis (Exploratory & KPI Validation)

File: KPIS DE EXCEL.xlsx

Content:

Pivot tables for exploratory data analysis

Calculation and validation of key metrics such as:

Average Cost per Delivery

Delayed Percentage

Total Orders

Average Delivery Rating

Early identification of trends before building the Power BI model

Excel was used as an intermediate analysis layer to validate KPIs and better understand data behavior before visualization.

3. Power BI Dashboard

File: DeliveryDashboard.pbix

The final dashboard consolidates multiple visualizations to provide a comprehensive view of logistics performance:
Key KPIs

•	Total Orders

•	Average Cost per Delivery

•	On-Time vs Delayed Orders

Delay Analysis

•	Delay percentage by region

•	Delay percentage by weather condition

•	Delay percentage by package type

•	Overall On-Time vs Delayed comparison

Cost & Operational Performance

•	Average delivery cost by distance category (Short, Medium, Long)

•	Relationship between delivery cost and delay percentage by region

•	Total and average cost by delivery partner

Service Quality

•	Average delivery rating by region

•	Delivery rating by delivery status (Delivered, Delayed, Failed)

Key Insights Enabled by the Dashboard
•	Long-distance deliveries show significantly higher costs and lower average ratings.

•	Adverse weather conditions (stormy, rainy, foggy) account for a substantial share of delivery delays.

•	Clear performance differences exist among delivery partners in terms of cost, delay rate, and service quality.

•	Some regions incur higher delivery costs without proportional improvements in on-time performance.

Key DAX Measures
The following calculated columns and measures were created to support KPI computation, segmentation, and performance analysis within the dashboard.

Distance Category

Distance_Category = 
IF(
    Delivery_Logistics[distance_km] <= 50, "Short",
    IF(
        Delivery_Logistics[distance_km] <= 150, "Medium",
        "Long"
    )
)

Purpose: Categorizes deliveries based on distance traveled.

Business Value: Enables comparison of cost, delay rate, and delivery time across short-, medium-, and long-distance deliveries.

Delivery Category

Delivery_Category = 
SWITCH(
    TRUE(),
    Delivery_Logistics[delivery_time_hours] <= 30, "Fast",
    Delivery_Logistics[delivery_time_hours] <= 60, "Medium",
    "Slow"
)

Purpose: Groups deliveries by delivery speed using delivery time thresholds.

Business Value: Helps identify trade-offs between speed, cost, and service quality.

Delay Indicators

Is_Delayed = 
IF(Delivery_Logistics[delayed] = "yes", 1, 0)

On_Time = 
IF(Delivery_Logistics[delayed] = "no", 1, 0)

Purpose: Converts delivery delay status into binary indicators.

Business Value: Enables accurate calculation of delay and on-time performance rates.

Delivery Success Indicator

Successful_Delivery = 
IF(Delivery_Logistics[delivery_status] = "delivered", 1, 0)

Purpose: Flags successfully delivered orders.

Business Value: Supports calculation of overall delivery success rate.

Core KPIs

Avg Cost per Delivery = 
AVERAGE(Delivery_Logistics[delivery_cost])

Avg Delivery Time = 
AVERAGE(Delivery_Logistics[delivery_time_hours])

On Time % = 
AVERAGE(Delivery_Logistics[On_Time])

Delay Rate = 
AVERAGE(Delivery_Logistics[Is_Delayed])

Delayed % = 
1 - [On Time %]

Success Rate = 
AVERAGE(Delivery_Logistics[Successful_Delivery])

Total Orders = 
COUNTROWS(Delivery_Logistics)

Purpose: Calculates the main KPIs displayed in the dashboard.

Business Value: These measures allow evaluation of operational efficiency, service reliability, and overall logistics performance.

Tools & Technologies

•	Excel: Exploratory analysis and pivot tables

•	Power BI: Data modeling, DAX measures, and dashboard visualization

•	CSV: Structured data source

Business Questions Answered

•	Which delivery distances and speed categories drive higher costs without proportional improvements in on-time performance?

•	How do weather conditions and regions impact delivery delays and overall service reliability?

•	Which delivery partners show the best balance between cost efficiency, on-time performance, and success rate?

•	How does delivery speed (Fast, Medium, Slow) affect customer satisfaction and operational efficiency?

Project Purpose

This project was developed to demonstrate data analysis and visualization skills, show the ability to translate data into actionable business insights and to serve as a portfolio project for Data Analyst / Business Intelligence roles

Notes

•	The dataset is simulated and intended for educational and demonstration purposes only.

•	The dashboard design prioritizes clarity, executive-level insights, and decision-making support.
