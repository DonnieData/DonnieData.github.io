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

Then I the Identiy Access Managemnt tools in GCP to create a new private key and service account thaty will allow remote access.

![image](https://user-images.githubusercontent.com/55963911/229972141-3a12e383-ab1e-4baf-a906-ddd0c4fab32c.png)


####  Python 
