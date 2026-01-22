Day – 3 (11/01/2026)

Database
 	•A database is a collection of processed data.
 	•The database is stored on a server.
 	•The database is managed by a DBMS (Database Management System).
 	•Data in the database is communicated using SQL.

How is data stored?
Data is stored in tables, i.e., in rows and columns.

Schema
 	•A schema defines how a table should look.
 	•It acts like a template for the table structure.

SQL- structured query language

SQL Commands are categorized into:
 	DDL
 	DML
 	DQL
 	DCL
 	TCL

DDL – Data Definition Language: Used for defining the data structure.
commands: CREATE, ALTER, DROP,TRUNCATE,RENAME

DML – Data Manipulation Language: Used to manipulate data in tables.
commands: INSERT, DELETE

DQL – Data Query Language: Used for querying data.
commands: SELECT

DCL – Data Control Language: Used to control access and permissions on data.
Commands: GRANT, REVOKE

TCL – Transaction Control Language: Used to ensure data integrity and consistency.
commands: COMMIT, ROLLBACK,SAVEPOINT

--Create Database- Used to create a new database.

Syntax- CREATE DATABASE database_name;

--Use Database- After creating a database, we must select it to work on it.

USE database_name;

--Insert Data into Database (Table)

Used to insert records into a table.

Syntax
INSERT INTO table_name (column1, column2, column3)
VALUES (value1, value2, value3);

--ALTER-Used to modify the structure of a table (add, modify, or delete columns).

Syntax Examples
ALTER TABLE table_name ADD column_name datatype;
ALTER TABLE table_name MODIFY column_name datatype;
ALTER TABLE table_name DROP column_name;

--RENAME- Used to rename a table.
Syntax
RENAME TABLE old_table_name TO new_table_name;

--DROP-Used to completely remove a database or table (structure + data).

Syntax
DROP DATABASE database_name;
DROP TABLE table_name;
*Entire table/database is removed permanently.

--DELETE-Used to delete specific records based on a condition

Syntax
DELETE FROM table_name WHERE condition;
*Table structure remains

--TRUNCATE- Used to remove all data from a table.

Syntax
TRUNCATE TABLE table_name;
*Only data is removed, table structure remains.

Constraints: Rules applied to columns to ensure valid data.

Types of Constraints

1.NOT NULL – Does not allow NULL values
Syntax Example
column_name datatype NOT NULL UNIQUE;

2.UNIQUE – Ensures unique values

3.PRIMARY KEY: Uniquely identifies each record in a table.

              Cannot be NULL.

              Only one primary key per table.
Syntax
PRIMARY KEY (column_name);

4.FOREIGN KEY: Used to create a relationship between two tables.

              Refers to the primary key of another table.
Syntax
FOREIGN KEY (column_name)
REFERENCES parent_table(primary_key_column);

5.CHECK – Checks a condition, Ensures values meet a condition.

CHECK (age >= 18)

6.DEFAULT – Sets default value

Sets a default value if no value is provided.

salary INT DEFAULT 30000;


Parent–Child Relationship

Parent table: Contains the primary key.

Child table: Contains the foreign key.

Referencing Table-the table that contains the foreign key.

Referenced Table-The table whose primary key is referenced.

*To delete a parent record, first delete related child records unless CASCADE is used.

Safe Mode: Prevents deleting or updating data without a WHERE condition.

--Cascading: means automatically applying changes from a parent table to a child table when there is a foreign key relationship between them.

Types of Cascading
1. ON DELETE CASCADE: When a record in the parent table is deleted, all related records in the child table are automatically deleted.
2. ON UPDATE CASCADE: When a primary key value in the parent table is updated, the foreign key values in the child table are updated automatically.