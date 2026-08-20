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
Insert the below data into the Customers table, allowing the City and ZipCode columns to take their default values.

CustomerID  Name          Address
----------  ------------  ----------
304         Peter Parker  Spider St      

Note: The City and ZipCode columns will use their default values.
 
For example:

Test	Result
SELECT CustomerID, Name, Address
FROM Customers;
CustomerID  Name          Address
----------  ------------  ----------
304         Peter Parker  Spider St


```sql
INSERT INTO Customers (CustomerID,Name,Address)
VALUES('304','Peter Parker','Spider St')
```

**Output:**

<img width="1212" height="397" alt="image" src="https://github.com/user-attachments/assets/b0c333d9-29df-45f0-8015-8ff5e0e4d2ee" />


**Question 2**
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
CREATE TABLE ProjectAssignments (
    AssignmentID INTEGER PRIMARY KEY,
    EmployeeID INTEGER,
    ProjectID INTEGER,
    AssignmentDate DATE NOT NULL,
    FOREIGN KEY (EmployeeID) REFERENCES Employees(EmployeeID)
    FOREIGN KEY (ProjectID) REFERENCES Projects(ProjectID)
    );
```

**Output:**

<img width="1217" height="362" alt="image" src="https://github.com/user-attachments/assets/75ccce4a-73a6-4717-b79a-b51e344bca55" />


**Question 3**
---
Create a table named Reviews with the following columns:

ReviewID as INTEGER
ProductID as INTEGER
Rating as REAL
ReviewText as TEXT
For example:

Test	Result
pragma table_info('Reviews');
cid         name        type        notnull     dflt_value  pk
----------  ----------  ----------  ----------  ----------  ----------
0           ReviewID    INTEGER     0                       0
1           ProductID   INTEGER     0                       0
2           Rating      REAL        0                       0
3           ReviewText  TEXT        0                       0


```sql
CREATE TABLE Reviews (
    ReviewID INTEGER,
    ProductID INTEGER,
    Rating REAL,
    ReviewText TEXT 
    );
```

**Output:**

<img width="1227" height="452" alt="image" src="https://github.com/user-attachments/assets/18d1a038-ea9f-4592-935c-fb641d5b1664" />


**Question 4**
---
Create a table named Members with the following columns:

MemberID as INTEGER
MemberName as TEXT
JoinDate as DATE
For example:

Test	Result
pragma table_info('Members');
cid         name        type        notnull     dflt_value  pk
----------  ----------  ----------  ----------  ----------  ----------
0           MemberID    INTEGER     0                       0
1           MemberName  TEXT        0                       0
2           JoinDate    DATE        0                       0


```sql
CREATE TABLE Members (
    MemberID INTEGER,
    MemberName TEXT,
    JoinDate DATE
);
```

**Output:**

<img width="1227" height="477" alt="image" src="https://github.com/user-attachments/assets/8f3718e4-c0a9-489c-8904-41484d5d4a28" />


**Question 5**
---
Create a table named Events with the following columns:

EventID as INTEGER
EventName as TEXT
EventDate as DATE
For example:

Test	Result
pragma table_info('Events');
cid         name        type        notnull     dflt_value  pk
----------  ----------  ----------  ----------  ----------  ----------
0           EventID     INTEGER     0                       0
1           EventName   TEXT        0                       0
2           EventDate   DATE        0                       0

```sql
CREATE TABLE Events (
    EventID INTEGER,
    EventName TEXT,
    EventDate DATE
);
```

**Output:**

<img width="1227" height="462" alt="image" src="https://github.com/user-attachments/assets/b6badc09-1210-49fc-b988-d4c56defd0ac" />


**Question 6**
---
Insert all products from Discontinued_products into Products.

Table attributes are ProductID, ProductName, Price, Stock

For example:

Test	Result
select * from Products;
ProductID   ProductName     Price       Stock
----------  --------------  ----------  ----------
101         Old Smartphone  199.99      0
102         Vintage Laptop  399.99      10
103         Classic Tablet  149.99      5


```sql
INSERT INTO Products (ProductID, ProductName, Price, Stock)
SELECT ProductID, ProductName, Price, Stock
FROM Discontinued_products;
```

**Output:**

<img width="1266" height="372" alt="image" src="https://github.com/user-attachments/assets/6392cc42-a106-45a8-9133-b6ac9d80b05c" />


**Question 7**
---
Write an SQL query to change the name of the column id to employee_id in the table employee.

 

 

 

 

For example:

Test	Result
pragma table_info('employee');
cid         name         type        notnull     dflt_value  pk
----------  -----------  ----------  ----------  ----------  ----------
0           employee_id  integer     0                       0
1           salary       number      0                       0


```sql
ALTER TABLE employee
RENAME COLUMN id TO employee_id;
```

**Output:**

<img width="1236" height="347" alt="image" src="https://github.com/user-attachments/assets/ad5049b0-5e52-412f-994a-126a4c31f1c6" />


**Question 8**
---
Create a new table named item with the following specifications and constraints:
item_id as TEXT and as primary key.
item_desc as TEXT.
rate as INTEGER.
icom_id as TEXT with a length of 4.
icom_id is a foreign key referencing com_id in the company table.
The foreign key should set NULL on updates and deletes.
item_desc and rate should not accept NULL.
For example:

Test	Result
INSERT INTO item VALUES("ITM5","Charlie Gold",700,"COM4");
UPDATE company SET com_id='COM5' WHERE com_id='COM4';
SELECT * FROM item;
item_id     item_desc     rate        icom_id
----------  ------------  ----------  ----------
ITM5        Charlie Gold  700


```sql
CREATE TABLE item (
     item_id TEXT PRIMARY KEY,
     item_desc TEXT NOT NULL,
     rate INTEGER NOT NULL,
     icom_id TEXT(4),
     FOREIGN KEY (icom_id) REFERENCES company(com_id)
      ON UPDATE SET NULL
      ON DELETE SET NULL
);
      
     
```

**Output:**

<img width="1231" height="446" alt="image" src="https://github.com/user-attachments/assets/452aba43-2549-4163-bad1-c9fb089782b3" />

**Question 9**
---
Create a table named Reviews with the following columns:

ReviewID as INTEGER
ProductID as INTEGER
Rating as REAL
ReviewText as TEXT
For example:

Test	Result
pragma table_info('Reviews');
cid         name        type        notnull     dflt_value  pk
----------  ----------  ----------  ----------  ----------  ----------
0           ReviewID    INTEGER     0                       0
1           ProductID   INTEGER     0                       0
2           Rating      REAL        0                       0
3           ReviewText  TEXT        0                       0

```sql
CREATE TABLE Reviews (
    ReviewID INTEGER,
    ProductID INTEGER,
    Rating REAL,
    ReviewText TEXT 
    );
```

**Output:**

<img width="1227" height="480" alt="image" src="https://github.com/user-attachments/assets/19d348bd-e795-45be-99bb-8cc529d875a4" />


**Question 10**
---
Write a SQL Query for inserting the below values in the table Customers

ID               NAME             AGE  ADDRESS     SALARY      
---------------  ---------------  ---  ----------  ----------  
1                Ramesh           32   Ahmedabad   2000
2                Khilan           25   Delhi       1500
3                Kaushik          23   Kota        2000
 

For example:

Test	Result
SELECT * FROM Customers;
ID          NAME        AGE         ADDRESS     SALARY
----------  ----------  ----------  ----------  ----------
1           Ramesh      32          Ahmedabad   2000
2           Khilan      25          Delhi       1500
3           Kaushik     23          Kota        2000


```sql
INSERT INTO Customers
VALUES('1','Ramesh','32','Ahmedabad','2000'),('2','Khilan','25','Delhi','1500'),('3','Kaushik','23','Kota','2000')
```

**Output:**

<img width="1230" height="392" alt="image" src="https://github.com/user-attachments/assets/d1edde4c-9163-4ae2-8b20-c02f86aba3b3" />



## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
