<img width="1000" height="500" alt="image" src="https://github.com/user-attachments/assets/0d686946-f555-4705-badc-109821d6b88c" />

#  Fairness Analysis in Diabetes Prediction

This project investigates the fairness of various machine learning models when predicting diabetes using the **Pima Indians Diabetes dataset**. In addition to traditional performance metrics like accuracy and AUC, we focus on **fairness metrics** to assess whether predictions are equitable across different population subgroups.

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

- Statistical Parity
- Equal Opportunity
- Demographic Parity
- Predictive Equality

This allows us to understand how fairly each model performs, beyond accuracy.


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



<img width="1352" height="502" alt="image" src="https://github.com/user-attachments/assets/1f55be51-f39d-4de4-a31c-0e2b99462cb0" />

XGB out performed the other models with the highest accuracy, AUC and sensitivity. It is the best model for identifying positive diabetes

Logistic regression was the strongest for identifying non-diabetes, but missed many true positive cases. 

Random forest offered a fairly balanced performance, but XGBoost was stronger overall, as shown by the balance AUC, Sensitivity, specificity and accuracy results 




<img width="1422" height="570" alt="image" src="https://github.com/user-attachments/assets/a323ed6e-ecc0-494d-940f-aad80d4d4ad7" />

Since XGBoost was the best-performing model overall, we based our interpretation primarily on its results.
According to the XGBoost feature importance plot, four main predictors stood out:
Glucose – This was by far the most influential. Given that high blood sugar is a defining characteristic of diabetes, this makes perfect clinical sense.
BMI – A high body mass index is strongly associated with insulin resistance, making it a significant risk factor.
Age – As people get older, their risk of developing type 2 diabetes increases. 
Diabetes Pedigree Function – This reflects genetic predisposition or family history, and although less dominant than the top three, it still contributed meaningfully to predictions.
Other variables like Insulin, Pregnancies, and Blood Pressure had very low importance in XGBoost and didn’t significantly influence the model’s decisions.
So, based on our analysis, these four features — Glucose, BMI, Age, and Pedigree Function — contribute the most to predicting diabetes in this dataset




<img width="1354" height="613" alt="image" src="https://github.com/user-attachments/assets/e51c241a-52a9-4966-a59e-f41a3e01812f" />

table shows the model’s predictive performance across age groups. ROC AUC is highest for the 55–80 group at 1.00, slightly lower for 20–35 at (0.89), and lowest for 35–55 at (0.85). 
ROC AUC Parity compares each group to the reference group which is the 20–35 group. For all groups, the parity is close to 1, and the 55–80 group exceeds it at 1.13, which indicates a slight overperformance. 
However, this group has the smallest sample size of 6, which may exaggerate metrics. 
Overall, the model does perform consistently, but we should be cautious for performance variation due to the smaller age group for older adults. 





<img width="1296" height="562" alt="image" src="https://github.com/user-attachments/assets/454dabd9-74b4-46e7-8615-bc88df81b30e" />



analysis shows how well the Random Forest model predicts diabetes across age groups. 
ROC AUC remains strong for 20–35 (0.87) and perfect for 55–81 (1.00), but drops to 0.79 for the 35–55 group. 

ROC AUC Parity is within the acceptable 0.8–1.25 range, though performance is lower for 35–55 (0.91) and relatively high for the smallest group, 55–81 (1.16). 
This indicates that our model's predictive fairness is relatively consistent across all age demographics.
However, the 55–81 group has only 6 samples, so results may not be reliable.
 Overall, the model performs well but could benefit from improving performance for the mid-age group and increasing data for older adults





<img width="1344" height="607" alt="image" src="https://github.com/user-attachments/assets/b19eb657-c79d-4986-af8f-d585fc936b27" />





For model performance, our ROC AUC metrics are strong across all age groups. We see a 0.90 for the youngest group, 0.89 for the middle group, and a perfect 1.0 for the oldest group. As indicated on the right, any score above 0.8 is considered a strong model, between 0.7-0.8 is acceptable, and below 0.7 is weak. Our model performs well for all groups, with the highest accuracy for the 55-80 age group, though this may be influenced by the small sample size.
The ROC AUC Parity metric, which ideally should be between 0.8 and 1.25, shows values of 1.0, 0.93, and 1.11 across our age groups. This indicates that our model's predictive fairness is relatively consistent across all age demographics. As noted in the interpretation column, parity is close to 1 across all age groups, suggesting our model doesn't systematically favor or disadvantage any particular age group.
However, we should interpret the results for the oldest group with caution given the very small sample size of just 6 individuals.







 










