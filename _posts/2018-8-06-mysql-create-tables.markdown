---
layout: post
title:  "Creating Tables in MySQL"
date:   2018-08-05 11:45:00 -0700
categories: SQL
---
This is a continuation of my walkthrough of the Sams Teach Yourself SQL in 24 Hours. I've already completed the [Relational Database Design and SQL Programming class], but I think it's always important to be learning more. I just finished the third hour, of the 24 Hour SQL book, which is titled Managing Database Objects. Check out my [GitHub] for my solutions to the quiz. In this article I'll describe how I completed the exercises component.

Now, lets check out some MySQL commands. I created the database in the last article, so check that one out for some backstory. I'm doing this in Ubuntu Linux, so the commands might slightly differ for you Windows folks. For example, the book says to use 'Mysql -h localhost -u username -ppassword' to log into the database, but capitalizing the first letter of 'mysql' in Linux throws an error.
```console
mysql -h localhost -u root -p
```

This chapter's exercise call for adding several tables to a database. First, here's how to create the 'learnsql' database that the activities call for. Also, I've included how to start using the desired database.
```console
create database learnsql;
use learnsql;
```

You'll find the syntax that I used to create the five required tables below. I'll be describing some of the commands in more detail where I see fit. CREATE TABLE is fairly obvious; it's how I create the tables. CAPITALZING everything isn't required for commands to work, but it is the preferred syntax. You shouldn't be trying to type the commands into the terminal and run them each time; you'll run into loads of errors doing that. I recommend typing the commands into a code editor (I use Atom), checking them for errors, and then copying them int their entirety to be run in the MySQL window. You should use tabbing to make the columns line up, otherwise it'll be much harder to read and to spot errors.
```sql
CREATE TABLE EMPLOYEE_TBL
(
  EMP_ID      VARCHAR(9)  NOT NULL,
  LAST_NAME   VARCHAR(15) NOT NULL,
  FIRST_NAME  VARCHAR(15) NOT NULL,
  MIDDLE_NAME VARCHAR(15),
  ADDRESS     VARCHAR(30) NOT NULL,
  CITY        VARCHAR(15) NOT NULL,
  STATE       CHAR(2)     NOT NULL,
  ZIP         INTEGER(5)  NOT NULL,
  PHONE       CHAR(10),
  PAGER       CHAR(10),
  CONSTRAINT  EMP_PK PRIMARY KEY (EMP_ID)
);
```
'VARCHAR' stands for variable character and it can hold letters or numbers. 'NOT NULL' means that that column CANNOT be empty. Note that 'MIDDLE_NAME' does not have the 'NOT NULL' requirement. This is because not everyone has a middle name, so it'd be wrong to force a value there. Be careful to allow the right number of digits for each type. Note the difference between the 15 character allowance for 'FIRST_NAME' vs. the 30 character allowance for 'ADDRESS'.

This is because addresses are typically much longer than names. Be very careful when assigning character lengths for items with *specific* numbers. For example, 'ZIP' will always have 5, 'STATE' will always have 2, and 'PHONE' will always have 10. Note that 'VARCHAR' is used for items with *varying* character lengths and 'CHAR' is used for items that have a *specific* length.  
```sql
CREATE TABLE EMPLOYEE_PAY_TBL
(
  EMP_ID          VARCHAR(9)  NOT NULL primary key,
  POSITION        VARCHAR(15) NOT NULL,
  DATE_HIRE       DATE,
  PAY_RATE        DECIMAL(4,2),
  DATE_LAST_RAISE DATE,
  SALARY          DECIMAL(8,2),
  BONUS           DECIMAL(6,2),
  CONSTRAINT EMP_FK FOREIGN KEY (EMP_ID) REFERENCES EMPLOYEE_TBL (EMP_ID)
);
```
A 'primary key' uniquely identifies each item in a database. Obviously, primary keys cannot be 'NULL'. A given table can only have one primary key (because it's used to lookup individual records). Note that the 'DATE' data type format for data entry is 'YYYY-MM-DD'. 'DECIMAL(p,s)' allows for numbers to have a decimal point; the first number, p, is the total width of the required number, and the second number, s, is the allowed number of digits to the right of the decimal place. A 'FOREIGN KEY' links two tables together by connecting the the 'primary key' of another table. The table containing the foreign key is the child table and the table with the primary key is the parent table.  
```sql
CREATE TABLE CUSTOMER_TBL
(
  CUST_ID       VARCHAR(10) NOT NULL  primary key,
  CUST_NAME     VARCHAR(30) NOT NULL,
  CUST_ADDRESS  VARCHAR(20) NOT NULL,
  CUST_CITY     VARCHAR(15) NOT NULL,
  CUST_STATE    CHAR(2)     NOT NULL,
  CUST_ZIP      INTEGER(5)  NOT NULL,
  CUST_PHONE    CHAR(10),
  CUST_FAX      INTEGER(10)
);
```
An 'INTEGER' data type allows for values between -32,768 and 32,767. In the 'CUST_ZIP' case only values that have a width of 5 are allowed.
```sql
CREATE TABLE ORDERS_TBL
(
  ORD_NUM     VARCHAR(10) NOT NULL primary key,
  CUST_ID     VARCHAR(10) NOT NULL,
  PROD_ID     VARCHAR(10) NOT NULL,
  QTY         INTEGER(6)  NOT NULL,
  ORD_DATE    DATE
);
```
```sql
CREATE TABLE PRODUCTS_TBL
(
  PROD_ID   VARCHAR(10)   NOT NULL  primary key,
  PROD_DESC VARCHAR(40)   NOT NULL,
  COST      DECIMAL(6,2)  NOT NULL
);
```
If you're doing the method I suggest (typing the MySQL commands in a code editor before submitting), you should give them another readthrough to make sure that you've typed them correctly. For example, I mistakenly entered 4 as the 'INTEGER' value for 'CUST_ZIP' on my first try. On my instance of MySQL, correct table entries return this statement in the terminal.

```console
QUERY OK, 0 rows affected (0.01 sec)
```
Once you've finished entering the tables, you can check the list of tables with the command 'show tables;'. It's recommended to use 'describe TABLE_NAME;' for each of the entered tables and compare the result against what you were trying to enter. Yes, this means that I triple checked the entries. If you've ever encountered errors in MySQL before, you know how important it is to check your code before submitting!

```sql
show tables;
describe employee_tbl;
```
That's all for the third hour of Teach Yourself SQL in 24 Hours. I'll see you in another article!

[Relational Database Design and SQL Programming class]:https://www.ucsc-extension.edu/certificate-program/offering/relational-database-design-and-sql-programming
[GitHub]:https://github.com/DaveHalvorsen/SQL_in_24_Hours
