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
## How tables are related
- Tables are related to each other by keys.
- Relationships are built typically through primary and foriegn keys.
- The primary key of one table stored in other table is referred to as foreign
key of that table.