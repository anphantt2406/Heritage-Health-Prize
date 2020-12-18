# Heritage-Health-Prize-REPORT
This project is part of VEF Academy Machine Learning Course of Winter 2020 and all done by Phan Thi Thuy An
## Introduction
Heritage Health Prize (HHP) is a Kaggle challenge held in 2012. HHP challenge purpose is predicting days a patient will spend in the hospital in the next year base on claims data of the year before. Once known, health care providers can develop new care plans and strategies to reach patients before emergencies occur, thereby reducing the number of unnecessary hospitalizations. Read more information at \url{https://www.kaggle.com/c/hhp}.
## The Datasets
In this project, dataset is used from \textbf{HHP dataset release 3}, can be downloaded at \url{https://foreverdata.org/1015/index.html}.
The dataset using include:
1. Members.csv
2. Claims.csv
3. DrugCount.csv
4. LabCount.csv
5. DaysInHospital_Y2.csv
6. DaysInHospital_Y3.csv
## Data Processing
### Members Information
Members information have 2 feature columns:
Sex with Male, Female and Null value. All will be binary One-Hot coded for each MemberID.
Age at first claim with categories value type from '0-9' age range to '69-79' age and '80+' age. These values will be converted to integer mean average, for example, '10-19' will be replaced with 15.
### Claims Information
Claims table is claims level information with features:
MemberID: Patient ID
ProviderID: Claims provider ID
Vendor: Claims vendor ID
PCP: Claims PCP ID
Year: Y1, Y2 or Y3
Specialty: Categorical data of Specialty
PlaceSvc: Categorical data of service place
PayDelay: Number in range 0-161 with 95% percentile top-coded as string "162+"
LengthOfSay: Categorical data of day length up to 6 days and weeks length range up to 8 weeks. If above that length, Suppression is applied and value at SupLOS column is 1, else 0
DSFS: Categorical data of number of month, range from 1 to 12.
PrimaryConditionGroup: Categorical data of diagnostic
CharlsonIndex: Categorical data of CharlsonIndex
ProcedureGroup: Categorical data of procedures
SupLOS: 0 and 1 for none suppression and suppressed in Length of Stay values, respectively.
This processing step will only use Y1 data for training and Y2 for testing. Each will convert features from claims level to member level following rules:

ID data like Provider, Vendor and PCP will only sum the unique ID values of each MemberID.
Numeric data like PayDelay will convert to integer and sum for each MemberID.
Other Categorical data will One-Hot with value_counts based on MemberID.
Each feature will be converted and save to separated csv file.

Count Unique ID: Provider

One-Hot with value_counts for categorical features.
Specialty
PlaceSvc
PrimaryConditionGroup
CharlsonIndex
ProcedureGroup
DSFS
LengthOfStay with SupLOS
Summing values with

PayDelay
Number of member's claims
4.1.3. DrugCount and LabCount Information
DrugCount is count of unique prescription drugs filled and top-coded at 7
LabCount is count of unique laboratory and pathology tests and top-coded at 10
Both are numeric data and will be converted to integer and sum for each MemberID in each Year.
## Predictive Models
We run these models on different versions of the dataset with/without features selection. Therefore, we have 6 files of predictive models in total. 
## Result
