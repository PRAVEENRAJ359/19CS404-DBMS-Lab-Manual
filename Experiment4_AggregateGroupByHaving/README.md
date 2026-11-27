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
--
-- <img width="1185" height="581" alt="image" src="https://github.com/user-attachments/assets/a1603a32-5d3a-4fa4-8867-ebb27a7c3391" />



```sql
--
select DoctorID,COUNT(AppointmentID) as TotalAppointments
from Appointments
group by DoctorID;
```

**Output:**

<img width="832" height="717" alt="image" src="https://github.com/user-attachments/assets/6f326820-0b68-493b-b049-729aa71ac338" />



**Question 2**
---
-- <img width="1117" height="602" alt="image" src="https://github.com/user-attachments/assets/63d997c4-9700-46a8-8dc3-a2582a630905" />


```sql
--
select Frequency,count(PrescriptionID) as TotalPrescriptions
from Prescriptions
group by Frequency
order by Frequency asc;
```

**Output:**

<img width="962" height="607" alt="image" src="https://github.com/user-attachments/assets/4c6e9679-26f6-497a-84bf-232121b2f028" />



**Question 3**
---
-- <img width="1080" height="590" alt="image" src="https://github.com/user-attachments/assets/fd522135-e34e-4487-acbd-69557529ca3a" />



```sql
--
select strftime("%Y" , ValidityPeriod) as ValidityYear,count(PatientID) as TotalPatients
from insurance 
group by ValidityYear
order by ValidityYear;
```

**Output:**

<img width="1087" height="480" alt="image" src="https://github.com/user-attachments/assets/141b605f-d411-4107-b55c-c56c75a1d029" />



**Question 4**
---
-- <img width="987" height="501" alt="image" src="https://github.com/user-attachments/assets/ba853eb2-1edd-41f2-9c14-7f64c0583480" />



```sql
--
select name,email,length(email) as min_email_length
from customer 
order by length(email) asc
limit 1;
```

**Output:**

<img width="1197" height="397" alt="image" src="https://github.com/user-attachments/assets/9e3fbc92-9ed4-4a20-9f82-f151ace8f3e4" />



**Question 5**
---
-- <img width="987" height="502" alt="image" src="https://github.com/user-attachments/assets/da9f483b-8d95-4b87-aba8-91e0a0fe724b" />



```sql
--
select count(*) as COUNT
from customer where city='Noida';

```

**Output:**

<img width="877" height="395" alt="image" src="https://github.com/user-attachments/assets/d5d8ced0-344a-445c-abc6-df91d4e6227c" />



**Question 6**
---
-- <img width="1117" height="506" alt="image" src="https://github.com/user-attachments/assets/78c6af53-ff75-4962-b114-b95913f65cd6" />



```sql
--
select count(*) as COUNT
from(
select age
from employee
group by age
having count(age)>=1
)
as duplicate_ages;
```

**Output:**

<img width="671" height="401" alt="image" src="https://github.com/user-attachments/assets/e160e24e-a33f-46e8-a4cb-c5ee9afd3724" />



**Question 7**
---
-- <img width="1142" height="537" alt="image" src="https://github.com/user-attachments/assets/44d1fa95-f9df-48cd-a847-553890b25b74" />



```sql
--
select count(*) as COUNT
from customer 
where city !='Noida';
```

**Output:**

<img width="1186" height="420" alt="image" src="https://github.com/user-attachments/assets/dae46d8c-bfd0-45e5-9251-785cfa4c5ec2" />



**Question 8**
---
-- <img width="1257" height="522" alt="image" src="https://github.com/user-attachments/assets/97cfee10-4cbd-4c27-b916-f994629e391d" />



```sql
--
select jdate,SUM(workhour)
from employee1
group by jdate
having sum(workhour)>40;

```

**Output:**

<img width="887" height="482" alt="image" src="https://github.com/user-attachments/assets/38bf67f9-7dfe-45ff-bda2-46092b006585" />



**Question 9**
---
-- <img width="1232" height="537" alt="image" src="https://github.com/user-attachments/assets/a45b39ef-b8f5-4271-bb44-8d2bc2c47a6b" />



```sql
--
select category_id,sum(price * category_id) as Revenue
from products
group by category_id 
having sum(price * category_id)>25;
```

**Output:**

<img width="732" height="522" alt="image" src="https://github.com/user-attachments/assets/e94c490a-3913-446a-9627-a97dff883071" />



**Question 10**
---
-- <img width="1187" height="462" alt="image" src="https://github.com/user-attachments/assets/70fb4e31-3846-4996-b6af-17b04622f3b7" />



```sql
--
select ((age/5) * 5) as age_group,MIN(salary)
from customer1
group by age_group
having MIN(salary)<2000;
```

**Output:**

<img width="1055" height="427" alt="image" src="https://github.com/user-attachments/assets/30f63a3a-f1a0-4be8-b085-655809521bd3" />

<img width="1011" height="122" alt="image" src="https://github.com/user-attachments/assets/fd64402c-d9cc-47f5-93c9-23b3fe039401" />



## RESULT
Thus, the SQL queries to implement aggregate functions, GROUP BY, and HAVING clause have been executed successfully.
