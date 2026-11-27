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
Write a SQL Query  to change the name of attribute "name" to "first_name"  and add mobilenumber as number ,DOB as Date in the table Companies. 

```sql
ALTER TABLE Companies RENAME COLUMN name TO first_name;
ALTER TABLE Companies ADD COLUMN mobilenumber number;
ALTER TABLE Companies ADD COLUMN DOB Date;
```

**Output:**

<img width="1228" height="453" alt="image" src="https://github.com/user-attachments/assets/a0529f00-8759-4bac-a2e4-a3548d971d9e" />


**Question 2**
---
Create a table named Orders with the following constraints:
OrderID as INTEGER should be the primary key.
OrderDate as DATE should be not NULL.
CustomerID as INTEGER should be a foreign key referencing Customers(CustomerID).

```sql
CREATE TABLE Orders(
OrderID INTEGER PRIMARY KEY,
OrderDate DATE NOT NULL,
CustomerID INTEGER,
FOREIGN KEY(CustomerID) REFERENCES Customers(CustomerID)
);
```

**Output:**

<img width="1222" height="363" alt="image" src="https://github.com/user-attachments/assets/73d80733-eb66-4061-9b0b-75c1b6ce373e" />

**Question 3**
---
Create a table named Customers with the following columns:

CustomerID as INTEGER
Name as TEXT
Email as TEXT
JoinDate as DATETIME
```sql
CREATE TABLE Customers(
CustomerID INTEGER,
Name TEXT,
Email TEXT,
JoinDate DATETIME );
```

**Output:**

<img width="1232" height="471" alt="image" src="https://github.com/user-attachments/assets/40f206f9-1bd6-4d7c-be5d-4cb205907908" />

**Question 4**
---
Insert all books from Out_of_print_books into Books

Table attributes are ISBN, Title, Author, Publisher, YearPublished
```sql
INSERT INTO Books SELECT* FROM Out_of_print_books;
```

**Output:**
<img width="1220" height="357" alt="image" src="https://github.com/user-attachments/assets/dff7f2fa-fa22-4c86-85f9-fa39aa564024" />


**Question 5**
---
Create a table named Department with the following constraints:
DepartmentID as INTEGER should be the primary key.
DepartmentName as TEXT should be unique and not NULL.
Location as TEXT.
```sql
CREATE TABLE Department(
DepartmentID INT PRIMARY KEY,
DepartmentName TEXT UNIQUE NOT NULL,
Location TEXT);
```

**Output:**

<img width="1206" height="352" alt="image" src="https://github.com/user-attachments/assets/08071592-3cbb-4897-a446-6a0bd0282a8d" />

**Question 6**
---
Write a SQL Query  to add attribute Date_of_joining as Date and rename the attribute job_title as Designation in the table 'Employees'


```sql
ALTER TABLE Employees ADD Date_of_joining Date;
ALTER TABLE Employees RENAME COLUMN job_title TO Designation;
```

**Output:**

<img width="1222" height="396" alt="image" src="https://github.com/user-attachments/assets/41a01186-ec28-41b1-a20f-ad53cd4d697d" />

**Question 7**
---
In the Products table, insert a record where some fields are NULL, another record where all fields are filled without any NULL values, and a third record where some fields are filled, and others are left as NULL.

ProductID   Name              Category    Price       Stock
----------  ---------------   ----------  ----------  ----------
106         Fitness Tracker   Wearables
107         Laptop            Electronics  999.99      50
108         Wireless Earbuds  Accessories              100
 
```sql
INSERT INTO Products (ProductID, Name, Category, Price, Stock)
VALUES(106,'Fitness Tracker','Wearables',NULL,NULL);

INSERT INTO Products (ProductID, Name, Category, Price, Stock)
VALUES(107,'Laptop','Electronic','999.99','50');

INSERT INTO Products (ProductID, Name, Category, Price, Stock)
VALUES(108, 'Wireless Earbud', 'Accessorie', NULL, '100');
```

**Output:**

<img width="1217" height="360" alt="image" src="https://github.com/user-attachments/assets/3bf34aac-b216-4c65-a501-46501a330cd0" />

**Question 8**
---
Create a table named Shipments with the following constraints:
ShipmentID as INTEGER should be the primary key.
ShipmentDate as DATE.
SupplierID as INTEGER should be a foreign key referencing Suppliers(SupplierID).
OrderID as INTEGER should be a foreign key referencing Orders(OrderID).

```sql
CREATE TABLE Shipments(
ShipmentID INT PRIMARY KEY,
ShipmentDate DATE,
SupplierID INT,
OrderID INT,
FOREIGN KEY(SupplierID) REFERENCES Suppliers(SupplierID),
FOREIGN KEY(OrderID) REFERENCES Orders(OrderID)
);
```

**Output:**

<img width="1221" height="301" alt="image" src="https://github.com/user-attachments/assets/6f914624-2de6-44c1-a119-e489d27deffd" />

**Question 9**
---
Insert the below data into the Employee table, allowing the Department and Salary columns to take their default values.

EmployeeID  Name         Position
----------  -----------  ----------
4           Emily White  Analyst

Note: The Department and Salary columns will use their default values.    

```sql
INSERT INTO Employee(EmployeeID,Name,Position)
VALUES(4,'Emily White','Analyst');
```

**Output:**

<img width="1222" height="387" alt="image" src="https://github.com/user-attachments/assets/10fdf62d-de6c-445e-a5b4-03fa38b027f4" />

**Question 10**
---
Create a new table named products with the following specifications:
product_id as INTEGER and primary key.
product_name as TEXT and not NULL.
list_price as DECIMAL (10, 2) and not NULL.
discount as DECIMAL (10, 2) with a default value of 0 and not NULL.
A CHECK constraint at the table level to ensure:
list_price is greater than or equal to discount
discount is greater than or equal to 0
list_price is greater than or equal to 0

```sql
CREATE TABLE products(
product_id INT PRIMARY KEY,
product_name TEXT NOT NULL,
list_price DECIMAL(10,2) NOT NULL,
discount DECIMAL(10,2) NOT NULL DEFAULT 0,
CONSTRAINT products CHECK (
list_price >=discount
AND discount >=0
AND list_price >=0)
);
```

**Output:**

<img width="1222" height="347" alt="image" src="https://github.com/user-attachments/assets/4628af7a-11a3-4b4b-b9ff-a494279f9be4" />

## Screenshot of Module 1 SEB Completion Grades

<img width="1037" height="76" alt="image" src="https://github.com/user-attachments/assets/d1299037-e98d-4759-8947-d73aaa7a7cfb" />

## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
