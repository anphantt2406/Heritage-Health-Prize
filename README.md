# Heritage-Health-Prize-REPORT
This project is part of VEF Academy Machine Learning Course of Winter 2020 and all done by Phan Thi Thuy An
## Introduction
Heritage Health Prize (HHP) is a Kaggle challenge held in 2012. HHP challenge purpose is predicting days a patient will spend in the hospital in the next year base on claims data of the year before. Once known, health care providers can develop new care plans and strategies to reach patients before emergencies occur, thereby reducing the number of unnecessary hospitalizations. Read more information at https://www.kaggle.com/c/hhp.
## The Datasets
In this project, dataset is used from \textbf{HHP dataset release 3}, can be downloaded at https://foreverdata.org/1015/index.html.
The dataset using include:
1. Members.csv
2. Claims.csv
3. DrugCount.csv
4. LabCount.csv
5. DaysInHospital_Y2.csv
6. DaysInHospital_Y3.csv
## Data Processing
### Members table
Members information have 2 feature columns:
Sex with Male, Female and Null value. All will be One-Hot encoded for each MemberID.
Age at first claim with categories value type from '0-9' age range to '69-79' age and '80+' age. These values will be converted to integer mean average, for example, '10-19' will be replaced with 15.
### Claims table
Claims processing step will only use Y1 data for training and Y2 for testing. Each will convert features from claims level to member level following rules:

ID data like Provider, Vendor and PCP will only sum the unique ID values of each MemberID.
Numeric data like PayDelay will convert to integer and sum for each MemberID.
Other Categorical data will One-Hot with value_counts based on MemberID.

- ProviderID: 	Count values of Provider to find number of Claims, Count distinct value for unique MemberID.
- PayDelay: Sum the values for each unique MemberID.
- LengthOfStay: Replace string (1 day, 2 day, …) by specific numbers, then Sum the values for each unique MemberID.
- Specialty, PlaceSvc, DSFS, PrimaryConditionGroup, CharlsonIndex, ProcedureGroup: Onehot-Encoding, Count values for unique MemberID.
### DrugCount and LabCount table
DrugCount is count of unique prescription drugs filled and top-coded at 7
LabCount is count of unique laboratory and pathology tests and top-coded at 10
Both are numeric data and will be converted to integer and sum for each MemberID in each Year.
### Features Selection 
After calculating correlation matrix, we keep 27 features which have correlation with target > 0.1 and with others (excluding MemberID, Target, Class) < 0.9.
### Dropped data
We dropped patients having extreme values on PayDelay: [PayDelay = 162+], patients who tended to have more DrugCount, LabCount: [DrugCount = 7+]; [LabCount = 10+].
## Predictive Models
The four major models assessed were:
• Linear Regression - use available package of Scikit-learn.
• Stochastic Regression - use default hyperparameters of Scikit-learn. Here, we also use Lasso Regression model.
• Neural Network - use default hyperparameters, random hyperparameters, grid search to find the best hyperparameters.
• XGBoost - use ensemble Gradient Boosting Regressor of Scikit-learn and Gradient Boost Linear Regression Function.
We run these models on different versions of the dataset with/without features selection. Therefore, we have 6 files of predictive models in total:
- Model for full data of each year.
- Model for full data of each year applied Features Selection.
- Model for dropped data of each year.
- Model for dropped data of each year applied Features Selection.
- Model for full data of 2 years.
- Model for full data of 2 years applied Features Selection.
## Result
