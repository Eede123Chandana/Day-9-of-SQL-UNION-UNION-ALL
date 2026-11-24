# 📊 SQL UNION & UNION ALL | Combining Multiple Result Sets

## 🎯 Overview

SQL `UNION` and `UNION ALL` combine the results of multiple SELECT queries into one result set.

These operators are useful for consolidating customer records, combining sales data across branches, and preparing datasets for business reporting.

**Objective:** Understand UNION, UNION ALL, their differences, usage rules, performance considerations, and real-world applications.

---

## 1️⃣ What is UNION?

`UNION` combines the results of two or more SELECT queries and removes duplicate rows.

### Syntax

```sql
SELECT column_name FROM table1
UNION
SELECT column_name FROM table2;
```

### Example Datasets

**Table: customers_ny**

| customer_name |
|---|
| Amit |
| Ravi |
| Neha |

**Table: customers_mumbai**

| customer_name |
|---|
| Ravi |
| Kiran |
| Neha |

### UNION Query

```sql
SELECT customer_name FROM customers_ny
UNION
SELECT customer_name FROM customers_mumbai;
```

### Output

| Customer Name |
|---|
| Amit |
| Ravi |
| Neha |
| Kiran |

**Explanation:** Duplicate customer names are removed from the combined result.

**Note:** UNION does not guarantee output order without ORDER BY.

---

## 2️⃣ What is UNION ALL?

`UNION ALL` combines multiple SELECT results and preserves duplicate rows.

### Syntax

```sql
SELECT column_name FROM table1
UNION ALL
SELECT column_name FROM table2;
```

### Example

```sql
SELECT customer_name FROM customers_ny
UNION ALL
SELECT customer_name FROM customers_mumbai;
```

### Output

| Customer Name |
|---|
| Amit |
| Ravi |
| Neha |
| Ravi |
| Kiran |
| Neha |

**Explanation:** All six records are retained, including repeated names.

---

## 3️⃣ UNION vs UNION ALL

| Feature | UNION | UNION ALL |
|---|---|---|
| Combines SELECT results | Yes | Yes |
| Removes duplicates | Yes | No |
| Preserves repeated rows | No | Yes |
| Performance | May require extra processing | Generally faster |
| Best Use | Unique combined results | Complete combined data |

### Important Concept

UNION removes duplicate **entire rows**, not just duplicate values in one column.

When multiple columns are selected, all corresponding values must match for rows to be considered duplicates.

---

## 4️⃣ Rules for Using UNION

### Rule 1: Same Number of Columns

Both SELECT statements must return the same number of columns.

```sql
SELECT customer_id, customer_name
FROM customers_ny

UNION

SELECT customer_id, customer_name
FROM customers_mumbai;
```

### Rule 2: Compatible Data Types

Corresponding columns must have compatible data types.

For example:

- Customer ID → Customer ID
- Customer Name → Customer Name
- Sales Amount → Sales Amount

### Rule 3: Matching Column Order

Columns are matched by position, not by their names.

**Correct:**

```sql
SELECT customer_id, customer_name
FROM customers_ny

UNION ALL

SELECT customer_id, customer_name
FROM customers_mumbai;
```

### Rule 4: ORDER BY at the End

```sql
SELECT customer_name FROM customers_ny
UNION
SELECT customer_name FROM customers_mumbai
ORDER BY customer_name;
```

**Purpose:** Sort the final combined result alphabetically.

---

## 5️⃣ UNION vs JOIN

| UNION | JOIN |
|---|---|
| Combines rows vertically | Combines columns horizontally |
| Appends compatible result sets | Relates rows between tables |
| Uses multiple SELECT queries | Uses JOIN conditions |
| Useful for combining similar datasets | Useful for related datasets |

### UNION Example

```sql
SELECT customer_name FROM customers_ny
UNION ALL
SELECT customer_name FROM customers_mumbai;
```

Combines customer records vertically.

### JOIN Example

```sql
SELECT
    c.customer_name,
    o.order_id
FROM customers c
INNER JOIN orders o
    ON c.customer_id = o.customer_id;
```

Combines customer information with related orders.

---

## 6️⃣ Performance Differences

### UNION

- Removes duplicate rows.
- May require sorting, hashing, or other duplicate-elimination operations.
- Can add processing overhead on large datasets.

### UNION ALL

- Preserves duplicate rows.
- Avoids duplicate-removal overhead.
- Generally performs faster for large result sets.

### Performance Recommendation

✅ Use UNION when unique combined rows are required.

✅ Use UNION ALL when duplicate records are meaningful or acceptable.

✅ Avoid unnecessary duplicate removal.

✅ Compare execution plans for performance-sensitive queries.

**Note:** Actual performance depends on dataset size, indexes, query complexity, and the database engine.

---

## 7️⃣ Real-World Business Applications

### 🏬 Retail – Combining Branch Sales

```sql
SELECT order_id, amount
FROM hyderabad_sales

UNION ALL

SELECT order_id, amount
FROM mumbai_sales;
```

**Business Use Case:** Consolidate transactions from multiple branches.

### 👥 Customer Analytics

```sql
SELECT customer_email FROM online_customers
UNION
SELECT customer_email FROM offline_customers;
```

**Business Use Case:** Identify unique email addresses across customer sources.

### 💳 Financial Analytics

```sql
SELECT transaction_id, amount
FROM card_transactions

UNION ALL

SELECT transaction_id, amount
FROM upi_transactions;
```

**Business Use Case:** Combine card and UPI transaction records.

### 📈 Business Intelligence

```sql
SELECT region, revenue
FROM january_sales

UNION ALL

SELECT region, revenue
FROM february_sales;
```

**Business Use Case:** Consolidate monthly reporting datasets.

*These examples assume compatible columns and appropriate source-table structures.*

---

## 8️⃣ Important Interview Questions

**Q1. What is UNION?**

UNION combines SELECT results and eliminates duplicate rows.

**Q2. What is UNION ALL?**

UNION ALL combines SELECT results while preserving duplicates.

**Q3. Which is faster?**

UNION ALL is generally faster because it skips duplicate elimination.

**Q4. Does UNION remove duplicates from the original tables?**

No. It only removes duplicate rows from the query result.

**Q5. Can UNION combine different numbers of columns?**

No. Corresponding SELECT queries must return the same number of columns.

**Q6. Does UNION guarantee sorted results?**

No. Use ORDER BY for guaranteed sorting.

**Q7. UNION vs JOIN?**

UNION combines query results vertically; JOIN combines related table data using join conditions.

---

## 🎯 Key Takeaways

✅ UNION combines results and removes duplicates.

✅ UNION ALL combines results and preserves duplicates.

✅ Both require the same number of output columns.

✅ Corresponding data types must be compatible.

✅ Column positions must align meaningfully.

✅ ORDER BY controls final result ordering.

✅ UNION ALL is generally faster.

✅ UNION and JOIN solve different data-combination problems.

---

## 💡 Final Thoughts

**UNION and UNION ALL are essential SQL tools for combining datasets and building reliable business reports.**

Choosing the correct operator depends on whether duplicate elimination is needed and whether preserving all records is important.

### 🏷️ Topics

`SQL` `UNION` `UNION ALL` `JOIN` `MySQL` `Data Analytics` `Business Analytics` `Query Optimization` `SQL Interviews` `Business Intelligence`
