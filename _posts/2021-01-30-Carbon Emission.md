---
title: Predicting Carbon Emission of Cars
date: 2021-01-03T15:34:30.000-04:00
categories:
- blog
tags:
- Python
- Numpy
- Matplotlib
- Pandas
- Plotly
- Scikit Learn
- Tensorflow

---

# Initial

The goal of the project was to analyze a dataset of car specifications and based on certain parameters, predict future model carbon emissions.

# The Dataset

The Dataset contains the following informations,
- model year	
- maker of the car
- model name
- vehicle type
- engine size
- number of cylinders
- transimission type
- fuel type
- fuel consumption in the city
- fuel consumption on highway
- combined fuel consumption
- fuel efficiency
- Carbon Emission

# Data Cleaning

Since not all information is required, only certain information is extracted to build up a model. Only the engine size, number of cylinders and the combined fuel consumption is taken into consideration to predict a model to find future model carbon emissions.

The following figure shows a scatter plot showing the engine size on the x-axis, carbon emissions on the y-axis, the size of the plots denotes the combined fuel consumption and the color scale denotes the number of cylinders.

![carbon-emission-plot]('/assets/images/carbon-emission-plot-1.png')