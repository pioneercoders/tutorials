# DBMS Medium 


1. **How does a DBMS handle concurrent access to data?**
   - A DBMS manages concurrent access to data through techniques like locking and transaction management. Locks are used to control access to data, ensuring that multiple users or processes do not modify the same data simultaneously. Transactions allow multiple operations to be grouped together, ensuring that they either all succeed or all fail.

2. **Explain the concept of SQL JOIN operations.**
   - SQL JOIN operations are used to combine rows from two or more tables based on a related column between them. There are various types of joins: INNER JOIN (returns only matching rows), LEFT JOIN (returns all rows from the left table and matching rows from the right), RIGHT JOIN (opposite of LEFT JOIN), and FULL JOIN (returns all rows when there is a match in either table).

3. **What is the difference between a full backup and an incremental backup in database management?**
   - A full backup copies all the data in a database, while an incremental backup only copies the data that has changed since the last backup. Incremental backups are more space and time-efficient but require a series of backups to restore the database to a specific point in time.

4. **Describe the advantages and disadvantages of using stored procedures in a DBMS.**
    - Advantages: Reusability, security, performance optimization, and encapsulation of business logic.
    - Disadvantages: Limited portability, debugging complexity, and potential for inefficiency in some cases.

5. **What is a candidate key in a database, and how is it different from a primary key?**
    - A candidate key is a set of one or more columns in a table that can uniquely identify each row. A primary key is a specific candidate key chosen as the main method for uniquely identifying rows. A table can have multiple candidate keys, but only one primary key.

6. **Explain the concept of a bitmap index in a database.**
   - A bitmap index is a type of indexing technique that uses bitmaps to represent data. It's useful for columns with a small number of distinct values. Each distinct value is associated with a bitmap, where each bit represents a row. This makes it efficient for fast Boolean operations like AND, OR, and NOT.

7. **What is a database transaction, and how is it different from a database query?**
   - A database transaction is a series of one or more SQL statements that are executed as a single unit of work. Transactions ensure the consistency and integrity of data. A database query is a single SQL statement used to retrieve or manipulate data in a database.

8. **Describe the differences between OLTP and OLAP systems.**
    - OLTP (Online Transaction Processing) systems are designed for day-to-day operations and handle a large volume of short, simple transactions. OLAP (Online Analytical Processing) systems are used for complex queries and reporting, focusing on data analysis and business intelligence.

9. **What is the CAP theorem, and how does it relate to distributed databases?**
   - The CAP theorem states that a distributed system cannot simultaneously guarantee Consistency, Availability, and Partition Tolerance. In distributed databases, you must make trade-offs between these three properties. You can choose to prioritize Consistency and Availability but sacrifice Partition Tolerance, or vice versa.

10. **Explain the concept of ACID properties and their importance in database transactions.**
    - ACID stands for Atomicity, Consistency, Isolation, and Durability. These properties ensure that database transactions are reliable and meet specific criteria for success, data integrity, isolation, and durability, even in the face of system failures.

11. **What is a database trigger, and what are its various types?**
    - A database trigger is a predefined action that automatically executes in response to a specific database event (e.g., an INSERT, UPDATE, or DELETE operation). Types of triggers include BEFORE and AFTER triggers, which execute before or after the event, and FOR EACH ROW and FOR EACH STATEMENT triggers, which determine when the trigger fires.

12. **Describe the differences between the SQL DELETE and TRUNCATE statements.**
    - DELETE removes specific rows from a table and logs individual row deletions. TRUNCATE removes all rows from a table and is faster but doesn't log individual deletions.

13. **What is a materialized view in a database, and when is it used?**
    - A materialized view is a precomputed snapshot of data from one or more tables. It's used to improve query performance by storing aggregated or frequently used data, reducing the need to recompute results in real-time.

14. **Explain the concept of a surrogate key in a database.**
    - A surrogate key is an artificial, system-generated primary key used in place of a natural key (e.g., a social security number). Surrogate keys help ensure uniqueness and improve performance in situations where a natural key may change.

15. **What is the purpose of the SQL HAVING clause, and how is it different from the WHERE clause?**
    - The HAVING clause is used with the GROUP BY clause to filter rows in the result set based on aggregated values. The WHERE clause filters rows before aggregation. HAVING is used after aggregation.

16. **Describe the differences between a clustered index and a non-clustered index.**
    - A clustered index determines the physical order of data rows in a table and is created on the primary key column. A non-clustered index is a separate structure that contains a copy of a portion of the data and includes a pointer to the actual row.

17. **What is the use of the SQL UNION and UNION ALL operators?**
    - UNION combines the result sets of two or more SELECT statements and removes duplicates. UNION ALL also combines result sets but retains duplicates.

18. **Explain the concept of ACID properties in DBMS transactions.**
    - As mentioned earlier, ACID stands for Atomicity, Consistency, Isolation, and Durability. These properties ensure that database transactions are reliable, consistent, isolated from other transactions, and durable even in the face of failures.

19. **What is a database link in Oracle, and how is it used for distributed databases?**
    - In Oracle, a database link is a schema object that connects to a remote database. It's used to access and manipulate data in a remote database, making it useful for distributed databases and data integration.

20. **Define the term "database sharding" and its role in scalability.**
    - Database sharding is a technique used to horizontally partition a database into smaller, more manageable pieces called shards. Each shard contains a subset of data. Sharding is used to improve database performance and scalability by distributing data across multiple servers or instances.

21. **What is a database view, and what are the advantages and disadvantages of using views?**
    - A database view is a virtual table created by defining a query on one or more base tables. Advantages include simplified data access, security, and abstraction of complexity. Disadvantages may include performance overhead and potential limitations on updatable views.
