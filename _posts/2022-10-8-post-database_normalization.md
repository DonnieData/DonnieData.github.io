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
### Why normalize The Data
Normalizing a database gratly reduces redendancy in data and can allow you to save disk space which is extremly important when storage resources are limited.
Performing database normalization will optimze data storage, and allow for easier analysis of the meter transaction data locally. 

### Testing Normalization 
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


#### Where Can We Normalize 
In order to have a normalized databade model we need to review datasets attributes and identify opportunities to reduce redundancys.
<div class="notice" style="display:flex; justify-content: center; width:300;">
<figure>
  <a href="/assets/images/normalization/uniquedf.png"><img src="/assets/images/normalization/uniquedf.png"></a>
</figure>
  </div>
  
  *transmission_datetime* column is clearly the unique identifier/primary key for the transaction data with the column being 100% uniue. 
  The majority of columns have a low percentage of unique values, giving us a clear answer on if they are worth normalizing into dimension tables. 
  
We do however have 2 datetime columns that have a high percentage of unique values This is due to the datetime date type Having a combination of days, hours, minutes, and seconds it is easy to have several thousand unique values. 

<div class="notice" style="display:flex; justify-content: center; width:300;">
<figure>
  <a href="/assets/images/normalization/datetime info.png"><img src="/assets/images/normalization/datetime info.png"></a>
</figure>
  </div>

However hardly 50% of the total balues are unique for one day, and with the plan to insert data for at least the month of August, we can easlily begin to start seeing more redundacny. It could be interesting and fun to see how we attempt to normalzie the data. 
  
## Normalization Methods 
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


<div class="notice" style="display:flex; justify-content: center;">

  <a href="/assets/images/normalization/sf_trans_ERD.png"><img src="/assets/images/normalization/sf_trans_ERD.png"></a>
  </div>
  
  

#### Database 
- create schema 
- load data 


### Execution - Retrieving & Normalizing 
The below diagram outlines the entire data process:


<div class="notice" style="display:flex; justify-content: center;">

  <a href="/assets/images/normalization/normalization etl diagram .png"><img src="/assets/images/normalization/normalization etl diagram .png"></a>
  </div>

below is a log of the data which was retrieved via api by date. The data is logged once retreival and insertion into the database is complete. 

**1819348** rows of data for the entire month of August, 2022 is now ready to be freely analyzed with data being stored locally with the most minial ammount of disk space being used. 

<div style="overflow-y: scroll; width:400px;height:400px">
	<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Data Date</th>
      <th>Rows</th>
      <th>Execution Time(minutes)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2022-08-01</td>
      <td>65382.0</td>
      <td>1.89</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2022-08-02</td>
      <td>67550.0</td>
      <td>2.97</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2022-08-03</td>
      <td>69231.0</td>
      <td>2.59</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2022-08-04</td>
      <td>68049.0</td>
      <td>2.38</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2022-08-05</td>
      <td>69557.0</td>
      <td>2.69</td>
    </tr>
    <tr>
      <th>5</th>
      <td>2022-08-06</td>
      <td>67796.0</td>
      <td>3.01</td>
    </tr>
    <tr>
      <th>6</th>
      <td>2022-08-07</td>
      <td>4689.0</td>
      <td>0.24</td>
    </tr>
    <tr>
      <th>7</th>
      <td>2022-08-08</td>
      <td>65700.0</td>
      <td>2.60</td>
    </tr>
    <tr>
      <th>8</th>
      <td>2022-08-09</td>
      <td>67161.0</td>
      <td>2.37</td>
    </tr>
    <tr>
      <th>9</th>
      <td>2022-08-10</td>
      <td>68173.0</td>
      <td>3.23</td>
    </tr>
    <tr>
      <th>10</th>
      <td>2022-08-11</td>
      <td>67634.0</td>
      <td>12.37</td>
    </tr>
    <tr>
      <th>11</th>
      <td>2022-08-12</td>
      <td>71181.0</td>
      <td>3.86</td>
    </tr>
    <tr>
      <th>12</th>
      <td>2022-08-13</td>
      <td>68853.0</td>
      <td>2.33</td>
    </tr>
    <tr>
      <th>13</th>
      <td>2022-08-14</td>
      <td>6186.0</td>
      <td>0.23</td>
    </tr>
    <tr>
      <th>14</th>
      <td>2022-08-15</td>
      <td>65764.0</td>
      <td>2.66</td>
    </tr>
    <tr>
      <th>15</th>
      <td>2022-08-16</td>
      <td>68726.0</td>
      <td>2.77</td>
    </tr>
    <tr>
      <th>16</th>
      <td>2022-08-17</td>
      <td>69201.0</td>
      <td>2.82</td>
    </tr>
    <tr>
      <th>17</th>
      <td>2022-08-18</td>
      <td>67794.0</td>
      <td>2.80</td>
    </tr>
    <tr>
      <th>18</th>
      <td>2022-08-19</td>
      <td>71052.0</td>
      <td>2.95</td>
    </tr>
    <tr>
      <th>19</th>
      <td>2022-08-20</td>
      <td>63106.0</td>
      <td>2.54</td>
    </tr>
    <tr>
      <th>20</th>
      <td>2022-08-21</td>
      <td>4489.0</td>
      <td>0.19</td>
    </tr>
    <tr>
      <th>21</th>
      <td>2022-08-22</td>
      <td>65905.0</td>
      <td>2.71</td>
    </tr>
    <tr>
      <th>22</th>
      <td>2022-08-23</td>
      <td>67687.0</td>
      <td>2.67</td>
    </tr>
    <tr>
      <th>23</th>
      <td>2022-08-24</td>
      <td>68177.0</td>
      <td>2.79</td>
    </tr>
    <tr>
      <th>24</th>
      <td>2022-08-25</td>
      <td>67286.0</td>
      <td>2.65</td>
    </tr>
    <tr>
      <th>25</th>
      <td>2022-08-26</td>
      <td>64411.0</td>
      <td>2.55</td>
    </tr>
    <tr>
      <th>26</th>
      <td>2022-08-27</td>
      <td>67914.0</td>
      <td>2.75</td>
    </tr>
    <tr>
      <th>27</th>
      <td>2022-08-28</td>
      <td>132.0</td>
      <td>0.01</td>
    </tr>
    <tr>
      <th>28</th>
      <td>2022-08-29</td>
      <td>51754.0</td>
      <td>1.98</td>
    </tr>
    <tr>
      <th>29</th>
      <td>2022-08-30</td>
      <td>62497.0</td>
      <td>2.39</td>
    </tr>
    <tr>
      <th>30</th>
      <td>2022-08-31</td>
      <td>66311.0</td>
      <td>2.87</td>
    </tr>
  </tbody>
</table>	
</div>

#### Future Updates 
Python 
- update script to allow for user input for date span/ranges
-  log size of all original data combined and compare to entire normalized schema 
-  creating non materialized database views for data analysis 








