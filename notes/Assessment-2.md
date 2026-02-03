#Assessment-2#
#1. Identify if there are duplicates in Customer table. Don't use customer id to check the duplicates
SELECT email, COUNT(*) AS duplicate_count
FROM sakila.customer
GROUP BY email
HAVING COUNT(*) > 1;

select store_id, first_name,last_name, count(*) as duplicate_count
from sakila.customer
group by store_id,first_name,last_name
having count(*)>1;

select store_id,email, count(*) as duplicate_count
from sakila.customer
group by store_id,email
having count(*)>1;

#2. Number of times letter 'a' is repeated in film descriptions
select * from sakila.film;
SELECT 
  sum(LENGTH(REGEXP_REPLACE(LOWER(description), '[^a]', '')
             )
	)AS total_a_count
FROM sakila.film;

SELECT 
  SUM(
    LENGTH(description)
    - LENGTH(REPLACE(LOWER(description), 'a', ''))
  ) AS total_a_count
FROM sakila.film;

#3. Number of times each vowel is repeated in film descriptions 
select * from sakila.film;
SELECT 
  sum(LENGTH(REGEXP_REPLACE(LOWER(description), '[^aeiou]', '')
             )
	)AS total_a_count
FROM sakila.film; --- total vowels sum

SELECT
  SUM(LENGTH(REGEXP_REPLACE(LOWER(description), '[^a]', ''))) AS a_count,
  SUM(LENGTH(REGEXP_REPLACE(LOWER(description), '[^e]', ''))) AS e_count,
  SUM(LENGTH(REGEXP_REPLACE(LOWER(description), '[^i]', ''))) AS i_count,
  SUM(LENGTH(REGEXP_REPLACE(LOWER(description), '[^o]', ''))) AS o_count,
  SUM(LENGTH(REGEXP_REPLACE(LOWER(description), '[^u]', ''))) AS u_count
FROM sakila.film;

#4. Display the payments made by each customer 1. Month wise 2. Year wise 3. Week wise
select customer_id, year(payment_date) as pay_year
from sakila.payment
group by customer_id, pay_year; ------- just shows customer

SELECT customer_id,YEAR(payment_date) AS pay_year, COUNT(payment_id)  AS payment_count
FROM sakila.payment
GROUP BY customer_id, YEAR(payment_date); -------- shows how many payments made
#Monthwise
SELECT customer_id,YEAR(payment_date)  AS pay_year,MONTH(payment_date) AS pay_month,
  COUNT(payment_id)   AS payment_count
FROM sakila.payment
GROUP BY customer_id, YEAR(payment_date), MONTH(payment_date)
ORDER BY customer_id, pay_year, pay_month;

#WEEKWISE
#5. Check if any given year is a leap year or not. You need not consider any table from sakila database. Write within the select query with hardcoded date

select 
case
when(year('2020-11-15') % 4 = 0  AND year('2020-11-15')% 100 !=0) 
         or
      ( year('2020-11-15')% 400 =0)
      then 'Leap Year'
      else 'Not a Leap Year'
      end as leapyear_status;
      
 # 6. Display number of days remaining in the current year from today.
 
SELECT DATEDIFF(CURRENT_DATE, joining_date)
FROM students;

 SELECT
  DATEDIFF(
    LAST_DAY(CONCAT(YEAR(CURDATE()), '-12-01')),
    CURDATE()
  ) AS days_remaining_in_year;
  
#7. Display quarter number(Q1,Q2,Q3,Q4) for the payment dates from payment table. 
select * from sakila.payment ;
SELECT
    payment_date,
    CASE
        WHEN MONTH(payment_date) BETWEEN 1 AND 3 THEN 'Q1'
        WHEN MONTH(payment_date) BETWEEN 4 AND 6 THEN 'Q2'
        WHEN MONTH(payment_date) BETWEEN 7 AND 9 THEN 'Q3'
        WHEN MONTH(payment_date) BETWEEN 10 AND 12 THEN 'Q4'
    END AS quarter_number
FROM sakila.payment;

# 8. Display the age in year, months, days based on your date of birth. 
   For example: 21 years, 4 months, 12 days
   SELECT
  YEAR(CURDATE()) - YEAR('2000-01-15') AS years,
  MONTH(CURDATE()) - MONTH('2000-01-15') AS months,
  DAY(CURDATE()) - DAY('2000-01-15') AS days;
  