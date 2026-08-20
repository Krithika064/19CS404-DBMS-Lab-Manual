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
Write a SQL statement to change the EMAIL and COMMISSION_PCT column of the following EMPLOYEES table with 'not available' and 0.55 for those employees whose DEPARTMENT_ID is 110.


Employees table

---------------
employee_id
first_name
last_name
email
phone_number
hire_date
job_id
salary
commission_pct
manager_id
department_id
For example:

Test	Result
SELECT EMPLOYEE_ID,FIRST_NAME,EMAIL,COMMISSION_PCT FROM EMPLOYEES 
WHERE DEPARTMENT_ID=110 LIMIT 1;
EMPLOYEE_ID  FIRST_NAME  EMAIL          COMMISSION_PCT
-----------  ----------  -------------  --------------
205          Shelley     not available  0.55

```sql
UPDATE EMPLOYEES
SET EMAIL = 'not available',
    COMMISSION_PCT = 0.55
WHERE DEPARTMENT_ID = 110;
```

**Output:**

<img width="1217" height="492" alt="image" src="https://github.com/user-attachments/assets/c580519a-5cba-4727-819d-10e4e5f850c7" />


**Question 2**
---
write a SQL query to identify customers who do not belong to the city of 'New York' or have a grade value that exceeds 100. Return customer_id, cust_name, city, grade, and salesman_id.

Sample table: customer

 customer_id |   cust_name    |    city    | grade | salesman_id 
-------------+----------------+------------+-------+-------------
        3002 | Nick Rimando   | New York   |   100 |        5001
        3007 | Brad Davis     | New York   |   200 |        5001
        3005 | Graham Zusi    | California |   200 |        5002
For example:

Result
customer_id  cust_name     city        grade       salesman_id
-----------  ------------  ----------  ----------  -----------
3002         Nick Rimando  Chennai     100         5001
3001         Brad Guzan    London      100         5005


```sql
SELECT customer_id,
       cust_name,
       city,
       grade,
       salesman_id
FROM customer
WHERE city <> 'New York'
  AND grade = 100;
```

**Output:**

<img width="1222" height="502" alt="image" src="https://github.com/user-attachments/assets/2a75129c-a5de-4155-8374-c6dcc26e180b" />


**Question 3**
---
Write a SQL query to categorize decimal as 'High', 'Medium', or 'Low' based on whether it is greater than 100, between 50 and 100, or less than 50 in the Calculations table

cid         name        type        notnull     dflt_value  pk
----------  ----------  ----------  ----------  ----------  ----------
0           id          INTEGER     0                       1
1           value1      REAL        0                       0
2           value2      REAL        0                       0
3           base        INTEGER     0                       0
4           exponent    INTEGER     0                       0
5           number      REAL        0                       0
6           decimal     REAL        0                       0
 

For example:

Result
id          decimal     category
----------  ----------  ----------
1           123.4567    High
2           567.891     High
3           78.234      Medium
4           45.78       Low


```sql
SELECT 
    id,
    decimal,
    CASE 
        WHEN decimal > 100 THEN 'High'
        WHEN decimal BETWEEN 50 AND 100 THEN 'Medium'
        ELSE 'Low'
    END AS category
FROM 
    Calculations;
```

**Output:**
<img width="1207" height="527" alt="image" src="https://github.com/user-attachments/assets/1841c4ee-4b61-4b0e-87f8-263f756fb34f" />




**Question 4**
---
Write a SQL query to Delete All Doctors with a NULL Last Name

Sample table: Doctors

attributes: doctor_id, first_name, last_name, specialization
For example:

Test	Result
SELECT * FROM doctors;
doctor_id   first_name  last_name   specialization
----------  ----------  ----------  --------------
1           John        Smith       Cardiology
2           Emily       Johnson     Orthopedics
3           Michael     Brown       Pediatrics
4           Febin                   Cardiology
doctor_id   first_name  last_name   specialization
----------  ----------  ----------  --------------
1           John        Smith       Cardiology
2           Emily       Johnson     Orthopedics
3           Michael     Brown       Pediatrics


```sql
DELETE FROM Doctors
WHERE last_name IS NULL;
```

**Output:**
<img width="1272" height="857" alt="image" src="https://github.com/user-attachments/assets/3513ac5a-b3b4-457d-8157-0958c7f291ea" />




**Question 5**
---
Write a SQL query to remove rows from the table 'customer' with the following condition -

1. 'cust_country' must be 'India',

2. 'cus_city' must not be 'Chennai',

Sample table: Customer

+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+  
|CUST_CODE  | CUST_NAME   | CUST_CITY   | WORKING_AREA | CUST_COUNTRY | GRADE | OPENING_AMT | RECEIVE_AMT | PAYMENT_AMT |OUTSTANDING_AMT| PHONE_NO     | AGENT_CODE |
+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+
| C00013    | Holmes      | London      | London       | UK           |     2 |     6000.00 |     5000.00 |     7000.00 |       4000.00 | BBBBBBB      | A003       |
| C00001    | Micheal     | New York    | New York     | USA          |     2 |     3000.00 |     5000.00 |     2000.00 |       6000.00 | CCCCCCC      | A008       |
| C00020    | Albert      | New York    | New York     | USA          |     3 |     5000.00 |     7000.00 |     6000.00 |       6000.00 | BBBBSBB      | A008       |
For example:

Test	Result
SELECT * FROM customer WHERE cust_country='India';
CUST_CODE   CUST_NAME   CUST_CITY   WORKING_AREA  CUST_COUNTRY  GRADE       OPENING_AMT  RECEIVE_AMT  PAYMENT_AMT  OUTSTANDING_AMT  PHONE_NO    AGENT_CODE
----------  ----------  ----------  ------------  ------------  ----------  -----------  -----------  -----------  ---------------  ----------  ----------
C00025      Ravindran   Bangalore   Bangalore     India         2           5000         7000         4000         8000             AVAVAVA     A011
C00019      Yearannaid  Chennai     Chennai       India         1           8000         7000         7000         8000             ZZZZBFV     A010
C00005      Sasikant    Mumbai      Mumbai        India         1           7000         11000        7000         11000            147-258963  A002
C00007      Ramanathan  Chennai     Chennai       India         1           7000         11000        9000         9000             GHRDWSD     A010
C00022      Avinash     Mumbai      Mumbai        India         2           7000         11000        9000         9000             113-123456  A002
C00017      Srinivas    Bangalore   Bangalore     India         2           8000         4000         3000         9000             AAAAAAB     A007
C00009      Ramesh      Mumbai      Mumbai        India         3           8000         7000         3000         12000            Phone No    A002
C00014      Rangarappa  Bangalore   Bangalore     India         2           8000         11000        7000         12000            AAAATGF     A001
C00016      Venkatpati  Bangalore   Bangalore     India         2           8000         11000        7000         12000            JRTVFDD     A007
C00011      Sundariya   Chennai     Chennai       India         3           7000         11000        7000         11000            PPHGRTS     A010
CUST_CODE   CUST_NAME    CUST_CITY   WORKING_AREA  CUST_COUNTRY  GRADE       OPENING_AMT  RECEIVE_AMT  PAYMENT_AMT  OUTSTANDING_AMT  PHONE_NO    AGENT_CODE
----------  -----------  ----------  ------------  ------------  ----------  -----------  -----------  -----------  ---------------  ----------  ----------
C00019      Yearannaidu  Chennai     Chennai       India         1           8000         7000         7000         8000             ZZZZBFV     A010
C00007      Ramanathan   Chennai     Chennai       India         1           7000         11000        9000         9000             GHRDWSD     A010
C00011      Sundariya    Chennai     Chennai       India         3           7000         11000        7000         11000            PPHGRTS     A010

```sql
DELETE FROM customer
WHERE cust_country = 'India' 
  AND cust_city != 'Chennai';
```

**Output:**
<img width="1296" height="972" alt="image" src="https://github.com/user-attachments/assets/ef2315b4-f593-4bf3-b131-fc33026e1a4f" />




**Question 6**
---
Write a SQL query to calculate the final price after applying both the discount and the tax. Return product_id, original_price, discount_percentage, tax_rate, and final_price.

Sample table: Products

product_id | original_price | discount_percentage | tax_rate

 ------------+----------------+---------------------+--------- 

101 | 50.00 | 0.10 | 0.08 

102 | 75.00 | 0.15 | 0.05 

103 | 100.00 | 0.20 | 0.10

 

For example:

Result
product_id  original_price  discount_percentage  tax_rate    final_price
----------  --------------  -------------------  ----------  -----------
101         50.0            0.1                  0.08        48.6
102         75.0            0.15                 0.05        66.9375
103         100.0           0.2                  0.1         88.0


```sql
SELECT 
    product_id,
    original_price,
    discount_percentage,
    tax_rate,
    ROUND(
        original_price * (1 - discount_percentage) * (1 + tax_rate), 
        4
    ) AS final_price
FROM 
    Products;
```

**Output:**
<img width="1302" height="352" alt="image" src="https://github.com/user-attachments/assets/487d3b2f-022b-43fa-935a-d6464c827423" />



**Question 7**
---
Write a SQL query to retrieve the details of all customers whose ID belongs to any of the values 3007, 3008 or 3009. Return customer_id, cust_name, city, grade, and salesman_id.

Sample table: customer

 customer_id |   cust_name    |    city    | grade | salesman_id 
-------------+----------------+------------+-------+-------------
        3002 | Nick Rimando   | New York   |   100 |        5001
        3007 | Brad Davis     | New York   |   200 |        5001
        3005 | Graham Zusi    | California |   200 |        5002
For example:

Result
customer_id  cust_name   city        grade       salesman_id
-----------  ----------  ----------  ----------  -----------
3007         Brad Davis  New York    200         5001
3008         Julian Gre  London      300         5002
3009         Geoff Came  Berlin      100         5003

```sql
SELECT 
    customer_id, 
    cust_name, 
    city, 
    grade, 
    salesman_id
FROM 
    customer
WHERE 
    customer_id IN (3007, 3008, 3009);
```

**Output:**

<img width="1217" height="476" alt="image" src="https://github.com/user-attachments/assets/16089ac4-2f3e-4094-b527-be3fd13b9853" />


**Question 8**
---
Write a SQL query to Delete a Specific Surgery which was made on 28th Feb 2024.

Sample table: Surgeries


attributes: surgery_id, patient_id, surgeon_id, surgery_date

For example:

Test	Result
SELECT * FROM surgeries;
surgery_id  patient_id  surgeon_id  surgery_date
----------  ----------  ----------  ------------
1           1           1           2024-01-15
2           2           2           2024-02-28
3           3           3           2024-03-25
surgery_id  patient_id  surgeon_id  surgery_date
----------  ----------  ----------  ------------
1           1           1           2024-01-15
3           3           3           2024-03-25


```sql
DELETE FROM Surgeries
WHERE surgery_date = '2024-02-28';
```

**Output:**

<img width="1270" height="486" alt="image" src="https://github.com/user-attachments/assets/f114aed0-75de-4fe6-8fd8-49883bedf9f4" />


**Question 9**
---
Write a SQL query to calculate the number of years each employee has been with the company till '2024-08-30'.

Calculations table

cid         name        type        
----------  ----------  ---------- 
0           empno       INT         
1           ename       VARCHAR(100)
2           job         VARCHAR(50)
3           mgr         INT        
4           hiredate    DATE        
5           sal         DECIMAL(10,2)  
6           comm        DECIMAL(10,2)  
7           deptno      INT         
For example:

Result
ename       Tenure
----------  ----------
JONES       43
MARTIN      42
BLAKE       43
CLARK       43
SCOTT       41
KING        42
TURNER      42


```sql
SELECT 
    ename,
    CAST((julianday('2024-08-30') - julianday(hiredate)) / 365.25 AS INTEGER) AS Tenure
FROM 
    emp;
```

**Output:**

<img width="730" height="430" alt="image" src="https://github.com/user-attachments/assets/c0e3fad0-7153-409a-b2b9-9b1b0a59ca61" />


**Question 10**
---
Write a SQL query to display hire dates in the format "DD-MM-YYYY" from the emp table

cid         name        type        
----------  ----------  ---------- 
0           empno       INT         
1           ename       VARCHAR(100)
2           job         VARCHAR(50)
3           mgr         INT        
4           hiredate    DATE        
5           sal         DECIMAL(10,2)  
6           comm        DECIMAL(10,2)  
7           deptno      INT         
For example:

Result
ename       HireDateFormatted
----------  -----------------
JONES       02-04-1981
MARTIN      28-09-1981
BLAKE       01-05-1981
CLARK       09-06-1981
SCOTT       09-12-1982
KING        17-11-1981
TURNER      08-09-1981


```sql
SELECT 
    ename,
    strftime('%d-%m-%Y', hiredate) AS HireDateFormatted
FROM 
    emp;
```

**Output:**

<img width="1042" height="442" alt="image" src="https://github.com/user-attachments/assets/e2e7aeaa-7d47-4a22-9ea9-80c0c1670018" />


## RESULT
Thus, the SQL queries to implement DML commands have been executed successfully.
