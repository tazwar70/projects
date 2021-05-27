---
title: Capstone Project - Bank Stock Analysis
date: 2021-05-20
author_profile: false
tagline: ""
header:
  overlay_image: https://raw.githubusercontent.com/tazwar70/Finance-Project/d8ca92b3c81520dde3ff8d6316961384d20d4123/plots/Finance_project_38_1.png
  overlay_filter: rgba(0,128,128,0.5)
  teaser: https://raw.githubusercontent.com/tazwar70/Finance-Project/d8ca92b3c81520dde3ff8d6316961384d20d4123/plots/Finance_project_38_1.png
toc: true
toc_label: "Contents"
toc_icon: "cog"

tags:
- Python
---

This is a Data Science Capstone project, a part of the Data Science Bootcamp course from Udemy, that focuses on exploratory data analysis of stock prices of different Banks for a set duration.

## The Data

Pandas is used to get data from Yahoo Finance.

Pandas [DataReader](https://github.com/pydata/pandas-datareader) is used to read the [stock data](http://pandas.pydata.org/pandas-docs/stable/remote_data.html).

Using pandas-datareader, stock information from the following banks are taken,

*  Bank of America
* CitiGroup
* Goldman Sachs
* JPMorgan Chase
* Morgan Stanley
* Wells Fargo


### Bank Import

The following snippets were used to get the stock information of the following banks

```python
# Bank of America
BAC = data.DataReader("BAC", 'yahoo', begining_time, end_time)
# CitiGroup
C = data.DataReader("C", 'yahoo', begining_time, end_time)
# Goldman Sachs
GS = data.DataReader("GS", 'yahoo', begining_time, end_time)
# JPMorgan Chase
JPM = data.DataReader("JPM", 'yahoo', begining_time, end_time)
# Morgan Stanley
MS = data.DataReader("MS", 'yahoo', begining_time, end_time)
# Wells Fargo
WFC = data.DataReader("WFC", 'yahoo', begining_time, end_time)
```

## Returns

### Data Overview

The following pairplot shows the returns of stocks from the dataset.

### Pairplot


{% include figure image_path="https://raw.githubusercontent.com/tazwar70/Finance-Project/main/plots/Finance_project_21_1.png" 
alt="pairplot-overview" 
caption="Overview Pairplot" 
%}

## EDA


```python
bank_stocks.xs(key='Close',axis=1,level='Stock Info').max()
```

    Bank Ticker
    BAC     54.900002
    C      588.750000
    GS     273.380005
    JPM    141.089996
    MS     109.375000
    WFC     65.930000
    dtype: float64

### Best Returns

    BAC Return   2009-04-09
    C Return     2008-11-24
    GS Return    2008-11-24
    JPM Return   2009-01-21
    MS Return    2008-10-13
    WFC Return   2008-07-16
    dtype: datetime64[ns]

### Worst Returns

    BAC Return   2009-01-20
    C Return     2009-02-27
    GS Return    2009-01-20
    JPM Return   2009-01-20
    MS Return    2008-10-09
    WFC Return   2009-01-20
    dtype: datetime64[ns]

### Standard Deviatiion

    BAC Return    0.029140
    C Return      0.031082
    GS Return     0.023626
    JPM Return    0.024819
    MS Return     0.031759
    WFC Return    0.024702
    dtype: float64

### Recent Risk

    BAC Return    0.036933
    C Return      0.042502
    GS Return     0.032929
    JPM Return    0.034272
    MS Return     0.036164
    WFC Return    0.038573
    dtype: float64

## Distribution plot - 2020


### Morgan Stanley

{% include figure image_path="https://raw.githubusercontent.com/tazwar70/Finance-Project/main/plots/Finance_project_32_1.png" 
alt="Morgan Stanley Distribution plot" 
caption="Morgan Stanley Distribution plot" 
%}

### Citigroup


{% include figure image_path="https://raw.githubusercontent.com/tazwar70/Finance-Project/main/plots/Finance_project_34_1.png" 
alt="Citigroup Distribution plot" 
caption="Citigroup Distribution plot" 
%}

## More Visualization

### Import

{% include figure image_path="https://raw.githubusercontent.com/tazwar70/Finance-Project/main/plots/Finance_project_38_1.png" 
alt="Stocks Returns line plot" 
caption="Stocks Returns line plot" 
%}


## Moving Averages

Analyzing the moving averages for the stocks between 2020-Present.

### Line Plot

{% include figure image_path="https://raw.githubusercontent.com/tazwar70/Finance-Project/main/plots/Finance_project_42_1.png" 
alt="Moving Averages line plot" 
caption="Moving Averages line plot" 
%}


### Heatmap

Correlation between the stocks Close Price.

{% include figure image_path="https://raw.githubusercontent.com/tazwar70/Finance-Project/main/plots/Finance_project_44_1.png" 
alt="Returns Heatmap" 
caption="Returns Heatmap" 
%}

### Clustermap

{% include figure image_path="https://raw.githubusercontent.com/tazwar70/Finance-Project/main/plots/Finance_project_46_1.png" 
alt="Returns Clustermap" 
caption="Returns Clustermap" 
%}

GitHub: [here](https://github.com/tazwar70/Finance-Project/)
