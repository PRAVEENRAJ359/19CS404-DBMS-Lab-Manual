# Experiment 5: Subqueries and Views

## AIM
To study and implement subqueries and views.

## THEORY

### Subqueries
A subquery is a query inside another SQL query and is embedded in:
- WHERE clause
- HAVING clause
- FROM clause

**Types:**
- **Single-row subquery**:
  Sub queries can also return more than one value. Such results should be made use along with the operators in and any.
- **Multiple-row subquery**:
  Here more than one subquery is used. These multiple sub queries are combined by means of ‘and’ & ‘or’ keywords.
- **Correlated subquery**:
  A subquery is evaluated once for the entire parent statement whereas a correlated Sub query is evaluated once per row processed by the parent statement.

**Example:**
```sql
SELECT * FROM employees
WHERE salary > (SELECT AVG(salary) FROM employees);
```
### Views
A view is a virtual table based on the result of an SQL SELECT query.
**Create View:**
```sql
CREATE VIEW view_name AS
SELECT column1, column2 FROM table_name WHERE condition;
```
**Drop View:**
```sql
DROP VIEW view_name;
```

**Question 1**
--
-- <img width="1260" height="532" alt="image" src="https://github.com/user-attachments/assets/82770a92-9437-457b-8f2a-35836cb8fb6a" />


```sql
--
SELECT name, city
FROM customer
WHERE city IN (
    SELECT city 
    FROM customer 
    WHERE id IN (3, 7)
);
```

**Output:**

<img width="1285" height="547" alt="image" src="https://github.com/user-attachments/assets/a6b170ec-187f-4a7f-843b-868d76ee5451" />


**Question 2**
---
-- <img width="1271" height="682" alt="image" src="https://github.com/user-attachments/assets/5a76692c-888b-414b-9933-3f4299806b34" />


```sql
--
SELECT *
FROM Employee
WHERE age < (
    SELECT AVG(age)
    FROM Employee
    WHERE income > 250000
);
```

**Output:**

<img width="1277" height="615" alt="image" src="https://github.com/user-attachments/assets/3b21284a-f4ee-4ceb-8d14-efcfcfba2de8" />


**Question 3**
---
-- <img width="1277" height="686" alt="image" src="https://github.com/user-attachments/assets/92911ea1-92e1-495d-83cc-5d3f478920a3" />


```sql
--
SELECT student_name, grade
FROM GRADES g
WHERE grade = (
    SELECT MIN(grade)
    FROM GRADES
    WHERE subject = g.subject
);
```

**Output:**

<img width="1265" height="432" alt="image" src="https://github.com/user-attachments/assets/1e5ff30f-d8e5-4941-a8a4-b1643ad1a30b" />


**Question 4**
---
-- <img width="1255" height="842" alt="image" src="https://github.com/user-attachments/assets/e23952b1-0dfa-48b0-887c-d736029b02eb" />


```sql
--
SELECT * 
FROM CUSTOMERS 
WHERE SALARY > 1500;
```

**Output:**

<img width="1285" height="700" alt="image" src="https://github.com/user-attachments/assets/1055dff8-88ed-4432-a09e-ab091765467c" />


**Question 5**
---
-- <img width="1261" height="432" alt="image" src="https://github.com/user-attachments/assets/8e331355-1b98-47a5-bd96-e073ac3ee42e" />


```sql
--
SELECT *
FROM GRADES g
WHERE grade = (
    SELECT MIN(grade)
    FROM GRADES
    WHERE subject = g.subject
);

```

**Output:**

<img width="1285" height="700" alt="image" src="https://github.com/user-attachments/assets/ea47b8fc-4c36-4e1c-9e77-59ad8dda1e47" />


**Question 6**
---
-- <img width="1252" height="586" alt="image" src="https://github.com/user-attachments/assets/7cbf1d99-a85f-4031-83b3-ee236592f5b5" />


```sql
--
SELECT id, name, city, email, phone
FROM customer
WHERE city <> (
    SELECT city
    FROM customer
    ORDER BY id DESC
    LIMIT 1
);
```

**Output:**

<img width="1281" height="582" alt="image" src="https://github.com/user-attachments/assets/addd5c1e-882d-45ed-9f0b-7aa5e7bbdbb4" />


**Question 7**
---
-- <img width="1262" height="762" alt="image" src="https://github.com/user-attachments/assets/4bb3a8b5-c5fb-4c52-8d26-caa8586f9250" />


```sql
--
SELECT o.ord_no AS ord_no,
       o.purch_amt,
       o.ord_date AS ord_date,
       o.customer_id,
       o.salesman_id
FROM orders o
JOIN salesman s
ON o.salesman_id = s.salesman_id
WHERE s.name = 'Paul Adam';
```

**Output:**

<img width="1285" height="475" alt="image" src="https://github.com/user-attachments/assets/636d1ab1-93b4-45ca-a5d7-9761490f804c" />


**Question 8**
---
-- <img width="1267" height="696" alt="image" src="https://github.com/user-attachments/assets/694a3ea6-7b37-4dc6-a9fd-a0a71304f9d2" />


```sql
--
SELECT commission
FROM salesman
WHERE salesman_id IN (
    SELECT salesman_id 
    FROM customer 
    WHERE city = 'Paris'
);

```

**Output:**

<img width="920" height="415" alt="image" src="https://github.com/user-attachments/assets/7c33247c-9a35-4f5b-999d-242afd22ae1e" />


**Question 9**
---
-- <img width="1251" height="727" alt="image" src="https://github.com/user-attachments/assets/464cd5b4-eaf2-4b76-afe0-1bdc12b53844" />


```sql
--
SELECT s.salesman_id, s.name
FROM salesman s
JOIN customer c ON s.salesman_id = c.salesman_id
GROUP BY s.salesman_id, s.name
HAVING COUNT(c.customer_id) > 1;
```

**Output:**

<img width="1047" height="560" alt="image" src="https://github.com/user-attachments/assets/6432ad71-de56-42d9-aff3-588521182524" />


**Question 10**
---
-- <img width="1215" height="632" alt="image" src="https://github.com/user-attachments/assets/ae6cb5a8-1d39-46d2-9a60-6ca567876631" />


```sql
--
SELECT 
    ord_no, 
    purch_amt, 
    ord_date, 
    customer_id, 
    salesman_id
FROM 
    ORDERS
WHERE 
    purch_amt > (
        SELECT AVG(purch_amt) 
        FROM ORDERS 
        WHERE ord_date = '2012-10-10'
    );
```

**Output:**

<img width="1277" height="540" alt="image" src="https://github.com/user-attachments/assets/04ccaa2b-1db9-4d69-a422-a74e8ffe0297" />



## RESULT
Thus, the SQL queries to implement aggregate functions, GROUP BY, and HAVING clause have been executed successfully.
