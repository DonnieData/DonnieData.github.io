---
title: "Sqlite to Postgres Database Migration"
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
#connect to sqlite db file 
sqlite_conn = sqlite3.connect("../sqlite/database.sqlite")
sqlite_cur = sqlite_conn.cursor()

#query all table names 
tables_df = pd.DataFrame(sqlite_cur.execute("SELECT name FROM sqlite_master WHERE type='table'"))
tables_df.columns = [i[0] for i in sqlite_cur.description
```

<div class="notice">
<figure>
  <a href=""><img src=""></a>
</figure>
  </div>

-query data from the loaded data model and convert into dataframes

```python 
#create dictionary with table names that will hold table data
df_dict = {'reviews':None,'artists':None,'genres':None,'labels':None,
           'years':None,'content':None}

for i in list(df_dict.keys()): #iterate through dictionary 
    df_dict[i] = pd.DataFrame(sqlite_cur.execute(f'SELECT * FROM {i}')) #query each table and create dataframe object
    df_dict[i].columns = [i[0] for i in sqlite_cur.description] #get header/columns
```

<div class="notice">
<figure>
  <a href=""><img src=""></a>
</figure>
  </div>
  

-use pandas "to_sql" attribute to crete tables and load data into database via the defined database connection .

```python
#create sqlaclechemy database connection with newly created database 
database = f"postgresql+psycopg2://{config.db_user}:{config.db_password}@localhost:5432/pitchfork?gssencmode=disable"
engine = create_engine(database)   

for i in list(df_dict.keys()): #iterate through dictionary taht holds dataframes of data
    df_dict[i].to_sql(name=i, index=False, con=engine, if_exists='replace', chunksize=100000) # load data into database 
    print(f"Table {i} loaded")
    
```

-Once the data migration is complete, we can review the tables and thier stucture within the database 
-ERD 


## Database Design: Non-materialized Views 
With the data now fully loaded, we can query it dirctly through the database managemnt system. As well as use tools native to the environment, succh as ERD Diagrams. Which allow an easy overhead view of the tables and its columns: 




With confirmation that our data has been loaded in the same format as it was held in the sqlite db file, we can now create some views. 




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





  






