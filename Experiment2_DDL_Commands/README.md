# Experiment 2: DDL Commands

## AIM
To study and implement DDL commands and different types of constraints.

## THEORY

### 1. CREATE
Used to create a new relation (table).

**Syntax:**
```sql
CREATE TABLE (
  field_1 data_type(size),
  field_2 data_type(size),
  ...
);
```
### 2. ALTER
Used to add, modify, drop, or rename fields in an existing relation.
(a) ADD
```sql
ALTER TABLE std ADD (Address CHAR(10));
```
(b) MODIFY
```sql
ALTER TABLE relation_name MODIFY (field_1 new_data_type(size));
```
(c) DROP
```sql
ALTER TABLE relation_name DROP COLUMN field_name;
```
(d) RENAME
```sql
ALTER TABLE relation_name RENAME COLUMN old_field_name TO new_field_name;
```
### 3. DROP TABLE
Used to permanently delete the structure and data of a table.
```sql
DROP TABLE relation_name;
```
### 4. RENAME
Used to rename an existing database object.
```sql
RENAME TABLE old_relation_name TO new_relation_name;
```
### CONSTRAINTS
Constraints are used to specify rules for the data in a table. If there is any violation between the constraint and the data action, the action is aborted by the constraint. It can be specified when the table is created (using CREATE TABLE) or after it is created (using ALTER TABLE).
### 1. NOT NULL
When a column is defined as NOT NULL, it becomes mandatory to enter a value in that column.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) NOT NULL
);
```
### 2. UNIQUE
Ensures that values in a column are unique.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) UNIQUE
);
```
### 3. CHECK
Specifies a condition that each row must satisfy.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) CHECK (logical_expression)
);
```
### 4. PRIMARY KEY
Used to uniquely identify each record in a table.
Properties:
Must contain unique values.
Cannot be null.
Should contain minimal fields.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) PRIMARY KEY
);
```
### 5. FOREIGN KEY
Used to reference the primary key of another table.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size),
  FOREIGN KEY (column_name) REFERENCES other_table(column)
);
```
### 6. DEFAULT
Used to insert a default value into a column if no value is specified.

Syntax:
```sql
CREATE TABLE Table_Name (
  col_name1 data_type,
  col_name2 data_type,
  col_name3 data_type DEFAULT 'default_value'
);
```

**Question 1**
--
Insert all employees from Former_employees into Employee

Table attributes are EmployeeID, Name, Department, Salary

For example:

Test	Result
select * from Employee;
EmployeeID  Name        Department  Salary
----------  ----------  ----------  ----------
201         John Doe    HR          50000
202         Jane Smith  Engineerin  75000
203         Emily Davi  Marketing   60000


```sql
INSERT into Employee(EmployeeID, Name, Department, Salary)
SELECT EmployeeID, Name, Department, Salary from Former_employees
```

**Output:**
<img width="1227" height="362" alt="image" src="https://github.com/user-attachments/assets/da0c56ad-5f56-48c7-a78c-e2661c16ecce" />



**Question 2**
---
Create a table named Bonuses with the following constraints:
BonusID as INTEGER should be the primary key.
EmployeeID as INTEGER should be a foreign key referencing Employees(EmployeeID).
BonusAmount as REAL should be greater than 0.
BonusDate as DATE.
Reason as TEXT should not be NULL.
For example:

Test	Result
INSERT INTO Bonuses (BonusID, EmployeeID, BonusAmount, BonusDate, Reason) VALUES (1, 6, 1000.0, '2024-08-01', 'Outstanding performance');
SELECT * FROM Bonuses;

```sql
CREATE table Bonuses(
BonusID INTEGER primary key,
EmployeeID INTEGER,
BonusAmount REAL CHECK(BonusAmount>0),
BonusDate DATE,
Reason TEXT NOT NULL,
FOREIGN KEY(EmployeeID) REFERENCES Employees(EmployeeID) 
);
```

**Output:**
<img width="1226" height="407" alt="Screenshot 2025-10-17 103047" src="https://github.com/user-attachments/assets/55792b65-3ad1-4e38-8dd7-6df183195e91" />



**Question 3**
---
Insert a product with ProductID 104, Name Tablet, and Category Electronics into the Products table, where Price and Stock should use default values.

For example:

Test	Result
SELECT ProductID, Name, Category, Price, Stock 
FROM Products 
WHERE ProductID = 104;
ProductID   Name        Category     Price       Stock
----------  ----------  -----------  ----------  ----------
104         Tablet      Electronics  100         50


```sql
INSERT INTO Products(ProductID, Name,Category)
VALUES (104,"Tablet","Electronics");
```

**Output:**

<img width="1226" height="331" alt="image" src="https://github.com/user-attachments/assets/f77abd3e-6671-4ff0-92e8-d86eebd9b6af" />



**Question 4**
---
n the Student_details table, insert a student record where some fields are NULL, another record where all fields are filled without any NULL values, and a third record where some fields are filled, and others are left as NULL.

RollNo      Name            Gender      Subject      MARKS
----------  ------------    ----------  ----------   ----------
205         Olivia Green    F
207         Liam Smith      M           Mathematics  85
208         Sophia Johnson  F           Science
For example:

Test	Result
select * from Student_details;
RollNo      Name          Gender      Subject     MARKS
----------  ------------  ----------  ----------  ----------
205         Olivia Green  F
207         Liam Smith    M           Mathematic  85
208         Sophia Johns  F           Science

```sql
INSERT into Student_details(RollNo,Name,Gender,Subject,MARKS)
Values
(205,"Olivia Green","F",NULL,NULL),
(207,"Liam Smith","M","Mathematics",85),
(208,"Sophia Johnson","F","Science",NULL)
```

**Output:**

<img width="1233" height="377" alt="image" src="https://github.com/user-attachments/assets/c49de01b-e616-4f15-af07-a56b7b167726" />


**Question 5**
---
Create a table named ProjectAssignments with the following constraints:
AssignmentID as INTEGER should be the primary key.
EmployeeID as INTEGER should be a foreign key referencing Employees(EmployeeID).
ProjectID as INTEGER should be a foreign key referencing Projects(ProjectID).
AssignmentDate as DATE should be NOT NULL.
For example:

Test	Result
INSERT INTO ProjectAssignments (AssignmentID, EmployeeID, ProjectID, AssignmentDate) VALUES (2, 99, 1, '2024-01-03');
Error: FOREIGN KEY constraint failed

```sql
CREATE TABLE ProjectAssignments(
AssignmentID INTEGER PRIMARY KEY,
EmployeeID INTEGER,
ProjectID INTEGER,
AssignmentDate DATE NOT NULL,
FOREIGN KEY(EmployeeID) REFERENCES Employees(EmployeeID),
FOREIGN KEY(ProjectID) REFERENCES Projects(ProjectID)
);
```

**Output:**

<img width="1227" height="370" alt="image" src="https://github.com/user-attachments/assets/04bf08ee-72d7-4d7f-8569-84f429db6510" />


**Question 6**
---
Write a SQL Query to add an attribute designation in the employee table with the data type VARCHAR(50).

For example:

Test	Result
pragma table_info('employee');
cid         name        type        notnull     dflt_value  pk
----------  ----------  ----------  ----------  ----------  ----------
0           id          integer     0                       0
1           salary      number      0                       0
2           designatio  varchar(50  0                       0

```sql
ALTER TABLE employee add designation varchar(50)
```

**Output:**

<img width="1236" height="377" alt="image" src="https://github.com/user-attachments/assets/d8ba3e80-5abb-42b3-88eb-68eb32377d3b" />


**Question 7**
---
Create a table named Products with the following constraints:
ProductID as INTEGER should be the primary key.
ProductName as TEXT should be unique and not NULL.
Price as REAL should be greater than 0.
StockQuantity as INTEGER should be non-negative.
For example:

Test	Result
INSERT INTO Products (ProductID, ProductName, Price, StockQuantity) VALUES (1, 'Laptop', 999.99, 10);
select * from Products;
ProductID   ProductName  Price       StockQuantity
----------  -----------  ----------  -------------
1           Laptop       999.99      10


```sql
CREATE TABLE Products(
ProductID INTEGER PRIMARY KEY,
ProductName TEXT UNIQUE NOT NULL,
Price REAL CHECK(Price>0),
StockQuantity INTEGER CHECK(StockQuantity>=0)
);
```

**Output:**

<img width="1226" height="370" alt="image" src="https://github.com/user-attachments/assets/2032f52c-e3fb-4903-b8ec-8e8e462c64f7" />


**Question 8**
---
Write an SQL command can to add a column named email of type TEXT to the customers table

 

For example:

Test	Result
pragma table_info('Customers');
cid         name        type        notnull     dflt_value  pk
----------  ----------  ----------  ----------  ----------  ----------
0           id          integer     0                       0
1           name        text        0                       0
2           email       TEXT        0                       0

```sql
ALTER TABLE customers ADD column email TEXT;
```

**Output:**

<img width="1235" height="376" alt="image" src="https://github.com/user-attachments/assets/e13cc496-98c0-47a5-9653-75eff3ea2f76" />


**Question 9**
---
Create a table named Invoices with the following constraints:
InvoiceID as INTEGER should be the primary key.
InvoiceDate as DATE.
Amount as REAL should be greater than 0.
DueDate as DATE should be greater than the InvoiceDate.
OrderID as INTEGER should be a foreign key referencing Orders(OrderID).
For example:

Test	Result
INSERT INTO Orders (OrderID, OrderDate, CustomerID) VALUES (1, '2024-08-01', 1);
INSERT INTO Invoices (InvoiceID, InvoiceDate, Amount, DueDate, OrderID) VALUES (1, '2024-08-01', 100.0, '2024-09-01', 1);
SELECT * FROM Invoices;
InvoiceID   InvoiceDate  Amount      DueDate     OrderID
----------  -----------  ----------  ----------  ----------
1           2024-08-01   100.0       2024-09-01  1

```sql
CREATE TABLE Invoices(
InvoiceID INTEGER PRIMARY KEY,
InvoiceDate DATE,
Amount REAL CHECK(Amount>0),
DueDate DATE check(DueDate>InvoiceDate),
OrderID INTEGER,
FOREIGN KEY(OrderID) REFERENCES Orders(OrderID)
);
```

**Output:**

<img width="1221" height="301" alt="image" src="https://github.com/user-attachments/assets/cf6694bb-73c7-4e8b-aabf-8bf03c66c474" />


**Question 10**
---
Create a table named Tasks with the following columns:

TaskID as INTEGER
TaskName as TEXT
DueDate as DATE
For example:

Test	Result
pragma table_info('Tasks');
cid         name        type        notnull     dflt_value  pk
----------  ----------  ----------  ----------  ----------  ----------
0           TaskID      INTEGER     0                       0
1           TaskName    TEXT        0                       0
2           DueDate     DATE        0                       0


```sql
CREATE TABLE Tasks(
TaskID INTEGER,
TaskName TEXT,
DueDate DATE
);
```

**Output:**
<img width="1216" height="386" alt="image" src="https://github.com/user-attachments/assets/eb1637fe-95ae-4b74-8097-a2522e1390ac" />



## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
