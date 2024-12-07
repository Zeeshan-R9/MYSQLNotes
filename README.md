# MySQL Notes

## Key Concepts
1. **Backup Storage**:  
   To ensure data safety, servers typically utilize:
   - A **backup disk drive** for redundancy.
   - **Offline storage** for additional protection.

2. **Database Management Systems (DBMS)**:  
   Servers rely on DBMS tools like **MySQL** or **Microsoft SQL Server** to manage databases stored on them.

3. **Data Access**:  
   - Application programs interact with databases through the *data access* **API**.  
   - For **Java applications**, this API is known as **JDBC** (*Java Database Connectivity*).

---

## Primary Keys
- A **Composite Primary Key** is a primary key that consists of two or more columns.

---

## Indexing
- **Indexes** significantly enhance data retrieval efficiency by optimizing access to row values.  
- Since applications often use keys for data access, an index is automatically created for every key defined.
- If for example, we frequenty sort the rows by **ZIP Codes**, then we can define an **Index** for 
that column. Like a primary key, an index can contain more than one columns.

---
## How Tables Are Related  

- **Table Relationships**:  
  Tables are connected to each other using **keys**.  

- **Types of Keys**:  
  - **Primary Key**: A unique identifier for each record in a table.  
  - **Foreign Key**: A primary key from one table that is stored in another table to establish a relationship.  

- **Foreign Key Definition**:  
  The **primary key** of one table, when stored in another table, is referred to as the **foreign key** of that table.  

- If two tables have a 1-1 relationship, the  data of two tables can be stored in
  a single table.

- Many-Many Relationship is established by using an intermediate table that has
  a 1-Many relationship with the two tables in the many-many relationship.

- By making the **foreign key** enforce the *Refrential Integrity*, we can make
  sure that the value that we set in the foriegn cell is also present in the other
  tables primary key.

---
## How columns are defined
- Columns whose values are automatically generate by the **DBMS** are called
  **Auto-incremented columns**.
- **Columns Data Types:**
  - *CHAR, VCHAR: A string of letters, numbers or symbols.*
  - *INT, DECIMAL: Integer or Decimal numbers that contain exact values.*
  - *FLOAT: Floating-point numbers that contain approximate values.*
  - *DATE: Date & Time*

## Working with SQL statements
- The **select** statement is also called a query.
- The result of the **select** statement (query) is a **result
table** or **result set** that can have calculated values. It is 
also know as a **Logical Table**
- When an application requests data from the database it receives
a **Result Set**.

### *Joining data from two or more tables*
*A join lets us combine data from two or more tables and get back a resutl table or result set.*

*An **inner join** allows us to join data from two tables only
if the values of the columns in the **FROM** clause match.*

**EXAMPLE:**
```sql
SELECT vender_name, invoice_no, invoice_date, invoice_total
FROM vendors INNER JOIN invoices 
  ON vendors.vendor_id = invoices.invoice_id
WHERE invoice_total >= 500
ORDER BY vendor_name, invoice_total DESC 
```
---
### INSERT, UPDATE, DELETE data from tables
```sql
-- INSERT Statement
INSERT INTO invoices 
  (vendor_id, invoice_number, invoice_date, 
  invoice_total, terms_id, invoice_due_date) 
VALUES (12, 132891751 , '2018-07-18', 165, 3, ' 2018-08-17') 

-- UPDATE Statement
UPDATE invoices 
SET credit_total = 35.89 
WHERE invoice_number = '367447'

-- DELETE Statement
DELETE FROM invoices 
WHERE invoice_number = '4-342-8069'
```

## MySQL Coding Guidelines
- MySQL is a *case-insensitive* language.
- **CAPITALIZE** all keywords.
- Separate the words in names with *underscores*.
- Start each clause on a new line.
- Split long clauses into multiple lines and use 
indentation for continued lines.
--- 
## How to access database through an application program
To access MySQL database programming languages provide an API. These API classes use a **driver** to communicate with
the database server.

For some languages, the database driver is built-in while
for others it needs to be downloaded.

---
## Using MySQL Command line client
If you don't have MySQL Workbench installed on your system then you 
can use this command line tool to connect to the server and execute the queries.

| Option   | Usage    
|----------|----------
| -p       | To prompt for password    
| -h       | For host IP address or URL
| -u       | For specifying username

```bash
cd <path_to_mysql_executale_file>
mysql -u root -p
Password>
```
Or

```bash
cd <path_to_mysql_executale_file>
mysql -h murach.com -u root -p
Password>
```

For localhost
```bash
cd <path_to_mysql_executale_file>
# Any of these two command will work fine.
mysql -h localhost -u root -p
mysql -u root -p    
Password>            
```
---
To view the avaiable databases
```sql
show databases;
```
To select a database

```sql
use database_name;
```
---
## Basic MySQL Statments
1. ```select```

![Select](./images/select_syntax.png)

**Expanded Syntax**
![Select](./images/select_syntax2.png)

**Using Aliases**
![Select](./images/select_syntax3.png)

**Arithematic Operators**
![Select](./images/arithematic_ops.png)


**```Concat()``` function**

![Select](./images/concat.png)


### Using functions with ```strings```, ```dates``` and ```numbers```
- The ```LEFT()``` function operates on strings. It returns the number of characters from the string.
- The ```DATE_FORMAT()``` function operates on dates. It formats
the date according to the specified format.
- The ```ROUND()``` function operates on numbers. The second parameter specifies how many decimal places to keep, if omitted
rounds the number to the nearest value.

![Select](./images/left_format_date_format.png)


## Testing expressions & functions without using ```FROM``` clause
This is useful to test expressions before you use them in actual
queries using the ```FROM``` clause.

Here, the ```CURRENT_DATE()``` function returns the current date.
The paranthesis are optional for this function.

![Select](./images/testing_without_from.png)

We can eleminate the duplicated (identical) rows from the result set by using the ```DISTINCT``` keyword. Code it immediately after the ```SELECT``` clause. 

```DISTINCTROW``` is the same as ```DISTINCT```.

There is also another keyword ```ALL``` which is used by default when we use the ```SELECT```
clause.

## How to code the ```WHERE``` clause

- We can use comparison operators to compare values of unlike datatype e.g, '7' = 7.
- MySQL is case-insensitive for strings 'CA' is same as 'ca'.
But we can use ```CAST()``` or ```CONVERT()``` functions to cast as well.
- To test for null values use ```IS NULL```.
- When one of the parameters of the comparison is null the result
will always be a null value.

![Comparison Operators](./images/comp_ops.png)

With logical operators
![Logical Operators](./images/logical_ops.png)

With the ```IN``` keyword
![Logical Operators](./images/in.png)


With the ```BETWEEN``` keyword

The lower and upper values of the range are inclusive.

![Logical Operators](./images/between.png)
---

Using ```LIKE``` & ```REGEXP```

The ```LIKE``` is an older operator that allows us to match simple strings.
![Regex](./images/regex_like.png)

Using ```IS NULL```
```NULL``` is not the same as ```empty string ""```.

![Regex](./images/null.png)


Using ```ORDER BY``` clause

Here, in the below image in the last example, the rows are sorted first by state in ascending order then by city in ascending order and then by name in ascending order.

Ascending order is the default sorting order.

![ORDER BY](./images/order_by.png)


We can also use the column numbers to specify the sort.

**For Example:** 
In this figure below we have used columns numbers where 2 represents the 2nd column which is the concatenation of 3 columns and the by first column which is the name.

We can also use the aliases in the ```ORDER BY``` clause
```sql
SELECT CONCAT(vendor_name, ' ', vendor_address) 
AS vendor_info
FROM vendors
ORDER BY vendor_info, vendor_id; -- Here, we've used alias
```
![ORDER BY](./images/order_by2.png)
---

## Working with the ```LIMIT``` clause

![LIMIT](./images/limit.png)
---

## How to work with ìnner joins

*A Join lets us combine the results of two or more tables in a single **result set**.*

![LIMIT](./images/inner_join.png)

## How to use table aliases
A table alias is typically as a single character or two characters. Used to shorten the table name.
![TABLE ALIAS](./images/table_alias.png)


## Join tables from different databases
MySQL databases are sometimes called ```schemas```.
To use the table of another database prefix the name of the table with database name.
![JOIN tables of different database](./images/join2.png)


## Using self join
We need to qualify the volumn names with the aliases here.

![JOIN tables of different database](./images/selfjoin.png)


## Implicit INNER JOIN
![Implicit Inner Join](./images/implicit_inner_join.png)


## Explicit Outer Joins
*Outer Join returns all the rows regardless of whether the join condition is true.*

The ```OUTER``` keyword is optional and is usually omitted.

It returns all the matched rows of condition plus the umatched rows from the first(LEFT) or second(RIGHT) table 
based on specification.

![Outer Join](./images/outer.png)


## Join tables with ```USING``` & ```NATURAL``` keyword
![USING keword](./images/using.png)


WE don't specify the column name when using the ```NATURAL``` keyword. Database automaticall picks the 
columns that are common in both tables. If there are more than one common column then the database also includes those in the join.

![NATURAL keword](./images/natural.png)

## Using ```CROSS JOINS```
![CROSS JOIN](./images/cross_join.png)


## Using ```UNIONS```
*Unions are like joins except that they combine rows from two **Result sets.***

![UNION](./images/union.png)

![UNION](./images/union2.png)

A **Full Outer Join** using ```UNIONS```

![UNION](./images/full_outer_join_using_unions.png)

---
[Visit Repository](https://github.com/Zeeshan-R9/MYSQLNotes.git)
