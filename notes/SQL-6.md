**Stored Procedure**

A stored procedure is a pre-written SQL program stored inside the database that can be executed whenever needed. 

It allows you to group multiple SQL statements into a single reusable unit.



Why Do We Use Stored Procedures?

1\. Reusability – Write once, use many times

2\. Performance – Compiled once and executed faster

3\. Security – Users can execute procedures without direct table access

4\. Maintainability – Business logic changes in one place



Basic Syntax (MySQL):

DELIMITER //

CREATE PROCEDURE procedure\_name()

BEGIN

&nbsp;   SQL statements;

END //

DELIMITER ;



Example 1: Simple Stored Procedure (No Parameters)

CREATE PROCEDURE GetAllCustomers()

BEGIN

&nbsp;   SELECT \* FROM customer;

END;



CALL GetAllCustomers();



**Types of Parameters:**

IN – Input value: Pass value into procedure

OUT – Output value:Return value from procedure

INOUT – Input and output: Pass value in and return modified value



Example: Total payment by customer

DELIMITER //



CREATE PROCEDURE sp\_total\_payment(

&nbsp;   IN  p\_customer\_id INT,

&nbsp;   OUT p\_total\_amount DECIMAL(10,2)

)

BEGIN

&nbsp;   SELECT IFNULL(SUM(amount), 0)

&nbsp;   INTO p\_total\_amount

&nbsp;   FROM payment

&nbsp;   WHERE customer\_id = p\_customer\_id;

END //



DELIMITER ;

CALL sp\_total\_payment(5, @total);

SELECT @total AS total\_payment;



-- easy to write more number of queries at a time

Stored Procedure vs Function:

Stored Procedure – Used for business logic, can return multiple values

Function – Used for calculations, must return one value







