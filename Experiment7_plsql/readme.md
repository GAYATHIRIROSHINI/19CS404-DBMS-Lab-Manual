# Experiment 7: PL/SQL – Variables, Control Structures and Loops

## AIM
To write and execute simple PL/SQL programs using variables, loops, and conditional statements.


## THEORY

PL/SQL, which stands for Procedural Language extensions to the Structured Query Language (SQL). It is a combination of SQL along with the procedural features of programming languages.

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

# PL/SQL Programs – Steps and Expected Output

## 1. Write a PL/SQL program to find the Greatest of Two Numbers

### Steps:
- Declare two numeric variables and initialize them.
- Use an `IF` statement to compare the values.
- Display the greater number using `DBMS_OUTPUT.PUT_LINE`.
- PROGRAM
```
- SET SERVEROUTPUT ON;

DECLARE
    a NUMBER := 45;
    b NUMBER := 80;
    greater NUMBER;
BEGIN
    IF a > b THEN
        greater := a;
    ELSE
        greater := b;
    END IF;

    DBMS_OUTPUT.PUT_LINE('Greater number is: ' || greater);
END;
```


**Expected Output:**  
Greater number is: 80

<img width="656" height="278" alt="image" src="https://github.com/user-attachments/assets/ccd8c6b0-e0d1-4c3c-9afe-53b59cc2a26f" />


---

## 2. Write a PL/SQL program to Calculate Sum of First N Natural Numbers

### Steps:
- Declare a variable `n` and assign a value (e.g., 10).
- Initialize a `sum` variable to 0.
- Use a `WHILE` loop to iterate from 1 to `n`, adding each number to the sum.
- Display the result using `DBMS_OUTPUT.PUT_LINE`.
PROGRAM
```
SET SERVEROUTPUT ON;

DECLARE
    n NUMBER := 10;
    i NUMBER := 1;
    total NUMBER := 0;
BEGIN
    WHILE i <= n LOOP
        total := total + i;
        i := i + 1;
    END LOOP;

    DBMS_OUTPUT.PUT_LINE('Sum of first ' || n || ' natural numbers is: ' || total);
END;
/
```
**Expected Output:**  
Sum of first 10 natural numbers is: 55

<img width="626" height="276" alt="image" src="https://github.com/user-attachments/assets/57be9e57-d396-4556-b61e-7c9481292ea8" />

---

## 3. Write a PL/SQL program to generate Fibonacci series

### Steps:
- Declare the variable `n` to indicate how many terms to generate.
- Initialize the first two Fibonacci numbers (0 and 1).
- Use a loop to generate the next terms using the formula `c = a + b`.
- Print each term in the series.
PROGRAM
```
SET SERVEROUTPUT ON;

DECLARE
    n NUMBER := 7;
    a NUMBER := 0;
    b NUMBER := 1;
    c NUMBER;
    i NUMBER := 3;
BEGIN
    DBMS_OUTPUT.PUT_LINE('Fibonacci sequence:');
    DBMS_OUTPUT.PUT(a || ', ' || b);

    WHILE i <= n LOOP
        c := a + b;
        DBMS_OUTPUT.PUT(', ' || c);
        a := b;
        b := c;
        i := i + 1;
    END LOOP;
END;
/
```
**Expected Output:**  
n = 7  
Fibonacci sequence: 0, 1, 1, 2, 3, 5, 8

<img width="593" height="279" alt="image" src="https://github.com/user-attachments/assets/40cc7c21-4498-48c9-a911-49966072797f" />


---

## 4. Write a PL/SQL Program to display the number in Reverse Order

### Steps:
- Declare a variable `n` and assign a value (e.g., 1535).
- Use a loop to extract each digit using modulo and reverse the number.
- Display the reversed number.
- PROGRAM
```
  SET SERVEROUTPUT ON;

DECLARE
    n NUMBER := 1535;
    num NUMBER := n;
    rev NUMBER := 0;
    digit NUMBER;
BEGIN
    WHILE num > 0 LOOP
        digit := MOD(num, 10);       -- extract last digit
        rev := rev * 10 + digit;     -- build reversed number
        num := FLOOR(num / 10);      -- remove last digit
    END LOOP;

    DBMS_OUTPUT.PUT_LINE('Reversed number is ' || rev);
END;
/
```
  

**Expected Output:**  
n = 1535  
Reversed number is 5351

<img width="591" height="274" alt="image" src="https://github.com/user-attachments/assets/f3e18202-9ad5-4fac-908b-b4bc01d1fc27" />

---

## 5. Write a PL/SQL program to find the largest of three numbers

### Steps:
- Declare three numeric variables `a`, `b`, and `c`.
- Use nested `IF-ELSIF-ELSE` conditions to find the largest among the three.
- Display the largest number.
- PROGRAM
```
SET SERVEROUTPUT ON;

DECLARE
    a NUMBER := 10;
    b NUMBER := 9;
    c NUMBER := 15;
    largest NUMBER;
BEGIN
    IF a >= b AND a >= c THEN
        largest := a;
    ELSIF b >= a AND b >= c THEN
        largest := b;
    ELSE
        largest := c;
    END IF;

    DBMS_OUTPUT.PUT_LINE('Largest of three number is ' || largest);
END;
/
```
**Expected Output:**  
a = 10, b = 9, c = 15  
Largest of three number is 15

<img width="573" height="272" alt="image" src="https://github.com/user-attachments/assets/d89b8866-5e77-4cf1-a28b-8988cda8d1c0" />

## RESULT
Thus, the PL/SQL programs using variables, conditionals, and loops were executed successfully.






