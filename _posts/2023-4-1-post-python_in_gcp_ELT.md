---
title: "Python With Google Cloud"
excerpt: Migrating SQLite database to PostgreSQL for enhanced Data Management
classes: wide
categories:
  - Post
tags:
  - Google Cloud
  - Python
  - Big Query
  - Datawarehouse 
  - Data Modeling 
header:
  overlay_image: /assets/images/splash_project/phone_line.jpg
  actions:
    - label: "View Dashboard" 
      url: ""
    - label: "GitHub Repo"
      url: ""
author_profile: True 
---
### Overview 

<b>Google CLoud Platform</b> Is a powerful ecosystem with a plethora of products for different needs. One of its offerings is Big Query, which is a robust cloud based datawarehouse. Data warehouses are genrally used to house historical data for business intellignece purposes. 
Like many data bases and warehouses, python 

Via googles credentials api remote access to cloud environments and recsources are accesible remotly. Utilizing this, In this project I develope an ELT(Extract, Load, Transform) pipeline, Using python and SQL with Big Query. I then connect one of Googles Data visualizations tool Data Studio to create an intuitive dashbaord to allow for easy interaction and analyzing of data from a businees intelligence stadnpoint. 


### Steps 

#### Google Cloud  
In the google cloud console, I lauch the cloud shell and use the necesseary shell commands to create the schema (Project_id,dataset and table structure, location etc) in Big Query.

![image](https://user-images.githubusercontent.com/55963911/229971264-6f9c1485-1e4e-4a11-aaa2-989fdd4ae60c.png)

Then I use google cloud administration tools (IAM) to create a new private key and service account thaty will allow remote access.

![image](https://user-images.githubusercontent.com/55963911/229972141-3a12e383-ab1e-4baf-a906-ddd0c4fab32c.png)


####  Python 

With the service account key setup. I can connect to the Big Query Datawarehouse via python.
I will be retrieving Dallas city 311 data for 2022, through API's. In order to do this I need to develope the socrata system query for the kind of dat a I want add it the the endpoint for the 311 dataset. The endpoint will be stored in file with other arguments such as the google cloud project name that will be used. 
![image](https://user-images.githubusercontent.com/55963911/229973706-7866b6f2-6a5c-4e59-9a48-f0c04751813b.png)


These arguemnts and the seperate credential file will be imported when the python script is ran 
![image](https://user-images.githubusercontent.com/55963911/229973375-1f15417f-b41b-4819-a607-7c0c45daa127.png)

Once executed python will retrieve the data and insert it into the "l1_tables" dataset. which will hold the raw unmodified data.

#### Data Transformation 
After the data is loaded into the datawarehouse. SQL is used to transform the data and create new fields. This data is housed in the l2_tables dataset.
Then the l2 data is used to create smaller tables for specific calculations, aggregations and groupings.  


![image](https://user-images.githubusercontent.com/55963911/229974780-0a998a28-9971-4b7f-9aff-f1821a5fbb55.png)





