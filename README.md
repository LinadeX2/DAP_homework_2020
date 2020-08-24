# DAP_homework_2020
Solution for Data Analysis Platforms homework 2020.


# Description of the problem 
The full description is available here in Hungarian: https://www.kaggle.com/c/dmlab-dap2020/overview. 

Given a dataset of 50000 entries and 67 columns the task is to predict the probability of loan repayment problem of the clients. Half of the data is labelled, the prediction has to be done in the other half. For the evaluation of the solution the ROC curve and the AUC value are used. 


# Solution
My solution consists of three steps: data preparation, feature selection and prediction. 

## 1 Data preparation
**DAP_HF_data_preparation.ipynb**

The dataset contains a lot of information about the clients that should be treated with caution for reliable results. During the prepocessing the following actions were taken.

### Treating missing data
In case of categorical variables, the "missing data" category was introduced. For numerical variables the median was taken considering only the corresponding age group. 

### Encoding Categorical Data 
*One hot Encoding* and *Dummy Encoding* technics were implemented to convert categorical data to numerical depending on the properties of the arguments. 

### Treating outliers
For features with high variance ('NUMBER_OF_DEPENDANTS', 'M_IN_THE_JOB', 'MONTHS_IN_RES') a maximal value was set and all originally higher occurences were limited to this maximum. The maximal has been chosen empirically. 

### Introducing new attributes
The following attributes were introduced:
* age ranges with 3 divisions
* decimal logarithm of money type variables (P_MONTHLY_INCOME, O_INCOMES, P_ASSETS_VALUE, L_BALANCE)
* average income according to the corresponding age range
* deviation from the average income
* all income per head in the household
* statistical features (min, max, average, variance, sum) of pay and bill type variables 

With all these modifications I got a dataset with 99 columns that can be found in *prep_df.csv*.

### 2 Feature selection
**DAP_HF_feature_selection.ipynb**

For feature selection I used the tutorial from https://stackabuse.com/applying-filter-methods-in-python-for-feature-selection/.

I excluded constant, quasi-constant features. Then duplicates and correlated features (more than 0.95) were also removed. Because of the dummy encoding not all of the filtered features were neglected. This way, 79 columns were kept for predictive modelling. The data can be found in *selected_df.csv*.  

### 3 Prediction
**DAP_HF_prediction.ipynb**

I built three models for the prediction: an XGBoost, a Random Forest and a Gradient Boosting Classifier. For each model the parameters were optimised to the *myxval* function. This part is not included in the notebook. Then, the product and the average of the prediction probabilities were taken and the three best results were submitted to the Kaggle challenge.  

I got the following scores. 

| Submission | Private Score | Public Score |
| --- | --- | --- |
| Sub4.csv | 0.79939 | 0.79223 |
| Sub2.csv | 0.80294 | 0.79636 |
| Sub1.csv | 0.80263 | 0.79606 |
