# Book Collection Database

This project demonstrates how to create and manage a simple SQLite database for a collection of books using Python in a Google Colab environment. The project includes steps to create the database, insert records, and perform various SQL queries to retrieve and manipulate the data.

## Table of Contents

- [Overview](#overview)
- [Setup](#setup)
- [Creating the Database Table](#creating-the-database-table)
- [Inserting Data into the Table](#inserting-data-into-the-table)
- [Writing SQL Queries](#writing-sql-queries)
- [Closing the Database Connection](#closing-the-database-connection)
- [License](#license)

## Overview

This project involves the following tasks:

1. Creating a `Books` table in an SQLite database.
2. Inserting sample book records into the table.
3. Writing and executing various SQL queries to explore and manipulate the data.
4. Displaying query results directly in the Google Colab notebook.

## Setup

To run this project, you'll need access to a Google Colab environment. The following steps guide you through setting up and running the project in Colab:

1. **Clone or download the repository.**
2. **Open the `books_database.ipynb` notebook in Google Colab.**
3. **Run each code cell sequentially** to create the database, insert data, and execute SQL queries.

## Creating the Database Table

The database table is created using the following SQL command:

```python
import sqlite3

# Connect to SQLite database (it will create a new database file if it doesn't exist)
conn = sqlite3.connect('books.db')

# Create a cursor object to execute SQL commands
cursor = conn.cursor()

# Create the Books table
cursor.execute('''
CREATE TABLE IF NOT EXISTS Books (
  BookID INTEGER PRIMARY KEY AUTOINCREMENT,
  Title TEXT NOT NULL,
  Author TEXT NOT NULL,
  Genre TEXT,
  PublishedYear INTEGER,
  Price REAL,
  ISBN TEXT UNIQUE
)
''')

# Commit the changes
conn.commit()
```

## Inserting Data into the Table

After creating the table, we insert the following sample records:

```python
# Insert records into the Books table
cursor.executemany('''
INSERT INTO Books (Title, Author, Genre, PublishedYear, Price, ISBN) 
VALUES (?, ?, ?, ?, ?, ?)
''', [
    ('To Kill a Mockingbird', 'Harper Lee', 'Fiction', 1960, 10.99, None),
    ('1984', 'George Orwell', 'Dystopian', 1949, 8.99, '9780451524935'),
    ('The Great Gatsby', 'F. Scott Fitzgerald', 'Classic', 1925, 12.50, '9780743273565'),
    ('The Catcher in the Rye', 'J.D. Salinger', 'Classic', 1951, 7.99, None),
    ('Pride and Prejudice', 'Jane Austen', 'Romance', 1813, 9.99, '9780141439518')
])

# Commit the changes
conn.commit()
```

## Writing SQL Queries

The following SQL queries are executed to explore and manipulate the data:

- **Retrieve All Records:**

  ```python
  cursor.execute('SELECT * FROM Books')
  all_books = cursor.fetchall()
  ```

- **List Distinct Genres:**

  ```python
  cursor.execute('SELECT DISTINCT Genre FROM Books')
  distinct_genres = cursor.fetchall()
  ```

- **Filter by Price:**

  ```python
  cursor.execute('SELECT * FROM Books WHERE Price < 10')
  cheap_books = cursor.fetchall()
  ```

- **Order by Year:**

  ```python
  cursor.execute('SELECT * FROM Books ORDER BY PublishedYear ASC')
  ordered_books = cursor.fetchall()
  ```

- **Filter with Multiple Conditions:**

  ```python
  cursor.execute('''
  SELECT * FROM Books
  WHERE (Genre = 'Classic' OR Price BETWEEN 8.00 AND 12.00)
  AND PublishedYear >= 1950
  ''')
  filtered_books = cursor.fetchall()
  ```

- **Find NULL ISBNs:**

  ```python
  cursor.execute('SELECT * FROM Books WHERE ISBN IS NULL')
  books_with_null_isbn = cursor.fetchall()
  ```

- **Use of IN Clause:**

  ```python
  cursor.execute("SELECT * FROM Books WHERE Author IN ('Harper Lee', 'George Orwell')")
  specific_authors_books = cursor.fetchall()
  ```

- **Apply an Alias:**

  ```python
  cursor.execute('SELECT Title, Price AS Cost FROM Books')
  books_with_cost = cursor.fetchall()
  ```

Each query's results are printed in the Colab notebook for review.

## Closing the Database Connection

After performing all the queries, it's important to close the database connection to ensure all changes are saved:

```python
# Close the connection
conn.close()
```
