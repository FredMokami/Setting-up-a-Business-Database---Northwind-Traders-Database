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

Explore the northwind_db schema data dictionary [here](https://docs.google.com/document/d/1aerklP4KTvpbVj7pnZTngDIbgp8oHB3qykUmFSW9zVY/edit#heading=h.he9pyhahsu72)

# Entity Relationship Diagram (ERD)

An entity relationship diagram will help us visualize the relationships between tables in our model and will serve as a reference when creating tables.

Here is an Entity Relationship Diagram I created using MySQL Workbench’s Models menu, aligned with the available CSV data:

![image](https://github.com/FredMokami/Setting-up-a-Business-Database---Northwind-Traders-Database/assets/132344241/f96e6007-4860-4300-95d0-8513e05969e6)
```Northwind_db Entity Relationship Diagram```

# Database Creation

This script will be utilized to create the northwind_db database:

![Screenshot 2024-02-15 132159](https://github.com/FredMokami/Setting-up-a-Business-Database---Northwind-Traders-Database/assets/132344241/2d068841-feae-4123-b888-c17ff9d364e4)

# Table Creation

Each table will be defined by its name and the nature of the data it will hold. Specifically, we will ensure that each column has an appropriate name and data type based on the available data.

Create these tables to store the CSV data: ```orders```, ```orders_details```, ```customers```, ```products```, ```categories```, ```employees```,and ```shippers```.

```orders``` - represents customer orders.

![1](https://github.com/FredMokami/Setting-up-a-Business-Database---Northwind-Traders-Database/assets/132344241/4df7aa03-b1bc-4e16-911e-d4f953d22769)


We need to set an ```auto_increment``` constraint on the primary key for order_idto generate unique IDs automatically when new orders are placed. Additionally, the first order_id will start at 10248 to align with the provided CSV data.

![2](https://github.com/FredMokami/Setting-up-a-Business-Database---Northwind-Traders-Database/assets/132344241/c33b6641-4ee5-4267-b05f-b288c2b73f10)


```order_details``` - this table contains details of products within orders.

![image](https://github.com/FredMokami/Setting-up-a-Business-Database---Northwind-Traders-Database/assets/132344241/7c9e99e7-31d7-4af1-9e9a-5775f8468e2a)


The ```order_details``` table has a composite primary key which uniquely identifies each record through a combination of the order_id and product_id columns.

I’d prefer a single-column primary key (```order_details_id```) for its simplicity, readability, and ease of record access.

![3](https://github.com/FredMokami/Setting-up-a-Business-Database---Northwind-Traders-Database/assets/132344241/4fa17896-8f95-44ee-b9c0-7ada9cc3cc03)


```customers``` - contains information about customers.

![4](https://github.com/FredMokami/Setting-up-a-Business-Database---Northwind-Traders-Database/assets/132344241/a83a6d1e-9493-4ca0-a20e-c4d0d5b93f33)

```products``` - this table stores information about products.

I applied a ```CHECK``` constraint to discontinued to allow only values of 0 or 1, where 0 signifies product availability, and 1 indicates discontinuation.

Additionally, I implemented a ```UNIQUE``` constraint on product_name to ensure distinct names for each product.

![5](https://github.com/FredMokami/Setting-up-a-Business-Database---Northwind-Traders-Database/assets/132344241/c19421ff-602c-4844-9351-bd6268948a70)

```categories``` - this table contains information describing product categories.

The ```UNIQUE``` constraint on ```category_name``` column guarantees that each category will have a distinct name.

![6](https://github.com/FredMokami/Setting-up-a-Business-Database---Northwind-Traders-Database/assets/132344241/63ca0b3f-9124-4447-aaa1-9b9b6678f609)

```employee``` - this table stores employee details.

![8](https://github.com/FredMokami/Setting-up-a-Business-Database---Northwind-Traders-Database/assets/132344241/1c8454da-5b71-4305-9cc2-18f1b52edf6d)


```shippers``` - contains details about shipping companies or shippers.

![image](https://github.com/FredMokami/Setting-up-a-Business-Database---Northwind-Traders-Database/assets/132344241/f05a009d-1ead-4126-8318-eb021062f540)

# Load Data

Now that our database and tables are set up, we will proceed to import CSV data. We can either use the ```LOAD DATA INFILE``` statement to import data via the command line or use the import wizard in MySQL’s user interface. For this project, I will be using the import wizard.

The wizard is accessible from the object browser’s context menu by right-clicking on a table and choosing Table Data Import Wizard. This process will be repeated for each table.

# Enforce Referential Integrity

After loading the data, we need to link our tables.

Referential integrity ensures the accuracy and consistency of data across related tables. It guarantees that foreign keys in one table point to valid primary keys in another, preventing inconsistencies and maintaining data integrity.

We will refer to the to the Entity Relationship Diagram we created earlier to help us understand relationships between tables.

![image](https://github.com/FredMokami/Setting-up-a-Business-Database---Northwind-Traders-Database/assets/132344241/84c3c8cf-e9a8-4888-a0e2-a3b1579c931c)


After connecting Tableau to the Northwind database, here’s the dashboard I designed to assist the executive team in tracking key performance areas for the current year (2015 YTD), including sales, shipping costs, orders, and customer trends, enabling them to make data-driven decisions for the business.


You can interact with this dashboard on my Tableau public profile.

Thanks for reading! Please feel free to share any advice on how to improve this project.

I will walk you through Key Performance Indicators analysis with SQL in an upcoming post.# Setting-up-a-Business-Database---Northwind-Traders-Database
