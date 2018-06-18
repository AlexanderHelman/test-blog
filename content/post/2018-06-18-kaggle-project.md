---
title: Kaggle Project
author: ~
date: '2018-06-18'
slug: kaggle-project
categories: []
tags: []
---

This week I switched from using R to using python for the currenty credit default Kaggle project. Here's what I have so far:

```
import pandas as pd
from sklearn.model_selection import train_test_split
from sklearn.preprocessing import Imputer
from xgboost import XGBRegressor, XGBClassifier

data = pd.read_csv('/Users/alexanderhelman/Downloads/golden-thread/input/application_train.csv')

y = data.TARGET
X = data.drop(['TARGET'], axis=1).select_dtypes(exclude=['object'])
train_X, test_X, train_y, test_y = train_test_split(X.as_matrix(), y.as_matrix(),
                                                  test_size=0.15)
                                                  
my_imputer = Imputer()
train_X = my_imputer.fit_transform(train_X)
test_X = my_imputer.transform(test_X)

my_model = XGBClassifier(n_estimators=1000, objective="binary:logistic")
my_model.fit(train_X, train_y, early_stopping_rounds=10, eval_metric="auc",
             eval_set=[(train_X, train_y), (test_X, test_y)], verbose=True)
             
my_model2 = XGBClassifier(n_estimators=223, objective="binary:logistic")
my_model2.fit(X.as_matrix(), y.as_matrix(), verbose=True)

kaggle_test = pd.read_csv('/Users/alexanderhelman/Downloads/golden-thread/input/application_test.csv')
kaggle_test_X = kaggle_test.select_dtypes(exclude=['object']).as_matrix()

y_pred = my_model2.predict_proba(kaggle_test_X)

list = []
for i in y_pred:
    list.append(i[1])
    
my_submission = pd.DataFrame({'SK_ID_CURR': kaggle_test.SK_ID_CURR, "TARGET": list})
my_submission.to_csv("submission2.csv", index=False)
```
