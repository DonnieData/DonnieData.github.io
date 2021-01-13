---
title: "Exploring Data Through Custom Dashboards"
excerpt_separator: "<!--more-->" 
classes: wide
categories:
  - Post
tags:
excerpt: Building ETL Pipelines to clean, transform and store data. 
header:
  overlay_filter: rgba(66, 127, 188,1)
  actions:
    - label: "View the Web App" 
      url: "https://donniedata.github.io/Button_Biodiversity/"
    - label: "GitHub Repo"
      url: "https://github.com/DonnieData/Button_Biodiversity"
author_profile: True 

    
---
<b>Dashboards</b> are a powerful tool which allows us to explore and analyze data from several viewpoints at once through a singular interface/layout. This presents the possibility to 
highlight relationships and trends that are not the most clear on the surface. 

Of the many tools and features a dashboard can offer, the most prominent are customizability and interactiveness. Providing the ability for users to intuitively explore data on their own allows the possibility of limitless insights. 

With this in mind, I have created a simple dahsboard layout using HTML and Bootstrap CSS, and a javascript script in the backend to parse data and display it using the Plotly library.  



While this dashobard may be simple it will....

How it was made:....

<p>A dashboard to dynamically visualize and share bacteria samples data. The drop down within the dashboard allows you to select a volunteer's id number. The interactive tables and charts will then update with the corresponding data, allowing for further analysis and exploration.</p>


## Resources 
Including the D3, resources needed to create our web application are : 
  - a code editor (that supports JavaScript and HTML) 
  - D3.js 
  - HTML
  - Javascript 
  - CSS & 
  - Bootstrap 
 


<div class="notice">
<b>Note:</b> Adding the link to D3.js allows the library to "listen" in on our code, or react to user input. For example, if we did not add this link, our d3.select section of code in app.js wouldn't know where to insert data. <br>
  <a href="https://www.cdnpkg.com/d3"><b>D3.js CDN Link reference</b></a><br> 
  <a href="https://www.imperva.com/learn/performance/what-is-cdn-how-it-works/"><b>More on CDNs</b></a>
   </div>
   

<div class="notice">
<figure>
  <a href="/assets/images/ufo/app_test_2.gif"><img src="/assets/images/ufo/app_test_2.gif"></a>
</figure>
</div>


[design table]

### The Deployed Project


<div class="notice" style="text-align: center">
<figure>
  <a href="/assets/images/ufo/app_test_3.gif"><img src="/assets/images/ufo/app_test_3.gif"></a>
</figure>
</div>



<div style="text-align: center"><a href="https://donniedata.github.io/Button_Biodiversity/"><button style="color:#636769; background-color:white; border: 2px solid gray; padding: 7px; border-radius: 3px;" type="button"
onMouseOver="this.style.color='#157198'"
   onMouseOut="this.style.color='#636769'"><b>View the Web App</b></button></a></div>
   
### Further Development 
With all great projects and applications, there is always room for improvement and further development. This is especially the case in tech, in which new tools and features are consistently made available. 

Amongst several ideas I have for improving this project, I'm most excited about building-out a method to retrieve live data and to have automated visualizations based on the data. 
The application itself was meant to be quite versatile and reusable. Thanks to this the code can be easily refactored to fit many data sources and forms. 
Please feel free to review the projects repository on GitHub and use the code as you like for your own practice/work. 

Thank you for reading and exploring the data! 
