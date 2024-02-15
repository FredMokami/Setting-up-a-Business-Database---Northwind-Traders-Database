# Project Overview

As a Data Analyst at Northwind Traders, a gourmet food supplier, I have been assigned the responsibility of building and optimizing a MySQL database with the goal of efficiently managing data and ensuring high standards of data quality.

The database will cover multiple aspects of company operations, such as customer details, product information, order records, shipper details, and employee data.

The data, currently in CSV files, needs to be imported into MySQL, and can be accessed by searching ‘Northwind Traders’ from Maven Analytics’ Data Playground.

# The Task

* Create a data dictionary to display information about each field in a database.
* Generate an Entity Relationship Diagram (ERD) to serve as a tool for understanding and reporting data in the Northwind database.
* Create the northwind_db schema to host the necessary related tables for the business based on the Entity Relationship Diagram.
* Establish database entities or tables.
* Set data types and formats.
* Load data from the CSV files into the respective tables.
* Ensure the enforcement of referential integrity constraints.
* Connect to the northwind_db with Tableau and create an executive-level dashboard to visualize KPI performance.

# Data Dictionary

Explore the northwind_db schema data dictionary here:

Entity Relationship Diagram (ERD)

An entity relationship diagram will help us visualize the relationships between tables in our model and will serve as a reference when creating tables.

Here is an Entity Relationship Diagram I created using MySQL Workbench’s Models menu, aligned with the available CSV data:


Northwind_db Entity Relationship Diagram
Database Creation

This script will be utilized to create the northwind_db database:

-- Drop the Northwind database if it exists
DROP DATABASE IF EXISTS northwind_db;

-- Create the Northwind database
CREATE DATABASE northwind_db;

-- Confirm if northwind_db is in the list of databases
SHOW DATABASES;

-- Switch to the Northwind database
USE northwind_db;
Table Creation

Each table will be defined by its name and the nature of the data it will hold. Specifically, we will ensure that each column has an appropriate name and data type based on the available data.

Create these tables to store the CSV data: orders, orders_details, customers, products, categories, employees,and shippers.

orders

Represents customer orders.

CREATE TABLE orders (
   order_id BIGINT NOT NULL,
   customer_id VARCHAR(50) NOT NULL,
   employee_id BIGINT NOT NULL,
   order_date DATE NOT NULL,
   required_date DATE NOT NULL,
   shipped_date DATE,
   shipper_id BIGINT NOT NULL,
   freight DECIMAL(10, 2) NOT NULL,
   PRIMARY KEY (order_id)
 );
We need to set an auto_increment constraint on the primary key for order_idto generate unique IDs automatically when new orders are placed. Additionally, the first order_id will start at 10248 to align with the provided CSV data.

ALTER TABLE orders
MODIFY COLUMN order_id BIGINT AUTO_INCREMENT,
AUTO_INCREMENT = 10248;
order_details

This table contains details of products within orders.

CREATE TABLE order_details (
  order_id BIGINT NOT NULL,
  product_id BIGINT NOT NULL,
  unit_price DECIMAL(10, 2) NOT NULL,
  quantity INT NOT NULL,
  discount DECIMAL(6, 2) NOT NULL,
  PRIMARY KEY (order_id, product_id)
);
The order_details table has a composite primary key which uniquely identifies each record through a combination of the order_id and product_id columns.

I’d prefer a single-column primary key (order_details_id) for its simplicity, readability, and ease of record access.

-- Drop the existing primary key
ALTER TABLE order_details
DROP PRIMARY KEY;

-- Add order_details_id column as primary key
ALTER TABLE order_details
ADD order_details_id BIGINT AUTO_INCREMENT FIRST,
ADD PRIMARY KEY (order_details_id);
customers

Contains information about customers.

CREATE TABLE customers (
  customer_id VARCHAR(50) NOT NULL,
  company_name VARCHAR(50) NOT NULL,
  contact_name VARCHAR(50) NOT NULL,
  contact_title VARCHAR(50) NOT NULL,
  city VARCHAR(50) NOT NULL,
  country VARCHAR(50) NOT NULL,
  PRIMARY KEY (customer_id)
);
products

This table stores information about products.

I applied a CHECK constraint to discontinued to allow only values of 0 or 1, where 0 signifies product availability, and 1 indicates discontinuation.

Additionally, I implemented a UNIQUE constraint on product_name to ensure distinct names for each product.

CREATE TABLE products (
  product_id BIGINT NOT NULL AUTO_INCREMENT,
  product_name VARCHAR(50) NOT NULL,
  quantity_per_unit VARCHAR(50) NOT NULL,
  unit_price DECIMAL(6, 2) NOT NULL,
  discontinued TINYINT CHECK (discontinued IN (0, 1)) NOT NULL,
  category_id INT NOT NULL,
  PRIMARY KEY (product_id),
  UNIQUE (product_name)
);
categories

This table contains information describing product categories.

The unique constraint on category_name column guarantees that each category will have a distinct name.

CREATE TABLE categories (
  category_id INT NOT NULL AUTO_INCREMENT,
  category_name VARCHAR(50) NOT NULL,
  category_description VARCHAR(255) NOT NULL,
  PRIMARY KEY (category_id),
  UNIQUE (category_name)
);
employee

This table stores employee details.

CREATE TABLE employees (
  employee_id BIGINT NOT NULL AUTO_INCREMENT,
  employee_name VARCHAR(50) NOT NULL,
  title VARCHAR(50) NOT NULL,
  city VARCHAR(50) NOT NULL,
  country VARCHAR(50) NOT NULL,
  reports_to BIGINT,
  PRIMARY KEY (employee_id)
);
shippers

Contains details about shipping companies or shippers.

CREATE TABLE shippers (
  shipper_id BIGINT NOT NULL AUTO_INCREMENT,
  company_name VARCHAR(255) NOT NULL,
  PRIMARY KEY (shipper_id),
  UNIQUE (company_name)
);
Load Data

Now that our database and tables are set up, we will proceed to import CSV data. We can either use the LOAD DATA INFILE statement to import data via the command line or use the import wizard in MySQL’s user interface. For this project, I will be using the import wizard.

The wizard is accessible from the object browser’s context menu by right-clicking on a table and choosing Table Data Import Wizard. This process will be repeated for each table.

Enforce Referential Integrity

After loading the data, we need to link our tables.

Referential integrity ensures the accuracy and consistency of data across related tables. It guarantees that foreign keys in one table point to valid primary keys in another, preventing inconsistencies and maintaining data integrity.

We will refer to the to the Entity Relationship Diagram we created earlier to help us understand relationships between tables.

-- orders foreign keys
ALTER TABLE orders
  ADD FOREIGN KEY (customer_id) REFERENCES customers(customer_id),
  ADD FOREIGN KEY (employee_id) REFERENCES employees(employee_id),
  ADD FOREIGN KEY (shipper_id) REFERENCES shippers(shipper_id);

-- order_details foreign keys
ALTER TABLE order_details
  ADD FOREIGN KEY (order_id) REFERENCES orders(order_id),
  ADD FOREIGN KEY (product_id) REFERENCES products(product_id);

-- products foreign key
ALTER TABLE products
  ADD FOREIGN KEY (category_id) REFERENCES categories(category_id);

-- employees - self-referencing foreign key
ALTER TABLE employees
  ADD FOREIGN KEY (reports_to) REFERENCES employees(employee_id);
Northwind Traders’ Performance Dashboard

After connecting Tableau to the Northwind database, here’s the dashboard I designed to assist the executive team in tracking key performance areas for the current year (2015 YTD), including sales, shipping costs, orders, and customer trends, enabling them to make data-driven decisions for the business.


You can interact with this dashboard on my Tableau public profile.

Thanks for reading! Please feel free to share any advice on how to improve this project.

I will walk you through Key Performance Indicators analysis with SQL in an upcoming post.# Setting-up-a-Business-Database---Northwind-Traders-Database
