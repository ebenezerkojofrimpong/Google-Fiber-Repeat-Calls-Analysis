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
This methodology outlines the ETL(Extract, Transform and Load)  pipeline of extracting data from multiple sources, transforming it to the desired format, and loading it into the final destination table for analysis using BigQuery. 
It ensures that the data is prepared and structured appropriately for the subsequent analysis and dashboard creation.

<br>

**Extract**:

- Data is extracted from three different source tables (market_1, market_2, market_3) containing information on date created, contacts, new types, and markets.

- These source tables are consolidated into a temporary table named 'market'.

<br>

**Transform**:

- A staging table named 'staging_market' is created with defined columns for date, contacts for each of the 7 days, problem type, and city service area.

- String data types are converted to INT64 for numerical calculations.

- Null values are handled by replacing them with 0 for numerical calculations

- The problem_type column is categorized based on specific conditions (ie., type_1 to 'account management', type_2 to 'technician troubleshooting', type_3 to 'scheduling', type_4 to 'construction' and type_5 to 'internet & wifi' ).

<br>

**Additional Transformation and Loading**:

- Data from the market table is transformed and inserted into the staging_market table.

- The transformed data includes the date created, contacts for each of the 7 days, categorized problem types, and city service areas.

<br>

**Load**:

- The 'target table' is created with columns for date, contacts for each of the 7 days, total repeat calls, problem type, and city service area.

- Data from the 'staging_market' table is aggregated to calculate the total repeat calls for each entry.

- The transformed and aggregated data is then inserted into the target table, 'final_data'.


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

Google Fiber, renowned for its high-speed internet and TV services, places a premium on customer satisfaction. Understanding customer interactions and inquiries is paramount to enhancing their experience. The project delves into the frequency and nature of customers contacting support after their first inquiry. By analyzing these repeat calls, Google Fiber aims to identify patterns, trends, and potential areas of improvement in their customer service.

The analysis focuses on three 2022 datasets 'market_1', 'market_2' and 'market_3'. This data, while anonymized and approved for analysis, offers valuable insights into customer behavior and service needs.

With the primary goal of reducing call volumes by improving first-time issue resolution and overall customer satisfaction, the analysis aims to provide actionable insights to Google Fiber's leadership team. By creating a comprehensive dashboard, this project aims to present visualizations that highlight repeat caller volumes, issue types, and trends across different market cities. The ultimate aim is to empower decision-makers with data-driven recommendations to optimize operational efficiency and enhance customer experience.


[](image)
![pic-1](https://github.com/ebenezerkojofrimpong/Google-Fiber-Repeat-Calls-Analysis/assets/154938134/69798b53-4a8f-4204-a35f-703952e49109)


---

We will address this case study using the following methodology:

`ASK` `PREPARE`  `PROCESS`  `ANALYSE`  `SHARE`  `ACT`

<br>














## **ASK**
This phase involves defining the issue to be solved, identifying stakeholders and what their expectations from the project are.

<br>

These questions will guide the future deliverables:

1. How does the box office perform?
    - What is the overall box office performance of RSVP Movies' productions in the past three years?
    - What is the total revenue generated by all movies in the past three years?
    - Which movies have been the top performers in terms of box office revenue?
    - How does RSVP Movies' box office performance compare with production companies?
    -
   

      
<br>

## Business Task
The ultimate goal of this project is to reduce call volume by increasing customer satisfaction and improving operational optimization.

<br>


## Tools
The tools used in this project are **BigQuery** and **Tableau**.

<br>


## Skills / Concepts Applied

For this project, a combination of SQL and Tableau skills were crucial for extracting, processing, and visualizing insights from the dataset. 
Here are the key skills needed:

### SQL Skills:
`ETL Pipeline`
`Performance Optimization`
`Data Extraction`
`Data Transformation`
`Union operations`
`Subqueries`
`Table Creation `

`Data Validation and Quality Checks`
`Data Manipulation and Insertion`
`SQL Functions`
`Filtering and Sorting`
`Grouping and Aggregation`



### Tableau Skills:
`Dashboard Design`
`Data Connection`
`Data Analysis`
`Data Visualization`
`Calculated Fields`
`Filtering and Sorting`
`Data Storytelling`

<br>

## Stakeholders:

- Emma Santiago, Hiring Manager

- Keith Portone, Project Manager

- Minna Rah, Lead BI Analyst

<br>

## Team members: 

- Ian Ortega, BI Analyst

- Sylvie Essa, BI Analyst

---

<br>













## PREPARE
Involves collecting data and information and ensuring it satisfies necessary parameters.

<br>

### Data Location
Kindly follow the link to download the three separate datasets 'market_1', 'market_2' and 'market_3'.
> Download datasets [here](https://drive.google.com/drive/folders/197jb8jmwkpc7HU2ib16Jn56_RPLLShPf)

<br>


### Data Organization
The dataset contains 6 separate tables with 75873 observations in all.

<br>







