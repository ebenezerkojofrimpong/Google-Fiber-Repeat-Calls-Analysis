<div align = "center">
  
# Google Business Intelligence Capstone Project
# Google Fiber: Customer Repeat Calls Analysis
## Ebenezer Kojo Frimpong
## February 28, 2024

</div>

---

[](image)
![repeat-1](https://github.com/ebenezerkojofrimpong/Google-Fiber-Repeat-Calls-Analysis/assets/154938134/5f8df53d-d4e3-4840-a303-3ab36108efcd)

## Executive Summary
The objective of this project is to delve into the frequency of customers phoning customer support again after their initial inquiry. This analysis is crucial for leadership to gauge the team's effectiveness in resolving customer queries on the first interaction. Additionally, the project aims to uncover patterns in repeat calls, shedding light on why customers may need to call multiple times and identifying opportunities to enhance the overall customer experience. To achieve these goals, a comprehensive dashboard will be created, providing insightful visualizations on repeat caller trends.

<br>

### Methodology: 
This methodology outlines the ETL(Extract, Transform and Load)  pipeline of extracting data from multiple sources, transforming it to the desired format, and loading it into the final destination table for analysis. 
It ensures that the data is prepared and structured appropriately for the subsequent analysis and dashboard creation.

<br>

**Extract**:

- Data is extracted from three different source tables (market_1, market_2, market_3) containing information on date created, contacts, new types, and markets.

- These source tables are consolidated into a temporary table named market.

<br>

**Transform**:

- A staging table named staging_market is created with defined columns for date, contacts for each of the 7 days, problem type, and city service area.

- String data types are converted to INT64 for numerical calculations.

- Null values are handled by replacing them with 0.

- The problem_type column is categorized based on specific conditions (e.g., type_1 to 'account management', type_2 to 'technician troubleshooting', etc.).

<br>

**Additional Transformation and Loading**:

- Data from the market table is transformed and inserted into the staging_market table.

- The transformed data includes the date created, contacts for each of the 7 days, categorized problem types, and city service areas.

<br>

**Load**:

- The final_data table is created with columns for date, contacts for each of the 7 days, total repeat calls, problem type, and city service area.

- Data from the staging_market table is aggregated to calculate the total repeat calls for each entry.

- The transformed and aggregated data is then inserted into the final_data table.


<br>

### Project Scope and Deliverables:

The project scope outlined by Mr. Portone, Project Manager, emphasizes these key deliverables:

- A chart or table measuring repeat calls by their first contact date

-  A chart or table exploring repeat calls by market and problem type

-  Charts showcasing repeat calls by week, month, and quarter

<br>

### Goals and Success Metrics:

The primary goal of this project is to uncover actionable insights that can lead to a reduction in call volumes, ultimately improving customer satisfaction and operational efficiency. Success will be measured by the ability of the dashboard to provide stakeholders with clear insights into repeat caller volumes across different markets and the types of issues they encounter.

<br>

### Key Findings:

- The analysis revealed distinct patterns in repeat customer support calls based on the initial contact dates.

- Notably, Mondays consistently showed higher volumes of repeat calls, suggesting a potential correlation with weekend inquiries that require follow-up during the beginning of the week.

- Furthermore, the last week of each month exhibited a noticeable spike in repeat calls, indicating a trend possibly tied to billing cycles or promotional activities.

- Market A consistently reported the highest number of repeat calls, especially concerning issues related to product delivery and order tracking.

- Issues related to product malfunction and technical difficulties consistently generated a significant number of repeat calls across all market segments.

<br>

### Recommendations:

- Develop a proactive customer outreach strategy, particularly for Market A where repeat caller volumes are consistently high.

- Utilize customer feedback from initial interactions to personalize outreach efforts, addressing specific concerns and providing tailored solutions.

- Provide specialized training for customer support agents, focusing on troubleshooting technical issues and product malfunctions.

- For Market B with varied problem types, create specialized support teams or channels dedicated to specific categories of customer inquiries.


---


## Introduction
