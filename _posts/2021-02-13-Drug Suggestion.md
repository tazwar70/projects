---
title: Drug Suggestion - Decision Tree
date: 2021-02-13T15:34:30.000-04:00
header:
  teaser: https://github.com/tazwar70/blog/raw/master/_posts/images/drug%20suggestion%20decision%20tree.png
categories:
- post
tags:
- Python
- Machine Learning
- Sci-kit Learn
- Decision Tree

---

This project deals with a Data-set of patient information and using Supervised Learning - Classification technique to make a decision tree to suggest an appropriate medication.

# The Data-set

The following table is a sample from the entire Data-set.

| Age | Sex | BP     | Cholesterol | Na_to_K | Drug  |
|-----|-----|--------|-------------|---------|-------|
| 23  | F   | HIGH   | HIGH        | 25.355  | drugY |
| 47  | M   | LOW    | HIGH        | 13.093  | drugC |
| 47  | M   | LOW    | HIGH        | 10.114  | drugC |
| 28  | F   | NORMAL | HIGH        | 7.798   | drugX |

Age - 15 to 74

Sex - Male and Female

BP - Low, Normal and High Blood Pressure

Drug - A, B, C, X and Y

# Objective

Based on the Data-set, build a decision tree to suggest the appropriate medication.

# Model Parameters

## Label Encoding

```python
le_sex = preprocessing.LabelEncoder()
le_sex.fit(['F','M'])
data[:,1] = le_sex.transform(data[:,1]) 


le_BP = preprocessing.LabelEncoder()
le_BP.fit([ 'LOW', 'NORMAL', 'HIGH'])
data[:,2] = le_BP.transform(data[:,2])


le_Chol = preprocessing.LabelEncoder()
le_Chol.fit([ 'NORMAL', 'HIGH'])
data[:,3] = le_Chol.transform(data[:,3])
```

## Test-train split

From the Data-set of 200 cases, 75% was used for training the model.

```python
x_train, x_test , y_train, y_test = train_test_split(
    x,
    y,
    test_size = 0.25,
    random_state = 5
)
```

Shape of the data,

    X-Train: (150, 5)
    Y-Train: (150,)
    X-Test: (50, 5)
    Y-Test: (50,)

## Modeling

The following snippet was used for the model fitting.

```python
model = DecisionTreeClassifier(criterion="entropy")
model.fit(x_train,y_train)
```

## Evaluation

Using the model and metrics an accuracy of 1 was achieved.

```python
predicted_y = model.predict(x_test)

metrics.accuracy_score(y_test, predicted_y)
```

    Decision Tree Accuracy:  1.0


# Decision Tree

The following diagram shows the decision tree breakdown of the model.

![Decision Tree](https://github.com/tazwar70/blog/raw/master/_posts/images/drug%20suggestion%20decision%20tree.png)

Link to Notebook: [GitHub](https://github.com/tazwar70/Drug-Suggestion)

Link to Database: [GitHub](https://github.com/tazwar70/Databases/blob/main/drug_stats.csv)

Note: The original Data-set is from IBM. This a practice project, please do not use this for any sort of real-life application.