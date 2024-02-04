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

notice: all charts are interactive, can be hovered over and clicked. 

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

We will focus on the compute layer, becuase it is where virtual warehouses are handled and how credit consumption is calcualted. 

Running a virtual warehouse will cause spending credits to be consummed. Credit consumption is effected by various things but primarly determined by the size of a warehouse and ammount of time its running. Digging deeper the ammount of time it is running dpeends on the complexity of a query and the ammount of data being queried/ scanned  

Snowflake allows you to spin up numerous warehouses that auto suspend when not being used. This allows users to create differnet sized warehosues for differnt or specifc jobs, which allows us to optimize for time and speedi n query performance. 

## Testing Warehosue Performance 
I will be using an enterprise edtition of snowflake with a US Central 1 (Iowa) storage region. For this setup 1 Snowflake credit = $3 USD 

#### Warehouse setup 
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


<query> 


##  Cost & Performance Analysis 

<iframe width="1000" height="550" src="https://lookerstudio.google.com/embed/reporting/225f4ea2-e3d9-482f-8125-9972eaceb14f/page/PTDoD" frameborder="0" style="border:0" allowfullscreen sandbox="allow-storage-access-by-user-activation allow-scripts allow-same-origin allow-popups allow-popups-to-escape-sandbox"></iframe>


<iframe width="1000" height="550" src="https://lookerstudio.google.com/embed/reporting/7e473c99-2c13-43b2-bb3b-d8e068e03b66/page/PTDoD" frameborder="0" style="border:0" allowfullscreen sandbox="allow-storage-access-by-user-activation allow-scripts allow-same-origin allow-popups allow-popups-to-escape-sandbox"></iframe>


<iframe width="1000" height="550" src="https://lookerstudio.google.com/embed/reporting/5ee1d556-9e16-4e82-989f-d278e2a2d593/page/PTDoD" frameborder="0" style="border:0" allowfullscreen sandbox="allow-storage-access-by-user-activation allow-scripts allow-same-origin allow-popups allow-popups-to-escape-sandbox"></iframe>


