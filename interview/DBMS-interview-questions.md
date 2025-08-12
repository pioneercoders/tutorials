#### 1. What is DBMS? How is it different from RDBMS?

- DBMS (Database Management System): Software to store, retrieve, and manage data. Example: MS Access.
- RDBMS (Relational DBMS): Stores data in tables with relationships based on keys. Example: MySQL, PostgreSQL.
- Key difference: RDBMS follows relational model, supports normalization and ACID properties, while DBMS may not.

#### 2. Advantages of DBMS over file system:
 - Reduces data redundancy.

 - Provides data security.

 - Ensures data consistency.

 - Supports concurrent access.

 - Allows backup and recovery.

#### 3.What is data independence?
- The ability to change the database schema without changing the application programs.

- Logical data independence: Change in logical schema doesn’t affect applications.

- Physical data independence: Change in physical storage doesn’t affect logical structure.

#### 4.Types of databases:
- Hierarchical – Data in tree-like structure.

- Network – Data as records connected via links.

- Relational – Data in tables (most common).

- Object-oriented – Data as objects.

#### 5.What is a primary key? Can it be NULL?
- A primary key uniquely identifies a record in a table and cannot be NULL or duplicate.

#### 6.What is a foreign key?
- A foreign key is a field in one table that refers to the primary key in another table to maintain referential integrity.

#### 7.Candidate key, primary key, super key

- Candidate key: Minimum set of attributes that can uniquely identify a row.

- Primary key: One selected candidate key.

- Super key: Any set of attributes that uniquely identifies a row (may have extra attributes).

#### 8.Schema vs. instance:

- Schema: Structure/blueprint of the database (design).

- Instance: Actual data at a given time.

#### 9. Levels of data abstraction

- Physical level – How data is stored.

- Logical level – What data is stored and relationships.

- View level – User interaction with the data.

#### 10.Data redundancy

-Unnecessary duplication of data. Reduced by normalization.


















