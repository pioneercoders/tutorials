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

#### 11. DELETE vs TRUNCATE vs DROP

- DELETE: Removes rows, can use WHERE, logs each row delete, slower.

- TRUNCATE: Removes all rows, faster, no WHERE, resets identity.

- DROP: Deletes entire table structure.

#### 12.Joins types

- INNER JOIN – Matches rows in both tables.

- LEFT JOIN – All rows from left + matches from right.

- RIGHT JOIN – All rows from right + matches from left.

- FULL JOIN – All rows from both, matching or not.

#### 13.WHERE vs HAVING:

- WHERE: Filters rows before grouping.

- HAVING: Filters after grouping.

#### 14.Clustered vs Non-clustered index

- Clustered: Rearranges table rows, only one allowed.

- Non-clustered: Separate structure with pointers.

#### 15. ACID properties

- Atomicity – All or nothing.

- Consistency – DB moves from one valid state to another.

- Isolation – Transactions don’t interfere.

- Durability – Changes persist after commit.

#### 16.What is database normalization beyond 3NF? Explain BCNF, 4NF, and 5NF.
- BCNF (Boyce–Codd Normal Form): A stronger version of 3NF; ensures that for every functional dependency X → Y, X is a superkey.

- Fixes cases where a non-prime attribute functionally determines part of a candidate key.

- 4NF (Fourth Normal Form): Handles multi-valued dependencies — ensures that no table has two or more independent multi-valued facts about an entity.

- 5NF (Fifth Normal Form): Handles join dependencies — ensures a table cannot be decomposed into smaller tables without loss of information.


#### 17.What is the difference between clustered and non-clustered indexes?

- Clustered Index: Physically rearranges the table rows to match the index order. Only one per table.

- Non-Clustered Index: Creates a separate structure with pointers to the table rows; multiple allowed.

- Key Point: Clustered index defines the table’s storage order, while non-clustered index is like a book’s index pointing to page numbers.

- Clustered: Dictionary words in alphabetical order.

- Non-clustered: Index at the back of the dictionary pointing to page numbers.

#### 18.Explain transaction isolation levels and their anomalies.

- Isolation levels prevent concurrent transactions from interfering with each other:

- Read Uncommitted → Allows dirty reads (reading uncommitted data).

- Read Committed → Prevents dirty reads, but allows non-repeatable reads.

- Repeatable Read → Prevents non-repeatable reads, but allows phantom reads.

- Serializable → Prevents all three anomalies (dirty, non-repeatable, phantom reads).

#### 19.What is a deadlock and how do you prevent it?

- Deadlock happens when two or more transactions are waiting for each other to release locks.

Prevention strategies:

- Lock ordering: Always acquire locks in the same order.

- Timeout: Abort transaction if it waits too long.

- Deadlock detection: Database periodically checks for cycles in the wait graph.

T1 locks Row A, waits for Row B.

T2 locks Row B, waits for Row A.
→ Deadlock.

#### 20.What is query optimization in DBMS?

- Query Optimization: The process of choosing the most efficient way to execute a SQL query.

- DBMS uses query optimizer which considers:

Index usage

- Join algorithms (nested loop, merge join, hash join)

- Execution plan cost (I/O, CPU)

Tools: EXPLAIN in MySQL/PostgreSQL or EXPLAIN PLAN in Oracle.

#### 21.What is the difference between OLTP and OLAP systems?

- OLTP (Online Transaction Processing): Handles day-to-day operations, highly normalized, supports fast INSERT/UPDATE/DELETE.

- OLAP (Online Analytical Processing): For analytics, reporting, aggregated queries; often denormalized for speed.

Example:

- OLTP: Banking system recording transactions.

- OLAP: Data warehouse generating quarterly sales reports.














