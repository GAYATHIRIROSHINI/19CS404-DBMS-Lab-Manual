# Experiment 8: PL/SQL Cursor Programs

## AIM
To write and execute PL/SQL programs using cursors and exception handling to manage runtime errors effectively and display appropriate messages.

## THEORY

In PL/SQL, cursors are used to handle query result sets row-by-row. 

There are two types of cursors:

- Implicit Cursors: Automatically created by PL/SQL for single-row queries.
- Explicit Cursors: Declared and controlled by the programmer for multi-row queries.

Types of Explicit Cursors:

1. Simple Cursor: Basic cursor to iterate over multiple rows.

2. Parameterized Cursor: Accepts parameters to filter the result dynamically.

3. Cursor FOR Loop: Simplifies cursor operations (open, fetch, close).

4. %ROWTYPE Cursor: Fetches entire row into a record using %ROWTYPE.

5. Cursor with FOR UPDATE: Used for row-level locking and updating the rows while looping.

**Syntax:**
```sql
DECLARE 
   <declarations section> 
BEGIN 
   <executable command(s)>
EXCEPTION 
   <exception handling> 
END;
```

### Basic Components of PL/SQL Block:

- DECLARE: Section to declare variables and constants.
- BEGIN: The execution section that contains PL/SQL statements.
- EXCEPTION: Handles errors or exceptions that occur in the program.
- END: Marks the end of the PL/SQL block.

**Exception Handling**

PL/SQL provides a robust mechanism to handle runtime errors using exception handling blocks. When an error occurs during execution, control is passed to the EXCEPTION section, where specific or general errors can be handled gracefully.

### Components of Exception Handling:
- Predefined Exceptions: Automatically raised by PL/SQL for common errors (e.g., NO_DATA_FOUND, TOO_MANY_ROWS, ZERO_DIVIDE).
- User-defined Exceptions: Declared explicitly in the declaration section using the EXCEPTION keyword.
- WHEN OTHERS: A generic handler for all exceptions not handled explicitly.

```sql
BEGIN
   -- Statements
EXCEPTION
   WHEN exception_name THEN
      -- Handling code
   WHEN OTHERS THEN
      -- Handling for unknown errors
END;
```

### **Question 1: Simple Cursor with Exception Handling**

**Write a PL/SQL program using a simple cursor to fetch employee names and designations from the `employees` table. Implement exception handling for the following cases:**

1. **NO_DATA_FOUND**: When no rows are fetched.
2. **OTHERS**: Any other unexpected errors during execution.

**Steps:**

- Create an `employees` table with fields `emp_id`, `emp_name`, and `designation`.
- Insert some sample data into the table.
- Use a simple cursor to fetch and display employee names and designations.
- Implement exception handling to catch the relevant exceptions and display appropriate messages.
- PROGRAM
```
SET SERVEROUTPUT ON;

-- Creating employees table
BEGIN
    EXECUTE IMMEDIATE 'DROP TABLE employees';
EXCEPTION
    WHEN OTHERS THEN
        NULL; -- ignore if table does not exist
END;
/

CREATE TABLE employees (
    emp_id NUMBER,
    emp_name VARCHAR2(50),
    designation VARCHAR2(50)
);

-- Insert sample data
INSERT INTO employees VALUES (1, 'Arun', 'Manager');
INSERT INTO employees VALUES (2, 'Deepa', 'Developer');
INSERT INTO employees VALUES (3, 'Kavi', 'Analyst');

COMMIT;


-- PL/SQL Block using Simple Cursor
DECLARE
    CURSOR emp_cursor IS
        SELECT emp_name, designation FROM employees;

    v_name employees.emp_name%TYPE;
    v_desg employees.designation%TYPE;

    no_rows BOOLEAN := TRUE;
BEGIN
    OPEN emp_cursor;

    LOOP
        FETCH emp_cursor INTO v_name, v_desg;
        EXIT WHEN emp_cursor%NOTFOUND;

        no_rows := FALSE;

        DBMS_OUTPUT.PUT_LINE('Name: ' || v_name || ', Designation: ' || v_desg);
    END LOOP;

    CLOSE emp_cursor;

    IF no_rows THEN
        RAISE NO_DATA_FOUND;
    END IF;

EXCEPTION
    WHEN NO_DATA_FOUND THEN
        DBMS_OUTPUT.PUT_LINE('No employee records found.');
    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('An unexpected error occurred: ' || SQLERRM);
END;
/
```

**Output:**  
The program should display the employee details or an error message.

<img width="608" height="280" alt="image" src="https://github.com/user-attachments/assets/d364d071-e14f-45da-bc6d-f0b2f6d105fc" />

---

### **Question 2: Parameterized Cursor with Exception Handling**

**Write a PL/SQL program using a parameterized cursor to retrieve and display employees with a salary in a given range. Implement exception handling for the following errors:**

1. **NO_DATA_FOUND**: When no employees meet the salary criteria.
2. **OTHERS**: For any unexpected errors during the execution.

**Steps:**

- Modify the `employees` table by adding a `salary` column.
- Insert sample salary values for the employees.
- Use a parameterized cursor to accept a salary range as input and fetch employees within that range.
- Implement exception handling to catch and display relevant error messages.
- PROGRAM
```
SET SERVEROUTPUT ON;

-- Add salary column (ignore error if already exists)
BEGIN
    EXECUTE IMMEDIATE 'ALTER TABLE employees ADD (salary NUMBER)';
EXCEPTION
    WHEN OTHERS THEN
        NULL;
END;
/

-- Update salary values
UPDATE employees SET salary = 50000 WHERE emp_id = 1;
UPDATE employees SET salary = 35000 WHERE emp_id = 2;
UPDATE employees SET salary = 25000 WHERE emp_id = 3;

COMMIT;


-- PL/SQL block using parameterized cursor
DECLARE
    -- Parameterized cursor accepts min & max salary
    CURSOR emp_salary_cur(min_sal NUMBER, max_sal NUMBER) IS
        SELECT emp_name, designation, salary
        FROM employees
        WHERE salary BETWEEN min_sal AND max_sal;

    v_name employees.emp_name%TYPE;
    v_design employees.designation%TYPE;
    v_salary employees.salary%TYPE;

    no_rows BOOLEAN := TRUE;

    min_range NUMBER := 20000;
    max_range NUMBER := 40000;
BEGIN
    DBMS_OUTPUT.PUT_LINE('Employees with salary between ' ||
                         min_range || ' and ' || max_range || ':');

    OPEN emp_salary_cur(min_range, max_range);

    LOOP
        FETCH emp_salary_cur INTO v_name, v_design, v_salary;
        EXIT WHEN emp_salary_cur%NOTFOUND;

        no_rows := FALSE;

        DBMS_OUTPUT.PUT_LINE('Name: ' || v_name ||
                             ', Designation: ' || v_design ||
                             ', Salary: ' || v_salary);
    END LOOP;

    CLOSE emp_salary_cur;

    IF no_rows THEN
        RAISE NO_DATA_FOUND;
    END IF;

EXCEPTION
    WHEN NO_DATA_FOUND THEN
        DBMS_OUTPUT.PUT_LINE('No employees found in the given salary range.');
    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('Unexpected error occurred: ' || SQLERRM);
END;
/
```

**Output:**  
The program should display the employee details within the specified salary range or an error message if no data is found.

<img width="794" height="284" alt="image" src="https://github.com/user-attachments/assets/e137c45e-e513-4a7b-866b-9d6085a17b90" />

---

### **Question 3: Cursor FOR Loop with Exception Handling**

**Write a PL/SQL program using a cursor FOR loop to retrieve and display all employee names and their department numbers from the `employees` table. Implement exception handling for the following cases:**

1. **NO_DATA_FOUND**: If no employees are found in the database.
2. **OTHERS**: For any other unexpected errors.

**Steps:**

- Modify the `employees` table by adding a `dept_no` column.
- Insert sample department numbers for employees.
- Use a cursor FOR loop to fetch and display employee names along with their department numbers.
- Implement exception handling to catch the relevant exceptions.
- PROGRAM
```
SET SERVEROUTPUT ON;

-- Add dept_no column (ignore if already exists)
BEGIN
    EXECUTE IMMEDIATE 'ALTER TABLE employees ADD (dept_no NUMBER)';
EXCEPTION
    WHEN OTHERS THEN
        NULL;
END;
/

-- Update department numbers
UPDATE employees SET dept_no = 10 WHERE emp_id = 1;
UPDATE employees SET dept_no = 20 WHERE emp_id = 2;
UPDATE employees SET dept_no = 30 WHERE emp_id = 3;

COMMIT;


-- PL/SQL block using Cursor FOR Loop
DECLARE
    no_rows BOOLEAN := TRUE;
BEGIN
    DBMS_OUTPUT.PUT_LINE('Employee Names with Department Numbers:');

    -- Cursor FOR loop automatically handles open, fetch, close
    FOR emp_rec IN (
        SELECT emp_name, dept_no FROM employees
    ) LOOP
        no_rows := FALSE;
        DBMS_OUTPUT.PUT_LINE('Name: ' || emp_rec.emp_name ||
                             ', Department: ' || emp_rec.dept_no);
    END LOOP;

    -- Raise exception manually if no rows
    IF no_rows THEN
        RAISE NO_DATA_FOUND;
    END IF;

EXCEPTION
    WHEN NO_DATA_FOUND THEN
        DBMS_OUTPUT.PUT_LINE('No employees found in the database.');
    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('An unexpected error occurred: ' || SQLERRM);
END;
/
```

**Output:**  
The program should display employee names with their department numbers or the appropriate error message if no data is found.

<img width="751" height="272" alt="image" src="https://github.com/user-attachments/assets/ba72c977-9d54-48e4-b705-e2c4c15a82e6" />

---

### **Question 4: Cursor with `%ROWTYPE` and Exception Handling**

**Write a PL/SQL program that uses a cursor with `%ROWTYPE` to fetch and display complete employee records (emp_id, emp_name, designation, salary). Implement exception handling for the following errors:**

1. **NO_DATA_FOUND**: When no employees are found in the database.
2. **OTHERS**: For any other errors that occur.

**Steps:**

- Modify the `employees` table by adding `emp_id`, `emp_name`, `designation`, and `salary` fields.
- Insert sample data into the `employees` table.
- Declare a cursor using `%ROWTYPE` to fetch complete rows from the `employees` table.
- Implement exception handling to catch the relevant exceptions and display appropriate messages.
- PROGRAM
```
DECLARE
    -- Cursor to fetch full employee row
    CURSOR emp_cur IS
        SELECT emp_id, emp_name, designation, salary FROM employees;

    emp_rec emp_cur%ROWTYPE;   -- %ROWTYPE record variable

    record_count NUMBER := 0;
BEGIN
    OPEN emp_cur;

    LOOP
        FETCH emp_cur INTO emp_rec;
        EXIT WHEN emp_cur%NOTFOUND;

        record_count := record_count + 1;

        DBMS_OUTPUT.PUT_LINE(
            'ID: ' || emp_rec.emp_id ||
            ', Name: ' || emp_rec.emp_name ||
            ', Designation: ' || emp_rec.designation ||
            ', Salary: ' || emp_rec.salary
        );
    END LOOP;

    CLOSE emp_cur;

    IF record_count = 0 THEN
        RAISE NO_DATA_FOUND;
    END IF;

EXCEPTION
    WHEN NO_DATA_FOUND THEN
        DBMS_OUTPUT.PUT_LINE('❌ No employee records found in the database.');

    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('⚠ Unexpected error: ' || SQLERRM);
END;
/
```

**Output:**  
The program should display employee records or the appropriate error message if no data is found.

<img width="759" height="280" alt="image" src="https://github.com/user-attachments/assets/26f4e59a-8109-4371-be85-d661ccdd071a" />

---

### **Question 5: Cursor with FOR UPDATE Clause and Exception Handling**

**Write a PL/SQL program using a cursor with the `FOR UPDATE` clause to update the salary of employees in a specific department. Implement exception handling for the following cases:**

1. **NO_DATA_FOUND**: If no rows are affected by the update.
2. **OTHERS**: For any unexpected errors during execution.

**Steps:**

- Modify the `employees` table to include a `dept_no` and `salary` field.
- Insert sample data into the `employees` table with different department numbers.
- Use a cursor with the `FOR UPDATE` clause to lock the rows of employees in a specific department and update their salary.
- Implement exception handling to handle `NO_DATA_FOUND` or other errors that may occur.
- PROGRAM
```
DECLARE
    v_dept NUMBER := 10;       -- Department to update
    updated_rows NUMBER := 0;

    CURSOR emp_cur IS
        SELECT emp_id, salary
        FROM employees
        WHERE dept_no = v_dept
        FOR UPDATE;   -- Locks rows

BEGIN
    -- Loop through cursor
    FOR emp_rec IN emp_cur LOOP
        
        -- Increase salary by 10%
        UPDATE employees
        SET salary = emp_rec.salary * 1.10
        WHERE CURRENT OF emp_cur;

        updated_rows := updated_rows + 1;

        DBMS_OUTPUT.PUT_LINE(
            'Updated Employee ID ' || emp_rec.emp_id || 
            ' New Salary: ' || (emp_rec.salary * 1.10)
        );
    END LOOP;

    -- If no rows updated, raise exception
    IF updated_rows = 0 THEN
        RAISE NO_DATA_FOUND;
    END IF;

    COMMIT;

EXCEPTION
    WHEN NO_DATA_FOUND THEN
        DBMS_OUTPUT.PUT_LINE('❌ No employees found in department ' || v_dept);

    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('⚠ Unexpected error: ' || SQLERRM);
END;
/
```

**Output:**  
The program should update employee salaries and display a message, or it should display an error message if no data is found.

<img width="678" height="282" alt="image" src="https://github.com/user-attachments/assets/fb30f506-0129-47ba-a1ca-df533881108d" />

---

## RESULT
Thus, the program successfully executed and displayed employee details using a cursor. 

