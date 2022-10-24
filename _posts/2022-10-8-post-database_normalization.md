---
title: "Database Normalization"
excerpt: Modeling data to reduce redundancy and provide scalabilty for reporting
classes: wide
categories:
  - Post
header:
  overlay_image: /assets/images/norm1.jpeg
  actions:
    - label: "View the Repo" 
      url: ""
author_profile: True 
---

How can we utilize database normalization to assist with analysis. 

Why normalize the data?

all transaction data for one day has been inserted into th database. Ocne as a regular table and another time within a normalized database model. 
The below query will get the size of the normalized schema and non-normalized table(original data) in bytes, and compare the sizes.

```sql
    SELECT NORMALIZED_SCHEMA "Normalized Schema",
	NON_NORMALIZED_TABLE " Non-normalized Table",
	ROUND(((NON_NORMALIZED_TABLE - NORMALIZED_SCHEMA) / NON_NORMALIZED_TABLE) * 100,
		2) "Difference (%)"
    FROM
	(SELECT SUM(PG_RELATION_SIZE(QUOTE_IDENT(SCHEMANAME) || '.' || QUOTE_IDENT(TABLENAME))) NORMALIZED_SCHEMA
		FROM PG_TABLES
		WHERE SCHEMANAME = 'sf_ticket_trans') STAT1,

    (SELECT PG_RELATION_SIZE('public.data_08012022') NON_NORMALIZED_TABLE) STAT2	
````
	
Output: 
<table>
<thead>
<tr>
  <th>Normalized Schema</th>
  <th>Non-normalized Table </th>
 <th>Difference (%) </th>
</tr>
</thead>
<tbody>
<tr>
  <td>6979584</td>
  <td>7733248</td>
  <td>9.75</td>
</tr>
</tbody>
</table>
  
From the above output we can see that we have been able to save almost 10% of space through normalization. While that is not currently a huge difference, as more data for each day is added to the databaase model we can save 10% of kilobytes , megabytes, and so on. 

### Purpose 
Performing database normalization to optimze data storage, and allow for easier analysis of the meter transaction data locally. 


#### Review Data 
In order to have a normalized databade model we need to review datasets attributes and identify opportunities to reduce redundancys.
<div class="notice">
  <p>tables in SQLite database </p>
<figure>
  <a href="/assets/images/normalization/uniquedf.png"><img src="/assets/images/normalization/uniquedf.png"></a>
</figure>
  </div>
  
  *transmission_datetime* column is clearly the unique identifier/primary key for the transaction data with the column being 100% uniue. 
  The majority of columns have a low percentage of unique values, giving us a clear answer on if they are worth normalizing into dimension tables. 
  
We do however have 2 datetime columns that have a high percentage of unique values This is due to the datetime date type Having a combination of days, hours, minutes, and seconds it is easy to have several thousand unique values. 

<div class="notice">
  <p>tables in SQLite database </p>
<figure>
  <a href="/assets/images/normalization/datetime info.png"><img src="/assets/images/normalization/datetime info.png"></a>
</figure>
  </div>

However hardly 50% of the total balues are unique for one day, and with the plan to insert data for at least the month of August, we can easlily begin to start seeing more redundacny. It could be interesting and fun to see how we attempt to normalzie the data. 
  
## normalizing methods for each column
<table>
<thead>
<tr>
  <th>Attribute</th>
  <th>Normalization Method</th>
</tr>
</thead>
<tbody>
<tr>
  <td>post_id</td>
  <td>Create dimension table for unique meter post id's</td>
</tr>
<tr>
  <td>street_block</td>
  <td>Create dimension table for unique street blocks</td>
</tr>
<tr>
  <td>Create dimension table for unique payment types</td>
  <td>7733248</td>
</tr>
<tr>
  <td>session_start_dt</td>
  <td>
	<ul>  
		<li> split into separate date and time column</li>
		<li>reduce redundant unqique values by stripping second <br> from time and grouping time by 5 minute intervals</li> 
		<li>create dimension table for unique times</li>
	  </ul>
</td>
</tr>
<tr>
  <td>session_end_dt</td>
  <td>
  <ul>  
		<li> split into separate date and time column</li>
		<li>reduce redundant unqique values by stripping second <br> from time and grouping time by 5 minute intervals</li> 
		<li>create dimension table for unique times</li>
	  </ul>
  </td>
</tr>
<tr>
  <td>gross_paid_amt</td>
  <td>
  <ul>
  <li>round currency float by nearest .50 to reduce redunant unique <br> values/create grouping </li>
  <li>
  create dimension table for unique payment ammounts 
  </li>
  </ul>
   </td>
</tr>
</tbody>
</table>


#### Model Data 

Below is an entity relationship diagram which delineates our fact table and dimension tables. effectively showing how data will be normailzed and how the tables will interact with each other vbased on the aformentioned normalization.


<div class="notice" style="display:block;
    margin:auto;">
<figure>
  <a href="/assets/images/normalization/sf_trans_ERD.png"><img src="/assets/images/normalization/sf_trans_ERD.png"></a>
</figure>
  </div>
  
  

#### Database 
- create schema 
- load data 








