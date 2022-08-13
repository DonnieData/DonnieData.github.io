---
title: "Sqlite to Postgres Database Migration with Python"
excerpt: Migrating SQLite database to PostgreSQL for enhanced Data Management
classes: wide
categories:
  - Post
tags:
  - SQLite
  - Python
  - PostreSQL
  - Views
  - Data Modeling 
header:
  overlay_image: /assets/images/splash_project/mig_peg.jpg
  actions:
    - label: "View the Project" 
      url: ""
author_profile: True 
---

<b>SQLite</b> gives us the ability to create a simple relational database model which can be perfect for quickly getting data projects off the ground. However for any long-standing project, infrastructure needs to scale with demand and the data itself. The tables in your model will grow overtime and so will your data management needs. Enter PostreSQL! Postgres is a relational database maangement system that offers many features. 

In this projectI migrate an entire SQLite database into PostgreSQL and explore the use of Views, which is a common but powerful feature. 

## Database Migration 
-loadd sqlite database file into python environment using sqlite3 library 

```python 
import pandas as pd
from sqlalchemy import create_engine
import psycopg2
import sqlite3
import config

#connect to sqlite db file 
sqlite_conn = sqlite3.connect("../sqlite/database.sqlite")
sqlite_cur = sqlite_conn.cursor()

#query all table names 
df = pd.DataFrame(sqlite_cur.execute("SELECT name FROM sqlite_master WHERE type='table'"))
df.columns = [i[0] for i in sqlite_cur.description]
```

-query data from the loaded data model and convert into dataframes using pandas library 


-use pandas to_sql feature which essentially creates a table via defineddatabase connection and iterates an insert statement.


-Once the data migration is complete, we can review the tables and thier stucture within the database 
-ERD 


## Insights with views 




<div class="notice">
<figure>
  <a href=""><img src=""></a>
</figure>
  </div>
  
  
<!--[recordind]-->

<!--[future upates]-->

<br>
<div style="text-align: center; text-shadow: 3px 3px;"><a href=" "><button style="color:#FFFFFF; background-color:#D2691E; border: 1px solid gray; padding: 7px; border-radius: 3px;" type="button"
onMouseOver="this.style.color='#4787F0'"
   onMouseOut="this.style.color='#FFFFFF'"><b>View The Project</b></button></a></div>





  






