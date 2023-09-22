# DSA SQL MASTERCLASS
# Library Management System Database Documentation

# 1. Introduction
This document provides an overview and documentation of the Library Management System (LMS) database. The LMS is designed to manage the library's collection of books, book Issuance, and related activities.

# 2. Database Schema

The LMS database follows a relational database model and is composed of several tables connected through relationships. The primary entities include:
•	Book
•	Patron
•	Membership
•	Book Issuance (checkouts, returns)
•	Genre (book genres)

[Setup Database in SSMS using this script](https://github.com/kera13th/DSAProjects/blob/LMS-Database/lmsdatabase_script)

# 3. Entity-Relationship Diagram (ERD)

![LMS Entity Relationship Diagram](https://drive.google.com/uc?export=download&id=176DjE3y2ZX6svhTsPrgruq2U-HOAlZkF)

# 4. Tables and Descriptions

## 4.1. Books

Stores information about books in the library.
Fields include ISBN, title, author ID, category ID, publication year, and available copies.
```
+------------------+--------------+-----------------------+--------------+
| Column Name      | Data Type    | Description           | Constraints  |
+------------------+--------------+-----------------------+--------------+
| BookOrderNumber  | NVARCHAR(20) | Order number of book  | NOT NULL     |
|                  |              | issuance              |              |
+------------------+--------------+-----------------------+--------------+
| BookID           | BIGINT       | Unique identifier for | NULL         |
|                  |              | the book being issued |              |
+------------------+--------------+-----------------------+--------------+
| UserID           | BIGINT       | Unique identifier for | NULL         |
|                  |              | the user or borrower   |              |
+------------------+--------------+-----------------------+--------------+
| IssuanceDate     | DATETIME     | Date and time when    | NULL         |
|                  |              | the book was issued   |              |
+------------------+--------------+-----------------------+--------------+
| ReturnDate       | DATETIME     | Date and time when    | NULL         |
|                  |              | the book was returned |              |
+------------------+--------------+-----------------------+--------------+
| DueDate          | DATETIME     | Due date for          | NULL         |
|                  |              | returning the book    |              |
+------------------+--------------+-----------------------+--------------+
```

## 4.2. Genre
Stores information about book authors.
Fields include author ID, first name, and last name.

## 4.3. Patrons
Stores information about library patrons.
Fields include patron ID, first name, last name, contact information.

## 4.4. Transactions
Records transactions related to book checkouts and returns.
Fields include transaction ID, book ID, patron ID, checkout date, return date.

## 4.5. Categories
Categorizes books into genres or categories.
Fields include category ID and category name.

# 5. Populate Database



# 6. Sample Queries
Sample SQL queries for common tasks:

# 7. Set Access Control (DCL)
Retrieve a list of all books in a specific category.
Check the number of available copies of a book.
View a patron's borrowing history.
Add a new book to the collection.
Check out a book to a patron.

# 6. User Roles and Permissions

Administrator: Full access to all database functions.
Librarian: Can manage books, patrons, and transactions.
Patron: Can view available books and borrow/return books.

# 7. Maintenance and Backup Procedures

Regular backups are scheduled weekly.
Maintenance tasks, such as index optimization, are performed monthly.

# 8. Revision History
Version 1.0 (Date): Initial database design.
Version 1.1 (Date): Added transaction history for patrons.
Version 2.0 (Date): Enhanced backup and maintenance procedures.
This documentation serves as a reference for those involved in managing and using the Library Management System database. It provides insights into the database's structure, relationships, and usage, helping ensure the efficient operation of the library system.
