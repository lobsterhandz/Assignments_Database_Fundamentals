# BookHaven Database Design

## ERD Diagram

![ERD](./images/erd.png)

## Objective
The aim of this assignment is to apply the concepts of relational database design, normalization, and entity-relationship modeling to create an efficient and structured database for a bookstore management system, "BookHaven."

## Problem Statement
"BookHaven" is facing challenges in managing its extensive collection of books, author information, customer data, and transaction records. The current system has issues with data redundancy, inconsistency, and inefficient data retrieval. Your task is to design a relational database that addresses these problems while ensuring data integrity and ease of access.
## ERD Diagram

![ERD](./images/erd.png)

## Task 1: Database Schema Design

### Tables and Columns
1. **Books**
   - `book_id` (Primary Key): INT, AUTO_INCREMENT
   - `title`: VARCHAR(255)
   - `author_id` (Foreign Key): INT
   - `genre`: VARCHAR(100)
   - `price`: DECIMAL(10, 2)
   - `publication_date`: DATE
   - `stock`: INT

2. **Authors**
   - `author_id` (Primary Key): INT, AUTO_INCREMENT
   - `name`: VARCHAR(255) NOT NULL
   - `bio`: TEXT

3. **Customers**
   - `customer_id` (Primary Key): INT, AUTO_INCREMENT
   - `first_name`: VARCHAR(255) NOT NULL
   - `last_name`: VARCHAR(255) NOT NULL
   - `email`: VARCHAR(255) NOT NULL
   - `phone`: VARCHAR(15)
   - `address`: VARCHAR(255)

4. **Transactions**
   - `transaction_id` (Primary Key): INT, AUTO_INCREMENT
   - `customer_id` (Foreign Key): INT
   - `book_id` (Foreign Key): INT
   - `transaction_date`: DATE NOT NULL
   - `quantity`: INT NOT NULL
   - `total_price`: DECIMAL(10, 2) NOT NULL

### Example SQL Statements to Create the Tables

```sql
-- Authors Table
CREATE TABLE Authors (
    author_id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(255) NOT NULL,
    bio TEXT
);

-- Books Table
CREATE TABLE Books (
    book_id INT AUTO_INCREMENT PRIMARY KEY,
    title VARCHAR(255) NOT NULL,
    author_id INT,
    genre VARCHAR(100),
    price DECIMAL(10, 2),
    publication_date DATE,
    stock INT,
    FOREIGN KEY (author_id) REFERENCES Authors(author_id)
);

-- Customers Table
CREATE TABLE Customers (
    customer_id INT AUTO_INCREMENT PRIMARY KEY,
    first_name VARCHAR(255) NOT NULL,
    last_name VARCHAR(255) NOT NULL,
    email VARCHAR(255) NOT NULL,
    phone VARCHAR(15),
    address VARCHAR(255)
);

-- Transactions Table
CREATE TABLE Transactions (
    transaction_id INT AUTO_INCREMENT PRIMARY KEY,
    customer_id INT,
    book_id INT,
    transaction_date DATE NOT NULL,
    quantity INT NOT NULL,
    total_price DECIMAL(10, 2) NOT NULL,
    FOREIGN KEY (customer_id) REFERENCES Customers(customer_id),
    FOREIGN KEY (book_id) REFERENCES Books(book_id)
);
