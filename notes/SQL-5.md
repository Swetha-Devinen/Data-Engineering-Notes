**Day 8: (CTE, Recursive CTE, Temporary Tables, Views)**



**1. Common Table Expressions (CTE)**



Definition: A Common Table Expression (CTE) is a temporary named result set that exists only during the execution of a query.

It improves readability, reusability, and reduces query complexity.



• Subqueries have limitations such as poor readability, reusability, and high complexity

• To overcome these limitations, CTEs are used

• CTEs make complex queries easier to understand



Syntax:

WITH cte\_name AS (

&nbsp;   SELECT columns

&nbsp;   FROM table

&nbsp;   WHERE condition

)

SELECT \* FROM cte\_name;





Example: Find customers who have made more than 5 payments.



WITH payment\_count AS (

&nbsp;   SELECT customer\_id, COUNT(\*) AS total\_payments

&nbsp;   FROM payment

&nbsp;   GROUP BY customer\_id

)

SELECT c.customer\_id, c.first\_name, c.last\_name, p.total\_payments

FROM customer c

JOIN payment\_count p ON c.customer\_id = p.customer\_id

WHERE p.total\_payments > 5;



**2. Recursive CTE**



&nbsp;A Recursive CTE is a CTE that references itself and is mainly used for hierarchical or sequence-based data.



• Recursive CTE has two parts:

&nbsp; 1. Anchor Member – starting point

&nbsp; 2. Recursive Member – generates the next records

like if statement, it repeats till the required condition is obtained.



Syntax:

WITH RECURSIVE cte\_name AS (

&nbsp;   anchor\_query

&nbsp;   UNION ALL

&nbsp;   recursive\_query

)

SELECT \* FROM cte\_name;





Example:

Generate numbers from 1 to 5.





WITH RECURSIVE numbers AS (

&nbsp;   SELECT 1 AS num

&nbsp;   UNION ALL

&nbsp;   SELECT num + 1

&nbsp;   FROM numbers

&nbsp;   WHERE num < 5

)

SELECT \* FROM numbers;



3\. Temporary Tables



A Temporary Table is created temporarily for a user session and is automatically dropped when the session ends

or when it is explicitly dropped.



• Created temporarily for a session

• Exists until explicitly dropped or session ends

• Stored in the server but not physically stored in the database

• Uses space and time and may duplicate data

• Not recommended for long-term storage



Syntax:

CREATE TEMPORARY TABLE temp\_table\_name AS

SELECT columns

FROM table;



Example:

Create a temporary table to store total payment amount per customer.



CREATE TEMPORARY TABLE temp\_payments AS

SELECT customer\_id, SUM(amount) AS total\_amount

FROM payment

GROUP BY customer\_id;



SELECT \* FROM temp\_payments WHERE total\_amount > 100;



4\. Views



A View is a virtual table created using a stored SQL query.

Only the query definition is stored, not the actual data.

• View is a virtual table

• Created using a SQL query

• Provides abstraction of data (hides original table and column names)

• Used for security to restrict access to sensitive data

• Data is not physically stored

• Only the schema (structure) is stored



Syntax:

CREATE VIEW view\_name AS

SELECT columns

FROM table

WHERE condition;



Example:

Create a view to show only active customers.



CREATE VIEW active\_customers AS

SELECT customer\_id, first\_name, last\_name, email

FROM customer

WHERE active = 1;



SELECT \* FROM active\_customers;





