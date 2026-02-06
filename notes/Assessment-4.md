#JOINS#
#1. List all customers along with the films they have rented.
SELECT c.customer_id, c.first_name,c.last_name,f.title
FROM sakila.customer c
JOIN sakila.rental r
  ON c.customer_id = r.customer_id
JOIN sakila.inventory i
  ON r.inventory_id = i.inventory_id
JOIN sakila.film f
  ON i.film_id = f.film_id
ORDER BY c.customer_id;

#2. List all customers and show their rental count, including those who haven't rented any films.
SELECT c.customer_id,c.first_name,c.last_name,f.title
FROM sakila.customer c
JOIN sakila.rental r
  ON c.customer_id = r.customer_id
JOIN sakila.inventory i
  ON r.inventory_id = i.inventory_id
JOIN sakila.film f
  ON i.film_id = f.film_id
ORDER BY c.customer_id;

#3. Show all films along with their category. Include films that don't have a category assigned.
select f.film_id,f.title,c.name as category
from sakila.film f
left join sakila.film_category fc
on f.film_id=fc.film_id
left join sakila.category c
on fc.category_id=c.category_id
order by f.film_id;
#4. Show all customers and staff emails from both customer and staff tables using a full outer join (simulate using LEFT + RIGHT + UNION).
select c.customer_id,c.email as customer_email, st.staff_id,st.email as store_email
from sakila.customer c
left join sakila.staff st
on c.store_id= st.store_id
union
select c.customer_id,c.email, st.staff_id,st.email
from sakila.customer c
right join sakila.staff st
on c.store_id= st.store_id;
#5. Find all actors who acted in the film "ACADEMY DINOSAUR".
select a.actor_id,a.first_name,a.last_name,f.title
from sakila.actor a
join sakila.film_actor fa
on a.actor_id=fa.actor_id
join sakila.film f
on fa.film_id=f.film_id
where title =  'ACADEMY DINOSAUR';
#6. List all stores and the total number of staff members working in each store, even if a store has no staff.
select st.store_id,count(s.staff_id) as total_staff
from sakila.staff s
right join sakila.store st
on s.store_id=st.store_id
group by st.store_id;

#7. List the customers who have rented films more than 5 times. Include their name and total rental count.
select c.customer_id,c.first_name,c.last_name,count(r.rental_id)
from sakila.customer c
join sakila.rental r
on c.customer_id=r.customer_id
join sakila.inventory i
on r.inventory_id=i.inventory_id
join sakila.film f
on i.film_id=f.film_id
group by c.customer_id,c.first_name,c.last_name
having count(r.rental_id)> 5
order by c.customer_id;