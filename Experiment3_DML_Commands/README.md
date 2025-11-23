# Experiment 3: DML Commands

## AIM
To study and implement DML (Data Manipulation Language) commands.

## THEORY

### 1. INSERT INTO
Used to add records into a relation.
These are three type of INSERT INTO queries which are as
A)Inserting a single record
**Syntax (Single Row):**
```sql
INSERT INTO table_name (field_1, field_2, ...) VALUES (value_1, value_2, ...);
```
**Syntax (Multiple Rows):**
```sql
INSERT INTO table_name (field_1, field_2, ...) VALUES
(value_1, value_2, ...),
(value_3, value_4, ...);
```
**Syntax (Insert from another table):**
```sql
INSERT INTO table_name SELECT * FROM other_table WHERE condition;
```
### 2. UPDATE
Used to modify records in a relation.
Syntax:
```sql
UPDATE table_name SET column1 = value1, column2 = value2 WHERE condition;
```
### 3. DELETE
Used to delete records from a relation.
**Syntax (All rows):**
```sql
DELETE FROM table_name;
```
**Syntax (Specific condition):**
```sql
DELETE FROM table_name WHERE condition;
```
### 4. SELECT
Used to retrieve records from a table.
**Syntax:**
```sql
SELECT column1, column2 FROM table_name WHERE condition;
```
**Question 1**
--
Write a SQL statement to Increase quantity of all products by 10% to adjust for surplus stock counted

Products table

---------------
product_id
product_name
category
cost_price
sell_price
reorder_lvl
quantity
supplier_id

```sql
UPDATE products set quantity=quantity*1.10
```

**Output:**

<img width="1233" height="633" alt="image" src="https://github.com/user-attachments/assets/4406ae7e-fa8a-457f-a954-f6983df88c50" />


**Question 2**
---
Write a SQL statement to Increase the selling price per unit by 5% for product ID 15 who's sale is on '2023-01-31'.

sales(sale_id,sale_date,product_id,quantity,sell_price,total_sell_price)

For example:

Test	Result
select changes();
changes()
----------
3


```sql
UPDATE sales 
SET sell_price=sell_price*1.05 
where product_id=15 
AND sale_date='2023-01-31';
```

**Output:**
<img width="1232" height="467" alt="image" src="https://github.com/user-attachments/assets/b81d01dd-7084-49d2-89df-b2e406e9e0cb" />


**Question 3**
---
Write a SQL statement to update the product_name as 'Grapefruit' whose product_id is 4 in the products table.

products table

---------------
product_id
product_name
category_id
availability

```sql
UPDATE products
SET product_name= 'Grapefruit'
WHERE product_id=4;
```

**Output:**
<img width="1246" height="256" alt="image" src="https://github.com/user-attachments/assets/30aad104-331b-4220-a9f7-0874bc35b0ed" />


**Question 4**
---
Write a SQL statement to Update the grade of all customers in Chennai city as  5. 

Customer table (customer_id,cust_name,city,grade,salesman_id)

```sql
UPDATE Customer 
SET grade=5
WHERE city='Chennai';
```

**Output:**
<img width="1231" height="484" alt="image" src="https://github.com/user-attachments/assets/7558b11d-84c1-45c5-90fc-8ac3d6d80c83" />


**Question 5**
---
Write a SQL query to delete a doctor from Doctors table whos specialization is 'Cardiology'

Sample table: Doctors

attributes : doctor_id, first_name, last_name, specialization

```sql
DELETE FROM DOCTORS
WHERE specialization='Cardiology';
```

**Output:**

<img width="1223" height="389" alt="image" src="https://github.com/user-attachments/assets/0366bfe9-4b4c-4342-8f9b-d4702b16328e" />


**Question 6**
---
 Write a SQL query to Delete customers from 'customer' table where 'CUST_NAME' has exactly 6 characters.

Sample table: Customer

+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+  
|CUST_CODE  | CUST_NAME   | CUST_CITY   | WORKING_AREA | CUST_COUNTRY | GRADE | OPENING_AMT | RECEIVE_AMT | PAYMENT_AMT |OUTSTANDING_AMT| PHONE_NO     | AGENT_CODE |
+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+
| C00013    | Holmes      | London      | London       | UK           |     2 |     6000.00 |     5000.00 |     7000.00 |       4000.00 | BBBBBBB      | A003       |
| C00001    | Micheal     | New York    | New York     | USA          |     2 |     3000.00 |     5000.00 |     2000.00 |       6000.00 | CCCCCCC      | A008       |
| C00020    | Albert      | New York    | New York     | USA          |     3 |     5000.00 |     7000.00 |     6000.00 |       6000.00 | BBBBSBB      | A008       |

```sql
-- DELETE FROM Customer
WHERE LENGTH(CUST_NAME)=6;
```

**Output:**

<img width="1241" height="742" alt="image" src="https://github.com/user-attachments/assets/6cd73ae0-be7e-474d-af84-b0b0957efb02" />


**Question 7**
---
Write a SQL query to Delete customers with 'GRADE' 3 and whose 'CUST_NAME' contains the substring 'BBB', and 'PAYMENT_AMT' is greater than 2000

Sample table: Customer

+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+  
|CUST_CODE  | CUST_NAME   | CUST_CITY   | WORKING_AREA | CUST_COUNTRY | GRADE | OPENING_AMT | RECEIVE_AMT | PAYMENT_AMT |OUTSTANDING_AMT| PHONE_NO     | AGENT_CODE |
+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+
| C00013    | Holmes      | London      | London       | UK           |     2 |     6000.00 |     5000.00 |     7000.00 |       4000.00 | BBBBBBB      | A003       |
| C00001    | Micheal     | New York    | New York     | USA          |     2 |     3000.00 |     5000.00 |     2000.00 |       6000.00 | CCCCCCC      | A008       |
| C00020    | Albert      | New York    | New York     | USA          |     3 |     5000.00 |     7000.00 |     6000.00 |       6000.00 | BBBBSBB      | A008       |
For example:

Test	Result
select changes();
changes()
----------
0


```sql
DELETE FROM CUSTOMER
WHERE GRADE=3
AND CUST_NAME LIKE '%BBB%'
AND PAYMENT_AMT>2000;
```

**Output:**

<img width="1211" height="493" alt="image" src="https://github.com/user-attachments/assets/182930ef-8b3e-4d6f-b635-0da499ea0093" />


**Question 8**
---
Write a SQL query to Delete customers with 'GRADE' 2 and 'CUST_NAME' starting with 'M', and whose 'PAYMENT_AMT' is less than 3000

Sample table: Customer

+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+  
|CUST_CODE  | CUST_NAME   | CUST_CITY   | WORKING_AREA | CUST_COUNTRY | GRADE | OPENING_AMT | RECEIVE_AMT | PAYMENT_AMT |OUTSTANDING_AMT| PHONE_NO     | AGENT_CODE |
+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+
| C00013    | Holmes      | London      | London       | UK           |     2 |     6000.00 |     5000.00 |     7000.00 |       4000.00 | BBBBBBB      | A003       |
| C00001    | Micheal     | New York    | New York     | USA          |     2 |     3000.00 |     5000.00 |     2000.00 |       6000.00 | CCCCCCC      | A008       |
| C00020    | Albert      | New York    | New York     | USA          |     3 |     5000.00 |     7000.00 |     6000.00 |       6000.00 | BBBBSBB      | A008       |
For example:

Test	Result
select changes();
changes()
----------
1


```sql
DELETE FROM CUSTOMER
WHERE GRADE=2
AND CUST_NAME LIKE 'M%'
AND PAYMENT_AMT<3000;
```

**Output:**

<img width="1225" height="420" alt="image" src="https://github.com/user-attachments/assets/ebcc0eb3-4c34-4d09-a8a1-5067fa4e5414" />


**Question 9**
---
 Write a SQL query to delete a doctor from Doctors table whose Specialization is 'Pediatrics' and First name is 'Michael'.

Sample table: Doctors

attributes : doctor_id, first_name, last_name, specialization

```sql
DELETE FROM DOCTORS
WHERE SPECIALIZATION ='Pediatrics'
AND First_name='Michael';
```

**Output:**
<img width="1220" height="396" alt="image" src="https://github.com/user-attachments/assets/e57ed40b-cb66-4446-ab4b-c2349666b531" />


**Question 10**
---
Write a query to fetch details of all employees excluding the employees with first names, “Sanjay” and “Sonia” from the EmployeeInfo table.
EmpID

EmpFname

EmpLname

Department

Project

Address

DOB

Gender

1

Sanjay

Mehra

HR

P1

Hyderabad(HYD)

01/12/1976

M

2

Ananya

Mishra

Admin

P2

Delhi(DEL)

02/05/1968

F
For example:

Result
EmpID       EmpFname    EmpLname    Department  Project     Address     DOB         Gender
----------  ----------  ----------  ----------  ----------  ----------  ----------  ----------
2           Ananya      Mishra      Admin       P2          Delhi(DEL)  1968-05-02  F
3           Rohan       Diwan       Account     P3          Mumbai(BOM  1980-01-01  M
5           Ankit       Kapoor      Admin       P2          Delhi(DEL)  1994-07-03  M


```sql
SELECT 
EmpID,
EmpFname,
EmpLname,
Department,
Project,
Address,
DOB,
Gender
FROM EmployeeInfo
WHERE EmpFname NOT IN('Sanjay','Sonia');
```

**Output:**

<img width="1230" height="297" alt="image" src="https://github.com/user-attachments/assets/253ecee7-facb-49b1-ad78-1da528fdc08e" />


## RESULT
Thus, the SQL queries to implement DML commands have been executed successfully.
