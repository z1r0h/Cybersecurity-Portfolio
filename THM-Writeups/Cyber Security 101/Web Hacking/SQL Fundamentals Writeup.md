# SQL Fundamentals

**Platform:** TryHackMe  
**Difficulty:** Easy  
**Category:** SQL
**Date:** 13 May 2026

---

## Objective
Learn the basics of databases, covering key terms, concepts and different types before getting to grips with SQL.

---

## Key Concepts Learned
- Two types of database 
	- **Relational databases** (aka SQL) - store in table format, store structured data, where accuracy is important.
	- **Non-relational databases** (aka NoSQL) -  non-tabular format, like html. used when data received vary greatly.
- Primary and Foreign Keys in table format. 
	- **Primary Keys**: A primary key is used to ensure that the data collected in a certain column is unique.
	- **Foreign Keys**: A foreign key is a column (or columns) in a table that also exists in another table within the database, and therefore provides a link between the two tables.
![[Pasted image 20260513153915.png]]
- Database Management System (DBMS) - serves as an interface between a database and an end user. Examples of DBMSs include MySQL, MongoDB, Oracle Database and Maria DB.
- Sturectured Query Language (SQL) - SQL is a programming language that can be used to query, define and manipulate the data stored in a relational database.
- Database and Table Statements
- CRUD Operations
	- **Create (INSERT statement)** - Adds a new record to the table.
	- **Read (SELECT statement)** - Retrieves record from the table.
	- **Update (UPDATE statement)** - Modifies existing data in the table.
	- **Delete (DELETE statement)** - Removes record from the table.
- Clauses statement: `DISTINCT`, `GROUP BY`, `ORDER BY`, and `HAVING`.
- Operators -  filter and manipulate data effectively.
- Functions - String, CONCAT(), 


---

## SQL Queries Practiced 

#### Database and Table Statement

```sql
mysql -u root -p
```
*what it does: connect to local database on same machine*

```SQL
	CREATE DATABASE thm_bookmarket_db;
```
*What it does: create a database named thm_bookmarket_db*

```SQL
SHOW DATABASES;
```
*What it does: list all present database*

```SQL
USE thm_bookmarket_db;
```
*What it does: choose database to interact*

```SQL
DROP database database_name;
```
*What it does: Delete Database*

```SQL
CREATE TABLE book_inventory ( book_id INT AUTO_INCREMENT PRIMARY KEY, book_name VARCHAR(255) NOT NULL, publication_date DATE );
```
*What it does: Create a table named book_inventory with 3 columns: book_id, book_name and publication_date with rules.
INT - only number 
AUTO_INCREMENT - auto add number to book_id every new row data is added
VARCHAR(255) -  can use variable characters (text/numbers/punctuation)
NO NULL - cant be empty 
DATE - data type is DATE.*

```SQL
SHOW TABLES;
```
*What it does: show all tables in current DB*

```SQL
DESCRIBE book_inventory;
```
*What id does: show all column contained within the table book_inventory*

```SQL
ALTER TABLE book_inventory ADD page_count INT;
```
*What id does: add another column that have page count on each book*

#### CRUD Operations

```SQL
INSERT INTO books (id, name, published_date, description) VALUES (7, "Android Security Internals", "2014-10-14", "An In-Depth Guide to Android's Security Architecture");
```
*what it dose: create a new record in **books** table, with value that match the table structure.*

```SQL
SELECT * FROM books;
```
*What it does: fetch all column from table **books** .

```SQL
SELECT name, description FROM books;
```
*What it does: fetch column **name** and **description** from table **books** using **SELECT**. 

```SQL
UPDATE books SET description = "An In-Depth Guide to Android's Security Architecture." WHERE id = 1;
```
*What it does: update record using **UPDATE, SET** and **WHERE id = 1**. 

```SQL
DELETE FROM books WHERE id = 1;
```
*What it does: delete record with ID = 1*

#### Clauses

```SQL
SELECT DISTINCT name FROM books;
```
*What it does: show record **name** from table **books** with duplicated record removed.*

```SQL
SELECT name, COUNT(*) FROM books GROUP BY name;
```
*what it does: Regroup and output result to **count**, duplicated name will show 2 or more count.

```SQL
SELECT * FROM books ORDER BY published_date ASC;
```
*What it does: sort table ASC or DESC by published_date*

```SQL
SELECT name, COUNT(*) FROM books GROUP BY name HAVING name LIKE '%Hack%';
```
*What it does: filter record and match name that contain **hack** and output to **count**. 

#### Operators

```SQL
SELECT * FROM books WHERE description LIKE "%guide%";
```
*what it does: filter specific pattern within column **description** from table **books**.*

```SQL
SELECT * FROM books WHERE category = "Offensive Security" AND name = "Bug Bounty Bootcamp";
```
*what it does: return data if 2 conditions are meet.*

```SQL
SELECT * FROM books WHERE name LIKE "%Android%" OR name LIKE "%iOS%";
```
*What it does: return data if **android** OR **iso** exist. 

```SQL
SELECT * FROM books WHERE NOT description LIKE "%guide%";
```
*What it does: return data from table **books** where description doesnt include the word **guide**.*

```SQL
SELECT * FROM books WHERE id BETWEEN 2 AND 4;
```
*What it does: return result from table **books** where id between 2 to 4.

```SQL
SELECT * FROM books WHERE name = "Designing Secure Software";
```
*What it does: return data that exact name **Designing Secure Software**.*

```SQL
SELECT * FROM books WHERE category != "Offensive Security";
```
*What it does: return data that category **IS NOT EQUAL (!=)** `Offensive Security`.

```SQL
SELECT * FROM books WHERE published_date < "2020-01-01";
```
*What it does: Return data where the record was published before 2020-01-01*

```SQL
SELECT * FROM books WHERE published_date > "2020-01-01";
```
*What it does: Return data where the record was published after 2020-01-01*

```SQL
SELECT * FROM books WHERE published_date <= "2021-11-15";
```
*What it does: Return data where the record was published before, or exactly at 2021-11-15*

```SQL
SELECT * FROM books WHERE published_date >= "2021-11-02";
```
*What it does: Return data where the record was published after, or exactly at 2021-11-02*

#### Functions 
```SQL
SELECT CONCAT(name, " is a type of ", category, " book.") AS book_info FROM books;
```
*What id does: create a new column name **book_info** at **books** table, combined column **name + "is a type of" + category + "book."**. example result `Android Security Internals is a type of Defensive Security book.`

```SQL
SELECT category, GROUP_CONCAT(name SEPARATOR ", ") AS books FROM books GROUP BY category;
```
*What it does: create a new column `books` at **books** table, sort the **books** by **category** and separate the **name** by **,  .

```SQL
SELECT SUBSTRING(published_date, 1, 4) AS published_year FROM books;
```
*What it does: create a new column `published_year` from **book** table, using first 4 digit from published_date column*

```SQL
SELECT LENGTH(name) AS name_length FROM books;
```
*What it does: create a new column `name_length`, count the length of the string from name column and store into `name_length`*

```SQL
SELECT COUNT(*) AS total_books FROM books;
```
*What it does: count total items in table **books** and output to `total_books`.

```SQL
SELECT SUM(price) AS total_price FROM books;
```
*What it does: count total sum of **price** colume and output to total_price.

```SQL
SELECT MAX(published_date) AS latest_book FROM books;
```
*What it does: get max value from **published_date** and output `latest_book` from book table* 

```SQL
SELECT MIN(published_date) AS earliest_book FROM books;
```
*What it does: get min value from **published_date** and output `earliest_book` from book table* 


## Answers & Analysis

### Task 2 Database 101
**Q: What type of database should you consider using if the data you're going to be storing will vary greatly in its format?**
**A:** Non-relational database - because data going to save is not structured, cant save in table format

**Q: What type of database should you consider using if the data you're going to be storing will reliably be in the same structured format?**
**A:** Relational database - because data received are in structured format, so can save in table format.

**Q: In our example, once a record of a book is inserted into our "Books" table, it would be represented as a ___ in that table?**
**A:** Row 

**Q: Which type of key provides a link from one table to another?**
**A:** Foreign key - to provides linking from other table in database

**Q: which type of key ensures a record is unique within a table?**
**A:** Primary key - the unique key within a table when data is stored.

### Task 3 SQL
**Q: What serves as an interface between a database and an end user?**
**A:** DBMS - Database Management System - A software like MySQL managed by end user.

**Q: What query language can be used to interact with a relational database?**
**A:** SQL - Structured query language - a programming language use to query database

### Task 4 Database and Table Statement
**Q: Using the statement you've learned to list all databases, it should reveal a database with a flag for a name; what is it?**
**A:** `THM{575a947132312f97b30ee5aeebba629b723d30f9}` - Once connected to database, issue `SHOW DATABASES;` to list all database and found the flag. 

**Q: In the list of available databases, you should also see the  `task_4_db` database. Set this as your active database and list all tables in this database; what is the flag present here?**
**A:** `THM{692aa7eaec2a2a827f4d1a8bed1f90e5e49d2410}` - Switch to database *task_4_db* by using `USE task_4_db;` and list all tables in database by issuing `SHOW TABLES;` and found the flag.

### Task 5 CRUD Operations
**Q: Using the `tools_db` database, what is the name of the tool in the `hacking_tools` table that can be used to perform man-in-the-middle attacks on wireless networks?**
**A:** Wi-Fi Pineapple - switch to database *tools_db* using `show databases;` and `use tools_db;`, then list the table using `show tables;` and retrieve `hacking_tools` , list down all record in `hacking_tools` using `select * from hacking tools;`

**Q: Using the `tools_db` database, what is the shared category for both **USB Rubber Ducky** and **Bash Bunny?**
**A:** USB attacks - same method as above answer.

### Task 6 Clauses
**Q: Using the `tools_db` database, what is the total number of distinct categories in the `hacking_tools` table?**
**A:** 6 - filter the duplicated data by using `SELECT DISTINCT category FROM hacking_tools;` 

**Q: Using the `tools_db` database, what is the first tool (by name) in ascending order from the `hacking_tools` table?**
**A:** Bash Bunny - sort by name in ascending order `SELECT * FROM hacking_tools ORDER BY name ASC;`

**Q: Using the tools_db database, what is the first tool (by name) in descending order from the hacking_tools table?**
**A:** Wi-Fi Pineapple - sort by name in descending order `SELECT * FROM hacking_tools ORDER BY name DESC;`

### Task 7 Operators
**Q: Using the `tools_db` database, which tool falls under the Multi-tool category and is useful for pentesters and geeks?**
**A:** Flipper Zero - `SELECT * FROM tools_db WHERE category = "multi-tool";` 

**Q: Using the `tools_db` database, what is the category of tools with an amount greater than or equal to 300?**
**A:** RFID cloning - `SELECT * FROM tools_db WHERE amount >= "300" `

**Q: Using the tools_db database, which tool falls under the Network intelligence category with an amount less than 100?**
**A:** Lan Turtle - `SELECT * FROM hacking_tools WHERE category = "Network intelligence" AND amount < "100";`  use ***WHERE*** and ***AND*** clauses. 

### Task 8 Functions
**Q: Using the `tools_db` database, what is the tool with the longest name based on character length?**
**A:** `SELECT name, LENGTH(name) AS name_length FROM hacking_tools ORDER BY name_length ASC;` - count the string of name and sort it by order, add name column so it show name and string_length.

**Q: Using the `tools_db` database, what is the total sum of all tools?**
**A:** `SELECT SUM(amount) AS total_amount FROM hacking_tools;` - use SUM function.

**Q: Using the `tools_db` database, what are the tool names where the amount does not end in 0, and group the tool names concatenated by " & ".**
**A:** `Flipper Zero & iCopy-XS` - use ``SELECT GROUP_CONCAT(name SEPARATOR ' & ') AS tool_names FROM tools_db.hacking_tools WHERE amount % 10 != 0;``

---


## Takeaways

I've hands on some SQL query and understand how the syntax work, plus the last question was hard as it doesnt show in the context, so i have to google to find out whats the correct way to solve that questions. eventually i found out how the query works in order. must write in SELECT → FROM → WHERE → GROUP BY → HAVING →  ORDER BY → LIMIT.
