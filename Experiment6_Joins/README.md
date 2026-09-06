# Experiment 6: Joins

## AIM
To study and implement different types of joins.

## THEORY

SQL Joins are used to combine records from two or more tables based on a related column.

### 1. INNER JOIN
Returns records with matching values in both tables.

**Syntax:**
```sql
SELECT columns
FROM table1
INNER JOIN table2
ON table1.column = table2.column;
```

### 2. LEFT JOIN
Returns all records from the left table, and matched records from the right.

**Syntax:**

```sql
SELECT columns
FROM table1
LEFT JOIN table2
ON table1.column = table2.column;
```
### 3. RIGHT JOIN
Returns all records from the right table, and matched records from the left.

**Syntax:**

```sql
SELECT columns
FROM table1
RIGHT JOIN table2
ON table1.column = table2.column;
```
### 4. FULL OUTER JOIN
Returns all records when there is a match in either left or right table.

**Syntax:**

```sql
SELECT columns
FROM table1
FULL OUTER JOIN table2
ON table1.column = table2.column;
```

**Question 1**
--
Write the SQL query that achieves the selection of the first name from the "patients" table (aliased as "patient_name") and all columns from the "test_results" table (aliased as "t"), with an inner join on the "patient_id" column and a condition filtering for test results with the test name 'Blood Pressure'.

PATIENTS TABLE:



TEST_RESULT TABLES:



For example:

Result
patient_name     result_id        patient_id       test_name        result      test_date
---------------  ---------------  ---------------  ---------------  ----------  ----------
Alice            1                1   

```sql
SELECT patients.first_name AS patient_name,t.*
FROM patients
INNER JOIN test_results t ON patients.patient_id=t.patient_id
WHERE t.test_name='Blood Pressure';
```

**Output:**

<img width="1222" height="432" alt="image" src="https://github.com/user-attachments/assets/9847afff-2a23-47c1-bfed-88bbe5dd140f" />


**Question 2**
---
Write the SQL query that achieves the selection of the date of birth from the "patients" table (aliased as "p") and all columns from the "appointments" table (aliased as "a"), with an inner join on the "patient_id" column and a condition filtering for patients with the first name 'Alice'.

PATIENTS TABLE:



APPOINTMENTS TABLE:



For example:

Result
date_of_birth    appointment_id   patient_id       doctor_id        appointment_date
---------------  ---------------  ---------------  ---------------  -------------------
1980-05-12       1                1                1                2024-01-05 10:00:00


```sql
SELECT p.date_of_birth, a.*
FROM patients p
INNER JOIN appointments a ON p.patient_id=a.patient_id
WHERE p.first_name='Alice';
```

**Output:**

<img width="1266" height="385" alt="image" src="https://github.com/user-attachments/assets/06e4f260-1343-459a-919b-9df80e77e7a6" />


**Question 3**
---
Write the SQL query that achieves the selection of the first name from the "patients" table (aliased as "patient_name") and the test name from the "test_results" table (aliased as "t"), with an inner join on the "patient_id" column.

PATIENTS TABLE:



TEST_RESULT TABLES:



For example:

Result
patient_name     test_name
---------------  ---------------
Alice            Blood Pressure
Bob              X-Ray
Charlie          Blood Test


```sql
SELECT
  p.first_name AS patient_name,
  t.test_name
FROM
  patients p
INNER JOIN
  test_results t ON p.patient_id=t.patient_id;
```

**Output:**

<img width="1247" height="521" alt="image" src="https://github.com/user-attachments/assets/56c2db9d-355d-41e0-a19e-f29aaaf9a204" />


**Question 4**
---
Write the SQL query that achieves the selection of all columns from the "patients" table (aliased as "p"), with an inner join on the "patient_id" column and a condition filtering for test results with a test date between '2024-03-01' and '2024-03-31'.

PATIENTS TABLE:



TEST_RESULT TABLES:



For example:

Result
patient_id       first_name       last_name        date_of_birth    admission_date  discharge_date  doctor_id
---------------  ---------------  ---------------  ---------------  --------------  --------------  ----------
2                Bob              Miller           1995-08-23       2024-02-15      2024-03-01      2


```sql
SELECT p.*
FROM patients p
INNER JOIN test_results tr ON p.patient_id=tr.patient_id
WHERE tr.test_date BETWEEN '2024-03-01' AND '2024-03-31';
```

**Output:**

<img width="1206" height="462" alt="image" src="https://github.com/user-attachments/assets/28f9d1af-e92f-4fff-9125-9799f90b1ed0" />


**Question 5**
---
Write the SQL query that achieves the selection of the first name from the "patients" table (aliased as "patient_name") and the first name from the "doctors" table (aliased as "doctor_name"), with an inner join on the "doctor_id" column and a condition filtering for patients with a null discharge date.

PATIENTS TABLE:



DOCTORS TABLE:



For example:

Result
patient_name     doctor_name
---------------  ---------------
Alice            John
Charlie          Michael


```sql
SELECT patients.first_name AS patient_name,doctors.first_name AS doctor_name
FROM patients
INNER JOIN doctors ON patients.doctor_id=doctors.doctor_id
WHERE patients.discharge_date IS NULL;
```

**Output:**

<img width="662" height="507" alt="image" src="https://github.com/user-attachments/assets/2fcc5907-7192-4118-aaf4-a68a1311b199" />


**Question 6**
---
Write the SQL query that achieves the selection of the "name" column from the "salesman" table (aliased as "s"), the "cust_name," "city," "grade," and "salesman_id" columns from the "customer" table (aliased as "c"), with a left join on the "salesman_id" column and a condition filtering for customers with a grade less than or equal to 100.

Customer Table:



Salesmen Table:



 

For example:

Result
name             cust_name        city             grade            salesman_id
---------------  ---------------  ---------------  ---------------  -----------
Bob Emily        Nick Rimando     Chennai          100              5001
Pit Alex         Brad Guzan       London           100              5005
Lauson Hen       Geoff Cameron    Berlin           100              5003


```sql
SELECT
s.name,
c.cust_name,
c.city,
c.grade,
c.salesman_id
FROM
customer c
LEFT JOIN
salesman s ON c.salesman_id=s.salesman_id
WHERE 
c.grade<=100;
```

**Output:**
<img width="1252" height="596" alt="image" src="https://github.com/user-attachments/assets/9c56b0f6-540d-4aec-aa87-1a46922c7aab" />


**Question 7**
---
Write the SQL query that achieves the selection of the "cust_name" column from the "customer" table (aliased as "c") and the "commission" column from the "salesman" table (aliased as "s"), with a left join on the "salesman_id" column.

Customer Table:



Salesmen Table:



 

For example:

Result
cust_name        commission
---------------  ---------------
Nick Rimando     0.15
Graham Zusi      0.13
Brad Guzan       0.11
Fabian Johns     0.14
Brad Davis       0.15
Geoff Cameron    0.12
Julian Green     0.13
Jozy Altidore    0.13


```sql
SELECT c.cust_name,s.commission
FROM customer c
LEFT JOIN salesman s
ON c.salesman_id=s.salesman_id;
```

**Output:**

<img width="741" height="891" alt="image" src="https://github.com/user-attachments/assets/139216a3-262d-4d7b-aa29-c545393bdc32" />


**Question 8**
---
Write the SQL query that achieves the selection of all columns from the "customer" table (aliased as "c"), with a left join on the "customer_id" column and a condition filtering for orders with an order date between '2012-08-01' and '2012-08-30'.

CUSTOMER TABLE:



ORDERS TABLE:



For example:

Result
customer_id      cust_name        city             grade            salesman_id
---------------  ---------------  ---------------  ---------------  -----------
3009             Geoff Cameron    Berlin           100              5003
3003             Jozy Altidore    Moscow           200              5007


```sql
SELECT c.*
FROM customer c
LEFT JOIN orders o ON c.customer_id=o.customer_id
WHERE o.
```

**Output:**
<img width="741" height="891" alt="image" src="https://github.com/user-attachments/assets/3c273340-7193-47c6-b704-8182746d2c30" />

**Question 9**
---
Write the SQL query that achieves the selection of the first name from the "patients" table (aliased as "patient_name") and the first name from the "doctors" table (aliased as "doctor_name"), with an inner join on the "doctor_id" column and a condition filtering for patients with a null discharge date.

PATIENTS TABLE:



DOCTORS TABLE:



For example:

Result
patient_name     doctor_name
---------------  ---------------
Alice            John
Charlie          Michael


```sql
SELECT patients.first_name AS patient_name,doctors.first_name AS doctor_name
FROM patients
INNER JOIN doctors ON patients.doctor_id=doctors.doctor_id
WHERE patients.discharge_date IS NULL;
```

**Output:**
<img width="746" height="487" alt="image" src="https://github.com/user-attachments/assets/f8f8ab32-289a-400b-9c17-01649845afe7" />


**Question 10**
---
Write the SQL query that achieves the selection of all columns from the "patients" table (aliased as "p"), with an inner join on the "patient_id" column and a condition filtering for test results with a test date between '2024-03-01' and '2024-03-31'.

PATIENTS TABLE:



TEST_RESULT TABLES:



For example:

Result
patient_id       first_name       last_name        date_of_birth    admission_date  discharge_date  doctor_id
---------------  ---------------  ---------------  ---------------  --------------  --------------  ----------
2                Bob              Miller           1995-08-23       2024-02-15      2024-03-01      2

```sql
SELECT p.*
FROM patients p
INNER JOIN test_results tr ON p.patient_id=tr.patient_id
WHERE tr.test_date BETWEEN '2024-03-01' AND '2024-03-31';
```

**Output:**

<img width="1237" height="476" alt="image" src="https://github.com/user-attachments/assets/88f653a5-1f0d-4eaa-abf2-fb7346ab0e9f" />



## RESULT
Thus, the SQL queries to implement different types of joins have been executed successfully.
