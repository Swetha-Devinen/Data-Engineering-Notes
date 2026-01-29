Day 6 
Date: January 26, 2026

1. Subqueries
A subquery is a query written inside another query. Subqueries are executed first and their results are used by the main query. They help build temporary results that support the main query logic.
SELECT customer_id, amount
FROM payment
WHERE amount > (
    SELECT AVG(amount)
    FROM payment
);

Types of Subqueries
- Subqueries in SELECT clause
- Derived tables (subqueries used as tables)
- Correlated subqueries (reference columns from the main query)
Limitations of Subqueries
- Increased complexity of code
- No reusability
- Higher time and space complexity
- Subqueries execute at the query execution level

Derived tables: 
SELECT customer_id, payment_count
FROM (
    SELECT customer_id, COUNT(*) AS payment_count
    FROM payment
    GROUP BY customer_id
) AS p
WHERE payment_count > 5;

2. Normalization
Normalization is the process of splitting data into multiple tables to organize data efficiently and reduce redundancy in the database.
3. Cardinality Relationships
Cardinality defines how tables are related to each other (mapping).
Four types of relationships:
- One-to-One (1:1)
- One-to-Many (1:Many)
- Many-to-One (Many:1)
- Many-to-Many (Many:Many)
4. Bridge Table
A bridge table is used to resolve many-to-many relationships. It contains foreign keys from both related tables.


