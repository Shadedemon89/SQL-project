# SQL-project
🗄️ Data Technician Week 3 — Databases & SQL Portfolio







📌 Overview

This repository documents my Data Technician Week 3 work, focused on databases, relational database design, SQL, PostgreSQL and Supabase.

During the week I explored database relationships and Entity Relationship Diagrams (ERDs), compared relational and non-relational databases, studied different SQL JOIN types, designed a database for a retail scenario, and completed practical PostgreSQL query exercises using the World combined 30 dataset in Supabase.

🛠️ Skills Demonstrated

SQL

PostgreSQL

Supabase

Relational databases

Non-relational / NoSQL concepts

Entity Relationship Diagrams (ERDs)

Primary and foreign keys

Database relationships

Database schema design

SQL JOINs

Data filtering and sorting

Aggregate functions

GROUP BY and HAVING

Subqueries

Data-quality checks

Database security and backups

Debugging SQL syntax

🧩 Database Fundamentals

Entity Relationship Diagram

As part of the database fundamentals work, I created an ERD to visualise how tables can be connected through keys and relationships.

The exercise helped reinforce how a database can be separated into logical tables while still allowing related information to be queried together.

🔑 Primary & Foreign Keys

The project explored the role of keys within relational databases.

Primary Key

A primary key uniquely identifies a record within a table.

Example:

CustomerID INT PRIMARY KEY

Foreign Key

A foreign key connects a record in one table to a primary key in another table.

Example:

SupplierID INT REFERENCES Suppliers(SupplierID)

This allows related tables to work together without unnecessarily duplicating data.

🔗 Database Relationships

The workbook explored common database relationship types:

Relationship

Example

One-to-One

A person associated with a unique identification record

One-to-Many

One football manager responsible for multiple players

Many-to-Many

Customers holding accounts across banks, while banks have many customers

Understanding these relationships is important when designing efficient relational databases and deciding where primary and foreign keys should be placed.

🗃️ Relational vs Non-Relational Databases

Relational Databases

Relational databases organise structured data into tables and allow relationships to be established between those tables.

Typical use cases include:

Customers

Sales

Products

Inventory

Suppliers

Transactions

Non-Relational Databases

The workbook also explored non-relational database concepts and how more flexible models may be useful for rapidly changing or less structured information.

A retail environment with seasonal products, changing offers and large volumes of incoming information was considered as an example where flexibility can be useful.

🔀 SQL JOINs

I researched several JOIN types and how they can be used to combine relational data.

INNER JOIN

Returns matching records from the tables being joined.

SELECT *
FROM Sales
INNER JOIN Customers
    ON Sales.CustomerID = Customers.CustomerID;

LEFT JOIN

Returns every record from the left table and matching records from the right table.

RIGHT JOIN

Returns every record from the right table and matching records from the left table.

FULL JOIN

Returns records from both tables, including rows without a match.

CROSS JOIN

Produces combinations between rows from two tables.

SELF JOIN

Joins a table to itself, which can be useful when comparing records stored in the same table.

🏪 Retail Database Design Project

A major Week 3 task involved considering how a database could support a retail business.

The database needed to support areas including:

Inventory

Sales

Suppliers

Customers

Loyalty information

Example Tables

Inventory

SKU
ProductName
ProductCategory
Price
StockCount
SupplierID

Sales

TransactionID
TransactionDate
Quantity
SKU
CustomerID

Suppliers

SupplierID
SupplierName
SupplierContactDetails

Customers

CustomerID
Name
Address
ContactNumber
Email
MembershipStatus
PointsTotal

These tables can be connected using primary and foreign keys so that sales can be related back to products, customers and suppliers.

🏗️ SQL Database Creation

The project included practising SQL statements for creating databases and tables.

Example:

CREATE DATABASE TescoExpress;

A simplified inventory table could be created as:

CREATE TABLE Inventory (
    SKU INT PRIMARY KEY,
    ProductName VARCHAR(100),
    ProductCategory VARCHAR(100),
    Price DECIMAL(10,2),
    StockCount INT,
    SupplierID INT,
    FOREIGN KEY (SupplierID)
        REFERENCES Suppliers(SupplierID)
);

And a supplier table:

CREATE TABLE Suppliers (
    SupplierID INT PRIMARY KEY,
    SupplierName VARCHAR(100),
    ContactDetails VARCHAR(255)
);

This exercise helped me understand how a logical database design is translated into an actual SQL schema.

➕ Populating a Database

After creating tables, records can be added using INSERT INTO.

Example:

INSERT INTO Inventory
    (SKU, ProductName, ProductCategory, Price, StockCount, SupplierID)
VALUES
    (1, 'Dairy Milk', 'Confectionery', 1.50, 25, 101);

This demonstrated the transition from defining a database structure to populating it with usable data.

🔐 Database Maintenance & Security

The project also considered how a database should be maintained after implementation.

Important considerations included:

Consistent data-entry standards

Standard date and price formats

Regular checks for incorrect records

Duplicate-data checks

Regular backups

Strong passwords

User access levels

Permissions

Data encryption

Appropriate protection of customer information

These controls help maintain data quality, availability, confidentiality and integrity.

🐘 PostgreSQL Practical — Supabase

The practical section used PostgreSQL queries against the World combined 30 dataset in Supabase.

A key part of the exercise was identifying minor errors in SQL queries, correcting them, running the queries and explaining what had been fixed.

This developed both SQL-writing and SQL-debugging skills.

🔎 Basic Selection & Filtering

Distinct Countries

SELECT DISTINCT country_name
FROM world_combined_30;

This query returns a unique list of countries.

Languages Spoken in Angola

SELECT language,
       language_percentage
FROM world_combined_30
WHERE country_name = 'Angola'
ORDER BY language_percentage DESC;

In the workbook exercise, Ovimbundo appeared at the top with a language percentage of 37.2.

Countries Where English Appears

SELECT DISTINCT
       country_name,
       country_code
FROM world_combined_30
WHERE language = 'English';

Population Range

SELECT DISTINCT
       country_name,
       country_population
FROM world_combined_30
WHERE country_population BETWEEN 100000 AND 3000000
ORDER BY country_population;

This exercise reinforced filtering numerical data with BETWEEN.

📊 Aggregation

Count Language Rows by Country

SELECT country_name,
       COUNT(*) AS language_count
FROM world_combined_30
GROUP BY country_name
ORDER BY language_count DESC;

This demonstrates the use of:

COUNT()

GROUP BY

aliases

descending sorting

Maximum Language Percentage

SELECT country_name,
       MAX(language_percentage) AS max_language_percentage
FROM world_combined_30
GROUP BY country_name
ORDER BY max_language_percentage DESC;

Countries With a Language Above 50%

SELECT DISTINCT country_name
FROM world_combined_30
WHERE language_percentage > 50;

🧮 GROUP BY & HAVING

The practical exercises also introduced filtering aggregated results.

For example, countries with more than one official language can be identified with:

SELECT country_name,
       COUNT(*) AS official_language_count
FROM world_combined_30
WHERE is_official = TRUE
GROUP BY country_name
HAVING COUNT(*) > 1
ORDER BY official_language_count DESC;

This helped demonstrate the difference between:

WHERE — filtering rows before aggregation

HAVING — filtering groups after aggregation

🔍 Pattern Matching

The exercises included using LIKE to search text fields.

For example:

SELECT *
FROM world_combined_30
WHERE city_name LIKE '%la%';

The % wildcard allows SQL to match text appearing anywhere within a value.

🧠 Subqueries

More advanced exercises introduced subqueries.

An example is finding countries whose population is above the overall average:

SELECT DISTINCT
       country_name,
       country_population
FROM world_combined_30
WHERE country_population > (
    SELECT AVG(country_population)
    FROM world_combined_30
);

This demonstrates how the result of one query can be used as a condition inside another query.

🧹 SQL for Data Quality

SQL can also be used to identify potential data-quality issues.

For example, the workbook included an exercise to identify countries where recorded language percentages total less than 100:

SELECT country_name,
       SUM(language_percentage) AS total_language_share
FROM world_combined_30
GROUP BY country_name
HAVING SUM(language_percentage) < 100
ORDER BY total_language_share;

This demonstrates that SQL is useful not only for retrieving information but also for validating and investigating datasets.

🐞 SQL Debugging

A particularly useful part of the practical work involved correcting incomplete or incorrect queries.

Examples of issues investigated included:

Missing table names after FROM

Missing column names in WHERE

Missing Boolean values

Missing comparison operators

Missing DESC

Incomplete HAVING conditions

Incorrect ORDER BY expressions

Missing values inside aggregate functions

Incomplete LIKE patterns

Debugging these queries improved my understanding of SQL syntax and helped me become more confident interpreting database error messages.

📚 Key SQL Commands Practised

SELECT
SELECT DISTINCT
FROM
WHERE
ORDER BY
GROUP BY
HAVING
COUNT()
MAX()
SUM()
AVG()
BETWEEN
LIKE
INSERT INTO
CREATE TABLE
CREATE DATABASE

I also practised:

PRIMARY KEY
FOREIGN KEY
INNER JOIN
LEFT JOIN
RIGHT JOIN
FULL JOIN
CROSS JOIN
SELF JOIN



🎯 What I Learned

Developed my understanding of how databases are designed, connected, queried and maintained.

I gained practical experience with:

Designing relational database structures

Understanding primary and foreign keys

Creating ERDs

Identifying database relationship types

Comparing relational and non-relational approaches

Using SQL JOINs

Creating and populating SQL tables

Filtering and sorting data

Aggregating data with SQL

Using GROUP BY and HAVING

Writing subqueries

Performing simple data-quality checks

Debugging incorrect SQL

Working with PostgreSQL through Supabase

Considering database security and backup requirements

These exercises strengthened my ability to move beyond analysing prepared datasets and understand the database layer where organisational data is structured, stored and queried.

👤 Author

Robert Anderson / Shadedemon89

This repository forms part of my Data Technician / Data Analyst portfolio and demonstrates practical experience with SQL, PostgreSQL, Supabase, database design, relational modelling, data quality and database security.
