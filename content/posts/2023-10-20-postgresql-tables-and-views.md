---
title: "PostreSQL Tables v Views"
date: 2023-10-20
author: 
  name: "Krystian Bucko"
  image: images/author/krys.jpg
  twitter: '@KrystianBucko'
categories: ["Data Warehouse", "Data Storage", "2023", "SQL"]
description: "Understand the key differences between two seemingly similar ways of viewing contents of a data warehouse"
thumbnail: "images/table-v-view.png"
image: "/images/table-v-view.png"
---

Let's start with the basics!

## What is a Table in PostgreSQL?

A **table** is a physical structure in the database that stores data. This can be compared to a spreadsheet with rows and columns.

**Key Characteristics:**
- Stores data physically on disk.
- Can be inserted into, updated, and deleted from.
- Has a defined schema (columns, data types, constraints).
- Used for long-term storage of data.


### Example

```sql
CREATE TABLE employees (
  joined TIMESTAMP,
  name VARCHAR(255),
  department VARCHAR(255),
  salary BIGINT
);
```

## What is a View in PostgreSQL?

A view is a virtual table. It doesn’t store data itself but presents data from one or more tables via a saved SQL SELECT query.

**Key Characteristics:**
-Does NOT store data; it's just a saved query.
-Can be 'useful' for security (e.g., hiding certain columns).
-Runs one or more underlying queries when refreshed.

```sql
CREATE VIEW high_salary_employees AS
SELECT name, salary
FROM employees
WHERE salary > 100000;
```

## Differences: Tables vs Views

| Feature           | **Table**                         | **View**                                   |
| ----------------- | --------------------------------- | ------------------------------------------ |
| Data storage      | Stores data physically            | Does not store data                        |
| Purpose           | Store and manage data             | Present data in a specific way             |
| Query Performance | Generally faster (no re-querying) | Slower (runs underlying query each time)   |
| Dependencies      | Independent                       | Depends on tables and other views          |
| Security          | Less granular                     | Present exactly what  is needed            |
| Maintenance       | May require indexing, tuning      | No physical tuning, but query can be tuned |


## Bonus: Materialized Views
Like views, but they store the result of the query physically.
Useful when performance matters, but data doesn’t need to be real-time.
Must be manually refreshed:

```sql
CREATE MATERIALIZED VIEW employee_summary AS
SELECT department, COUNT(*) as num_employees
FROM employees
GROUP BY department;

-- Later, when you want fresh data:
REFRESH MATERIALIZED VIEW employee_summary;
```

## Use Cases

So finally, with so much to chose from, what should we use and when?

- **Tables:** When you want to store and manage data directly.
- **Views:** When you want to present specific and/or mixed datasets.
- **Materialized Views:** When performance matters and you're okay with slightly stale data.