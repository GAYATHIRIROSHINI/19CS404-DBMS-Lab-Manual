# Experiment 4: Aggregate Functions, Group By and Having Clause

## AIM
To study and implement aggregate functions, GROUP BY, and HAVING clause with suitable examples.

## THEORY

### Aggregate Functions
These perform calculations on a set of values and return a single value.

- **MIN()** – Smallest value  
- **MAX()** – Largest value  
- **COUNT()** – Number of rows  
- **SUM()** – Total of values  
- **AVG()** – Average of values

**Syntax:**
```sql
SELECT AGG_FUNC(column_name) FROM table_name WHERE condition;
```
### GROUP BY
Groups records with the same values in specified columns.
**Syntax:**
```sql
SELECT column_name, AGG_FUNC(column_name)
FROM table_name
GROUP BY column_name;
```
### HAVING
Filters the grouped records based on aggregate conditions.
**Syntax:**
```sql
SELECT column_name, AGG_FUNC(column_name)
FROM table_name
GROUP BY column_name
HAVING condition;
```

**Question 1**
How many medical records were created in each month?
Sample table:MedicalRecords Table
For example:
Result
Month       TotalRecords
----------  ------------
2023-12     2
2024-01     6
2024-02     2


```sql
Select strftime('%Y-%m',date) as Month,count(*) as TotalRecords
from MedicalRecords group by strftime('%Y-%m',date);
```

**Output:**

<img width="795" height="450" alt="image" src="https://github.com/user-attachments/assets/402ef7a2-774d-4806-87cc-b86af1a206fe" />


**Question 2**
---
How many patients have expired insurance coverage for each insurance company?
Sample table:Insurance Table
For example:
Result
InsuranceCompany  TotalExpiredPatients
----------------  --------------------
ABC Insurance     1
DEF Insurance     1
GHI Insurance     1
JKL Insurance     1
MNO Insurance     1
PQR Insurance     1
STU Insurance     1
VWX Insurance     1
XYZ Insurance     1
YZA Insurance     1


```sql
select InsuranceCompany, count(*) as TotalExpiredPatients
from Insurance group by InsuranceCompany;
```

**Output:**

<img width="931" height="751" alt="image" src="https://github.com/user-attachments/assets/722038dd-872f-4514-87aa-d23f7cf074c5" />


**Question 3**
---
What is the count of male and female patients?
Sample table: Patients Table
For example:
Result
Gender      TotalPatients
----------  -------------
Female      5
Male        5


```
SELECT gender,
count(*) as TotalPatients
FROM Patients
GROUP BY gender;
```

**Output:**

<img width="782" height="385" alt="image" src="https://github.com/user-attachments/assets/ee5503ac-780e-4fde-b200-7880167e5ce5" />

**Question 4**
---
Write a SQL query to Calculate the average income of the employees with names starting with 'A': 

Table: employee

name        type
----------  ----------
id          INTEGER
name        TEXT
age         INTEGER
city        TEXT
income      INTEGER
For example:

Result
avg_income
----------
5000000.0


```sql
SELECT 
AVG(income) AS avg_income
FROM employee
WHERE name LIKE 'A%';
```

**Output:**

<img width="497" height="314" alt="image" src="https://github.com/user-attachments/assets/31c9d8f8-9c7d-4545-ac09-ea7190eeaa8a" />


**Question 5**
---
Write a SQL query to find the total number of unique cities in the customer table?

Table: customer

name        type
----------  ----------
id          INTEGER
name        TEXT
city        TEXT
email       TEXT
phone       INTEGER
For example:

Result
unique_cities
-------------
10


```sql
SELECT COUNT(DISTINCT city) AS unique_cities
FROM customer;
```

**Output:**

<img width="599" height="320" alt="image" src="https://github.com/user-attachments/assets/7ad50723-545a-4e00-bfb9-09e838c92f93" />


**Question 6**
---
Write a SQL query to find the average length of names for people living in Chennai?

Table: customer

name        type
----------  ----------
id          INTEGER
name        TEXT   
city        TEXT
email       TEXT
phone       INTEGER
For example:

Result
avg_name_length
---------------
10.0


```sql
SELECT AVG(LENGTH(name)) AS avg_name_length
FROM customer
WHERE city='Chennai';
```

**Output:**

<img width="519" height="316" alt="image" src="https://github.com/user-attachments/assets/c1ce8015-7a9f-4999-91f6-9db19cc7c18b" />


**Question 7**
---
Write a SQL query to find Who has the highest income among employee living in California?

Table: employee

name        type
----------  ----------
id          INTEGER
name        TEXT
age         INTEGER
city        TEXT
income      INTEGER
For example:

Result
name        max(income)
----------  -----------
Adam        5000000


```sql
SELECT name,max(income)
FROM employee
WHERE city='California'
ORDER BY max(income) DESC
LIMIT 1;
```

**Output:**

<img width="693" height="312" alt="image" src="https://github.com/user-attachments/assets/1886f9d3-4d7f-44bb-9e60-63abe948bc15" />


**Question 8**
---
Write the SQL query that achieves the grouping of data by age intervals using the expression (age/5)5, calculates the average age for each group, and excludes groups where the average age is not less than 24.
Sample table: customer1
For example:
Result
age_group   AVG(age)
----------  ----------
20          23.0


```sql
SELECT (age/5)*5 AS age_group,AVG(age)
FROM customer1
GROUP BY (age/5)*5
HAVING AVG(age)<24;
```

**Output:**

<img width="634" height="313" alt="image" src="https://github.com/user-attachments/assets/7f7188f0-92bf-4a37-83e5-a6b3a7e6f75d" />


**Question 9**
---
Write the SQL query that performs grouping by age groups and displays the maximum salary for each group, excluding groups where the maximum salary is not greater than 8000. 

Note: Calculate the age group as multiples of 5.

Eg., 20,22,23 comes in age group 20. 

25,27,29 comes in age group 25.

Sample table: customer1



For example:

Result
age_group   MAX(salary)
----------  -----------
20          10000
25          8500


```sql
SELECT (age/5)*5 AS age_group,MAX(salary) 
FROM customer1
GROUP BY (age/5)*5
HAVING MAX(salary)>8000;
```

**Output:**

<img width="720" height="361" alt="image" src="https://github.com/user-attachments/assets/a618387a-f7c6-44eb-a2f6-d698839380be" />


**Question 10**
---
Write the SQL query that accomplishes the grouping of data by age intervals using the expression (age/5)5, calculates the minimum age for each group, and excludes groups where the minimum age is not less than 25.
Sample table: customer1
For example:
Result
age_group   MIN(age)
----------  ----------
20          22


```sql
SELECT (age/5)*5 AS age_group,MIN(age) 
FROM customer1
GROUP BY (age/5)*5
HAVING MIN(age)<25;
```

**Output:**
<img width="784" height="318" alt="image" src="https://github.com/user-attachments/assets/c7a57af6-fc88-4645-96f9-c3717db5c074" />



## RESULT
Thus, the SQL queries to implement aggregate functions, GROUP BY, and HAVING clause have been executed successfully.
