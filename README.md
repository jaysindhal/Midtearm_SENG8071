# Midtearm_SENG8071
# Online Bookstore Database Design

## Team Members and Duties

### Team Members
1. *Ankit*:
    - Responsible for database design and schema creation.
    - Crafting SQL queries for data manipulation and retrieval.
    - Documentation wizard.

2. *Jay*:
    - Expert in SQL DDL/DML statements for table creation and data insertion.
    - Ensuring database integrity and performance.
    - Detailed-oriented in documentation tasks.

## Database Tables

### Authors Table

| Column        | Data Type     | Description                         |
|---------------|---------------|-------------------------------------|
| author_id     | INT           | Primary Key, Auto Increment         |
| name          | VARCHAR(100)  | Author's name                       |
| biography     | TEXT          | Brief biography of the author       |
| birth_date    | DATE          | Author's date of birth              |

### Publishers Table

| Column        | Data Type     | Description                         |
|---------------|---------------|-------------------------------------|
| publisher_id  | INT           | Primary Key, Auto Increment         |
| name          | VARCHAR(100)  | Publisher's name                    |
| address       | VARCHAR(255)  | Publisher's physical address        |
| phone         | VARCHAR(20)   | Publisher's contact number          |

### Books Table

| Column        | Data Type     | Description                         |
|---------------|---------------|-------------------------------------|
| book_id       | INT           | Primary Key, Auto Increment         |
| title         | VARCHAR(200)  | Title of the book                   |
| genre         | VARCHAR(50)   | Genre of the book                   |
| price         | DECIMAL(10, 2)| Price of the book                   |
| publish_date  | DATE          | Publication date of the book        |
| author_id     | INT           | Foreign Key referencing Authors     |
| publisher_id  | INT           | Foreign Key referencing Publishers  |

... (continue with other tables: Customers, Orders, Order_Items, Reviews)

## SQL Queries for Requirements

### Power Writers

Find authors with more than X books in the same genre published within the last X years.

```sql
SELECT author_id, name
FROM Authors
WHERE author_id IN (
    SELECT author_id
    FROM Books
    WHERE genre = 'Fiction' AND publish_date > DATE_SUB(CURDATE(), INTERVAL 4 YEAR)
    GROUP BY author_id
    HAVING COUNT(book_id) > 5
);



























Loyal Customers
Identify customers who have spent more than XXXX dollars in the past year.

SELECT customer_id, name, SUM(total_amount) as total_spent
FROM Orders
JOIN Customers ON Orders.customer_id = Customers.customer_id
WHERE order_date > DATE_SUB(CURDATE(), INTERVAL 2 YEAR)
GROUP BY customer_id
HAVING total_spent > 1000;


Well Reviewed Books
List books that have a better user rating than average.





SELECT book_id, title, AVG(rating) as average_rating
FROM Reviews
JOIN Books ON Reviews.book_id = Books.book_id
GROUP BY book_id
HAVING average_rating > (SELECT AVG(rating) FROM Reviews);














Sample Data Creation
Here's an example of how we populate our database with initial data:

-- Insert sample data into the Books table
INSERT INTO Books (title, genre, price, publish_date, author_id, publisher_id)
VALUES ('The Great Gatsby', 'Fiction', 10.99, '1925-04-10', 1, 1);

INSERT INTO Books (title, genre, price, publish_date, author_id, publisher_id)
VALUES ('To Kill a Mockingbird', 'Fiction', 7.99, '1960-07-11', 2, 2);

-- Add more sample data as needed for other t
