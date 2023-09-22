## DSA SQL MASTERCLASS
### Library Management System Database Documentation

## 1. Introduction
This document provides an overview and documentation of the Library Management System (LMS) database. The LMS is designed to manage the library's collection of books, book Issuance, and related activities.

## 2. Database Schema

The LMS database follows a relational database model and is composed of several tables connected through relationships. The primary entities include:
•	Book
•	Patron
•	Membership
•	Book Issuance (checkouts, returns)
•	Genre (book genres)

[Setup Database in SSMS using this script](https://github.com/kera13th/DSAProjects/blob/LMS-Database/lmsdatabase_script)

## 3. Entity-Relationship Diagram (ERD)

![LMS Entity Relationship Diagram](https://drive.google.com/uc?export=download&id=176DjE3y2ZX6svhTsPrgruq2U-HOAlZkF)

## 4. Tables and Descriptions

### 4.1. Book Table

Stores information about books in the library.
Fields include ISBN, title, author ID, Genre ID, publication year, and available copies.

```
+------------+----------------+-------------------+--------------+
|   Column   |   Data Type    |   Description     | Constraints  |
+------------+----------------+-------------------+--------------+
|            |                |                   |              |
|  BookID    |     BIGINT     | Unique identifier |   NOT NULL   |
|            |                | for the book.     |              |
|------------|----------------|-------------------|--------------|
|  Title     | NVARCHAR(350)  | The title of the  |   NOT NULL   |
|            |                | book.             |              |
|------------|----------------|-------------------|--------------|
|  Author    | NVARCHAR(300)  | The author of the |   NOT NULL   |
|            |                | book.             |              |
|------------|----------------|-------------------|--------------|
|  ISBN      | NVARCHAR(30)   | The International |   NOT NULL   |
|            |                | Standard Book     |              |
|            |                | Number (ISBN).    |              |
|------------|----------------|-------------------|--------------|
|  GenreID   |     BIGINT     | Unique identifier |   NOT NULL   |
|            |                | for the genre of  |              |
|            |                | the book.         |              |
|------------|----------------|-------------------|--------------|
|  LangCode  | NVARCHAR(30)   | The language code |              |
|            |                | of the book.      |              |
|------------|----------------|-------------------|--------------|
|  PageNum   |     BIGINT     | The number of     |              |
|            |                | pages in the book.|              |
|------------|----------------|-------------------|--------------|
|  PubDate   | NVARCHAR(300)  | The publication   |              |
|            |                | date of the book. |              |
|------------|----------------|-------------------|--------------|
|  Publisher | NVARCHAR(300)  | The publisher of  |              |
|            |                | the book.         |              |
|------------|----------------|-------------------|--------------|
|  Copies    |     INT        | The number of     |              |
|            |                | copies available  |              |
|            |                | for the book.     |              |
|            |                |                   |              |
+------------+----------------+-------------------+--------------+
```

### 4.2. Genre Table
Categorizes books into genres or categories. Fields include category ID and category name.
```
+------------+-------------+----------------+------------------+
|   Column   |  Data Type  |  Description   |   Constraints    |
+------------+-------------+----------------+------------------+
|            |             |                |                  |
|  GenreID   |     INT     |   Primary Key  |                  |
|            |             |   Identifier   |                  |
|            |             |  for the Genre |                  |
|------------|-------------|----------------|------------------|
| GenreName  | NVARCHAR(60)|   Genre Name   |                  |
|            |             |                |                  |
+------------+-------------+----------------+------------------+
```

### 4.3. Patrons
Stores information about library patrons.
Fields include patron ID, first name, last name, contact information.
```
+--------------+----------------+----------------------+--------------+
|    Column    |   Data Type    |     Description      | Constraints  |
+--------------+----------------+----------------------+--------------+
|              |                |                      |              |
|   PatronID   |     BIGINT     |  Unique identifier   |   NOT NULL   |
|              |                |  for Patrons.        |              |
|--------------|----------------|----------------------|--------------|
| MembershipID | NVARCHAR(100)  |  Membership ID of    |              |
|              |                |  the Patron.         |              |
|--------------|----------------|----------------------|--------------|
|  FirstName   | NVARCHAR(50)   |  First name of the   |   NOT NULL   |
|              |                |  Patron.             |              |
|--------------|----------------|----------------------|--------------|
| Middlename   | NVARCHAR(50)   |  Middle name of the  |              |
|              |                |  Patron.             |              |
|--------------|----------------|----------------------|--------------|
|   LastName   | NVARCHAR(50)   |  Last name of the    |   NOT NULL   |
|              |                |  Patron.             |              |
|--------------|----------------|----------------------|--------------|
|  BirthDate   |   DATETIME     |  Birth date of the   |              |
|              |                |  Patron.             |              |
|--------------|----------------|----------------------|--------------|
|    Gender    | NVARCHAR(1)    |  Gender of the       |              |
|              |                |  Patron.             |              |
|--------------|----------------|----------------------|--------------|
| EmailAddress | NVARCHAR(40)   |  Email address of    |              |
|              |                |  the Patron.         |              |
|--------------|----------------|----------------------|--------------|
|  Education   | NVARCHAR(40)   |  Education level of  |              |
|              |                |  the Patron.         |              |
|--------------|----------------|----------------------|--------------|
|  Occupation  | NVARCHAR(100)  |  Occupation of the   |              |
|              |                |  Patron.             |              |
|--------------|----------------|----------------------|--------------|
| AddressLine1 | NVARCHAR(120)  |  Address Line 1 of   |              |
|              |                |  the Patron.         |              |
|--------------|----------------|----------------------|--------------|
| AddressLine2 | NVARCHAR(120)  |  Address Line 2 of   |              |
|              |                |  the Patron.         |              |
|              |                |                      |              |
+--------------+----------------+----------------------+--------------+
```
### 4.4. Membership Table

```
+---------------+----------------+-------------------+--------------+
|    Column     |   Data Type    |   Description     | Constraints  |
+---------------+----------------+-------------------+--------------+
|               |                |                   |              |
|  MembershipID | NVARCHAR(100)  | Unique identifier |   NOT NULL   |
|               |                | for Membership.   |              |
|---------------|----------------|-------------------|--------------|
| MembershipType| NVARCHAR(50)   | Type of Membership|   NOT NULL   |
|               |                |                   |              |
+---------------+----------------+-------------------+--------------+
```

### 4.5. Book Issuance Table

```
+-----------------+----------------+------------------------+--------------+
|    Column       |   Data Type    |      Description       | Constraints  |
+-----------------+----------------+------------------------+--------------+
|                 |                |                        |              |
|  TransactionID  |     BIGINT     |  Unique identifier     |   NOT NULL   |
|                 |                |  for transactions.     |              |
|-----------------|----------------|------------------------|--------------|
| CheckoutOrderID | NVARCHAR(20)   |  Order ID for          |   NOT NULL   |
|                 |                |  checkout.             |              |
|-----------------|----------------|------------------------|--------------|
|      BookID     |     BIGINT     |  Unique identifier     |   NOT NULL   |
|                 |                |  for books.            |              |
|-----------------|----------------|------------------------|--------------|
|     PatronID    |     BIGINT     |  Unique identifier     |   NOT NULL   |
|                 |                |  for patrons.          |              |
|-----------------|----------------|------------------------|--------------|
|   CheckoutDate  |   DATETIME     |  Date of checkout.     |              |
|-----------------|----------------|------------------------|--------------|
|     DueDate     |   DATETIME     |  Due date for return.  |              |
|-----------------|----------------|------------------------|--------------|
|    ReturnDate   |   DATETIME     |  Date of return.       |              |
|                 |                |                        |              |
+-----------------+----------------+------------------------+--------------+

```
Records transactions related to book checkouts and returns.
Fields include transaction ID, book ID, patron ID, checkout date, return date.


## 5. Populate Database

[Populate Tables](https://github.com/kera13th/DSAProjects/tree/LMS-Database)

Here are the sample dataset that I used:

For Book Table:
[Kaggle - Book Recommendation Dataset](https://www.kaggle.com/datasets/arashnic/book-recommendation-dataset)

For missing info on other columns like 'Copies', I randomly generated numbers using MS Excel using this formula
```
=INDEX(data!A:A, RANDBETWEEN(2,COUNTA(data!A:A)))
```

![Book Table Screenshot](https://drive.google.com/uc?export=download&id=17H5BP9egBqctM7LvRCuB6eLlwC0s2OHm)

For Patron and BookIssuance table, I used the values from --- and FactInternetSales table respectively. 
[AdventureWorks2022](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks2022.bak)


## 6. Sample Queries

```
Select TOP 5 Title, Author, COUNT(*) AS MostBorrowedBook FROM BookIssuance bi
JOIN Books b ON bi.BookID = b.BookID
JOIN Genre g ON g.GenreID = b.GenreID
GROUP BY Title, GenreName, Author 
HAVING GenreName = 'History';
```



## 7. Set Access Control (DCL)
Retrieve a list of all books in a specific category.
Check the number of available copies of a book.
View a patron's borrowing history.
Add a new book to the collection.
Check out a book to a patron.

## 6. User Roles and Permissions

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
