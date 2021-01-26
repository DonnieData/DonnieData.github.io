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
- JavaScript 
- Leaflet: A open-source JavaScript library for mobile-friendly interactive maps.
- Mapbox: A JavaScript library for interactive, customizable vector maps on the Web.
- Bootstrap CSS 

### Overview 
Through javascript, recent earthquake data is retreived via API from <a href="https://earthquake.usgs.gov">earthquake.usgus.gov</a>, then parsed and transformed. Leaflet is then use to create the base map visualziation and map the data. Mapbox is used to add additional functionalilty and styling, helping to create an in-depth and powerful visualization. 

### Deployment 

The web apppiction hosts an interactive map in which you can review earthquake magnitutdes. 
The interactive map has been designed to have a toggle where you can switch map views (street, satelite, dark). You can also choose which levels of data you would like to be displayed by turning the selection on and off. The available data views are the following:
  - All Earthquakes: Displays all earthquake data
  - Tectonic plate outline: provides a visual of the earth's tectonic plates

<br>
<div style="text-align: center"><a href="https://donniedata.github.io/post/post-earthquakes/"><button style="color:#636769; background-color:#C8E7C8; border: 2px solid gray; padding: 7px; border-radius: 3px;" type="button"
onMouseOver="this.style.color='#62BDDA'"
   onMouseOut="this.style.color='#636769'"><b>Explore the Dashboard</b></button></a></div>






  






