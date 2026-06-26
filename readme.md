
#  Fairness Analysis in Diabetes Prediction

This project evaluates the fairness of different machine learning models for predicting diabetes using the Pima Indians Diabetes dataset. In addition to standard performance metrics such as accuracy and ROC-AUC, the analysis examines fairness metrics to determine whether each model performs equitably across different age groups. The goal is to understand not only which model is most accurate, but also whether its predictions are balanced and reliable for different subgroups. This is important because a model can achieve strong overall performance while still producing unfair or inconsistent results for specific groups

## Objectives
1.Understand model performance in predicting diabetes.

2.Evaluate how models perform across different demographic groups.

3.Highlight possible biases and provide insight into fair model development.


##  Project Files

- `fairness.Rmd` – The main R Markdown file containing all code, plots, and fairness evaluations.
- `Pima Indians Diabetes.csv` – The dataset used for training and testing the models.



##  Dataset Overview

The dataset includes medical diagnostic data for female patients of Pima Indian heritage, including:

- Pregnancies
- Glucose
- Blood Pressure
- Skin Thickness
- Insulin
- BMI
- Diabetes Pedigree Function
- Age
- Outcome: `0 = No Diabetes`, `1 = Yes Diabetes`


##  Models Used

The following machine learning models are applied:

- Logistic Regression (via `glmnet`)
- Decision Tree (`rpart`)
- Random Forest (`randomForest`)
- XGBoost (`xgboost`)


## Fairness Analysis

The `fairness` R package is used to evaluate model equity across groups (e.g., age groups, other possible features).

Metrics analyzed include:


  <img width="700" height="420" alt="image" src="https://github.com/user-attachments/assets/aa07b430-f3ac-4b2a-bc08-8bbed7755702" />


This analysis helps assess model performance beyond overall accuracy by showing whether prediction outcomes and error patterns are balanced across groups. In this project, fairness analysis is important because a model may perform well overall but still show unequal performance for specific age groups.


##  How to Run the Project

1.Open fairness.Rmd in RStudio.

2.Place Pima Indians Diabetes.csv in the same directory.

3.Install all required R packages (see below).

4.Knit the file to HTML Notebook or run each code chunk interactively.

##  Required R Libraries

```r
library(tidyverse)
library(ggplot2)
library(caret)
library(glmnet)
library(pROC)
library(randomForest)
library(rpart)
library(rpart.plot)
library(rattle)
library(xgboost)
library(fairness)
library(gtsummary)
library(scales)
library(patchwork)
library(RColorBrewer)
```





