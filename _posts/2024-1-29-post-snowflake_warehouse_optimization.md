---
title: "Snowflake Query & Warehouse Optimization"
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
---


## Project Overview 
With the advent of cloud computing and its related services such as cloud storage. data lifecyle ecosystems are going thorugh a big change. One common overhall hapening within companys due to this is going from onsite database and storage to cloud-based. With this comes a need for data related teams to have a better operational understanding. 
A new concept is cloud pricing models and credit consumption. 

This project will focus on operation optimizing through warehouses for query cost in Snowflake - a popular Software as a Service(SaaS) for cloud data services and tools. 

## Snowflake 

As a quick overview...
Snowflake operates in 3 layers that interact with each other: 
- Storage Layer - Where data is stored in micro partitions, data storage billing calculation
-  Compute Layer - virtual warehosues, compute credits/ consumption 
-  Cloud Services Layer - management, Query handling, security, metadata, cloud compute services

Snowflake operates in 3 layers that interact with each other: 
<ul style="padding-left:20px">
    <li>Storage Layer - Where data is stored in micro partitions, data storage billing calculation</li>
    <li>Compute Layer - virtual warehosues, compute credits/ consumption</li>
    <li>Cloud Services Layer - management, Query handling, security, metadata, cloud compute services</li>
</ul>

We will focus on the compute layer, becuase it is where virtual warehouses are handled and how credit consumption is calcualted. 

Running a virtual warehouse will cause spending credits to be consummed. Credit consumption is effected by various things but primarly determined by the size of a warehouse and ammount of time its running. Digging deeper the ammount of time it is running dpeends on the complexity of a query and the ammount of data being queried/ scanned  

Snowflake allows you to spin up numerous warehouses that auto suspend when not being used. This allows users to create differnet sized warehosues for differnt or specifc jobs, which allows us to optimize for time and speedi n query performance. 

## Testing Warehosue Performance 
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

#### Results
To understand and be able to compare warehouse peroformance with the test query I will gather query execution metrics from snowflake. These metrics can be retrieved via the query_id which is a system generated unique id for each query. Using query id I get the metrics from the snowflake system by querying internal system tables `snowflake.account_usage.query_history`

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


##  Cost & Performance Analysis 

<div class="notice">
<iframe width="1000" height="550" src="https://lookerstudio.google.com/embed/reporting/225f4ea2-e3d9-482f-8125-9972eaceb14f/page/PTDoD" frameborder="0" style="border:0" allowfullscreen sandbox="allow-storage-access-by-user-activation allow-scripts allow-same-origin allow-popups allow-popups-to-escape-sandbox"></iframe>
</div>
- steady decline / dramatic decline in execution time with each increase of warehouse size 
- there is also a clear decline in price ,showing that there  is alaso a finacnial upside to increasing warehouse size for our test report queery. 
<div class="notice">
  
</div>


<iframe width="1000" height="550" src="https://lookerstudio.google.com/embed/reporting/7e473c99-2c13-43b2-bb3b-d8e068e03b66/page/PTDoD" frameborder="0" style="border:0" allowfullscreen sandbox="allow-storage-access-by-user-activation allow-scripts allow-same-origin allow-popups allow-popups-to-escape-sandbox"></iframe>

- chart shows execution time(miutes) for test query by  warehosue size.
- table shows the percentage change in execution time(minutes) as the warehouse increases to the next size.
- execution time decreases roughly 50% or more all the way down to 2XL - this is a good relationship considering with each ware hosue size increase CPU resources and credit 
- 




<iframe width="1000" height="550" src="https://lookerstudio.google.com/embed/reporting/5ee1d556-9e16-4e82-989f-d278e2a2d593/page/PTDoD" frameborder="0" style="border:0" allowfullscreen sandbox="allow-storage-access-by-user-activation allow-scripts allow-same-origin allow-popups allow-popups-to-escape-sandbox"></iframe>


