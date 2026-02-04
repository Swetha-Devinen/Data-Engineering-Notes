#Assessment-3#
#1. display all customer details who have made more than 5 payments.
select * from sakila.customer
where customer_id in
(select customer_id, count(payment_id) as payments
from sakila.payment
group by customer_id
having count(payment_id)>5); --- for this error obtained as showing operand should contain 1 column,inner query should show the result in single column

select * from sakila.customer
where customer_id in
(select customer_id
from sakila.payment
group by customer_id
having count(payment_id)>5);

#2. Find the names of actors who have acted in more than 10 films.
select actor_id,first_name,last_name
from sakila.actor
where actor_id in
(select actor_id
 from sakila.film_actor
 group by actor_id
 having count(film_id)>10);

#3. Find the names of customers who never made a payment.
select customer_id,first_name,last_name
from sakila.customer
where customer_id not in (select customer_id
					 from sakila.payment);

#4. List all films whose rental rate is higher than the average rental rate of all films.
select *
 from sakila.film
 where rental_rate > (select avg(rental_rate) as avg_rate
					from sakila.film);
 
#5. List the titles of films that were never rented.
SELECT title
FROM sakila.film
WHERE film_id NOT IN (
  SELECT DISTINCT i.film_id
  FROM sakila.inventory i
  JOIN sakila.rental r
    ON i.inventory_id = r.inventory_id
);

#6. Display the customers who rented films in the same month as customer with ID 5.
SELECT DISTINCT customer_id
FROM sakila.rental
WHERE DATE_FORMAT(rental_date, '%Y-%m') IN (
    SELECT DATE_FORMAT(rental_date, '%Y-%m')
    FROM sakila.rental
    WHERE customer_id = 5
);

#7. Find all staff members who handled a payment greater than the average payment amount.
SELECT DISTINCT staff_id
FROM sakila.payment
WHERE amount > (
  SELECT AVG(amount)
  FROM sakila.payment
);

#8. Show the title and rental duration of films whose rental duration is greater than the average.
SELECT title, rental_duration
FROM sakila.film
WHERE rental_duration > (
  SELECT AVG(rental_duration)
  FROM sakila.film
);

#9. Find all customers who have the same address as customer with ID 1.
SELECT customer_id, first_name, last_name
FROM sakila.customer
WHERE address_id = (
  SELECT address_id
  FROM sakila.customer
  WHERE customer_id = 1
);

#10. List all payments that are greater than the average of all payments.
SELECT *
FROM sakila.payment
WHERE amount > (
  SELECT AVG(amount)
  FROM sakila.payment
);

