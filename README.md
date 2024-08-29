# Loan_Dataset_Analysis

## Table of Contents
- [Introduction](#introduction)
- [Tools Used](#tools-used)
- [Dataset Description](#dataset-description)
- [Data Dictionary](#data-dictionary)
- [Steps Performed](#steps-performed)
  - [1. Data Cleaning](#data-cleaning)
  - [2. Exploratory Data Analysis (EDA)](#exploratory-data-analysis-eda)
  - [3. Data Analysis](#data-analysis)
- [Results/Findings](#resultsfindings)
- [Recommendations](#recommendations)
- [Limitations](#limitations)

## Introduction
The Loans dataset is designed to identify variables that indicate if a person is likely to default. This analysis aims to help financial institutions identify risky loan applicants and prevent financial losses.

## Tools Used
- **Python**
  - Libraries:
    - Pandas
    - Numpy
    - Seaborn
    - Matplotlib

## Dataset Description
The dataset contains complete loan data for all loans issued between 2007 and 2011.

## Data Dictionary
1. **annual_inc**: The self-reported annual income provided by the borrower during registration.
2. **dti**: Debt-to-Income ratio, calculated using the borrower’s total monthly debt payments on the total debt obligations, excluding mortgage and the requested LC loan, divided by the borrower’s self-reported monthly income.
3. **emp_length**: Employment length in years, ranging from 0 (less than one year) to 10 (ten or more years).
4. **funded_amnt**: The total amount committed to that loan at that point in time.
5. **funded_amnt_inv**: The total amount committed by investors for that loan at that point in time.
6. **grade**: LC assigned loan grade.
7. **id**: A unique LC assigned ID for the loan listing.
8. **installment**: The monthly payment owed by the borrower if the loan originates.
9. **int_rate**: Interest rate on the loan.
10. **last_pymnt_amnt**: Last total payment amount received.
11. **last_pymnt_d**: Last month payment was received.
12. **loan_amnt**: The listed amount of the loan applied for by the borrower. If the credit department reduces the loan amount at any point, it is reflected here.
13. **loan_status**: Current status of the loan.
14. **member_id**: A unique LC assigned ID for the borrower member.
15. **purpose**: A category provided by the borrower for the loan request.
16. **term**: The number of payments on the loan, either 36 or 60 months.
17. **total_acc**: The total number of credit lines currently in the borrower’s credit file.
18. **total_pymnt**: Payments received to date for the total amount funded.
19. **total_pymnt_inv**: Payments received to date for the portion of the total amount funded by investors.
20. **total_rec_int**: Interest received to date.

## Steps Performed

### 1. Data Cleaning
1. **Import the Dataset**  
   - Loaded the dataset and explored its structure.
   
2. **Check Data Types**  
   - Verified the datatype of each column.
   
3. **Convert `int_rate` to Float**  
   - Converted the `int_rate` column from character type to float using a lambda function.

4. **Remove Columns with NaN Values**  
   - Removed columns with complete NaN values across all rows.

5. **Simplify `term` Column**  
   - Used a lambda function to remove the 'months' from the `term` column, leaving only numeric values (e.g., 36, 60).

6. **Filter `emp_length` Column**  
   - Filtered the `emp_length` column to extract numerical values from the string.

### 2. Exploratory Data Analysis (EDA)
7. **Shape of the Dataset**  
   - Listed the number of rows and columns.

8. **Loan Status Value Counts**  
   - Calculated value counts of the `loan_status` column and filtered out the ‘fully paid’ and ‘charged off’ categories.

### 3. Data Analysis
9. **Identify Risky Loan Applicants**  
   - Created a new column, `risky_loan_applicant`, by comparing `loan_amnt` and `funded_amnt`. Set the value to ‘0’ if `loan_amnt` is less than or equal to `funded_amnt`, otherwise ‘1’.

10. **Visualize Loan Status**  
    - Visualized the `loan_status` column against categorical columns `grade`, `term`, and `verification_status` using bar plots. Observations were noted from each graph.

11. **Convert `emp_len` to Categorical**  
    - Converted the `emp_len` column into a categorical column using a user-defined function:
      - `<=1 year`: Fresher
      - `>1 and <=3 years`: Junior
      - `>3 and <=7 years`: Senior
      - `>7 years`: Expert

12. **Sum and Visualize `loan_amnt` by Grade**  
    - Calculated the sum of `loan_amnt` for each grade and displayed the distribution using a pie plot.

## Results/Findings

### 1. Loan Status vs. Grade
- **Observation:** The majority of loans in Grades B and C are "Fully Paid," indicating lower risk. However, a significant portion of "Charged Off" loans is also observed in lower grades, particularly Grades D, E, and F.
  
### 2. Loan Status vs. Term
- **Observation:** Loans with a 36-month term have a higher count of "Fully Paid" status compared to those with a 60-month term, which shows a higher proportion of "Charged Off" loans. This suggests longer loan terms might be riskier.

### 3. Loan Status vs. Verification Status
- **Observation:** Loans with "Not Verified" and "Verified" statuses have a higher number of "Fully Paid" loans. However, the "Not Verified" status also shows a noticeable number of "Charged Off" loans, indicating a potential risk.

### 4. Employment Length (emp_len) Conversion
- **Observation:** By converting employment length into categorical values, it was found that most borrowers fall under the "Senior" and "Expert" categories, which may correlate with higher chances of loan repayment.

### 5. Loan Amount Distribution by Grade
- **Observation:** The pie chart shows that loans in Grade B have the highest sum of `loan_amnt`, followed by Grades C and A. This distribution indicates that most borrowers fall within the mid-range risk categories.

## Recommendations
- **Enhance Credit Evaluation:** Focus on applicants with lower-grade loans (D, E, F) as they show a higher likelihood of defaulting. More stringent credit checks and higher interest rates may be necessary for these categories.
  
- **Consider Term Length:** Given the higher risk associated with 60-month loans, financial institutions should consider offering incentives for shorter-term loans or require additional guarantees for longer-term loans.
  
- **Verification Processes:** Strengthen verification processes for loan applicants, especially those who are "Not Verified," to reduce the likelihood of defaults.
  
- **Focus on Experienced Borrowers:** Loans issued to borrowers categorized as "Senior" or "Expert" (based on employment length) seem less risky, indicating a preference for applicants with stable employment history.

## Limitations
- **Data Timeframe:** The dataset only includes loans issued from 2007 to 2011, which might not fully represent the current economic conditions or lending practices.
  
- **Limited Features:** The analysis only considers a subset of features, and other factors like credit scores, loan purpose, and macroeconomic indicators could provide additional insights into loan performance.
  
- **Self-Reported Data:** Features such as `annual_inc` and `emp_length` are self-reported, which may introduce biases or inaccuracies in the dataset.
  
- **Categorical Simplifications:** The simplification of employment length and loan terms into categorical values may overlook nuances in borrower behavior.

