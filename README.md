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

**Query Optimization**:

- The tables 'market', 'staging_market' and 'final_data' are clustered by frequently used column 'date_created' to significantly speed up queries and optimize query performance.




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

- March stands out as the month with the highest overall repeat call volume.

- Day 1 consistently records the highest repeat call volume across all three months.

- Internet and wifi, and technician troubleshooting issues account for 80.3% of all repeat calls. 

- Market_1 has the highest repeat call rate due to internet and technician issues, indicating a need for improved network stability whiles Market_2 closely follows with concerns about internet and account management.



<br>


### Recommendations:

- Implement focused training for agents on first call resolution best practices - techniques for fully resolving issues, setting proper expectations on issue timing and following up proactively.

- Implement real-time monitoring systems to identify and resolve network issues to improve internet stability, speed, and reliability.

- Invest in targeted network upgrades to improve reliability and equip customer service representatives with specialized training on technical troubleshooting and account management to resolve issues completely on first contact for both market 1 and market 2.


---













## Introduction

Google Fiber, renowned for its high-speed internet and TV services, places a premium on customer satisfaction. Understanding customer interactions and inquiries is paramount to enhancing their experience. The project delves into the frequency and nature of customers contacting support after their first inquiry. By analyzing these repeat calls, Google Fiber aims to identify patterns, trends, and potential areas of improvement in their customer service.

The analysis focuses on three 2022 datasets 'market_1', 'market_2' and 'market_3'. This data, while anonymized and approved for analysis, offers valuable insights into customer behavior and service needs.

With the primary goal of reducing call volumes by improving first-time issue resolution and overall customer satisfaction, the analysis aims to provide actionable insights to Google Fiber's leadership team. By creating a comprehensive dashboard, this project aims to present visualizations that highlight repeat caller volumes, issue types, and trends across different market cities. The ultimate aim is to empower decision-makers with data-driven recommendations to optimize operational efficiency and enhance customer experience.


[](image)
![pic-1](https://github.com/ebenezerkojofrimpong/Google-Fiber-Repeat-Calls-Analysis/assets/154938134/69798b53-4a8f-4204-a35f-703952e49109)


---

We will address this case study using the following methodology:

## `ASK` `PREPARE`  `PROCESS`  `ANALYSE`  `SHARE`  `ACT`

<br>














# `ASK`
This phase involves defining the issue to be solved, identifying stakeholders and what their expectations from the project are.

<br>

These questions will guide the future deliverables:

1. How often does the customer service team receive repeat calls from customers?

2. What problem types generate the most repeat calls?

3. Which market city’s customer service team receives the most repeat calls?
   

      
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
**`ETL Pipeline`**
**`Performance Optimization`**
**`Data Extraction`**
**`Data Transformation`
`Union operations`**
**`Subqueries`**
**`Table Creation`**

**`Data Validation and Quality Checks`**
**`Data Manipulation and Insertion`**
**`SQL Functions`**
**`Filtering and Sorting`**
**`Grouping and Aggregation`**



### Tableau Skills:
**`Dashboard Design`**
**`Data Connection`**
**`Data Analysis`**
**`Data Visualization`**
**`Calculated Fields`**
**`Filtering and Sorting`**
**`Data Storytelling`**

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













# `PREPARE`
Involves collecting data and information and ensuring it satisfies necessary parameters.

<br>

### Data Location
Kindly follow the link to download the three separate datasets 'market_1', 'market_2' and 'market_3'.
> Download datasets [here](https://drive.google.com/drive/folders/197jb8jmwkpc7HU2ib16Jn56_RPLLShPf)

<br>


### Data Organization
There are three separate datasets with a total of 1350 records in all.

In order to anonymize and fictionalize the data, the datasets the columns market_1, market_2, and market_3 to indicate three different city service areas the data represents. 

The data also lists five problem types:

- Type_1 is account management

- Type_2 is technician troubleshooting

- Type_3 is scheduling

- Type_4 is construction

- Type_5 is internet and wifi

Additionally, the dataset records repeat calls over seven-day periods. The initial contact date is listed as contacts_n.
The other call columns are then contacts_n_number of days since first call. For example, contacts_n_6 indicates six days since first contact. 

<br>



#### `Features:`

**date_created** => Date of call

**contacts_n** => First call

**contacts_n_1** => Day 1 after first call

**contacts_n_2** => Day 2 after first call

**contacts_n_3** => Day 3 after first call

**contacts_n_4** => Day 4 after first call

**contacts_n_5** => Day 5 after first call

**contacts_n_6** => Day 6 after first call

**contacts_n_7** => Day 7 after first call

**problem_type** => type of problem

**market** => City service area




---

<br>








# `PROCESS`
This phase of the analysis process includes cleaning the data and making sure it is fit for purpose. As well as making any modifications necessary.

<br>


The **ETL** Process:

**Extract**:

- Data is extracted from three different source tables (market_1, market_2, market_3) containing information on date created, contacts, new types, and markets.

- These source tables are consolidated into a temporary table named 'market'.

```sql

-- USING A TEMPORARY TABLE AS A FIRST STAGING TABLE
CREATE TEMPORARY TABLE IF NOT EXISTS market AS
SELECT
  date_created,
  contacts_n,
  contacts_n_1,
  contacts_n_2,
  contacts_n_3,
  contacts_n_4,
  contacts_n_5,
  contacts_n_6,
  contacts_n_7,
  new_type,
  new_market
FROM `business-intelligence-414900.fibre.market_1`
UNION ALL
SELECT
  date_created,
  contacts_n,
  contacts_n_1,
  contacts_n_2,
  contacts_n_3,
  contacts_n_4,
  contacts_n_5,
  contacts_n_6,
  contacts_n_7,
  new_type,
  new_market
FROM `business-intelligence-414900.fibre.market_2`
UNION ALL
SELECT
  date_created,
  contacts_n,
  contacts_n_1,
  contacts_n_2,
  contacts_n_3,
  contacts_n_4,
  contacts_n_5,
  contacts_n_6,
  contacts_n_7,
  new_type,
  new_market
FROM `business-intelligence-414900.fibre.market_3`;

```

[](sql_image)
![pic-2](https://github.com/ebenezerkojofrimpong/Google-Fiber-Repeat-Calls-Analysis/assets/154938134/16d48a23-0757-4adf-af85-05df5b119f28)

---



**Transform**:

- A staging table named 'staging_market' is created with defined columns for date, contacts for each of the 7 days, problem type, and city service area.

- String data types are converted to INT64 for numerical calculations.

- Null values are handled by replacing them with 0 for numerical calculations

- The problem_type column is categorized based on specific conditions (ie., type_1 to 'account management', type_2 to 'technician troubleshooting', type_3 to 'scheduling', type_4 to 'construction' and type_5 to 'internet & wifi' ).

```sql

-- CREATING A STAGING TABLE
DROP TABLE IF EXISTS fibre.staging_market;
CREATE TABLE IF NOT EXISTS fibre.staging_market ( -- STAGING TABLE
  date_created DATE NOT NULL,
  day_0 INT64 NOT NULL,
  day_1 INT64 NOT NULL,
  day_2 INT64 NOT NULL,
  day_3 INT64 NOT NULL,
  day_4 INT64 NOT NULL,
  day_5 INT64 NOT NULL,
  day_6 INT64 NOT NULL,
  day_7 INT64 NOT NULL,
  problem_type STRING NOT NULL,
  city_service_area STRING NOT NULL

); 



-- TRANSFORMATION
-- CHANGING STRING DATATYPES TO INT64 AND ADDING THE COLUMN TOTAL REPEAT CALLS
INSERT INTO fibre.staging_market (
  date_created,
  day_0,
  day_1,
  day_2,
  day_3,
  day_4,
  day_5,
  day_6,
  day_7,
  problem_type,
  city_service_area
)

SELECT
  date_created, 
  IFNULL(SAFE_CAST(contacts_n AS INT64), 0), 
  IFNULL(SAFE_CAST(contacts_n_1 AS INT64), 0), 
  IFNULL(SAFE_CAST(contacts_n_2 AS INT64), 0), 
  IFNULL(SAFE_CAST(contacts_n_3 AS INT64), 0),
  IFNULL(SAFE_CAST(contacts_n_4 AS INT64), 0), 
  IFNULL(SAFE_CAST(contacts_n_5 AS INT64), 0), 
  IFNULL(SAFE_CAST(contacts_n_6 AS INT64), 0), 
  IFNULL(SAFE_CAST(contacts_n_7 AS INT64), 0),
  CASE
      WHEN new_type = 'type_1' THEN 'account management'
      WHEN new_type = 'type_2' THEN 'technician troubleshooting'
      WHEN new_type = 'type_3' THEN 'scheduling'
      WHEN new_type = 'type_4' THEN 'construction'
      ELSE 'internet & wifi' 
      END AS problem_type,
  new_market
FROM market;

```

[](sql_image)
![pic-3](https://github.com/ebenezerkojofrimpong/Google-Fiber-Repeat-Calls-Analysis/assets/154938134/837c91a2-814f-4c58-a871-dd7ec1a41d31)


---



**Additional Transformation and Loading**:

- Data from the market table is transformed and inserted into the staging_market table.

- The transformed data includes the date created, contacts for each of the 7 days, categorized problem types, and city service areas.

<br>


**Load**:

- The 'target table' is created with columns for date, contacts for each of the 7 days, total repeat calls, problem type, and city service area.

- Data from the 'staging_market' table is aggregated to calculate the total repeat calls for each entry.

- The transformed and aggregated data is then inserted into the target table, 'final_data'.

```sql

-- CREATING A TARGET TABLE
DROP TABLE IF EXISTS fibre.final_data;
CREATE TABLE IF NOT EXISTS fibre.final_data ( -- TARGET TABLE
  date_created DATE NOT NULL,
  day_0 INT64 NOT NULL,
  day_1 INT64 NOT NULL,
  day_2 INT64 NOT NULL,
  day_3 INT64 NOT NULL,
  day_4 INT64 NOT NULL,
  day_5 INT64 NOT NULL,
  day_6 INT64 NOT NULL,
  day_7 INT64 NOT NULL,
  total_repeat_calls INT64 NOT NULL,
  problem_type STRING NOT NULL,
  city_service_area STRING NOT NULL

);


-- ADDING THE COLUMN TOTAL REPEAT CALLS
INSERT INTO fibre.final_data(
  date_created,
  day_0,
  day_1,
  day_2,
  day_3,
  day_4,
  day_5,
  day_6,
  day_7,
  total_repeat_calls,
  problem_type,
  city_service_area
)

SELECT
  date_created,
  day_0,
  day_1,
  day_2,
  day_3,
  day_4,
  day_5,
  day_6,
  day_7,
  SUM(day_1) + 
  SUM(day_2) +
  SUM(day_3) +
  SUM(day_4) + 
  SUM(day_5) +
  SUM(day_6) +
  SUM(day_7) AS total_repeat_calls,
  problem_type,
  city_service_area
FROM `business-intelligence-414900.fibre.staging_market`
GROUP BY
  date_created,
  day_0,
  day_1,
  day_2,
  day_3,
  day_4,
  day_5,
  day_6,
  day_7,    
  problem_type,
  city_service_area;


```

[](sql_image)
![pic-4](https://github.com/ebenezerkojofrimpong/Google-Fiber-Repeat-Calls-Analysis/assets/154938134/8e17920b-709f-4021-9754-8016f62795d2)


---



**Query Optimization**:

- The tables 'market', 'staging_market' and 'final_data' are clustered by frequently used column 'date_created' to significantly speed up queries and optimize query performance.

```sql

-- DROP EXISTING TEMPORARY TABLE
DROP TABLE IF EXISTS fibre.market;

-- CREATE TEMPORARY TABLE FOR market CLUSTERED BY date_created
CREATE TEMPORARY TABLE IF NOT EXISTS fibre.market AS
SELECT
  date_created,
  contacts_n,
  contacts_n_1,
  contacts_n_2,
  contacts_n_3,
  contacts_n_4,
  contacts_n_5,
  contacts_n_6,
  contacts_n_7,
  new_type,
  new_market
FROM `business-intelligence-414900.fibre.market_1`
UNION ALL
SELECT
  date_created,
  contacts_n,
  contacts_n_1,
  contacts_n_2,
  contacts_n_3,
  contacts_n_4,
  contacts_n_5,
  contacts_n_6,
  contacts_n_7,
  new_type,
  new_market
FROM `business-intelligence-414900.fibre.market_2`
UNION ALL
SELECT
  date_created,
  contacts_n,
  contacts_n_1,
  contacts_n_2,
  contacts_n_3,
  contacts_n_4,
  contacts_n_5,
  contacts_n_6,
  contacts_n_7,
  new_type,
  new_market
FROM `business-intelligence-414900.fibre.market_3`
CLUSTER BY date_created;  -- Clustering by date_created for efficient reads

-- DROP EXISTING STAGING TABLE
DROP TABLE IF EXISTS fibre.staging_market;

-- CREATE STAGING TABLE CLUSTERED BY date_created
CREATE TABLE IF NOT EXISTS fibre.staging_market (
  date_created DATE NOT NULL,
  day_0 INT64 NOT NULL,
  day_1 INT64 NOT NULL,
  day_2 INT64 NOT NULL,
  day_3 INT64 NOT NULL,
  day_4 INT64 NOT NULL,
  day_5 INT64 NOT NULL,
  day_6 INT64 NOT NULL,
  day_7 INT64 NOT NULL,
  problem_type STRING NOT NULL,
  city_service_area STRING NOT NULL
)
CLUSTER BY date_created;  -- Clustering by date_created for efficient reads

-- TRANSFORMATION
-- CHANGING STRING DATATYPES TO INT64 AND ADDING THE COLUMN TOTAL REPEAT CALLS
INSERT INTO fibre.staging_market (
  date_created,
  day_0,
  day_1,
  day_2,
  day_3,
  day_4,
  day_5,
  day_6,
  day_7,
  problem_type,
  city_service_area
)
SELECT
  date_created, 
  IFNULL(SAFE_CAST(contacts_n AS INT64), 0), 
  IFNULL(SAFE_CAST(contacts_n_1 AS INT64), 0), 
  IFNULL(SAFE_CAST(contacts_n_2 AS INT64), 0), 
  IFNULL(SAFE_CAST(contacts_n_3 AS INT64), 0),
  IFNULL(SAFE_CAST(contacts_n_4 AS INT64), 0), 
  IFNULL(SAFE_CAST(contacts_n_5 AS INT64), 0), 
  IFNULL(SAFE_CAST(contacts_n_6 AS INT64), 0), 
  IFNULL(SAFE_CAST(contacts_n_7 AS INT64), 0),
  CASE
      WHEN new_type = 'type_1' THEN 'account management'
      WHEN new_type = 'type_2' THEN 'technician troubleshooting'
      WHEN new_type = 'type_3' THEN 'scheduling'
      WHEN new_type = 'type_4' THEN 'construction'
      ELSE 'internet & wifi' 
      END AS problem_type,
  new_market
FROM fibre.market;

-- DROP EXISTING TARGET TABLE
DROP TABLE IF EXISTS fibre.final_data;

-- CREATE TARGET TABLE CLUSTERED BY date_created
CREATE TABLE IF NOT EXISTS fibre.final_data (
  date_created DATE NOT NULL,
  day_0 INT64 NOT NULL,
  day_1 INT64 NOT NULL,
  day_2 INT64 NOT NULL,
  day_3 INT64 NOT NULL,
  day_4 INT64 NOT NULL,
  day_5 INT64 NOT NULL,
  day_6 INT64 NOT NULL,
  day_7 INT64 NOT NULL,
  total_repeat_calls INT64 NOT NULL,
  problem_type STRING NOT NULL,
  city_service_area STRING NOT NULL
)
CLUSTER BY date_created;  -- Clustering by date_created for efficient reads

-- ADDING THE COLUMN TOTAL REPEAT CALLS
INSERT INTO fibre.final_data(
  date_created,
  day_0,
  day_1,
  day_2,
  day_3,
  day_4,
  day_5,
  day_6,
  day_7,
  total_repeat_calls,
  problem_type,
  city_service_area
)
SELECT
  date_created,
  day_0,
  day_1,
  day_2,
  day_3,
  day_4,
  day_5,
  day_6,
  day_7,
  SUM(day_1) + 
  SUM(day_2) +
  SUM(day_3) +
  SUM(day_4) + 
  SUM(day_5) +
  SUM(day_6) +
  SUM(day_7) AS total_repeat_calls,
  problem_type,
  city_service_area
FROM `business-intelligence-414900.fibre.staging_market`
GROUP BY
  date_created,
  day_0,
  day_1,
  day_2,
  day_3,
  day_4,
  day_5,
  day_6,
  day_7,
  problem_type,
  city_service_area;


```

---


<br>




















# `ANALYZE`

In this phase we analyze the data to find patterns, relationships, and trends.

<br>

**Outlined below are the key takeaways derived from the analysis of the data:**

1. How often does the customer service team receive repeat calls from customers?

[](repeat_calls_by_month_image)
![Repeat Calls By Month](https://github.com/ebenezerkojofrimpong/Google-Fiber-Repeat-Calls-Analysis/assets/154938134/ca96a0dc-df2a-4986-b3e3-e9d10b978215)

<br>

- Day 1 has the highest volume of repeat calls in all 3 months - over 2,000 in March, 1,827 in February, and 1,636 in January. 
This indicates a large number of customers are calling back the very next day, likely due to unresolved issues on the first call.

- Beyond Day 1, repeat calls decline but are still significant.
The high repeat rate in the early days directly after the first call indicates there are likely issues with resolving customer problems completely during the initial call.

- Comparing months, March had the most repeat calls overall. 


---

<br>
















2. What problem types generate the most repeat calls?

[](repeat_calls_by_problem_type_image)
![Repeat Calls By Problem Type](https://github.com/ebenezerkojofrimpong/Google-Fiber-Repeat-Calls-Analysis/assets/154938134/bae09922-f8e4-4860-a023-3575154cbc93)

- "Internet and Wifi" issues account for 50.7% of all repeat calls with a total of 10,253 making it the most common problem type.
This suggests that issues with connectivity and network performance are likely to prompt customers to reach out for further assistance, indicating a critical need for robust and reliable internet services.

- "Technician troubleshooting" follows, accounting for 29.6% of all repeat calls with a total of 5,987.
This suggests that customers often encounter persistent or recurring technical difficulties that require ongoing support and resolution.

---


<br>


















3. Which market city’s customer service team receives the most repeat calls?

[](repeat_calls_by_city_service_area_segmented_by_problem_type_image)
![Repeat Calls_ City Service Area Segmented By Problem Type](https://github.com/ebenezerkojofrimpong/Google-Fiber-Repeat-Calls-Analysis/assets/154938134/ffdee86b-f280-4cf0-bd60-9b350d0beb11)

- Market_1 shows the highest rate of repeat calls, primarily due to frequent issues with internet connectivity and the need for technician troubleshooting.
Customers often contact customer service for assistance with these challenges, indicating a demand for improved network stability and technical support in this market.

- Market_2 follows closely behind Market_1 in repeat calls, with customers often contacting customer service for issues related to internet connectivity and account management. This suggests a recurring need for support in these areas within this market.

---


<br>
















# `SHARE`

The outcomes are effectively communicated with pertinent stakeholders. The execution stage of this project was carried out utilizing Tableau for analysis for crafting insightful visual representations.

Dashboards created with visualizations also present relevant information at a glance.

<br>



[](dashboard_image)
![Dashboard](https://github.com/ebenezerkojofrimpong/Google-Fiber-Repeat-Calls-Analysis/assets/154938134/64441105-45c5-49c3-9e2c-5620be073552)

Interact with dashboard [here](https://public.tableau.com/views/GoogleFiberRepeatCalls_17090536867310/GoogleFiberRepeatCalls?:language=en-US&:sid=&:display_count=n&:origin=viz_share_link)



---



<br>





















# `ACT`

Upon completion of data processing, analysis, and insight dissemination, the conclusive phase involves formulating a well-aligned course of action for Google Fibre, congruent with its business goals and mission. 

My recommendations are as follows:

- Implement focused training for agents on first call resolution best practices - techniques for fully resolving issues, setting proper expectations on issue timing and following up proactively.

- Implement real-time monitoring systems to identify and resolve network issues to improve internet stability, speed, and reliability.

- Invest in targeted network upgrades to improve reliability and equip customer service representatives with specialized training on technical troubleshooting and account management to resolve issues completely on first contact for both market 1 and market 2.
