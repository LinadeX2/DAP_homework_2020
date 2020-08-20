# DAP_homework_2020
Solution for Data Analysis Platforms homework 2020.


# Description of the problem 
The full description is available here in hungarian: https://www.kaggle.com/c/dmlab-dap2020/overview. 

Given a dataset of 50000 entries the task is to predict the probability of loan repayment problem of the clients. Half of the data is labeled, the prediction has to be done in the other half. For the evaluation of the solution the ROC curve and the AUC value are used. 


# Solution
My solution consists of three steps: data preparation, feature selection and prediction. 

## 1 Data preparation
The dataset contains a lot of information about the clients that should be treated with caution for reliable results. During the prepocessing two major actions were done.

### Treating missing data
In case of categorical variables the "missing data" category was introduced. For numerical variables the median was taken considering only the corresponding age group. 

### Encoding Categorical Data 
One hot Encoding and Dummy Encoding technics were implemented to convert categorical data to numerical depending on the properties of the arguments. 

### Treating outliers
For features with high variance ('NUMBER_OF_DEPENDANTS', 'M_IN_THE_JOB', 'MONTHS_IN_RES') a maximal value was set and all originally higher occurances were limited to this maximum. The maximal has been chosen empirically. 

### Introducing new attributes
The following attributes were introduced:
* age ranges with 3 divisons
* decimal logarithm of money type variables (P_MONTHLY_INCOME, O_INCOMES, P_ASSETS_VALUE, L_BALANCE)
* average income according to the corresponding age range
* deviation from the average income
* all income per head in the houshold
* statistical features (min, max, average, variance, sum) of pay and bill type variables 

### 2 Feature selection

### 3 Prediction
