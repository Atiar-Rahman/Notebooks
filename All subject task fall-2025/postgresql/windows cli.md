তুমি যদি **PostgreSQL + Django/DRF** শিখতে চাও, তাহলে আমি সাজেস্ট করব **psql (CLI)** দিয়ে শেখা শুরু করো। এতে database ভিতর থেকে বুঝতে পারবে। পরে pgAdmin ব্যবহার করলে আরও সহজ লাগবে।

নিচে **Beginner → Advanced** roadmap দিলাম।

---

# Phase 1: PostgreSQL CLI Basics

## PostgreSQL এ Login

Linux

```bash
sudo -u postgres psql
```

অথবা

```bash
psql -U postgres
```

Prompt দেখাবে

```text
postgres=#
```

---

## সব Database দেখো

```sql
\l
```

অথবা

```sql
\list
```

Output

```text
Name
--------------------
postgres
template0
template1
```

---

## Database Create

```sql
CREATE DATABASE persondb;
```

---

## Database Delete

```sql
DROP DATABASE persondb;
```

⚠️ Connected থাকা অবস্থায় drop করা যায় না।

---

## Database Connect

```sql
\c persondb
```

Output

```text
You are now connected to database "persondb"
```

---

## Current Database

```sql
SELECT current_database();
```

Output

```text
persondb
```

---

## সব Table দেখো

```sql
\dt
```

---

## সব Relation দেখো

```sql
\d
```

---

## নির্দিষ্ট Table Structure

```sql
\d person
```

Output

```text
Column
-------------------
id
name
city
```

---

# Phase 2: Table

## Table Create

```sql
CREATE TABLE person(
    id INT,
    name VARCHAR(100),
    city VARCHAR(100)
);
```

---

## Table Delete

```sql
DROP TABLE person;
```

---

## Table Rename

```sql
ALTER TABLE person
RENAME TO people;
```

---

## সব Table

```sql
\dt
```

---

## Table Structure

```sql
\d people
```

---

# Phase 3: CRUD

CRUD মানে

- Create
    
- Read
    
- Update
    
- Delete
    

---

# CREATE (Insert)

একটি Record

```sql
INSERT INTO person(id,name,city)
VALUES
(1,'Atiar','Dhaka');
```

---

একাধিক Record

```sql
INSERT INTO person
VALUES
(2,'Rahim','Khulna'),
(3,'Karim','Rajshahi'),
(4,'Sakib','Sylhet');
```

---

# READ

সব Data

```sql
SELECT * FROM person;
```

---

শুধু একটি Column

```sql
SELECT name
FROM person;
```

---

দুইটি Column

```sql
SELECT name,city
FROM person;
```

---

# WHERE

```sql
SELECT *
FROM person
WHERE city='Dhaka';
```

---

```sql
SELECT *
FROM person
WHERE id=2;
```

---

Comparison

```sql
SELECT *
FROM person
WHERE id>2;
```

---

# ORDER BY

Ascending

```sql
SELECT *
FROM person
ORDER BY name ASC;
```

Descending

```sql
SELECT *
FROM person
ORDER BY id DESC;
```

---

# LIMIT

```sql
SELECT *
FROM person
LIMIT 2;
```

---

# OFFSET

```sql
SELECT *
FROM person
LIMIT 2
OFFSET 2;
```

---

# UPDATE

```sql
UPDATE person
SET city='Chittagong'
WHERE id=2;
```

---

একাধিক Column

```sql
UPDATE person
SET
name='Hasan',
city='Barisal'
WHERE id=3;
```

---

# DELETE

একটি Record

```sql
DELETE FROM person
WHERE id=2;
```

---

সব Record

```sql
DELETE FROM person;
```

---

Table Empty

```sql
TRUNCATE TABLE person;
```

---

# Phase 4: Data Types

```sql
CREATE TABLE employee(

id SERIAL PRIMARY KEY,

name VARCHAR(100),

salary NUMERIC(10,2),

age INT,

is_active BOOLEAN,

joining_date DATE

);
```

---

# Phase 5: Constraints

Primary Key

```sql
CREATE TABLE student(

id SERIAL PRIMARY KEY,

name VARCHAR(100)

);
```

---

Unique

```sql
email VARCHAR(100) UNIQUE
```

---

Not Null

```sql
name VARCHAR(100) NOT NULL
```

---

Default

```sql
status BOOLEAN DEFAULT TRUE
```

---

Check

```sql
age INT CHECK(age>=18)
```

---

# Phase 6: Foreign Key

Department

```sql
CREATE TABLE department(

id SERIAL PRIMARY KEY,

name VARCHAR(100)

);
```

Employee

```sql
CREATE TABLE employee(

id SERIAL PRIMARY KEY,

name VARCHAR(100),

department_id INT REFERENCES department(id)

);
```

---

# Phase 7: JOIN

Inner Join

```sql
SELECT employee.name,
department.name

FROM employee

INNER JOIN department

ON employee.department_id=department.id;
```

---

Left Join

```sql
SELECT *

FROM employee

LEFT JOIN department

ON employee.department_id=department.id;
```

---

# Phase 8: Aggregate Function

Count

```sql
SELECT COUNT(*)
FROM employee;
```

Average

```sql
SELECT AVG(salary)
FROM employee;
```

Maximum

```sql
SELECT MAX(salary)
FROM employee;
```

Minimum

```sql
SELECT MIN(salary)
FROM employee;
```

Sum

```sql
SELECT SUM(salary)
FROM employee;
```

---

# Phase 9: GROUP BY

```sql
SELECT department_id,
COUNT(*)

FROM employee

GROUP BY department_id;
```

---

# Phase 10: Index

```sql
CREATE INDEX idx_name

ON employee(name);
```

---

# Phase 11: Transaction

```sql
BEGIN;

UPDATE account

SET balance=balance-1000

WHERE id=1;

UPDATE account

SET balance=balance+1000

WHERE id=2;

COMMIT;
```

Rollback

```sql
ROLLBACK;
```

---

# psql CLI Cheat Sheet

|Command|কাজ|
|---|---|
|`\l`|সব database দেখো|
|`\c database_name`|Database connect|
|`SELECT current_database();`|বর্তমান database|
|`\dt`|সব table|
|`\d table_name`|Table structure|
|`\d`|সব relations|
|`\dn`|Schemas|
|`\du`|Users/Roles|
|`\df`|Functions|
|`\di`|Indexes|
|`\dv`|Views|
|`\timing`|Query execution time on/off|
|`\i file.sql`|SQL file execute|
|`\o output.txt`|Output file-এ save|
|`\conninfo`|Current connection info|
|`\password`|Password change|
|`\q`|Exit psql|
|`\?`|সব psql command|
|`\h`|SQL command help|

## Django/DRF-এর জন্য এরপর কী?

এই বেসিকগুলো শেষ হলে পরবর্তী ধাপ হবে:

1. Advanced `SELECT`
    
2. `LIKE`, `ILIKE`, `IN`, `BETWEEN`
    
3. `GROUP BY` + `HAVING`
    
4. সব ধরনের `JOIN`
    
5. Subquery
    
6. Common Table Expressions (CTE)
    
7. Window Functions
    
8. Views
    
9. Indexing ও `EXPLAIN ANALYZE`
    
10. Transactions ও Locking
    
11. PostgreSQL-এর JSON/JSONB
    
12. প্রতিটি SQL query-এর Django ORM সমতুল্য (`filter()`, `annotate()`, `select_related()`, `prefetch_related()` ইত্যাদি)
    

এই ক্রমে শিখলে PostgreSQL এবং Django ORM—দুটোই খুব শক্ত ভিত্তির উপর দাঁড়াবে।

-----
এগুলোই **Intermediate → Advanced PostgreSQL**-এর মূল বিষয়। বিশেষ করে Django/DRF developer হিসেবে এগুলো জানলে interview এবং production project—দুই ক্ষেত্রেই অনেক এগিয়ে থাকবে।

আমি নিচে **priority অনুযায়ী** সাজিয়ে দিচ্ছি।

---

# Phase 1: Advanced SELECT (⭐⭐⭐⭐⭐)

এটা সবচেয়ে গুরুত্বপূর্ণ।

ধরো table:

```sql
CREATE TABLE employees (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100),
    age INT,
    salary NUMERIC,
    department VARCHAR(50),
    city VARCHAR(50)
);
```

## DISTINCT

Duplicate remove

```sql
SELECT DISTINCT city
FROM employees;
```

Django

```python
Employee.objects.values("city").distinct()
```

---

## Alias

```sql
SELECT
name AS employee_name,
salary AS employee_salary
FROM employees;
```

Django

```python
Employee.objects.values(
employee_name=F("name"),
employee_salary=F("salary")
)
```

---

# Phase 2: LIKE / ILIKE / IN / BETWEEN (⭐⭐⭐⭐⭐)

## LIKE

Starts With

```sql
SELECT *
FROM employees
WHERE name LIKE 'A%';
```

Ends With

```sql
SELECT *
FROM employees
WHERE name LIKE '%n';
```

Contains

```sql
SELECT *
FROM employees
WHERE name LIKE '%ti%';
```

Django

```python
Employee.objects.filter(name__startswith="A")
Employee.objects.filter(name__endswith="n")
Employee.objects.filter(name__contains="ti")
```

---

## ILIKE

Case insensitive

```sql
SELECT *
FROM employees
WHERE name ILIKE 'atiar';
```

Django

```python
Employee.objects.filter(name__iexact="atiar")
```

---

## IN

```sql
SELECT *
FROM employees
WHERE city IN ('Dhaka','Khulna');
```

Django

```python
Employee.objects.filter(
city__in=["Dhaka","Khulna"]
)
```

---

## BETWEEN

```sql
SELECT *
FROM employees
WHERE salary BETWEEN 20000 AND 50000;
```

Django

```python
Employee.objects.filter(
salary__range=(20000,50000)
)
```

---

# Phase 3: GROUP BY + HAVING (⭐⭐⭐⭐⭐)

```sql
SELECT
department,
COUNT(*)

FROM employees

GROUP BY department;
```

Django

```python
Employee.objects.values(
"department"
).annotate(
total=Count("id")
)
```

---

HAVING

```sql
SELECT
department,
COUNT(*)

FROM employees

GROUP BY department

HAVING COUNT(*)>5;
```

Django

```python
Employee.objects.values(
"department"
).annotate(
total=Count("id")
).filter(total__gt=5)
```

---

# Phase 4: JOIN (⭐⭐⭐⭐⭐)

Most Important

- INNER JOIN
    
- LEFT JOIN
    
- RIGHT JOIN
    
- FULL JOIN
    
- SELF JOIN
    
- CROSS JOIN
    

Example

```sql
SELECT
employee.name,
department.name

FROM employee

INNER JOIN department

ON employee.department_id=department.id;
```

Django

```python
Employee.objects.select_related(
"department"
)
```

---

Many To Many

```python
Book.objects.prefetch_related(
"authors"
)
```

---

# Phase 5: Subquery (⭐⭐⭐⭐)

Highest Salary

```sql
SELECT *

FROM employees

WHERE salary=(

SELECT MAX(salary)

FROM employees

);
```

Django

```python
Subquery()

OuterRef()
```

---

# Phase 6: CTE (⭐⭐⭐⭐)

```sql
WITH high_salary AS (

SELECT *

FROM employees

WHERE salary>50000

)

SELECT *

FROM high_salary;
```

Django

সরাসরি ORM-এ CTE-এর support সীমিত। জটিল CTE-এর জন্য সাধারণত Raw SQL বা third-party package ব্যবহার করা হয়।

---

# Phase 7: Window Function (⭐⭐⭐⭐)

Ranking

```sql
SELECT

name,

salary,

RANK() OVER(

ORDER BY salary DESC

)

FROM employees;
```

Django

```python
Window()

Rank()
```

---

# Phase 8: Views (⭐⭐⭐⭐)

```sql
CREATE VIEW employee_view AS

SELECT

name,

salary

FROM employees;
```

Query

```sql
SELECT *

FROM employee_view;
```

---

# Phase 9: Index (⭐⭐⭐⭐⭐)

```sql
CREATE INDEX idx_name

ON employees(name);
```

Check Query

```sql
EXPLAIN ANALYZE

SELECT *

FROM employees

WHERE name='Atiar';
```

Django

```python
class Meta:

    indexes=[
        models.Index(fields=["name"])
    ]
```

---

# Phase 10: Transactions (⭐⭐⭐⭐⭐)

```sql
BEGIN;
```

```sql
UPDATE account

SET balance=balance-500

WHERE id=1;
```

```sql
UPDATE account

SET balance=balance+500

WHERE id=2;
```

```sql
COMMIT;
```

Rollback

```sql
ROLLBACK;
```

Django

```python
from django.db import transaction

with transaction.atomic():
    ...
```

---

# Phase 11: Locking (⭐⭐⭐⭐)

```sql
SELECT *

FROM account

FOR UPDATE;
```

Django

```python
Account.objects.select_for_update()
```

---

# Phase 12: JSONB (⭐⭐⭐⭐⭐)

Create

```sql
CREATE TABLE products(

id SERIAL PRIMARY KEY,

details JSONB

);
```

Insert

```sql
INSERT INTO products(details)

VALUES(

'{

"color":"Black",

"ram":"16GB"

}'

);
```

Query

```sql
SELECT *

FROM products

WHERE details->>'color'='Black';
```

Django

```python
models.JSONField()
```

```python
Product.objects.filter(
details__color="Black"
)
```

---

# Phase 13: ORM Mapping (সবচেয়ে গুরুত্বপূর্ণ)

|SQL|Django ORM|
|---|---|
|`SELECT *`|`Model.objects.all()`|
|`WHERE`|`filter()`|
|`LIMIT`|`[:10]`|
|`ORDER BY`|`order_by()`|
|`COUNT()`|`count()`|
|`GROUP BY`|`values().annotate()`|
|`HAVING`|`annotate().filter()`|
|`JOIN`|`select_related()`|
|Many-to-Many JOIN|`prefetch_related()`|
|`INSERT`|`create()`|
|`UPDATE`|`update()`|
|`DELETE`|`delete()`|
|`MAX/MIN/AVG/SUM`|`aggregate()`|
|`IN`|`__in`|
|`LIKE`|`__contains`, `__startswith`, `__endswith`|
|`ILIKE`|`__icontains`, `__istartswith`, `__iendswith`, `__iexact`|
|`BETWEEN`|`__range`|
|`FOR UPDATE`|`select_for_update()`|

---

# Django Backend Developer-এর জন্য শেখার অগ্রাধিকার

১. ⭐⭐⭐⭐⭐ CRUD + Advanced SELECT  
২. ⭐⭐⭐⭐⭐ WHERE, LIKE, ILIKE, IN, BETWEEN  
৩. ⭐⭐⭐⭐⭐ GROUP BY + HAVING + Aggregate Functions  
৪. ⭐⭐⭐⭐⭐ JOIN (INNER, LEFT, RIGHT)  
৫. ⭐⭐⭐⭐⭐ Index + `EXPLAIN ANALYZE`  
৬. ⭐⭐⭐⭐⭐ Transactions + Locking  
৭. ⭐⭐⭐⭐⭐ Django ORM Mapping  
৮. ⭐⭐⭐⭐ Subquery  
৯. ⭐⭐⭐⭐ CTE  
১০. ⭐⭐⭐⭐ Window Functions  
১১. ⭐⭐⭐⭐ Views  
১২. ⭐⭐⭐⭐ JSON/JSONB

**আমার পরামর্শ:** যেহেতু তুমি Django/DRF নিয়ে সিরিয়াস, তাই প্রতিটি SQL topic শেখার পর সঙ্গে সঙ্গে একই কাজ Django ORM দিয়ে করে দেখো। এতে interview-তে যদি কেউ জিজ্ঞেস করে, _"এই ORM query-এর SQL কী?"_ বা _"এই SQL-এর ORM কী?"_—দুটোরই উত্তর দিতে পারবে। এই দক্ষতা একজন Django backend developer-এর জন্য খুবই মূল্যবান।


---------
যদি প্রশ্নটি **"PostgreSQL এত ভালো হলে এর drawback কী?"** হয়, তাহলে উত্তর হলো—প্রতিটি database-এরই সুবিধা ও অসুবিধা আছে।

## PostgreSQL-এর Drawbacks

### 1. শেখা একটু কঠিন

MySQL-এর তুলনায় PostgreSQL-এ feature বেশি, তাই নতুনদের কাছে কিছুটা complex লাগতে পারে।

উদাহরণ:

- Window Functions
    
- CTE
    
- JSONB
    
- Partitioning
    
- Extensions
    

---

### 2. Configuration বেশি

Production-এ ভালো performance-এর জন্য কিছু configuration tune করতে হয়।

যেমন:

- `shared_buffers`
    
- `work_mem`
    
- `max_connections`
    

---

### 3. Simple project-এর জন্য Overkill হতে পারে

যদি শুধু একটি ছোট blog বা todo app বানাও, তাহলে PostgreSQL-এর সব feature ব্যবহারই নাও করতে পারো।

---

### 4. Memory Usage

MySQL-এর তুলনায় কিছু ক্ষেত্রে PostgreSQL একটু বেশি RAM ব্যবহার করতে পারে, যদিও আধুনিক server-এর জন্য এটি সাধারণত সমস্যা নয়।

---

### 5. Administration

Backup, replication, tuning ইত্যাদি শিখতে কিছুটা সময় লাগে।

---

# তাহলে সবাই PostgreSQL কেন ব্যবহার করে?

কারণ এর সুবিধাগুলো drawbacks-এর চেয়ে অনেক বেশি।

- ✅ ACID Compliance
    
- ✅ Strong Data Integrity
    
- ✅ Excellent JOIN Performance
    
- ✅ Advanced SQL Features
    
- ✅ JSONB Support
    
- ✅ Full Text Search
    
- ✅ Indexing Options
    
- ✅ Scalability
    
- ✅ Open Source
    

---

# Django-এর জন্য কি কোনো Drawback আছে?

**প্রায় নেই।** বরং Django-এর official documentation-এও PostgreSQL-কে সবচেয়ে feature-rich relational database হিসেবে ধরা হয়।

---

# তোমার ক্ষেত্রে

তুমি যেহেতু:

- Django
    
- DRF
    
- Job Portal
    
- Authentication
    
- Production Backend
    

শিখছ, তাই **PostgreSQL-এর drawbacks নিয়ে এখন চিন্তা করার দরকার নেই।**

এটি শেখার জন্য যে অতিরিক্ত সময় দেবে, তা ভবিষ্যতে production project এবং interview—দুই জায়গাতেই কাজে লাগবে।

**আমার পরামর্শ:** PostgreSQL-কে primary database হিসেবে শিখো। পরে প্রয়োজনে MySQL এবং MongoDB শিখলে বিভিন্ন ধরনের project-এ কাজ করার সক্ষমতা তৈরি হবে।

--------
PostgreSQL-এ **Data Type** নির্ধারণ করে একটি column কী ধরনের data সংরক্ষণ করবে। সঠিক data type নির্বাচন করলে database আরও efficient, secure এবং fast হয়।

---

# PostgreSQL Data Types

## 1. Numeric Data Types

সংখ্যা সংরক্ষণের জন্য।

|Data Type|Description|Example|
|---|---|---|
|`SMALLINT`|ছোট integer (-32,768 থেকে 32,767)|`20`|
|`INTEGER` / `INT`|সাধারণ integer|`100`|
|`BIGINT`|অনেক বড় integer|`1234567890123`|
|`SERIAL`|Auto Increment Integer|`1,2,3...`|
|`BIGSERIAL`|Auto Increment Big Integer|`100000000...`|
|`NUMERIC(p,s)`|নির্ভুল decimal|`99.99`|
|`REAL`|Single precision float|`12.5`|
|`DOUBLE PRECISION`|Double precision float|`12.56789`|

### Example

```sql
CREATE TABLE employee(
    id SERIAL PRIMARY KEY,
    age INT,
    salary NUMERIC(10,2),
    height REAL
);
```

---

# 2. Character Data Types

Text সংরক্ষণের জন্য।

|Data Type|Description|
|---|---|
|`CHAR(n)`|Fixed length|
|`VARCHAR(n)`|Variable length|
|`TEXT`|Unlimited text|

### Example

```sql
CREATE TABLE person(
    name VARCHAR(100),
    email VARCHAR(255),
    bio TEXT
);
```

---

## CHAR vs VARCHAR vs TEXT

```sql
code CHAR(5)
```

Save:

```text
ABC
```

Database-এ হবে

```text
ABC··
```

(5 character পূরণ করবে)

---

```sql
name VARCHAR(100)
```

Save

```text
Atiar
```

শুধু যতটুকু দরকার ততটুকুই store হবে।

---

```sql
description TEXT
```

Unlimited text

---

# 3. Boolean

```sql
is_active BOOLEAN
```

Value

```text
TRUE
FALSE
```

Example

```sql
CREATE TABLE users(
    is_verified BOOLEAN DEFAULT FALSE
);
```

---

# 4. Date & Time

|Type|Example|
|---|---|
|`DATE`|2026-07-01|
|`TIME`|10:30:00|
|`TIMESTAMP`|2026-07-01 10:30:00|
|`TIMESTAMPTZ`|Timezone সহ timestamp|
|`INTERVAL`|2 days|

Example

```sql
CREATE TABLE orders(
    order_date DATE,
    created_at TIMESTAMP,
    updated_at TIMESTAMPTZ
);
```

---

# 5. UUID

```sql
id UUID
```

Example

```text
550e8400-e29b-41d4-a716-446655440000
```

---

# 6. JSON

```sql
details JSON
```

Example

```json
{
  "color":"Black",
  "ram":"16GB"
}
```

---

# 7. JSONB

সবচেয়ে জনপ্রিয়।

```sql
details JSONB
```

Example

```json
{
  "brand":"Dell",
  "ram":"16GB"
}
```

JSONB indexing support করে এবং query দ্রুত হয়।

---

# 8. Array

```sql
skills TEXT[]
```

Example

```text
{"Python","Django","React"}
```

Insert

```sql
INSERT INTO employee(skills)
VALUES
('{"Python","Django"}');
```

---

# 9. ENUM

```sql
CREATE TYPE gender AS ENUM(
'Male',
'Female',
'Other'
);
```

Table

```sql
CREATE TABLE users(
    gender gender
);
```

---

# 10. Binary

```sql
BYTEA
```

Image বা Binary data সংরক্ষণে ব্যবহৃত হয়।

---

# 11. Network

|Type|Example|
|---|---|
|`INET`|192.168.1.1|
|`CIDR`|192.168.1.0/24|
|`MACADDR`|08:00:2b:01:02:03|

---

# 12. Money

```sql
price MONEY
```

বর্তমানে অনেক developer এর পরিবর্তে `NUMERIC(10,2)` ব্যবহার করেন।

---

# 13. XML

```sql
data XML
```

---

# Django ORM Mapping

|PostgreSQL|Django Model|
|---|---|
|`SERIAL`|`AutoField`|
|`BIGSERIAL`|`BigAutoField`|
|`INT`|`IntegerField`|
|`BIGINT`|`BigIntegerField`|
|`VARCHAR`|`CharField`|
|`TEXT`|`TextField`|
|`BOOLEAN`|`BooleanField`|
|`DATE`|`DateField`|
|`TIME`|`TimeField`|
|`TIMESTAMP`|`DateTimeField`|
|`NUMERIC`|`DecimalField`|
|`REAL`|`FloatField`|
|`UUID`|`UUIDField`|
|`JSONB`|`JSONField`|

---

# Django Project-এ সবচেয়ে বেশি ব্যবহৃত Data Types

এই ১০টি সবচেয়ে গুরুত্বপূর্ণ:

```sql
SERIAL
BIGSERIAL
VARCHAR
TEXT
INTEGER
BOOLEAN
DATE
TIMESTAMP
NUMERIC
JSONB
```

---

# Interview-তে সবচেয়ে বেশি জিজ্ঞাসা করা হয়

1. `CHAR` vs `VARCHAR` vs `TEXT`
    
2. `SERIAL` vs `IDENTITY`
    
3. `NUMERIC` vs `REAL` vs `DOUBLE PRECISION`
    
4. `DATE` vs `TIMESTAMP` vs `TIMESTAMPTZ`
    
5. `JSON` vs `JSONB`
    
6. `UUID` vs `SERIAL`
    
7. `VARCHAR(255)` কেন বেশি ব্যবহার করা হয়?
    
8. `BOOLEAN DEFAULT TRUE/FALSE`
    
9. `DECIMAL/NUMERIC` কেন টাকা (price, salary) সংরক্ষণে ব্যবহার করা হয়?
    
10. `TEXT` এবং `VARCHAR`-এর পার্থক্য
    

**Django/DRF developer হিসেবে এগুলো ভালোভাবে জানলেই বাস্তব project এবং interview—দুই ক্ষেত্রেই শক্ত ভিত্তি তৈরি হবে।**


------------

Database Design-এর সবচেয়ে গুরুত্বপূর্ণ topic হলো **Keys**। Django-এর `ForeignKey`, `OneToOneField`, `ManyToManyField` ঠিকমতো বুঝতে হলে database keys ভালোভাবে বুঝতে হবে।

---

# Database Keys

Database-এ প্রধানত এই keys গুলো বেশি ব্যবহৃত হয়:

1. Primary Key (PK)
    
2. Foreign Key (FK)
    
3. Unique Key
    
4. Composite Key
    
5. Candidate Key
    
6. Alternate Key
    
7. Super Key
    
8. Natural Key
    
9. Surrogate Key
    

---

# 1. Primary Key (PK) ⭐⭐⭐⭐⭐

একটি row-কে **uniqueভাবে identify** করে।

বৈশিষ্ট্য:

- Unique হতে হবে
    
- NULL হতে পারবে না
    
- একটি table-এ মাত্র ১টি Primary Key থাকে
    

Example

```sql
CREATE TABLE students(
    id SERIAL PRIMARY KEY,
    name VARCHAR(100)
);
```

Data

|id|name|
|---|---|
|1|Atiar|
|2|Rahim|

এখানে `id` হলো Primary Key।

### Django

```python
class Student(models.Model):
    name = models.CharField(max_length=100)
```

Django নিজেই

```python
id = models.BigAutoField(primary_key=True)
```

তৈরি করে।

---

# 2. Foreign Key (FK) ⭐⭐⭐⭐⭐

একটি table-এর Primary Key অন্য table-এ reference হিসেবে ব্যবহার করা।

Example

Department

```sql
CREATE TABLE departments(
    id SERIAL PRIMARY KEY,
    name VARCHAR(100)
);
```

Employee

```sql
CREATE TABLE employees(
    id SERIAL PRIMARY KEY,
    name VARCHAR(100),
    department_id INT REFERENCES departments(id)
);
```

Data

Departments

|id|name|
|---|---|
|1|IT|
|2|HR|

Employees

|id|name|department_id|
|---|---|---|
|1|Atiar|1|
|2|Rahim|2|

এখানে `department_id` হলো Foreign Key।

### Django

```python
department = models.ForeignKey(
    Department,
    on_delete=models.CASCADE
)
```

---

# 3. Unique Key ⭐⭐⭐⭐⭐

Duplicate value রাখা যাবে না।

```sql
CREATE TABLE users(
    id SERIAL PRIMARY KEY,
    email VARCHAR(255) UNIQUE
);
```

Allowed

```
a@gmail.com
b@gmail.com
```

Not Allowed

```
a@gmail.com
a@gmail.com
```

### Django

```python
email = models.EmailField(unique=True)
```

---

# 4. Composite Key ⭐⭐⭐⭐

দুই বা তার বেশি column একসাথে unique।

Example

Student + Course

```sql
PRIMARY KEY(student_id,course_id)
```

একই student একই course দুইবার নিতে পারবে না।

PostgreSQL

```sql
CREATE TABLE enrollments(
    student_id INT,
    course_id INT,
    PRIMARY KEY(student_id,course_id)
);
```

### Django

Django composite primary key সরাসরি support করে না।

সাধারণত

```python
class Meta:
    constraints = [
        models.UniqueConstraint(
            fields=["student","course"],
            name="unique_enrollment"
        )
    ]
```

---

# 5. Candidate Key ⭐⭐⭐

যে column Primary Key হতে পারে।

Example

|id|email|phone|
|---|---|---|

তিনটিই unique।

Primary Key করা হলো

```
id
```

তাহলে

Candidate Keys

- id
    
- email
    
- phone
    

---

# 6. Alternate Key ⭐⭐⭐

Candidate Key যেটা Primary Key হয়নি।

Example

Primary Key

```
id
```

Alternate Key

```
email
phone
```

---

# 7. Super Key ⭐⭐⭐

যেকোনো column-এর combination যা unique।

Example

```
id
```

এটিও Super Key

```
(id,name)
```

এটিও Super Key

```
(id,email)
```

কারণ `id` একাই unique।

---

# 8. Natural Key ⭐⭐⭐

Real-world data দিয়ে identify করা।

Example

```
NID Number
Passport Number
Email
```

---

# 9. Surrogate Key ⭐⭐⭐⭐⭐

Artificial key।

Example

```sql
id SERIAL PRIMARY KEY
```

এটি business data নয়।

শুধু identification-এর জন্য।

Django default

```python
id
```

এটাই Surrogate Key।

---

# Primary Key vs Unique Key

|Primary Key|Unique Key|
|---|---|
|১টি|একাধিক হতে পারে|
|NULL না|PostgreSQL-এ NULL রাখা যায় (একাধিক NULL-ও সম্ভব)|
|Record identify করে|Duplicate prevent করে|

Example

```sql
CREATE TABLE users(
    id SERIAL PRIMARY KEY,
    email VARCHAR(100) UNIQUE
);
```

---

# Primary Key vs Foreign Key

|Primary|Foreign|
|---|---|
|নিজের table identify করে|অন্য table reference করে|
|Unique|Duplicate হতে পারে|
|NULL নয়|NULL হতে পারে (যদি constraint না থাকে)|

---

# Foreign Key Actions

সবচেয়ে গুরুত্বপূর্ণ interview topic।

```sql
REFERENCES departments(id)
ON DELETE CASCADE
```

Options

### CASCADE

Parent delete

↓

Child delete

---

### SET NULL

Parent delete

↓

Foreign Key NULL

---

### RESTRICT

Delete করতে দিবে না।

---

### NO ACTION

Constraint check করবে।

---

### SET DEFAULT

Default value বসাবে।

---

# Django Mapping

|SQL|Django|
|---|---|
|PRIMARY KEY|`primary_key=True`|
|FOREIGN KEY|`ForeignKey()`|
|UNIQUE|`unique=True`|
|COMPOSITE UNIQUE|`UniqueConstraint()`|
|CASCADE|`on_delete=models.CASCADE`|
|SET NULL|`on_delete=models.SET_NULL`|
|PROTECT|`on_delete=models.PROTECT`|
|RESTRICT|`on_delete=models.RESTRICT`|
|SET DEFAULT|`on_delete=models.SET_DEFAULT`|

---

# Interview Priority (Django Developer)

⭐⭐⭐⭐⭐ অবশ্যই জানতে হবে:

- Primary Key
    
- Foreign Key
    
- Unique Key
    
- Composite Key (বা `UniqueConstraint`)
    
- Surrogate Key
    
- `on_delete` behavior (`CASCADE`, `SET_NULL`, `PROTECT`, `RESTRICT`)
    

⭐⭐⭐ ধারণা থাকলেই যথেষ্ট:

- Candidate Key
    
- Alternate Key
    
- Super Key
    
- Natural Key
    

## Django Developer হিসেবে সবচেয়ে গুরুত্বপূর্ণ

বাস্তব Django/DRF project-এ তুমি প্রতিদিন যেগুলো ব্যবহার করবে:

- `PRIMARY KEY`
    
- `FOREIGN KEY`
    
- `UNIQUE`
    
- `UNIQUE CONSTRAINT`
    
- `FOREIGN KEY`-এর `ON DELETE` behavior
    
- One-to-One, One-to-Many, Many-to-Many relationships
    

এই বিষয়গুলো ভালোভাবে বুঝতে পারলে database design এবং Django model design—দুটোই অনেক সহজ হয়ে যাবে।

----------------

যদি তুমি PostgreSQL-এর **CONCAT এবং string methods** বলতে চাও, তাহলে নিচে **Beginner → Advanced** সব গুরুত্বপূর্ণ function দিলাম।

---

# 1. CONCAT()

একাধিক string একসাথে যোগ করে।

```sql
SELECT CONCAT('Atiar', ' ', 'Rahman');
```

Output

```
Atiar Rahman
```

---

## Multiple Values

```sql
SELECT CONCAT(first_name, ' ', last_name)
FROM employees;
```

Output

|first_name|last_name|Result|
|---|---|---|
|Atiar|Rahman|Atiar Rahman|

---

# 2. CONCAT_WS()

WS = With Separator

```sql
SELECT CONCAT_WS('-', '2026', '07', '01');
```

Output

```
2026-07-01
```

Another Example

```sql
SELECT CONCAT_WS(', ', city, country);
```

Output

```
Dhaka, Bangladesh
```

---

# 3. ||

এটাও concatenate operator।

```sql
SELECT 'Hello' || ' World';
```

Output

```
Hello World
```

Example

```sql
SELECT first_name || ' ' || last_name
FROM employees;
```

---

# 4. LOWER()

সব ছোট হাতের।

```sql
SELECT LOWER('ATIAR');
```

Output

```
atiar
```

---

# 5. UPPER()

```sql
SELECT UPPER('atiar');
```

Output

```
ATIAR
```

---

# 6. INITCAP()

প্রতিটি word-এর প্রথম letter capital।

```sql
SELECT INITCAP('atiar rahman');
```

Output

```
Atiar Rahman
```

---

# 7. LENGTH()

Character count

```sql
SELECT LENGTH('Bangladesh');
```

Output

```
10
```

---

# 8. CHAR_LENGTH()

```sql
SELECT CHAR_LENGTH('Hello');
```

---

# 9. TRIM()

Space remove

```sql
SELECT TRIM('   Atiar   ');
```

Output

```
Atiar
```

---

# 10. LTRIM()

Left side remove

```sql
SELECT LTRIM('   Hello');
```

---

# 11. RTRIM()

Right side remove

```sql
SELECT RTRIM('Hello     ');
```

---

# 12. REPLACE()

```sql
SELECT REPLACE(
'Hello World',
'World',
'Bangladesh'
);
```

Output

```
Hello Bangladesh
```

---

# 13. SUBSTRING()

```sql
SELECT SUBSTRING(
'Bangladesh',
1,
4
);
```

Output

```
Bang
```

---

# 14. LEFT()

```sql
SELECT LEFT(
'Bangladesh',
4
);
```

Output

```
Bang
```

---

# 15. RIGHT()

```sql
SELECT RIGHT(
'Bangladesh',
4
);
```

Output

```
desh
```

---

# 16. POSITION()

```sql
SELECT POSITION(
'a'
IN
'Bangladesh'
);
```

Output

```
2
```

---

# 17. SPLIT_PART()

```sql
SELECT SPLIT_PART(
'atiar@gmail.com',
'@',
1
);
```

Output

```
atiar
```

```sql
SELECT SPLIT_PART(
'atiar@gmail.com',
'@',
2
);
```

Output

```
gmail.com
```

---

# 18. REPEAT()

```sql
SELECT REPEAT(
'*',
10
);
```

Output

```
**********
```

---

# 19. REVERSE()

```sql
SELECT REVERSE(
'Atiar'
);
```

Output

```
raitA
```

---

# 20. LPAD()

```sql
SELECT LPAD(
'25',
5,
'0'
);
```

Output

```
00025
```

---

# 21. RPAD()

```sql
SELECT RPAD(
'25',
5,
'0'
);
```

Output

```
25000
```

---

# 22. ASCII()

```sql
SELECT ASCII('A');
```

Output

```
65
```

---

# 23. CHR()

```sql
SELECT CHR(65);
```

Output

```
A
```

---

# 24. FORMAT()

```sql
SELECT FORMAT(
'Hello %s',
'Atiar'
);
```

Output

```
Hello Atiar
```

---

# 25. MD5()

```sql
SELECT MD5('password');
```

Output

```
5f4dcc3b5aa765d61d8327deb882cf99
```

> **নোট:** `MD5()` শুধু শেখার জন্য। Password hashing-এর জন্য এটি ব্যবহার করা উচিত নয়। Production-এ Django নিজস্ব password hashing ব্যবহার করে।

---

# Practical Example

Table

```sql
employees
```

|first_name|last_name|
|---|---|
|Atiar|Rahman|

Query

```sql
SELECT

UPPER(first_name),

LOWER(last_name),

CONCAT(first_name,' ',last_name),

LENGTH(first_name)

FROM employees;
```

Output

|UPPER|LOWER|CONCAT|LENGTH|
|---|---|---|---|
|ATIAR|rahman|Atiar Rahman|6|

---

# Django ORM Equivalent

|PostgreSQL|Django ORM|
|---|---|
|`CONCAT()`|`Concat()`|
|`UPPER()`|`Upper()`|
|`LOWER()`|`Lower()`|
|`LENGTH()`|`Length()`|
|`SUBSTRING()`|`Substr()`|
|`TRIM()`|`Trim()`|
|`REPLACE()`|`Replace()`|
|`LEFT()` / `RIGHT()`|`Left()` / `Right()` (বা `Substr()`)|

উদাহরণ:

```python
from django.db.models import Value
from django.db.models.functions import Concat

Employee.objects.annotate(
    full_name=Concat("first_name", Value(" "), "last_name")
)
```

## Interview-তে সবচেয়ে বেশি জিজ্ঞাসা করা হয়

- `CONCAT()` বনাম `||`
    
- `CONCAT_WS()`
    
- `UPPER()`, `LOWER()`, `INITCAP()`
    
- `LENGTH()`
    
- `TRIM()`
    
- `SUBSTRING()`
    
- `LEFT()` / `RIGHT()`
    
- `REPLACE()`
    
- `SPLIT_PART()`
    

এগুলো PostgreSQL-এর সবচেয়ে বেশি ব্যবহৃত string functions, বিশেষ করে report, search, data cleaning এবং Django ORM annotation-এর ক্ষেত্রে।


-----
