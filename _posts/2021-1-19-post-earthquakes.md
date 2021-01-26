---
title: "Mapping GeoJson Data"
excerpt_separator: "<!--more-->" 
classes: wide
categories:
  - Post
tags:
excerpt: Transforming geojson into a layered mapping visualization. 
header:
  overlay_image: /assets/images/post/earthquake_FB07F.png
  actions:
    - label: "View the Web App" 
      url: "https://donniedata.github.io/dash_quakes/"
    - label: "GitHub Repo"
      url: "https://github.com/DonnieData/Mapping_Earthquakes"
author_profile: True 

---

<b>GeoJson</b> is a widely-used data format for displaying geographical data in web maps and applications. GeoJson consits of <i>Geometry Object</i> can can contain a plethora of information including, the type of object being mapped including single markers on the map or even lines. As well as location names, longitude, latitude and even timestamps!
  
With the flexibilty to easily be parsed and transformed, it is no wonder GeoJson is the industry standard when it comes to making map visualizations. In order to explore and  GeoJson myself, I have created a web application to visualize Earthquake GeoJson data.


## Application Overview 


### Resources 
javascript 
Leaflet, open-source JavaScript library for mobile-friendly interactive maps
Mapbox 
Bootstrap CSS 

### Overview 
Through javascript, recent earthquake data is retreived via API from https://earthquake.usgs.gov/, then parsed and transformed. Leaflet is then use to create the base map visualziation and map the data. Mapbox is used to add additional functionalilty and styling, helping to create an in-depth and powerful visualization. 


### Deployment 

take a look 
review magnitudes and layers 

<div style="text-align: center"><a href="https://donniedata.github.io/Button_Biodiversity/"><button style="color:#636769; background-color:white; border: 2px solid gray; padding: 7px; border-radius: 3px;" type="button"
onMouseOver="this.style.color='#53AE74'"
   onMouseOut="this.style.color='#636769'"><b>Explore the Dashboard</b></button></a></div>






  






