#CTE AND VIEWS
#1. List all customers along with the films they have rented.
use sakila;
with  customer_film_rentals as (
select c.customer_id,c.first_name,c.last_name,f.title
from customer c
join rental r on c.customer_id=r.customer_id
join inventory i on r.inventory_id=i.inventory_id
join film f on i.film_id=f.film_id
)
select * from customer_film_rentals
order by customer_id;

#2. List all customers and show their rental count, including those who haven't rented any films.
with customer_rentals as (
select c.customer_id, c.first_name,c.last_name,count(r.rental_id) as rental_count
from sakila.customer c 
left join sakila.rental r on c.customer_id=r.customer_id
group by c.customer_id, c.first_name,c.last_name)
select customer_id,first_name,last_name, rental_count
from customer_rentals;


#3. Show all films along with their category. Include films that don't have a category assigned.
SELECT f.film_id,f.title,(
SELECT c.name
        FROM sakila.film_category fc
        JOIN sakila.category c
          ON fc.category_id = c.category_id
        WHERE fc.film_id = f.film_id
        LIMIT 1) AS category_name
FROM sakila.film f;
#4. Show all customers and staff emails from both customer and staff tables using a full outer join (simulate using LEFT + RIGHT + UNION).
CREATE  VIEW customer_staff_emails_full AS
SELECT c.customer_id,c.email AS customer_email,st.staff_id,st.email AS staff_email,
    COALESCE(c.store_id, st.store_id) AS store_id
FROM sakila.customer c
LEFT JOIN sakila.staff st
  ON c.store_id = st.store_id
UNION
SELECT c.customer_id,c.email AS customer_email,st.staff_id,st.email AS staff_email,
    COALESCE(c.store_id, st.store_id) AS store_id
FROM sakila.customer c
RIGHT JOIN sakila.staff st
  ON c.store_id = st.store_id;

SELECT * FROM customer_staff_emails_full
ORDER BY store_id, customer_id, staff_id;
#5. Find all actors who acted in the film "ACADEMY DINOSAUR".
CREATE VIEW actor_film AS
SELECT a.actor_id,a.first_name,a.last_name,f.title
FROM sakila.actor a
JOIN sakila.film_actor fa
    ON a.actor_id = fa.actor_id
JOIN sakila.film f
    ON fa.film_id = f.film_id;
SELECT actor_id, first_name, last_name
FROM actor_film
WHERE title = 'ACADEMY DINOSAUR';

#6. List all stores and the total number of staff members working in each store, even if a store has no staff.
CREATE or replace VIEW store_staff_count AS
SELECT s.store_id,COUNT(st.staff_id) AS total_staff
FROM sakila.store s
LEFT JOIN sakila.staff st
    ON s.store_id = st.store_id
GROUP BY s.store_id;
SELECT *
FROM store_staff_count
ORDER BY store_id;

#7. List the customers who have rented films more than 5 times. Include their name and total rental count.

CREATE OR REPLACE VIEW customer_rental_count AS
SELECT c.customer_id,c.first_name,c.last_name,COUNT(r.rental_id) AS total_rentals
FROM sakila.customer c
JOIN sakila.rental r
    ON c.customer_id = r.customer_id
GROUP BY c.customer_id,c.first_name,c.last_name;
SELECT *
FROM customer_rental_count
WHERE total_rentals > 5
ORDER BY total_rentals DESC;
