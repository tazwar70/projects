---
title: Capstone Project - 911 Calls
date: 2021-05-11T15:34:30.000-04:00
header:
  overlay_image: https://raw.githubusercontent.com/tazwar70/911-Calls/main/plots/reason-911-month-hist.jpg
  overlay_filter: rgba(0,128,128,0.5)
  teaser: https://raw.githubusercontent.com/tazwar70/911-Calls/main/plots/reason-911-month-hist.jpg
author_profile: false
# Table of Contents
toc: true
toc_label: "Contents"
toc_icon: "cog"

categories:
- Data Science
tags:
- Python


# Gallery Views
reason-hist:
  - url: https://raw.githubusercontent.com/tazwar70/911-Calls/main/plots/reason-911-day-of-week-dist-hist.jpg
    image_path: https://raw.githubusercontent.com/tazwar70/911-Calls/main/plots/reason-911-day-of-week-dist-hist.jpg
    alt: "Histogram of reason of calls weekly"
    title: "Histogram of reason of calls weekly"
  - url: https://raw.githubusercontent.com/tazwar70/911-Calls/main/plots/reason-911-month-hist.jpg
    image_path: https://raw.githubusercontent.com/tazwar70/911-Calls/main/plots/reason-911-month-hist.jpg
    alt: "Histogram of reason of calls monthly"
    title: "Histogram of reason of calls monthly"

heat-clustermap1:
  - url: https://raw.githubusercontent.com/tazwar70/911-Calls/main/plots/heatmap.jpg
    image_path: https://raw.githubusercontent.com/tazwar70/911-Calls/main/plots/heatmap.jpg
    alt: "Heatmap"
    title: "Heatmap"
  - url: https://raw.githubusercontent.com/tazwar70/911-Calls/main/plots/clustermap.jpg
    image_path: https://raw.githubusercontent.com/tazwar70/911-Calls/main/plots/clustermap.jpg
    alt: "Clustermap"
    title: "Clustermap"

heat-clustermap2:
  - url: https://raw.githubusercontent.com/tazwar70/911-Calls/main/plots/heatmap-2.jpg
    image_path: https://raw.githubusercontent.com/tazwar70/911-Calls/main/plots/heatmap-2.jpg
    alt: "Heatmap"
    title: "Heatmap"
  - url: https://raw.githubusercontent.com/tazwar70/911-Calls/main/plots/clustermap-2.jpg
    image_path: https://raw.githubusercontent.com/tazwar70/911-Calls/main/plots/clustermap-2.jpg
    alt: "Clustermap"
    title: "Clustermap"
---

This is a data science capstone project which analyzes some 911 call data from a [Kaggle](https://www.kaggle.com/mchirico/montcoalert) dataset.

The data contains the following fields:

* ***lat*** : String variable, Latitude
* ***lng***: String variable, Longitude
* ***desc***: String variable, Description of the Emergency Call
* ***zip***: String variable, Zipcode
* ***title***: String variable, Title
* ***timeStamp***: String variable, YYYY-MM-DD HH:MM:SS
* ***twp***: String variable, Township
* ***addr***: String variable, Address
* ***e***: String variable, Dummy variable (always 1)

# Overview

The following snippet shows a small overview of the dataset.

```python
df.info()

<class 'pandas.core.frame.DataFrame'>
RangeIndex: 99492 entries, 0 to 99491
Data columns (total 9 columns):
lat          99492 non-null float64
lng          99492 non-null float64
desc         99492 non-null object
zip          86637 non-null float64
title        99492 non-null object
timeStamp    99492 non-null object
twp          99449 non-null object
addr         98973 non-null object
e            99492 non-null int64
dtypes: float64(3), int64(1), object(5)
memory usage: 6.8+ MB
```

There are three primary reasons for the calls, with a total of 110 unique variations of the calls.

```python
df['Reason'].value_counts()

EMS        48877
Traffic    35695
Fire       14920
Name: Reason, dtype: int64

df['title'].nunique()

110
```

In order to get the reasons from the raw dataset, the following snippet was used,

```python
df['Reason'] = df['title'].apply(lambda title: title.split(':')[0])
```


The following histogram shows the distribution of the calls.

{% include figure image_path="https://raw.githubusercontent.com/tazwar70/911-Calls/main/plots/reason-call-hist-plot.jpg" alt="reason-call-hist-plot" caption="Histogram showing calls with corresponding reasons." %}

![reason-call-hist-plot.jpg]()

# Call Frequency Analysis

The timeStamp raw data is then further broken down into more readable data as follows:

```python
df['Hour'] = df['timeStamp'].apply(lambda time: time.hour)
df['Month'] = df['timeStamp'].apply(lambda time: time.month)
df['Day of Week'] = df['timeStamp'].apply(lambda time: time.dayofweek)

dmap = {0:'Mon',1:'Tue',2:'Wed',3:'Thu',4:'Fri',5:'Sat',6:'Sun'}
df['Day of Week'] = df['Day of Week'].map(dmap)
```

Following which the following histograms are produced.

{% include gallery layout="full" id="reason-hist" caption="Histograms showing the reason of calls with weekly and monthly representation." %}

In the histogram showing the call-reason distribution between the months, there are missing data between the months of 8 and 12. In order to mitigate the discontinuity in the data, the following line plot is used.

{% include figure image_path="https://raw.githubusercontent.com/tazwar70/911-Calls/main/plots/reason-911-month-line-plot.jpg" alt="reason-911-month-line-plot" caption="Monthly calls line plot." %}

# Daily Calls Analysis

Initially the dataframe was restructured to a better format to create a heatmap and clustermap.

```python
dayHour = df.groupby(by=['Day of Week','Hour']).count()['Reason'].unstack()
dayHour.head()

Hour 	0 	1 	2 	3 	4 	5 	6 	7 	8 	9 	... 	14 	15 	16 	17 	18 	19 	20 	21 	22 	23
Day of Week 																					
Fri 	275 	235 	191 	175 	201 	194 	372 	598 	742 	752 	... 	932 	980 	1039 	980 	820 	696 	667 	559 	514 	474
Mon 	282 	221 	201 	194 	204 	267 	397 	653 	819 	786 	... 	869 	913 	989 	997 	885 	746 	613 	497 	472 	325
Sat 	375 	301 	263 	260 	224 	231 	257 	391 	459 	640 	... 	789 	796 	848 	757 	778 	696 	628 	572 	506 	467
Sun 	383 	306 	286 	268 	242 	240 	300 	402 	483 	620 	... 	684 	691 	663 	714 	670 	655 	537 	461 	415 	330
Thu 	278 	202 	233 	159 	182 	203 	362 	570 	777 	828 	... 	876 	969 	935 	1013 	810 	698 	617 	553 	424 	354

5 rows × 24 columns
```

{% include gallery layout="wide" id="heat-clustermap1" caption="Daily Calls Analysis." %}

# Monthly Calls Analysis

The previous method is redone, initially reformatting the dataframe as follows,

```python
dayMonth = df.groupby(by=['Day of Week','Month']).count()['Reason'].unstack()
dayMonth.head()

Month 	1 	2 	3 	4 	5 	6 	7 	8 	12
Day of Week 									
Fri 	1970 	1581 	1525 	1958 	1730 	1649 	2045 	1310 	1065
Mon 	1727 	1964 	1535 	1598 	1779 	1617 	1692 	1511 	1257
Sat 	2291 	1441 	1266 	1734 	1444 	1388 	1695 	1099 	978
Sun 	1960 	1229 	1102 	1488 	1424 	1333 	1672 	1021 	907
Thu 	1584 	1596 	1900 	1601 	1590 	2065 	1646 	1230 	1266
```

Following which the following heatmap and clustermap was produced.

{% include gallery layout="full" id="heat-clustermap2" caption="Monthly Calls Analysis." %}


The complete Jupyter-Notebook and the dataset can be found from the resource below.

View Resources: [GitHub](https://github.com/tazwar70/911-Calls)