# Predict-Credit-Risk

In this project we build a model that can predict credit risk using a dataset provided by the company which consists of data on received and rejected loans.

## Dataset
Contains 75 columns and 466.285 rows.
The dataset is obtained from company customer data in 2011 - 2016 and data contains customers who have various backgrounds and conditions

- 17 columns with 100% null-values;
- 15 columns with missing values; 

## Exploratory Data Analysis (EDA)

1. Number of Applicants by Loan Status

> The company's performance has been quite good, where most of the borrowers have fully paid status and are ongoing (current). But the number of borrowers who experienced obstacles in the lending process was also quite a lot.

2. Loan Status by Term

> More people take shorter terms, but also the number of debtors who are categorized as bad is also greater in this term.

3. Loan Status by Home Ownership

> Most applicants have an existing mortgage or are currently renting a home.

> Applicants who have an existing mortgage or are currently renting a home have a higher probability of bad loan.

4. Loan Status by Purpose

> People who are categorized as bad borrowers mostly borrow with a purpose 'Debt Consolidation'. In the second position - 'Credit Card'.

> In the future, it is better to reject application that have 'Debt Consolidation' and 'Credit Card' purposes.

5. Loan Status by Grade

> The highest number of borrowers are those with grade B, but for the number of borrowers who are categorized as bad, more have grade C.

> The percentage of each group is the percentage of the number of applicants in a particular status compared to the total number of applicants for each grade.

> From Grade A to G, the percentage of borrowers who are categorized as good gets smaller, while the percentage of borrowers who are categorized as bad gets bigger.

## Modeling
### Data Preprocessing

- Data Type Adjustment: Change to datetime type that contains the date and calculate the days to May 1, 2017. Adjust 'term' and 'emp_lenght' columns to integer.
- Define the Target Column: Column 'loan_status' as target column, categorizes its values to 1 and 0. 1 - Good Debtur/Borrower, 0 - Bad  Debtur/Borrower.
- There are no duplicate data and no outliers.
- Feature Selection: delete features with unique id, text only, only 1 unique values and irrelevant / too much variation in values and drop columns with a lot of missing values and make imputation on some columns
- Feature Selection using WoE and IV - use Weight of Evidence (WoE) and Information Value (IV) to eliminate some features that have no effect on the target.
- Feature Transformation and Encoding - standardization to numerical features and One-Hot Encoding to categorical features.
- Class Imbalance -> oversample.

### Machine Learning

Used multiple machine learning to find the machine learning with the best performance.
Machine Learning used:     
- GaussianNB()
- KNeighborsClassifier()
- LogisticRegression()
- DecisionTreeClassifier()
- XGBClassifier()
- RandomForestClassifier()
- GradientBoostingClassifier()
- AdaBoostClassifier()
- LGBMClassifier()

> In this case, AUC score is the important metrics. AUC sroce LGBM in the highest score.

Confussion Matrix with LGBM


### Feature Importance

Top 5 important features that affect borrowers completing their loan:
- int_rate - the interest rate on the loan;
- revol_util - revolving line utilization rate, or the amount of credit the borrower is using relative to all available revolving credit;
- inq_last_6mths - the number of inquiries by creditors during the past 6 months;
- total_rec_late_fee - late fees received to date;
- initial_list_status_f - initial listing status of the loan (F - fractional).

> For evaluation, run machine learning again with only top 10 feature importance. The results are not much different, it can be said that the modeling is good enough

## Business Recommendation

1. Insure credit that has the potential to default (only for low-risk, reject high-risk applicants).
2. Collaborating with e-commerce to offer credit payments for loyal customers who have never experienced payment issues (with a lower tenor/term).
3. Provide a discount for the next credit application if the customer previously completed the credit without experiencing delays.


