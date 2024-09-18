 

# Book Database with SQLite in Python

This project demonstrates how to create, insert, and query a simple books database using SQLite in Python. The project is implemented using an in-memory database in Google Colab, where data is temporarily stored and various SQL queries are executed.

## Table of Contents
- [Overview](#overview)
- [Requirements](#requirements)
- [Setup and Execution](#setup-and-execution)
- [SQL Queries](#sql-queries)
- [Sample Queries](#sample-queries)

## Overview
This project covers the following tasks:
1. Creating a table named `Books` with columns for `BookID`, `Title`, `Author`, `Genre`, `PublishedYear`, `Price`, and `ISBN`.
2. Inserting sample data into the `Books` table.
3. Running various SQL queries to retrieve and manipulate the data, such as filtering, ordering, and applying conditions.

## Requirements
This project is designed to run in Google Colab or any environment with Python 3.x and the following libraries:
- `sqlite3`: For database creation and querying.
- `pandas`: For displaying query results in a tabular format.

In Google Colab, both libraries are pre-installed. If running locally, ensure you have these libraries installed.

## Setup and Execution

### Running in Google Colab:
1. Open [Google Colab](https://colab.research.google.com/).
2. Copy the Python code provided in `book_database.py`.
3. Paste the code into a new Colab cell.
4. Run the cell to create the in-memory database and execute the queries.
5. Query results will be displayed in the output section.

### Running Locally:
1. Ensure you have Python 3.x installed.
2. Create a virtual environment (optional but recommended):
   ```bash
   python3 -m venv env
   source env/bin/activate   # On Windows use `env\Scripts\activate`
   ```
3. Install dependencies (if not already installed):
   ```bash
   pip install pandas sqlite3
   ```
4. Run the script using Python:
   ```bash
   python book_database.py
   ```

## SQL Queries

Here are the operations performed in this project:

1. **Create the Books Table**:  
   A table to store book details, including title, author, genre, published year, price, and ISBN.
   ```sql
   CREATE TABLE Books (
       BookID INTEGER PRIMARY KEY AUTOINCREMENT,
       Title TEXT NOT NULL,
       Author TEXT NOT NULL,
       Genre TEXT NOT NULL,
       PublishedYear INTEGER CHECK (PublishedYear >= 1000 AND PublishedYear <= 2024) NOT NULL,
       Price REAL NOT NULL,
       ISBN TEXT UNIQUE
   );
   ```

2. **Insert Sample Data**:  
   Inserting a few books into the database using SQL commands.

3. **Retrieve All Records**:  
   Retrieve all book records from the `Books` table:
   ```sql
   SELECT * FROM Books;
   ```

4. **Distinct Genres**:  
   Find all unique genres in the `Books` table:
   ```sql
   SELECT DISTINCT Genre FROM Books;
   ```

5. **Filter by Price**:  
   Retrieve all books that cost less than $10:
   ```sql
   SELECT * FROM Books WHERE Price < 10;
   ```

6. **Order by Published Year**:  
   Retrieve books ordered by their publication year in ascending order:
   ```sql
   SELECT * FROM Books ORDER BY PublishedYear ASC;
   ```

7. **Filter with Multiple Conditions**:  
   Retrieve books that are either in the 'Classic' genre or have a price between $8.00 and $12.00, excluding books published before 1950:
   ```sql
   SELECT * FROM Books WHERE (Genre = 'Classic' OR Price BETWEEN 8.00 AND 12.00) AND PublishedYear >= 1950;
   ```

8. **Find NULL ISBNs**:  
   Retrieve all books where the ISBN is `NULL`:
   ```sql
   SELECT * FROM Books WHERE ISBN IS NULL;
   ```

9. **Use of IN Clause**:  
   Find books written by either 'Harper Lee' or 'George Orwell':
   ```sql
   SELECT * FROM Books WHERE Author IN ('Harper Lee', 'George Orwell');
   ```

10. **Apply Alias**:  
    Retrieve the book title and display the price as "Cost" using an alias:
    ```sql
    SELECT Title, Price AS Cost FROM Books;
    ```

## Sample Queries

Here’s an example of how you can run the queries in the provided Python script:

```python
# Retrieve all records from the Books table
print(run_query("SELECT * FROM Books"))

# List distinct genres
print(run_query("SELECT DISTINCT Genre FROM Books"))

# Filter by price (less than $10)
print(run_query("SELECT * FROM Books WHERE Price < 10"))

# Order by published year
print(run_query("SELECT * FROM Books ORDER BY PublishedYear ASC"))
```

## License
This project is for educational purposes and does not require a specific license.

##Link: https://sqlfiddle.com/mysql/online-compiler?id=2056bb26-e86c-4480-ac97-08932a5fd2c5
 
