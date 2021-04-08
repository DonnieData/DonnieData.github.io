---
title: "Exploring Data Through Custom Dashboards"
excerpt_separator: "<!--more-->" 
classes: wide
categories:
  - Post
tags:
excerpt: Building ETL Pipelines to clean, transform and store data. 
header:
  overlay_image: /assets/images/post/belly_427FC8.png
  actions:
    - label: "View the Web App" 
      url: "https://donniedata.github.io/Bacteria_Biodiversity/"
    - label: "GitHub Repo"
      url: "https://github.com/DonnieData/Button_Biodiversity"
author_profile: True 

    
---
<b>Dashboards</b> are a powerful tool which allows us to explore and analyze data from several viewpoints at once through a singular interface/layout. This presents the possibility to 
highlight relationships and trends that are not the most clear on the surface. 

Of the many tools and features a dashboard can offer, the most prominent are customizability and interactiveness. Providing the ability for users to intuitively explore data on their own allows the possibility of limitless insights. 

With this in mind, I have created a simple dashboard with bacteria samples data, to create a fun and interactive layout in which many insights can be derived from.  

## Resources & Components

- Plotly.js
The plotly library allows for powerful and interactive visualizations to be built through JavaScript code, without needed to download any extra components or files.

- Bootstrap & Additional CSS
Bootstrap's grid system is utilized to create and design a crisp page layout. 

- JavaScript 
The heart of this project is the script which is designed to parse the bacteria data which is in json format.

![img]

The data is then passed through several functions to transform it into the appropriate formats for each chart. 
The script then inserts the visualizations into the web page.


## Deployment 

The dashboard provides a dropdown menu of volunteer id numbers. When selected the table and charts will update with corresponding data of samples collected from the volunteer.



<div class="notice">
<b>Note:</b> There are strict protocols and laws in place in regards to working with medical data. Public analysis of medical data will always be anonymous in regards to people (e.g volunteers, patients, etc)
   </div>
   
<div class="notice">
<figure>
  <a href="/assets/images/post/biodiversity_dash_1.png"><img src="/assets/images/post/biodiversity_dash_1.png"></a>
</figure>
</div>

<div class="notice">
<figure>
  <a href="/assets/images/post/biodiversity_dash_2.gif"><img src="/assets/images/post/biodiversity_dash_2.gif"></a>
</figure>
</div>

<div style="text-align: center"><a href="https://donniedata.github.io/Button_Biodiversity/"><button style="color:#636769; background-color:white; border: 2px solid gray; padding: 7px; border-radius: 3px;" type="button"
onMouseOver="this.style.color='#157198'"
   onMouseOut="this.style.color='#636769'"><b>Explore the Dashboard</b></button></a></div>


## Further Development 

Thank you for reading and exploring the data! 

