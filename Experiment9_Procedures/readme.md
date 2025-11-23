# Experiment 9: PL/SQL – Procedures and Functions

## AIM
To understand and implement procedures and functions in PL/SQL for performing various operations such as calculations, decision-making, and looping.

---

## THEORY

PL/SQL (Procedural Language/SQL) extends SQL by adding procedural constructs like variables, conditions, loops, procedures, and functions. Procedures and functions are subprograms that help modularize the code and improve reusability.

### **Procedure**
A PL/SQL **procedure** is a subprogram that performs a specific action. It does not return a value directly but can return values using `OUT` parameters.

**Syntax:**
```sql
CREATE OR REPLACE PROCEDURE procedure_name (parameters)
IS
BEGIN
   -- statements
END;
```

To call the procedure

```sql
EXEC procedure_name(arguments);
```

### **Function**
A PL/SQL **function** is a subprogram that returns a single value using the RETURN keyword.

```sql
CREATE OR REPLACE FUNCTION function_name (parameters)
RETURN datatype
IS
BEGIN
   -- statements
   RETURN value;
END;
```

To call the function:

```sql
SELECT function_name(arguments) FROM DUAL;
```

Key Differences:

-A procedure does not return a value, whereas a function must return a value.
-Functions can be called from SQL queries, procedures cannot (in most cases).

## 1. Write a PL/SQL Procedure to Find the Square of a Number

### Steps:
- Create a procedure named `find_square`.
- Declare a parameter to accept a number.
- Inside the procedure, compute the square of the input number.
- Use `DBMS_OUTPUT.PUT_LINE` to display the result.
- Call the procedure with a number as input.
Program
CREATE OR REPLACE PROCEDURE find_square(num IN NUMBER) IS
    sq NUMBER;
BEGIN
    sq := num * num;
    DBMS_OUTPUT.PUT_LINE('Square of ' || num || ' is ' || sq);
END;
/


**Expected Output:**  
Square of 6 is 36

<img width="765" height="280" alt="image" src="https://github.com/user-attachments/assets/3a8907bc-101c-483b-bf47-49da7ef39acd" />


---

## 2. Write a PL/SQL Function to Return the Factorial of a Number

### Steps:
- Create a function named `get_factorial`.
- Declare a parameter to accept a number.
- Use a loop to calculate the factorial.
- Return the result using the `RETURN` statement.
- Call the function using a `SELECT` statement or in an anonymous block.
Program
DECLARE
    result NUMBER;
BEGIN
    result := get_factorial(5);
    DBMS_OUTPUT.PUT_LINE('Factorial of 5 is ' || result);
END;
/


**Expected Output:**  
Factorial of 5 is 120

<img width="857" height="285" alt="image" src="https://github.com/user-attachments/assets/111e6649-7e2c-4d7e-8a1a-3f805853f6e8" />

---

## 3. Write a PL/SQL Procedure to Check Whether a Number is Even or Odd

### Steps:
- Create a procedure named `check_even_odd`.
- Accept an input parameter.
- Use the `MOD` function to check if the number is divisible by 2.
- Display whether it is Even or Odd using `DBMS_OUTPUT.PUT_LINE`.
Program
BEGIN
    check_even_odd(12);
END;
/


**Expected Output:**  
12 is Even

<img width="827" height="242" alt="image" src="https://github.com/user-attachments/assets/591e07fa-da20-4dba-a7d9-c9ef11752bbc" />

---

## 4. Write a PL/SQL Function to Return the Reverse of a Number

### Steps:
- Create a function named `reverse_number`.
- Accept an input number as parameter.
- Use a loop to reverse the digits of the number.
- Return the reversed number.
- Call the function and display the output.
Program
DECLARE
    n NUMBER := 1234;
    result NUMBER;
BEGIN
    result := reverse_number(n);
    DBMS_OUTPUT.PUT_LINE('Reversed number of ' || n || ' is ' || result);
END;
/


**Expected Output:**  
Reversed number of 1234 is 4321

<img width="731" height="276" alt="image" src="https://github.com/user-attachments/assets/5d1423f2-912f-40f4-a66a-badcf5b909b8" />


---

## 5. Write a PL/SQL Procedure to Display the Multiplication Table of a Number

### Steps:
- Create a procedure named `print_table`.
- Accept an input number.
- Use a loop from 1 to 10 to multiply the input number.
- Display the multiplication results using `DBMS_OUTPUT.PUT_LINE`.
Program
DECLARE
    n NUMBER := 5;
BEGIN
    print_table(n);
END;
/


**Expected Output:**  
Multiplication table of 5:  
5 x 1 = 5  
5 x 2 = 10  
5 x 3 = 15  
...  
5 x 10 = 50

<img width="750" height="292" alt="image" src="https://github.com/user-attachments/assets/0fd8ca0c-3818-4f07-94f8-51ed1693f4a9" />


## RESULT
Thus, the PL/SQL programs using procedures and functions were written, compiled, and executed successfully.
