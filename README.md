### Problem statement:

To conduct a thorough exploratory data analysis (EDA) and deep analysis of a comprehensive dataset containing basic customer details and extensive credit-related information. The aim is to create new, informative features, calculate a hypothetical credit score, and uncover meaningful patterns, anomalies, and insights within the data.

### Data Dictionary

| Column Name              | Description                                                         |
| ------------------------ | ------------------------------------------------------------------- |
| ID                       | Represents a unique identification of an entry                      |
| Customer_ID              | Represents a unique identification of a person                      |
| Month                    | Represents the month of the year                                    |
| Name                     | Represents the name of a person                                     |
| Age                      | Represents the age of the person                                    |
| SSN                      | Represents the social security number of a person                   |
| Occupation               | Represents the occupation of the person                             |
| Annual_Income            | Represents the annual income of the person                          |
| Monthly_Inhand_Salary    | Represents the monthly base salary of a person                      |
| Num_Bank_Accounts        | Represents the number of bank accounts a person holds               |
| Num_Credit_Card          | Represents the number of other credit cards held by a person        |
| Interest_Rate            | Represents the interest rate on credit card                         |
| Num_of_Loan              | Represents the number of loans taken from the bank                  |
| Type_of_Loan             | Represents the types of loan taken by a person                      |
| Delay_from_due_date      | Represents the average number of days delayed from the payment date |
| Num_of_Delayed_Payment   | Represents the average number of payments delayed by a person       |
| Changed_Credit_Limit     | Represents the percentage change in credit card limit               |
| Num_Credit_Inquiries     | Represents the number of credit card inquiries                      |
| Credit_Mix               | Represents the classification of the mix of credits                 |
| Outstanding_Debt         | Represents the remaining debt to be paid (in USD)                   |
| Credit_Utilization_Ratio | Represents the utilization ratio of credit card                     |
| Credit_History_Age       | Represents the age of credit history of the person                  |
| Payment_of_Min_Amount    | Represents whether only the minimum amount was paid by the person   |
| Total_EMI_per_month      | Represents the monthly EMI payments (in USD)                        |
| Amount_invested_monthly  | Represents the monthly amount invested by the customer (in USD)     |
| Payment_Behaviour        | Represents the payment behavior of the customer (in USD)            |
| Monthly_Balance          | Represents the monthly balance amount of the customer (in USD)      |
### Insights 
- column to column relationships for age and credit history age is used to find a weak upper bound for credit history age credit utilization Ratio is a percentage cant be lower than 0 Outstanding_Debt,Annual_Income,Monthly_Inhand_Salary cant be negative IQR outlier treatment is done further on these values modified with intercolumn relationships for further treatment
- feature Debt to Income Ratio : shows how much leveraged the borrower is Feature FOIR(Fixed Obligations to Income Ratio): shows how much of monthly in-hand salary borrower is spending as EMI/Monthly payments there are anomalous values of FOIR and EMI in the dataset which require further context, to interpret
- left skewed distribution for annual income and monthly salary more quantity of lower to middle income people present in the dataset
- Credit Utilization ratio is approximately normally distributed, doesn't show skewness while debt to income ratio shows skewness most people are in 0-20 percent of annual income could indicate the these are short term lesser ticket size credits
- Outstanding Debt is higher for Bad Credit Mix Monthly In-hand Salary is lower for Bad Credit Mix shows these segment is highly leveraged
- Higher Debt to Income Ratio is related to delay from due date, shows a Bad Credit Mix indicates more delay in payment
- required values are normalized, using min max scaling since the data was skewed as evident from the visual analysis A credit score is designed to measure your risk as a borrower. the hypothetical credit score calculation incorporates five major components, with varying levels of importance. These categories with their relative weights are: as given below
- Payment history (35%) Amount owed (30%) Length of credit history (15%) New credit (10%) Credit mix (10%) each categories get its own column and is aggregated to get a credit score
- strategy for creating credit score Payment history (35%) - consists of delay from due date, number of delayed payments, whether only critical amount was paid Amount owed (30%) debt to income ratio, credit utilization, no of credit cards Length of credit history (15%) credit history age New credit (10%) number of credit inquiry, changed credit limit, FOIR Credit mix (10%) already credit mix is present
- Payment History(35%): our calculation includes delay from due date, as delay increases score should decrease, sub weightage of 40 % is given for days of delay, 40 % for number of dealyed payments, 20 % for whether minimum amount is paid Amount Owed(30%): borrowers debt to income ratio shows how leveraged the borrower is with current debt, similarly credit utilization ratio shows how much of credit limit borrower has used, more usage is not good. increasing number of credit cards and loans are also negatively affecting the score Length of credit history (15%): credit history age is standardized for this feature, more age implies less risk New Credit(10%): number of new loan enquires reduces the score since it represent financial instability Credit mix(10%): feature already present in data set.
- minimum score is 300 maximum score is 900 distribution clearly shows 3 peaks, on further analysis it shows that credit score shows there are 3 credit mixes in the data, and the scores are proportional to credit mixes with bad getting the lowest score and good getting the highest score this shows the scores are aggregating features to represent the potential creditworthiness of the applicant/customer
