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
--Write a SQL query to find the total amount of fruits with a unit type of 'LB'.

Note: Inventory attribute contains amount of fruits

Table: fruits

name        type
----------  ----------
id          INTEGER
name        TEXT
unit        TEXT
inventory   INTEGER
price       REAL
 

For example:

Result
total
----------
225

-- 

```sql
-- SELECT SUM(inventory) AS total
FROM fruits
WHERE unit='LB';
```

**Output:**

<img width="881" height="396" alt="image" src="https://github.com/user-attachments/assets/c171d200-e7f6-4226-aa69-37d740877b53" />


**Question 2**
---Write a SQL query to find the minimum purchase amount.

Sample table: orders

ord_no      purch_amt   ord_date    customer_id  salesman_id

----------  ----------  ----------  -----------  -----------

70001       150.5       2012-10-05  3005         5002

70009       270.65      2012-09-10  3001         5005

70002       65.26       2012-10-05  3002         5001

 

For example:

Result
MINIMUM
----------
65.26

-- 

```sql
-- SELECT MIN(purch_amt) AS MINIMUM
FROM orders;
```

**Output:**
<img width="815" height="412" alt="image" src="https://github.com/user-attachments/assets/79c935a6-2407-49b2-af0e-27723c81423c" />


**Question 3**
---
Write a SQL query to find the number of employees who are having the same age removing the duplicate values.

Sample table: employee

id

name

age

address

salary

1

Paul

32

California

20000

4

Mark

25

Richtown

65000

5

David

27

Texas

85000

 

For example:

Result
COUNT
----------
4


```sql
--SELECT COUNT(DISTINCT age)  AS COUNT
FROM employee;
```

**Output:**

<img width="842" height="436" alt="image" src="https://github.com/user-attachments/assets/cda45286-7eed-4df4-9914-e84a8fb6ea76" />


**Question 4**
---
Write a SQL Query to find how many medications are prescribed for each patient?

Sample table:MedicalRecords Table



For example:

Result
PatientID   AvgMedications
----------  --------------
4           5
6           1
7           1
8           3


```sql
-- SELECT PatientID, COUNT(*) AS AvgMedications
FROM MedicalRecords
GROUP BY PatientID;
```

**Output:**

<img width="852" height="682" alt="image" src="https://github.com/user-attachments/assets/0b83be3a-7c9e-46ee-a3ae-89f9217abf2b" />


**Question 5**
---
-- What is the average duration of insurance coverage for patients covered by each insurance company?

Sample table:Insurance Table

name               type
-----------------  ----------
InsuranceID        INTEGER
PatientID          INTEGER
InsuranceCompany   TEXT
PolicyNumber       TEXT
PolicyHolder       TEXT
StartDate          DATE
EndDate            DATE
For example:

Result
InsuranceCompany  AvgCoverageDurationDays
----------------  -----------------------
ABC Insurance     7.0
DEF Insurance     3.0
JKL Insurance     3.0
STU Insurance     3.0
VWX Insurance     3.0
XYZ Insurance     3.0
YZA Insurance     3.0


```
-- SELECT InsuranceCompany,
ROUND(AVG((julianday(EndDate) - julianday(StartDate))/365.25),1) AS AvgCoverageDurationDays
FROM Insurance
GROUP BY InsuranceCompany;
```

**Output:**

<img width="867" height="757" alt="image" src="https://github.com/user-attachments/assets/4ef8e532-7854-4912-a719-30e3754890e8" />


**Question 6**
---
-- How many male and female doctors are there in each medical specialty?

Sample table:Doctors Table



For example:

Result
Specialty          Gender    TotalDoctors
-----------------  --------  --------------
Cardiology         Male      1
Dermatology        Male      1
Gastroenterology   Female    4
Gastroenterology   Male      1
Pediatrics         Female    1
Pediatrics         Male      2


```sql
-- SELECT Specialty,Gender,COUNT(*) AS TotalDoctors
FROM Doctors
GROUP BY Specialty,Gender
ORDER BY Specialty,Gender;
```

**Output:**

<img width="837" height="757" alt="image" src="https://github.com/user-attachments/assets/9ad4e0cf-43ca-4587-993d-bfd42bf8e82d" />


**Question 7**
---
-- Write the SQL query that accomplishes the grouping of data by age intervals using the expression (age/5)5, calculates the minimum age for each group, and excludes groups where the minimum age is not less than 25.

Sample table: customer1



For example:

Result
age_group   MIN(age)
----------  ----------
20          22


```sql
-- SELECT (age/5)*5 AS age_group,
MIN(age) AS "MIN(age)"
FROM customer1
GROUP BY (age/5)*5
HAVING MIN(age)<25;
```

**Output:**

<img width="852" height="426" alt="image" src="https://github.com/user-attachments/assets/f1d1c25f-4c0d-4abc-a8cd-c2e99e7b7c80" />


**Question 8**
---
-- Write the SQL query that accomplishes the grouping of data by addresses, calculates the sum of salaries for each address, and excludes addresses where the total salary sum is not greater than 2000.

Sample table: customer1



For example:

Result
address     SUM(salary)
----------  -----------
Bhopal      8500
Hyderabad   4500
Indore      10000
Mumbai      6500


```sql
-- SELECT address,SUM(salary) AS "SUM(salary)"
FROM customer1
GROUP BY address
HAVING SUM(salary)>2000;
```

**Output:**

<img width="852" height="610" alt="image" src="https://github.com/user-attachments/assets/22ef9fa5-5e51-4d85-9007-d5a1842e7ed7" />


**Question 9**
---
-- Write the SQL query that accomplishes the grouping of data by joining date (jdate), calculates the maximum work hours for each date, and excludes dates where the maximum work hour is not greater than 12.

Sample table: employee1



For example:

Result
jdate       MAX(workhour)
----------  -------------
2004.0      15
2006.0      15


```sql
-- SELECT jdate,MAX(workhour) AS "MAX(workhour)"
FROM employee1
GROUP BY jdate
HAVING MAX(workhour)>12;
```

**Output:**

<img width="876" height="515" alt="image" src="https://github.com/user-attachments/assets/de8f42e0-fa50-48b1-9fc5-14e3d20a639e" />


**Question 10**
---
-- Write the SQL query that accomplishes the selection of product which has lowest price in each category from the "products" table and includes only those products where the minimum price is less than 10.

Sample table: products



For example:

Result
category_id  Price
-----------  ----------
3            7.5


```sql
-- SELECT category_id,
MIN(price) AS Price
FROM products
GROUP BY category_id
HAVING MIN(price)<10;
```

**Output:**
<img width="877" height="450" alt="image" src="https://github.com/user-attachments/assets/a499ff43-65f0-496e-9041-185476ceed01" />



## RESULT
Thus, the SQL queries to implement aggregate functions, GROUP BY, and HAVING clause have been executed successfully.
