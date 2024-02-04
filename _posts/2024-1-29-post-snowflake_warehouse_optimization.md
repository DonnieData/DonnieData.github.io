---
title: "Snowflake Virtual Warehouse Scaling"
excerpt: Analyzing query performance with Snowflake warehouses. 
classes: wide
categories:
  - Post
tags:
  - Snowflake
  - Database
  - Big Data
  - Data Warehouse 
  - Data Modeling 
header:
  overlay_image: /assets/images/splash_project/phone_line.jpg
  actions:
    - label: "GitHub Repo"
      url: ""
author_profile: True
sidebar:
  title: "Navigation"
  nav: sf1-navbar1
---


# Project Overview 
Snowflake is a Software as a Service(SaaS) for cloud data services and tools. 
This project will focus on optimizing operations in Snowflake through warehouse scaling. Scaling by warehouse size and testing performance with the same query will allow me to gather metrics and analyze which is the best virutal warehouse for the job.

# Snowflake - Quick Overview 
Snowflake operates in 3 primary layers that interact with each other: 
- Storage Layer - handles data storage in micro partitions, data storage billing
- Compute Layer - handles virtual warehouse, compute credits, credit consumption 
- Cloud Services Layer - handles account management, query execution, security, metadata, cloud compute services

#### Compute Layer & Virtual Warehouses
The compute layer is where virtual warehouses are handled and how credit consumption is calcualted. Virtual warehouses are CPU's that allow the processesing/executions of jobs.

Running a virtual warehouse will cause credits to be consummed. Credit consumption is effected by various things but primarly determined by the size of a warehouse and ammount of time its running. Digging deeper the ammount of time it is running dpeends on the complexity of a query and the ammount of data being queried/ scanned  

Snowflake allows you to spin up numerous warehouses that auto suspend when not being used. This allows users to create differnet sized warehosues for a specifc jobs, which allows us to optimize for time and cost ofr jobs.

# Testing Warehosue Performance 
I will be using an enterprise edtition of snowflake with a US Central 1 (Iowa) storage region. For this setup 1 Snowflake credit = $3 USD 

#### Warehouse Setup 
A standard warehouse for ecah size betwen x-small to 4X-Large is setup:

<div class="notice">
<figure>
  <a href="/assets/images/snowflake_op/warehouses_in_snowsight.png"><img src="/assets/images/snowflake_op/warehouses_in_snowsight.png"></a>
</figure>
</div>

#### Test Query
For this project scenario we are testing a query which will be ran once a day and will query a large ammount of data that will be used for a company report.
The same [test query](https://github.com/DonnieData/snowflake_warehouse_op/blob/main/SQL/project_test_query.sql) will be ran once for all of our warehouse sizes and we will track perfomance metrics. 

#### Execution Data
Query execution metrics metrics can be retrieved via the query_id which is a system generated unique id for each query. Using the query_id for each execution I get the metrics from the snowflake system by querying the internal system tables **snowflake.account_usage.query_history**.

```sql 
select 
query_id
,session_id
,credits_used_cloud_services
,total_elapsed_time
,bytes_scanned
,execution_time
,warehouse_name
,warehouse_size
from snowflake.account_usage.query_history
where query_id in (
'01b1fa62-0001-ad59-0002-81260002e02a',
'01b1da24-0001-a992-0002-812600016096',
'01b1dd9d-0001-a9b6-0002-81260001a026',
'01b1ddd6-0001-a9c1-0002-81260001d042',
'01b1ddff-0001-a9c1-0002-81260001d052',
'01b1ea5f-0001-ab26-0002-812600027062',
'01b1de5d-0001-aa23-0002-81260001e0a6',
'01b2011d-0001-adb9-0002-81260003a086'
);
````
<div class="notice">
<figure>
  <a href="/assets/images/snowflake_op/query_stats_shot1s.jpg"><img src="/assets/images/snowflake_op/query_stats_shot1s.jpg"></a>
</figure>
</div>


# Cost & Performance Analysis 

<iframe width="1000" height="550" src="https://lookerstudio.google.com/embed/reporting/225f4ea2-e3d9-482f-8125-9972eaceb14f/page/PTDoD" frameborder="0" style="border:0" allowfullscreen sandbox="allow-storage-access-by-user-activation allow-scripts allow-same-origin allow-popups allow-popups-to-escape-sandbox"></iframe>

<div style="background-color: #daedf1; padding:5px; border-radius: 10px; border-bottom: 10px;">
<li>Chart shows query exectuion time and cost of query execution by warehouse size from smallest to larges.</li>
<li>We see a steep declines in execution time as we increase warehosue size</li>
<li>There is also a clear decline in price ,showing that there  is also a finacnial upside to increasing warehouse size for our test report queery. </li>
</div>


<iframe width="1000" height="550" src="https://lookerstudio.google.com/embed/reporting/7e473c99-2c13-43b2-bb3b-d8e068e03b66/page/PTDoD" frameborder="0" style="border:0" allowfullscreen sandbox="allow-storage-access-by-user-activation allow-scripts allow-same-origin allow-popups allow-popups-to-escape-sandbox"></iframe>

<div style="background-color: #daedf1; padding:5px; border-radius: 10px;">
- Chart shows query execution time(miutes) by warehosue size.Table shows the percentage change in execution time(minutes) as the warehouse increases in size.
- We see execution time decreases roughly 50% or more all the way up to 2X-Large wareosue size. 
</div>

<iframe width="1000" height="550" src="https://lookerstudio.google.com/embed/reporting/5ee1d556-9e16-4e82-989f-d278e2a2d593/page/PTDoD" frameborder="0" style="border:0" allowfullscreen sandbox="allow-storage-access-by-user-activation allow-scripts allow-same-origin allow-popups allow-popups-to-escape-sandbox"></iframe>

<div style="background-color: #daedf1; padding:5px; border-radius: 10px;">
<li>Chart shows query cost by warehouse size. Table shows change in cost as warehosue size increases</li>
<li>We see cost decreases all the way to extra large warehouse</li>
<li>Cost begins to increases going from X-Large to 2X-Large warehouse</li>
</div>

# Conclusion 
For this optimization project I ran the same query in several warehouses and reviewed execution data to reveal which warehouse size is best for the job. 

Based on the data an X-large or 2X-large warehouse are the best choices for perfromance(execution time and cost). 
The X-Large warehouse provides the best combiniation of time eficney and cost. 
in a the scenario in which the need for updated data is urgent, we have 2X-Large warehouse as a secomdary option. In which this warehouse size almsot halfs execution time for a relativley small price increase(3%).

Although the execution time differnence of 5minutes between the X-Large and 2X-large can seem negligible at this scope level. It is important to note that this time and cost relationship will generally be maintained at scale. 
Given a scenario in which a X-Large warehouse takes 1 hour to finish running, its likey that scaling up to 2X-large will reduce the execution time around 50%* for a cost increase of roughly 3%.


#### Future Updates 
Testing Scaling up vs scaling out with multiple queries in same job block.

