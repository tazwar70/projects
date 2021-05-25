---
title: Classifying Flower Data
date: 2021-02-14T15:34:30.000-04:00
header:
  overlay_image: https://github.com/tazwar70/blog/raw/master/_posts/images/iris-scatterplot.png
  overlay_filter: linear-gradient(rgb(0,128,128,0.5))
  teaser: https://github.com/tazwar70/blog/raw/master/_posts/images/iris-scatterplot.png
toc: true
toc_label: "Contents"
toc_icon: "cog"
categories:
- post
tags:
- Python
- Machine Learning
- Classification
- KNN

---

This project focuses on classifying flowers based on the IRIS Data-set using the K Nearest Neighbors (KNN) method.

# The Data

The figure below shows the distribution of the Data-set using seaborn visualization.

![IRIS-scatterplot](https://github.com/tazwar70/blog/raw/master/_posts/images/iris-scatterplot.png)

The Data-set includes the following information,

A total of 150 rows of flower data with 3 different species,
    
- virginica
- setosa
- versicolor

*sepal_length* - ranging from 4.3 to 7.9

sepal_width	- ranging from 2 to 4.4

petal_length - ranging from 1 to 6.9

petal_width - ranging from 0.1 to 2.5

# The Model

In order to train the model, 2/3 of the data was used and 1/3 for testing.

```python
x_train, x_test , y_train, y_test = train_test_split(
    x,
    y,
    test_size = 1/3
)
```

The KNN model using 5 nearby neighbors,

```python
model = KNeighborsClassifier(n_neighbors=5)
model.fit(x_train, y_train)
```

The model parameters are as follows,

    KNeighborsClassifier(
        algorithm='auto',
        leaf_size=30, 
        metric='minkowski',
        metric_params=None, 
        n_jobs=None, 
        n_neighbors=5, 
        p=2,
        weights='uniform'
    )


# Evaluation

The table below shows the classification report of the model,

             precision    recall  f1-score   support

    setosa       1.00      1.00      1.00        20
    versicolor   0.92      0.92      0.92        12
    virginica    0.94      0.94      0.94        18

    accuracy                            0.96        50
    macro avg       0.95      0.95      0.95        50
    weighted avg    0.96      0.96      0.96        50


The image below shows the confusion matrix of the model,

![IRIS confusion matrix](https://github.com/tazwar70/blog/raw/master/_posts/images/iris-confusion-matrixpng.png)



Link to Notebook: [GitHub](https://github.com/tazwar70/IRIS-Dataset-Classification)

Link to Model: [Download](https://github.com/tazwar70/IRIS-Dataset-Classification/raw/main/iris_model.joblib)

Link to Database: [GIST-RAW-CSV](https://gist.githubusercontent.com/curran/a08a1080b88344b0c8a7/raw/0e7a9b0a5d22642a06d3d5b9bcbad9890c8ee534/iris.csv)

