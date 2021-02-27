---
title: "Portfolio"
layout: splash
permalink: /
header:
  overlay_color: "#000"
  overlay_filter: "0.5"
  overlay_image: /assets/images/unsplash-image-1.jpg
excerpt: "Projects that I consider benchmarks of my data analytics journey"
intro: 
  - excerpt: "<h1>Featured Projects<h1>"
feature_row:
  - image_path: /assets/images/splash_project/nasa_splash_1.jpg
    alt: "placeholder image 2"
    title: "Transforming & Dynamically Visualizing Data"
    excerpt: "Building a dynamic webpage to display and filter data using JavaScript." 
    url: "https://donniedata.github.io/post/post-ufo/"
    btn_label: "View Project"
    btn_class: "btn--primary"  
    actions:
  - image_path: /assets/images/splash_project/bacteria_splash_1.jpg
    alt: "placeholder image 1"
    title: "Exploring Data Through Custom Dashboards"
    excerpt: "Creating customizable and interactive charts with Javascript to share insights."
    url: "https://donniedata.github.io/post/post-belly/"
    btn_label: "View Project"
    btn_class: "btn--primary"
  - image_path: /assets/images/splash_project/rector.jpg
    alt: "placeholder image 1"
    title: "Mapping GeoJson Data"
    excerpt: "Traversing geoJson features and attributes"
    url: "https://donniedata.github.io/post/post-earthquakes/"
    btn_label: "View Project"
    btn_class: "btn--primary" 
feature_row2:
  - image_path: /assets/images/splash_project/tab2.png
    alt: "placeholder image 1"
    title: "Analyzing Bike-Sharing Data With Tableau"
    url: "https://donniedata.github.io/post/post-tableau/"
    btn_label: "View Project"
    btn_class: "btn--primary"
  - image_path: /assets/images/splash_project/crime_splash.jpg
    alt: "placeholder image 1"
    title: "Austin Crime Data Analysis"
    excerpt: "Austin Crime Data Analysis"
    url: "#test-link"
    btn_label: "Coming Soon"
    btn_class: "btn--primary" 
  - image_path: /assets/images/pipeline.jpg
    alt: "placeholder image 1"
    title: "Building ETL Pipelines"
    excerpt: "Buidling ETL pipelines with Python and PostgreSQL."
    url: "#test-link"
    btn_label: "Coming Soon"
    btn_class: "btn--primary" 
   
---

{% include feature_row id="intro" type="center" %}

{% include feature_row %}

{% include feature_row id="feature_row2" %}

