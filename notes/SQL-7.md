Day-10
1. INDEXES
An index is a database object used to speed up data retrieval operations on a table.

Why Indexes are Needed:
- Without an index, the database performs a full table scan.
- Indexes reduce time complexity and improve query performance.

Types of Indexes:
A. Clustered Index
- Physically sorts the table data based on the indexed column.
- Only one clustered index per table.
- Primary key is a clustered index by default.

Example:
CREATE TABLE sample (
  id INT PRIMARY KEY,
  name VARCHAR(50)
);

B. Non-Clustered Index
- Stores a separate structure pointing to table rows.
- Multiple non-clustered indexes allowed.

Example:
CREATE INDEX idx_last_name
ON customer(last_name);


2. AUTO INCREMENT: Auto Increment automatically generates unique numeric values.

Example:
CREATE TABLE orders (
  order_id INT AUTO_INCREMENT PRIMARY KEY,
  order_date DATE
);

Even if values are not inserted, MySQL increments automatically.

3. FULL TABLE SCAN VS INDEX SCAN

If no index exists, the database scans the entire table.

Example:
SELECT * FROM customer WHERE last_name = 'Smith';

Creating an index improves performance:
CREATE INDEX idx_customer_lastname ON customer(last_name);

4. NATURAL KEY vs SURROGATE KEY

Natural Key:
- Real-world meaningful data.
- Example: Email, SSN.

Surrogate Key:
- System-generated.
- Example: AUTO_INCREMENT ID.

5. PRIMARY KEY & UNIQUE KEY

Primary Key:
- Uniquely identifies each row.
- Cannot be NULL.

Unique Key:this constraint ensures that all values in a column(or group of columns) are unquie across the table
- Ensures uniqueness but allows NULL.
- prevents duplicate values
- helps to maintain dta integrity

Example:
ALTER TABLE customer
ADD UNIQUE(email);

6. QUERY OPTIMIZATION (FINE TUNING)

A. Select Only Required Columns

SELECT * FROM film;
use:
SELECT title, rental_rate FROM film;

B. WHERE before GROUP BY & HAVING

WHERE filters rows before grouping.
HAVING filters groups after aggregation.

Example:
SELECT rental_duration, COUNT(*)
FROM film
WHERE rental_rate > 2.99
GROUP BY rental_duration
HAVING COUNT(*) > 50;

C. JOIN vs SUBQUERY
JOINs are usually more efficient.

Subquery:
SELECT customer_id
FROM payment
WHERE amount > (SELECT AVG(amount) FROM payment);

JOIN:
SELECT p.customer_id
FROM payment p
JOIN (
  SELECT AVG(amount) avg_amt FROM payment
) a
ON p.amount > a.avg_amt;

D. Avoid Functions on Indexed Columns
SELECT * FROM payment WHERE YEAR(payment_date) = 2006;
use:
SELECT * FROM payment
WHERE payment_date BETWEEN '2006-01-01' AND '2006-12-31';

E. LIMIT Usage
Use LIMIT to restrict rows.

Example:
SELECT * FROM rental LIMIT 10;

F. CTE (Common Table Expression)
Improves readability.

Example:
WITH high_value_payments AS (
  SELECT * FROM payment WHERE amount > 5)
SELECT COUNT(*) FROM high_value_payments;

G. EXPLAIN Query
Used to analyze query execution plan.

Example:
EXPLAIN SELECT * FROM film WHERE rental_rate = 4.99;

H. ANALYZE / MAINTENANCE
Keeps index statistics updated.

Example:
ANALYZE TABLE film;

I. PAGINATION – Avoid Large OFFSET
SELECT * FROM rental LIMIT 10000, 10;
use:
SELECT * FROM rental WHERE rental_id > 10000 LIMIT 10;
