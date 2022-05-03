# Nelnet Loan Data Analysis Project

## Tools Used

* PgAdmin4
* Psql
* Postgres v14.2
* Tableau

## Loan Volume

### Queries Used

```
SELECT issue_d, COUNT(issue_d) AS loan_vol, ROUND(AVG(int_rate),2) AS avg_int_rate
FROM loan
		GROUP BY issue_d
 		ORDER BY RIGHT (issue_d, 4)

SELECT DISTINCT(issue_d)
FROM loan
WHERE (issue_d LIKE 'Jan%' OR
issue_d LIKE 'Feb%' OR
issue_d LIKE 'Mar%') AND
(issue_d LIKE '%2017')

SELECT ROUND(AVG(int_rate),2)
FROM loan
WHERE (issue_d LIKE 'Jan%' OR
issue_d LIKE 'Feb%' OR
issue_d LIKE 'Mar%') AND
(issue_d LIKE '%2017')

INSERT INTO loan(id, issue_d)
VALUES (#idvalue, #missing_dates);

```
## Loan Grades

### Queries Used

```
SELECT grade, SUM(chargeoff_within_12_mths) AS acct_w_chargeoff, 
settlement_status, COUNT(settlement_status) AS acct_w_settlement,
COUNT(delinq_amnt) AS acct_w_delinq
FROM loan
GROUP BY grade, settlement_status

SELECT grade, loan_status, COUNT(loan_status) AS count_of_loan_status, ((SUM(installment * term) - SUM(funded_amnt)) / COUNT(grade)) AS Avg_Profit_By_Grade
FROM loan
GROUP BY grade, loan_status

SELECT settlement_status, grade, ((SUM(chargeoff_within_12_mths) / COUNT(issue_d)) * 100) AS acct_w_chargeoff
FROM loan
WHERE settlement_status NOT LIKE 'null'
GROUP BY grade, settlement_status

SELECT grade, loan_status, COUNT(loan_status) AS count_of_loan_status
FROM loan
WHERE loan_status LIKE 'Late%' OR
loan_status LIKE 'Charged Off'
GROUP BY grade, loan_status

SELECT grade, ROUND((SUM(installment * term) - SUM(funded_amnt)) / 999999, 2) AS Avg_Profit_By_Grade
FROM loan
WHERE loan_status LIKE 'Fully Paid'
GROUP BY grade

SELECT grade, SUM(loan_amnt) AS tot_approved_loan, SUM(installment * term) AS tot_paid
FROM loan
WHERE loan_status LIKE 'Fully Paid'
GROUP BY grade

SELECT grade, (SUM(installment * term) - SUM(funded_amnt)) AS tot_profit
FROM loan
WHERE loan_status LIKE 'Fully Paid'
GROUP BY grade

```

## Borrower Characteristics

### Queries Used

```
SELECT grade, settlement_status, application_type, home_ownership, emp_length, purpose, delinq_2yrs, earliest_cr_line
FROM loan
GROUP BY grade, settlement_status, application_type, home_ownership, emp_length, purpose, delinq_2yrs, earliest_cr_line

SELECT SUM(chargeoff_within_12_mths), grade, settlement_status, application_type
FROM loan
GROUP BY grade, settlement_status, application_type

SELECT COUNT(disbursement_method),(SUM(installment * term) - SUM(funded_amnt)) AS tot_profit, ((SUM(installment * term) - SUM(funded_amnt)) / 999999) AS avg_profit, disbursement_method
FROM loan
GROUP BY disbursement_method

```
## Graphs
<img width="631" alt="Screen Shot 2022-05-02 at 7 26 08 PM" src="https://user-images.githubusercontent.com/102696081/166346552-793301f9-88f4-4075-87d2-726c07fe7feb.png">

<img width="590" alt="Screen Shot 2022-05-02 at 7 26 16 PM" src="https://user-images.githubusercontent.com/102696081/166346568-05798d46-5fe3-4b07-b078-be3d4b15812d.png">

<img width="702" alt="Screen Shot 2022-05-02 at 7 26 24 PM" src="https://user-images.githubusercontent.com/102696081/166346578-64a93113-2ac1-4960-ab34-54a0621b6a5f.png">

<img width="482" alt="Screen Shot 2022-05-02 at 7 26 31 PM" src="https://user-images.githubusercontent.com/102696081/166346592-1d85c667-510d-4372-9f66-89db5e9d0f4f.png">

<img width="375" alt="Screen Shot 2022-05-02 at 7 26 54 PM" src="https://user-images.githubusercontent.com/102696081/166346596-4e014f5b-23d3-4f7c-b28c-32df4a5f7de8.png">

<img width="634" alt="Screen Shot 2022-05-02 at 7 27 02 PM" src="https://user-images.githubusercontent.com/102696081/166346600-3f3116b8-17bb-4cb2-82ad-d1f433a627c5.png">

<img width="568" alt="Screen Shot 2022-05-02 at 7 27 10 PM" src="https://user-images.githubusercontent.com/102696081/166346604-7eabe746-cd4d-4f93-8046-717ecbec82b0.png">

<img width="568" alt="Screen Shot 2022-05-02 at 7 27 19 PM" src="https://user-images.githubusercontent.com/102696081/166346609-9f710dcb-2f68-4fdf-8eca-949c85844fa5.png">

<img width="233" alt="Screen Shot 2022-05-02 at 7 27 28 PM" src="https://user-images.githubusercontent.com/102696081/166346613-41aa11ab-c615-4c55-8b9a-9a1022662a7b.png">

<img width="239" alt="Screen Shot 2022-05-02 at 7 27 35 PM" src="https://user-images.githubusercontent.com/102696081/166346616-fcef9ab8-211d-48d8-b8b4-c398b9a9bde5.png">

<img width="561" alt="Screen Shot 2022-05-02 at 7 27 43 PM" src="https://user-images.githubusercontent.com/102696081/166346619-5ea667d1-3740-4e82-b673-5e08ae3bd785.png">
