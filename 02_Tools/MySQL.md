# MySQL Cheatsheet

## Table of Contents

* [Getting Started](#getting-started)
* [Database Statements](#database-statements)
* [Table Statements](#table-statements)
* [Examples](#examples)
---

## Getting Started

```bash
mysql -u USER          # Launch mysql
```

## Database Statements

```bash
CREATE DATABASE <database_name>;            # Create a new database
SHOW DATABASES;                             # Show all databases
USE <database_name>;                        # Select a database to use
DROP database <database_name>;              # Remove the database
```

## Table Statements

These statements can be used, once a database is active, menaing selected with `USE <database_name>`.

```bash
CREATE TABLE example_table_name (           # Create a new table in the selected database
    example_column1 data_type,
    example_column2 data_type,
    example_column3 data_type
);

SHOW TABLES;                                # List all the tables in the selected database
DESCRIBE <table_name>;                      # List information about the table

ALTER TABLE book_inventory                  # Change the table
ADD page_count INT;

DROP <table_name>;                          # Remove a table
```

## Examples
```bash
CREATE TABLE book_inventory (
    book_id INT AUTO_INCREMENT PRIMARY KEY,
    book_name VARCHAR(255) NOT NULL,
    publication_date DATE
);
```

