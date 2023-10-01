## DSA SQL MASTERCLASS
## Library Management System Database Documentation

### 1. Introduction
This document provides an overview and documentation of the Library Management System (LMS) database. The LMS is designed to manage the library's collection of books, book Issuance, and related activities.

### 2. Database Schema

The LMS database follows a relational database model and is composed of several tables connected through relationships. The primary entities include:
+	Book
+	Patron
+	Membership
+	Book Issuance (checkouts, returns)
+	Genre (book genres)

[Setup Database in SSMS using this script](https://github.com/kera13th/DSAProjects/blob/LMS-Database/lmsdatabase_script)

### 3. Entity-Relationship Diagram (ERD)

![LMS Entity Relationship Diagram](https://drive.google.com/uc?export=download&id=176DjE3y2ZX6svhTsPrgruq2U-HOAlZkF)

### 4. Tables and Descriptions

#### Book Table

| **Column**       | **Data Type**       | **Description**                                     | **Constraints**                |
|------------------|---------------------|-----------------------------------------------------|--------------------------------|
| BookID           | BIGINT              | Unique identifier for books.                        | IDENTITY(1,1)                  |
| Title            | NVARCHAR(350)       | The title of the book.                             | NOT NULL                       |
| Author           | NVARCHAR(300)       | The author of the book.                            | NOT NULL                       |
| isbn             | NVARCHAR(30)        | The International Standard Book Number (ISBN).     | NOT NULL                       |
| GenreID          | BIGINT              | Unique identifier for the genre of the book.        | NOT NULL                       |
| LangCode         | NVARCHAR(30)        | The language code of the book.                     |                                |
| PageNum          | BIGINT              | The number of pages in the book.                   |                                |
| PublicationDate  | NVARCHAR(300)       | The publication date of the book.                 |                                |
| Publisher        | NVARCHAR(300)       | The publisher of the book.                        |                                |
| Copies           | INT                 | The number of copies available for the book.       |                                |

#### Genre Table

| **Column**   | **Data Type**  | **Description**                 | **Constraints**  |
|--------------|----------------|---------------------------------|------------------|
| GenreID      | BIGINT         | Unique identifier for genres.    | NOT NULL         |
| GenreName    | NVARCHAR(60)   | Name of the genre.              |                  |

#### Membership Table

| **Column**     | **Data Type**  | **Description**                     | **Constraints**  |
|----------------|----------------|-------------------------------------|------------------|
| MembershipID   | NVARCHAR(100) | Unique identifier for memberships.   | NOT NULL         |
| MembershipType | NVARCHAR(50)  | Type of membership.                 | NOT NULL         |

#### Patron Table

| **Column**    | **Data Type**   | **Description**                      | **Constraints**                |
|---------------|-----------------|--------------------------------------|--------------------------------|
| PatronID      | BIGINT          | Unique identifier for patrons.        | IDENTITY(1,1)                  |
| MembershipID  | INT             | Membership ID of the patron.         | DEFAULT 1                       |
| FirstName     | NVARCHAR(50)    | First name of the patron.            | NOT NULL                       |
| Middlename    | NVARCHAR(50)    | Middle name of the patron.           |                                |
| LastName      | NVARCHAR(50)    | Last name of the patron.             | NOT NULL                       |
| BirthDate     | DATETIME        | Birth date of the patron.            |                                |
| Gender        | NVARCHAR(1)     | Gender of the patron.               |                                |
| EmailAddress  | NVARCHAR(40)    | Email address of the patron.        |                                |
| Education     | NVARCHAR(40)    | Education level of the patron.      |                                |
| Occupation    | NVARCHAR(100)   | Occupation of the patron.           |                                |
| AddressLine1  | NVARCHAR(120)   | Address Line 1 of the patron.       |                                |
| AddressLine2  | NVARCHAR(120)   | Address Line 2 of the patron.       |                                |

#### BookIssuance Table

| **Column**        | **Data Type**  | **Description**                          | **Constraints**                |
|-------------------|----------------|------------------------------------------|--------------------------------|
| TransactionID     | BIGINT         | Unique identifier for transactions.      | IDENTITY(1,1)                  |
| CheckoutOrderID   | NVARCHAR(20)   | Order ID for checkout.                   | NOT NULL                       |
| BookID            | BIGINT         | Identifier for books.                    |                                |
| PatronID          | BIGINT         | Identifier for patrons.                  |                                |
| CheckoutDate      | DATETIME       | Date of checkout.                        |                                |
| DueDate           | DATETIME       | Due date for return.                     |                                |
| ReturnDate        | DATETIME       | Date of return.                          |                                |

Records transactions related to book checkouts and returns.
Fields include transaction ID, book ID, patron ID, checkout date, return date.


### 5. Populate Database

#### :minidisc: Populating Book Table
Dataset: [Kaggle - Book Recommendation Dataset](https://www.kaggle.com/datasets/arashnic/book-recommendation-dataset)

I accomplished the task of populating the "Book" table by retrieving data from an established dataset acquired from Kaggle. Afterward, I carefully reorganized the columns to make sure they smoothly fit into the LMS (Library Management System) Database's structure, making sure they match the needed columns accurately.

To facilitate this data transformation, I opted for MS Excel as my tool of choice. Within Excel, I meticulously edited a CSV file, making necessary adjustments to the dataset. To enhance the richness and diversity of the data, I employed Excel's formula functionality to generate randomized entries for specific columns, thereby enriching the dataset with pertinent information.

```
=INDEX(data!A:A, RANDBETWEEN(2,COUNTA(data!A:A)))
```

Testing the table if populated properly

![Book Table Screenshot](https://drive.google.com/uc?export=download&id=17H5BP9egBqctM7LvRCuB6eLlwC0s2OHm)

#### :minidisc: Populating Patron Table
Dataset: [AdventureWorks2022](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks2022.bak)

To populate the Patron and Book Issuance tables, I leveraged the AdventureWorks2022 dataset for the Patron (User) entries and the FactInternetSales table for the Book Issuance Table. This approach allowed me to import and integrate relevant data from these sources, ensuring the accuracy and completeness of the information contained within these tables.

```
-- Insert data from specific columns in SourceTable into DestinationTable
INSERT INTO Patron (FirstName, MiddleName, LastName, BirthDate, Gender, EmailAddress, Education,
Occupation, AddressLine1, AddressLine2) -- Replace Column1, Column2, Column3 with your specific column names
SELECT FirstName, MiddleName, LastName, BirthDate, Gender, EmailAddress, Education,
Occupation, AddressLine1, AddressLine2 -- Replace with the actual column names you want to copy
FROM AdventureWorksDW2022.dbo.ProspectiveBuyer; -- Replace SourceTable with the name of your source table in SourceDB
```
Testing the table if populated properly

![Patron Table Screenshot](https://drive.google.com/uc?export=download&id=17H5BP9egBqctM7LvRCuB6eLlwC0s2OHm)](https://drive.google.com/uc?export=download&id=17IPgWt4z_28P_zFUdN0X-1MQUAavAi0q)
 
#### :minidisc: Populating BookIssuance Table

#### :minidisc: Populating Membership Table

```
INSERT INTO Membership (MembershipID, MembershipType)
VALUES
(1,'Student'),
(2,'Library Staff'),
(3,'Librarian'),
(4,'Database Admin');
```
![Membership Table Screenshot](https://drive.google.com/uc?export=download&id=17pi_vxjXB0rFrkDvqdgSASMyQQwhYiTi)

#### :minidisc: Populating Genre Table

```
INSERT INTO Genre (GenreID,GenreName)
VALUES
(1,'Action/adventure Fiction'),
(2,'Children’s Fiction'),
(3,'Classic Fiction')...
```
![Genre Table Screenshot](https://drive.google.com/uc?export=download&id=17Sl3Na8nCvZ2Abc-OPO3J309nHijB3BA)


##### For complete SQL Code used, please refer to the link:
[Populate Tables Script](https://github.com/kera13th/projects/edit/LMS-Database/populatetables_script)

### 6. Sample Queries
###### 1. Checking who is the librarian of DSA Library
```
SELECT
    PatronID,
    FirstName,
    LastName,
    MembershipType
FROM
    Patron p
JOIN
    Membership m ON p.MembershipID = m.MembershipID
WHERE
    MembershipType = 'Librarian';
```
###### Query Result:
```
+---------+---------+----------+----------------+
| PatronID| FirstName| LastName| MembershipType |
+---------+---------+----------+----------------+
|   101   |  Adrian |  Murphy  |   Librarian    |
+---------+---------+----------+----------------+
```

###### 2. Total Borrows Categorized by Occupation for Year 2014
```
SELECT
    Occupation,
    COUNT(*) AS CheckOutsForYr2014
FROM
    BookIssuance bi
JOIN
    Patron p ON p.PatronID = bi.PatronID
WHERE
    YEAR(CheckoutDate) = 2014 AND Occupation <> 'Database Admin'
GROUP BY
    Occupation;
```
###### Output

```
+--------------+-------------------+
|  Occupation  | CheckOutsForYr2014 |
+--------------+-------------------+
| Professional |        557        |
|   Clerical   |        320        |
|    Manual    |        247        |
|  Management  |        364        |
|  Librarian   |         1         |
| Skilled Manual|       480        |
+--------------+-------------------+
```
###### 2. Add title
```
SELECT TOP 5
    Title,
    Author,
    GenreName,
    COUNT(*) AS TimesBorrowed
FROM
    BookIssuance bi
JOIN
    Book b ON bi.BookID = b.BookID
JOIN
    Genre g ON g.GenreID = b.GenreID
GROUP BY
    Title,
    GenreName,
    Author;
```
###### Output
```


```



## 7. Set Access Control (DCL) /  User Roles and Permissions
#### 7.1. Create Roles

Three roles are created: librarian, librarystaff, and member. These roles are often used to group users based on their roles or responsibilities within the database.

#### 7.2. Add Users

User logins are created for different users who will access the database. For example, lmsadmin, dsalibrarymember, and dsalibrarystaff logins are created.
Corresponding database users (lmsadminuser, dsalibrarymemberuser, and dsalmsstaffuser) are created and associated with these logins.

#### 7.3. Adding Users to Role:

Users are added to the appropriate roles. For instance, lmsadminuser is added to the librarian role, dsalibrarymemberuser is added to the member role, and dsalmsstaffuser is added to the librarystaff role.
Setting Privileges for Member Role:

Members (likely students or general users) are granted SELECT privileges on the Book and Genre tables. This means they can only read data from these tables.
#### 7.4. Setting Privileges for Staff:

Library staff members are granted more extensive privileges. They are given SELECT, INSERT, UPDATE, and DELETE privileges on the Book table, SELECT, INSERT, and UPDATE privileges on the BookIssuance table, and SELECT privileges on the database schema.
#### 7.5. Setting Privileges for Librarian:

Librarians are granted extensive privileges, including SELECT, INSERT, UPDATE, and DELETE permissions on all tables in the schema, EXECUTE permissions on all stored procedures and functions in the database, VIEW DEFINITION permission to see object metadata, and additional SELECT, INSERT, UPDATE, and DELETE permissions on the entire database.
This script essentially sets up a role-based access control system for the database, allowing different levels of access and permissions based on user roles. It's a common practice to ensure that users only have the necessary privileges to perform their specific tasks within the database while maintaining security and data integrity.

### 8. User Roles and Permissions

Administrator: Full access to all database functions.
Librarian: Can manage books, patrons, and transactions.
Patron: Can view available books and borrow/return books.

### 9. Maintenance and Backup Procedures

Regular backups are scheduled weekly.
Maintenance tasks, such as index optimization, are performed monthly.

### 10. Revision History
Version 1.0 (Date): Initial database design.
Version 1.1 (Date): Added transaction history for patrons.
Version 2.0 (Date): Enhanced backup and maintenance procedures.
This documentation serves as a reference for those involved in managing and using the Library Management System database. It provides insights into the database's structure, relationships, and usage, helping ensure the efficient operation of the library system.
