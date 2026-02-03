use sakila;
show tables;
select * from customer;
# 1.Get all customers whose first name starts with 'J' and who are active.
select * from customer
where first_name like 'j%' and active = 1;
# 2.Find all films where the title contains the word 'ACTION' or the description contains 'WAR'.
select * from film
where title like '%ACTION%' or description like '%War%';
# 3. List all customers whose last name is not 'SMITH' and whose first name ends with 'a'.
select * from customer
where last_name!='SMITH' and first_name like '%a';

# 4. Get all films where the rental rate is greater than 3.0 and the replacement cost is not null.
select * from film
where rental_rate > 3.0 and replacement_cost is not Null;
# 5. Count how many customers exist in each store who have active status = 1.
select customer_id, store_id,active
from customer where active=1;
select store_id, count(customer_id) as Total_active_customers
from customer where active=1
group by store_id;

---- where: row level condition, having: group level condition
select select store_id, active, count(customer_id) as Total_active_customers
from customer
group by store_id having active = 1;

# 6. Show distinct film ratings available in the film table.
select * from film;
select distinct(rating) from film;

# 7. Find the number of films for each rental duration where the average length is more than 100 minutes.
select rental_duration,length,film_id
from film;
select rental_duration,count(film_id) as Number_of_films
from film
group by rental_duration
having avg(length)>100;

#8. List payment dates and total amount paid per date, but only include days where more than 100 payments were made.
-- select * from sakila.payment;

select 
date(payment_date) as date,
sum(amount) as Total_amount,
count(payment_id) as payment_count
from sakila.payment
group by date(payment_date) 
having payment_count > 100
order by payment_count;

# 9. Find customers whose email address is null or ends with '.org'.
select * from customer
where email is null or email like '%.org';

# 10. List all films with rating 'PG' or 'G', and order them by rental rate in descending order.
select * from film 
where rating ='PG' or rating='G'
order by rental_rate desc;
# 11. Count how many films exist for each length where the film title starts with 'T' and the count is more than 5.
select * from sakila.film;
select length, count(film_id) as total_films
from sakila.film
where title like 'T%'
group by length
having  count(film_id) > 5;

#12. List all actors who have appeared in more than 10 films.
select * from sakila.film_actor;
select actor_id, count(film_id) as films
from sakila.film_actor
group by actor_id
having count(film_id) > 10;

#13. Find the top 5 films with the highest rental rates and longest lengths combined, ordering by rental rate first and length second.
SELECT film_id, title, rental_rate, length
FROM sakila.film
ORDER BY rental_rate DESC, length DESC
LIMIT 5;

#14. Show all customers along with the total number of rentals they have made, ordered from most to least rentals.
SELECT
  c.customer_id,
  c.first_name,
  c.last_name,
  COUNT(r.rental_id) AS total_rentals
FROM sakila.customer c
LEFT JOIN sakila.rental r
  ON c.customer_id = r.customer_id
GROUP BY c.customer_id, c.first_name, c.last_name
ORDER BY total_rentals DESC;

#15. List the film titles that have never been rented.
SELECT f.title
FROM sakila.film f
LEFT JOIN sakila.inventory i
  ON f.film_id = i.film_id
LEFT JOIN sakila.rental r
  ON i.inventory_id = r.inventory_id
WHERE r.rental_id IS NULL;
