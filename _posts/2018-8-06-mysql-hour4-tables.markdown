---
layout: post
title:  "Normalizing MySQL Data"
date:   2018-08-05 11:45:00 -0700
categories: SQL
---
I just finished the fourth hour, of the 24 Hour SQL book, which is titled The Normalization Process. Check out my [GitHub] for my solutions to the quiz & exercises. The exercise for Hour 4 is to normalize data for a small company. There isn't much data, but there's certainly enough to construct tables. Here's that data:

#### Employees:

* Angela Smith, secretary, 317-545-6789, RR 1 Box 73, Greensburg, Indiana,
47890, $9.50 per hour, date started January 22, 1996, SSN is 323149669.
* Jack Lee Nelson, salesman, 3334 N Main St, Brownsburg, IN, 45687, 317-852-
9901, salary of $35,000.00 per year, SSN is 312567342, date started 10/28/95.

#### Customers:

* Robert’s Games and Things, 5612 Lafayette Rd, Indianapolis, IN, 46224, 317-
291-7888, customer ID is 432A.
* Reed’s Dairy Bar, 4556 W 10th St, Indianapolis, IN, 46245, 317-271-9823, customer
ID is 117A.

#### Customer Orders:

* Customer ID is 117A, date of last order is December 20, 1999, product ordered
was napkins, and the product ID is 661.

Angela Smith doesn't have a yearly salary, but Jack Lee Nelson does, so I made separate entries for salary and hourly rate. The rest of the choices for 'Employees' are self-explanatory. I didn't choose to have first, middle and last name information for the customers because those are listed to have singular company names. I've chosen to include 'CUST_ID' in the 'Products' table because I plan to use it as a foreign key to link back to the customers table. Also, check out this neat table I made! If you wanna learn how to write in Markdown, check out the [Markdown Cheatsheet].

| Employees             | Customers     | Products      |
| :-----------:         |:-------------:| :-----:       |
| EMPLOYEE_NAME         | CUSTOMER_NAME | CUST_ID       |
| EMPLOYEE_POSITION     | CUST_STREET   | DATE_ORDERED  |
| EMPLOYEE_PHONE_NUMBER | CUST_STATE    | PRODUCT       |
| EMPLOYEE_STREET       | CUST_ZIP      | PRODUCT_ID    |
| EMPLOYEE_CITY         | CUST_PHONE    |               |
| EMPLOYEE_ZIP          | CUST_ID       |               |
| EMPLOYEE_STATE        |               |               |
| EMPLOYEE_SSN          |               |               |
| EMPLOYEE_SALARY       |               |               |
| EMPLOYEE_HOURLY_RATE  |               |               |
| EMPLOYEE_START_DATE   |               |               |

The second exercise for Hour 4 is to create the tables that were just normalized. The authors suggest to use the same 'learnsql' database that is used for the rest of the textbook, but I'm concerned that it'll get messy. That's why I've decided to create a new database that I'm calling 'HOUR4'. Here's the code I used in ther Ubuntu terminal to get up and going:

```console
mysql -h localhost -u root -p
create database HOUR4;
use HOUR4;
```
I decided to use a constraint rather than an in-line 'primary key' declaration for 'EMPLOYEE_SSN'. It'd probably be better to use an employee id for security reasons, but this is all just workshopping, so it's no big deal. I chose 'VARCHAR(11)' to store social securityy numbers because I was thinking of having a format like '000-00-0000'. However, I chose the opposite style for storing phone numbers with 'CHAR(10)'; I'm just playing around with different styles, so please don't judge.

The '-' probably take up too much space in a real database, but I liked the readability of that format. The author tends to leave phone numbers as 'NULL', but I think that's crazy because these are the employees for a hypothetical company. How are you supposed to call your staff? I could've normalized this database further to split between employee information and employee salary information, but that seemed like extra work *and* the answer key doesn't bother to go into that level of normalization.
```sql
CREATE TABLE EMPLOYEES
(
  EMPLOYEE_SSN          VARCHAR(11)   NOT NULL,
  EMPLOYEE_FIRST_NAME   VARCHAR(15)   NOT NULL,
  EMPLOYEE_MIDDLE_NAME  VARCHAR(15),
  EMPLOYEE_LAST_NAME    VARCHAR(15)   NOT NULL,
  EMPLOYEE_POSITION     VARCHAR(15)   NOT NULL,
  EMPLOYEE_PHONE        CHAR(10)      NOT NULL,
  EMPLOYEE_STREET       VARCHAR(30)   NOT NULL,
  EMPLOYEE_CITY         VARCHAR(15)   NOT NULL,
  EMPLOYEE_ZIP          INTEGER(5)    NOT NULL,
  EMPLOYEE_STATE        CHAR(2)       NOT NULL,
  EMPLOYEE_SALARY       DECIMAL(8,2)  NOT NULL,
  EMPLOYEE_HOURLY_RATE  DECIMAL(4,2)  NOT NULL,
  EMPLOYEE_START_DATE   DATE,
  CONSTRAINT EMPLOY_PK  PRIMARY KEY (EMPLOYEE_SSN)
);
```
Here I've declared 'CUST_ID' to be a 'primary key' in-line. I don't think any of these rows should be 'NULL' because all of this information is essential for the company to be able to contact and/or send products to the customers.
```sql
CREATE TABLE CUSTOMERS
(
  CUST_ID       VARCHAR(10)   NOT NULL primary key,
  CUST_NAME     VARCHAR(30)   NOT NULL,
  CUST_STREET   VARCHAR(30)   NOT NULL,
  CUST_CITY     VARCHAR(15)   NOT NULL,
  CUST_STATE    CHAR(2)       NOT NULL,
  CUST_ZIP      INTEGER(5)    NOT NULL,
  CUST_PHONE    CHAR(10)      NOT NULL
);
```
Note that the 'CUST_ID' is declared as a 'FOREIGN KEY' for the 'CUSTOMERS' table.
```sql
CREATE TABLE ORDERS
(
  PRODUCT_ID    VARCHAR(10)   NOT NULL primary key,
  CUST_ID       VARCHAR(10)   NOT NULL,
  DATE_ORDERED  DATE          NOT NULL,
  PRODUCT_NAME  VARCHAR(30)   NOT NULL,
  CONSTRAINT CUST_FK FOREIGN KEY (CUST_ID) REFERENCES CUSTOMERS (CUST_ID)
);
```

That's all for the fourth hour of Teach Yourself SQL in 24 Hours. I'll see you in another article!

[GitHub]:https://github.com/DaveHalvorsen/SQL_in_24_Hours
[Markdown Cheatsheet]:https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet#tables
