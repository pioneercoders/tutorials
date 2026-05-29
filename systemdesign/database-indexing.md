# Database Indexing

Database indexing creates data structures that improve the speed of data retrieval operations on database tables at the cost of additional writes and storage space.

## Introduction

Database indexing creates data structures that improve the speed of data retrieval operations on database tables at the cost of additional writes and storage space. Indexes are like book indexes - they provide a quick way to find data without scanning the entire table. Without indexes, databases must perform full table scans to find specific rows, which is O(n) time complexity. With indexes, lookups become O(log n) for B-tree indexes or O(1) for hash indexes. Common index types include B-tree (balanced tree for range queries), Hash (hash table for exact matches), Bitmap (for low-cardinality columns), and Full-text (for text search). Indexes can be single-column, composite (multiple columns), unique (enforce uniqueness), or covering (include all query columns). While indexes dramatically improve read performance, they add overhead for write operations (insert, update, delete) because the index must be maintained. Indexing is essential for large databases and production systems where query performance is critical.

**Why Database Indexing Matters:**
- Dramatically improves query performance
- Reduces I/O operations
- Enables efficient range queries
- Supports unique constraints
- Essential for large databases
- Critical for production performance

**Where It Is Used:**
- User lookup by email or username
- Product search by category or price
- Order lookup by date or customer
- Analytics and reporting queries
- Text search applications
- All production databases

## Core Concept Explanation

Database indexing creates a separate data structure that maps column values to row locations, allowing the database to quickly locate rows without scanning the entire table. The most common index type is B-tree (Balanced Tree), which maintains sorted data in a tree structure where each node can have multiple children. B-trees are self-balancing, ensuring O(log n) lookup time and efficient range queries. Hash indexes use a hash function to map values to buckets, providing O(1) average lookup time for exact matches but no range query support. Composite indexes combine multiple columns, useful for queries that filter on multiple columns. Covering indexes include all columns needed by a query, eliminating the need to access the table data (index-only scan). The trade-off is that indexes consume additional storage space and add overhead to write operations because the index must be updated when data changes.

**Step-by-Step Breakdown:**
1. Identify frequently queried columns
2. Choose appropriate index type (B-tree, Hash, etc.)
3. Create index on selected columns
4. Database builds index data structure
5. Query optimizer uses index for queries
6. Index lookup finds row locations
7. Database retrieves data from those locations
8. Monitor index usage and performance
9. Rebuild or drop unused indexes

**Intuition Behind the Concept:**
Think of database indexing like a book index. Without an index, to find a specific topic, you'd have to scan every page (full table scan). With an index, you look up the topic in the index, find the page numbers, and go directly to those pages. This is much faster. The trade-off is that the index takes up space in the book and must be updated when pages are added or removed. Similarly, database indexes take up storage space and must be maintained when data changes, but they dramatically speed up data retrieval.

**Visual Thinking:**
```
Table Scan (No Index):
Table: [1, 5, 3, 8, 2, 7, 4, 6]
Find 3: Scan all 8 elements → O(n)

Index Lookup (B-tree Index):
Index Tree:
       [5]
      /    \
   [2,3]   [7,8]
  /   \   /   \
[1]  [4] [6]  [9]

Find 3: Go to [5] → [2,3] → 3 → O(log n)

Composite Index:
Index on (last_name, first_name):
Smith, John → Row 1
Smith, Jane → Row 2
Doe, John → Row 3
```

## Internal Working / Logic

Database indexing works by creating a separate data structure that maps indexed column values to the physical location of rows in the table. When a query includes a WHERE clause on an indexed column, the query optimizer checks if an index exists and if using it would be faster than a full table scan. If the index is used, the database performs an index lookup to find the row locations, then retrieves the actual data from those locations. For B-tree indexes, the database traverses the tree from the root to the leaf nodes, comparing values at each node to determine which branch to follow. For hash indexes, the database computes a hash of the search value and directly accesses the corresponding bucket. When data is inserted, updated, or deleted, the database must update all affected indexes, which adds overhead. The query optimizer uses statistics about the data distribution to decide whether to use an index, considering factors like selectivity (how unique the values are) and query patterns.

**Operation 1: Index Lookup**
- Query includes WHERE clause on indexed column
- Query optimizer checks for index
- Optimizer estimates cost of index vs table scan
- If index is cheaper, use index lookup
- Traverse index structure to find values
- Retrieve row locations from index
- Fetch actual data from table
- Return results

**Operation 2: Index Insert**
- New row inserted into table
- Database identifies affected indexes
- For each index, compute index key
- Insert key into index structure
- Update index statistics
- Commit transaction
- Index maintenance overhead added

**Operation 3: Index Update**
- Row updated in table
- Database identifies affected indexes
- For each index, check if indexed columns changed
- If changed, remove old key from index
- Insert new key into index
- Update index statistics
- Commit transaction

**Operation 4: Index Delete**
- Row deleted from table
- Database identifies affected indexes
- For each index, remove key from index
- Update index statistics
- Commit transaction
- Index maintenance overhead added

**Flow Explanation (B-tree Lookup):**
1. Query with WHERE clause on indexed column
2. Query optimizer checks for index
3. Optimizer estimates cost
4. If index chosen, start at root node
5. Compare search value with node values
6. Navigate to appropriate child node
7. Repeat until leaf node reached
8. Find row locations in leaf node
9. Retrieve data from table
10. Return results

**Decision Making Logic:**
The key decisions are:
- Which columns to index (frequently queried, selective)
- Which index type to use (B-tree, Hash, Bitmap, Full-text)
- Whether to use composite indexes (multi-column queries)
- Whether to use covering indexes (avoid table access)
- When to drop unused indexes (monitor usage)
- How to handle index maintenance (rebuild, statistics)

## Algorithm / Approach

**B-tree Lookup Algorithm**

```
1. Start at root node
2. Compare search value with node values
3. Find appropriate child node
4. Navigate to child node
5. Repeat until leaf node
6. Find value in leaf node
7. Return row location
8. Retrieve data from table
```

**Hash Index Lookup Algorithm**

```
1. Compute hash of search value
2. Access bucket at hash location
3. Scan bucket for matching value
4. If found, return row location
5. Retrieve data from table
6. If not found, return empty
```

**Composite Index Lookup Algorithm**

```
1. Parse composite key (col1, col2, ...)
2. Compare first column value
3. Navigate to matching subtree
4. Compare second column value
5. Navigate to matching subtree
6. Repeat for all columns
7. Find row location
8. Retrieve data from table
```

**Index Insertion Algorithm**

```
1. Compute index key from row data
2. Find appropriate position in index
3. Insert key into index structure
4. If node full, split node
5. Rebalance tree if needed
6. Update index statistics
7. Commit transaction
```

## Implementations

### 1. Create Index (SQL)

```sql
-- Single column index
CREATE INDEX idx_email ON users(email);

-- Composite index (order matters!)
CREATE INDEX idx_name_email ON users(last_name, first_name);

-- Unique index (enforces uniqueness)
CREATE UNIQUE INDEX idx_unique_email ON users(email);

-- Partial index (index only certain rows)
CREATE INDEX idx_active_users ON users(email) WHERE is_active = true;

-- Drop index
DROP INDEX idx_email ON users;

-- Rebuild index (optimize performance)
REINDEX INDEX idx_email ON users;
```

**Advantages:**
- Standard SQL syntax
- Multiple index types
- Flexible options
- Widely supported

### 2. Index Usage Analysis

```sql
-- Explain query plan
EXPLAIN ANALYZE SELECT * FROM users WHERE email = 'user@example.com';

-- Check if index is used
-- Look for "Index Scan" in output

-- Check index usage statistics
SELECT 
  schemaname,
  tablename,
  indexname,
  idx_scan as index_scans,
  idx_tup_read as tuples_read,
  idx_tup_fetch as tuples_fetched
FROM pg_stat_user_indexes 
WHERE tablename = 'users'
ORDER BY idx_scan DESC;

-- Find unused indexes
SELECT 
  schemaname,
  tablename,
  indexname
FROM pg_stat_user_indexes 
WHERE idx_scan = 0
AND indexname NOT LIKE '%_pkey';
```

**Advantages:**
- Identify slow queries
- Find unused indexes
- Optimize performance
- Monitor index usage

### 3. B-tree Index Implementation (Conceptual)

```javascript
// Conceptual B-tree index structure
class BTreeNode {
  constructor(isLeaf = false) {
    this.keys = [];
    this.children = [];
    this.isLeaf = isLeaf;
  }
  
  search(key) {
    let i = 0;
    while (i < this.keys.length && key > this.keys[i]) {
      i++;
    }
    
    if (this.isLeaf) {
      return this.keys[i] === key ? this.values[i] : null;
    }
    
    return this.children[i].search(key);
  }
  
  insert(key, value) {
    // Insert logic with node splitting
    // Simplified for illustration
    if (this.isLeaf) {
      this.keys.push(key);
      this.values.push(value);
      this.keys.sort();
      // Split if needed
    }
  }
}

// Usage
const root = new BTreeNode();
root.insert('user@example.com', 1);
root.insert('admin@example.com', 2);
console.log(root.search('user@example.com')); // 1
```

**Advantages:**
- O(log n) lookup
- Range query support
- Self-balancing
- Widely used

### 4. Hash Index Implementation (Conceptual)

```javascript
// Conceptual hash index structure
class HashIndex {
  constructor(size = 100) {
    this.buckets = new Array(size).fill(null).map(() => []);
    this.size = size;
  }
  
  _hash(key) {
    let hash = 0;
    for (let i = 0; i < key.length; i++) {
      hash = ((hash << 5) - hash) + key.charCodeAt(i);
      hash |= 0;
    }
    return Math.abs(hash) % this.size;
  }
  
  insert(key, value) {
    const bucket = this._hash(key);
    this.buckets[bucket].push({ key, value });
  }
  
  search(key) {
    const bucket = this._hash(key);
    const item = this.buckets[bucket].find(item => item.key === key);
    return item ? item.value : null;
  }
}

// Usage
const index = new HashIndex();
index.insert('user@example.com', 1);
index.insert('admin@example.com', 2);
console.log(index.search('user@example.com')); // 1
```

**Advantages:**
- O(1) average lookup
- Fast exact matches
- Simple implementation
- Good for equality checks

### 5. Covering Index

```sql
-- Regular index (requires table lookup)
CREATE INDEX idx_created_at ON orders(created_at);

-- Covering index (includes all query columns)
CREATE INDEX idx_created_at_covering ON orders(created_at) 
INCLUDE (customer_id, total_amount);

-- Query that benefits from covering index
SELECT customer_id, total_amount 
FROM orders 
WHERE created_at > '2024-01-01';

-- With covering index, no table lookup needed (index-only scan)
```

**Advantages:**
- Eliminates table lookup
- Faster queries
- Reduces I/O
- Better performance

## Dry Run

**Example: B-tree Index Lookup**

**Query:**
```sql
SELECT * FROM users WHERE email = 'user@example.com';
```

**Index Structure:**
```
B-tree Index on email:
            [m...z]
           /       \
     [f...m]       [s...z]
     /     \       /     \
[a...f] [g...l] [m...r] [s...z]
```

**Step-by-Step Execution:**

```
1. Query optimizer checks for index on email
2. Index exists, estimate cost
3. Index lookup cheaper than table scan
4. Start at root node [m...z]
5. Compare 'user@example.com' with 'm'
6. 'u' > 'm', go to right child [s...z]
7. Compare 'user@example.com' with 's'
8. 'u' > 's', go to right child [s...z]
9. Found in leaf node
10. Get row location: Row 5
11. Retrieve data from table at Row 5
12. Return result to client
```

**Request/Response Table:**

| Step | Component | Action | Status |
|------|-----------|--------|--------|
| 1 | Query Optimizer | Check for index | Index found |
| 2 | Query Optimizer | Estimate cost | Index cheaper |
| 3 | Database | Start index lookup | - |
| 4 | Index | Traverse to root | [m...z] |
| 5 | Index | Compare values | Go right |
| 6 | Index | Traverse to child | [s...z] |
| 7 | Index | Find in leaf | Found |
| 8 | Index | Get row location | Row 5 |
| 9 | Database | Retrieve data | - |
| 10 | Database | Return result | Success |

## Edge Cases

### 1. Index Fragmentation
```javascript
// Index becomes fragmented over time
- Performance degrades
// Solution: Rebuild index
```

### 2. Write Performance Degradation
```javascript
// Too many indexes slow down writes
- Insert/update/delete slow
// Solution: Remove unused indexes
```

### 3. Query Optimizer Not Using Index
```javascript
// Query optimizer chooses table scan
- Index not used
// Solution: Update statistics, force index
```

### 4. Low Selectivity
```javascript
// Index on column with few unique values
- Index not effective
// Solution: Don't index low-selectivity columns
```

### 5. Composite Index Order
```javascript
// Wrong column order in composite index
- Index not used
// Solution: Order columns by selectivity
```

### 6. Index Size Too Large
```javascript
// Index consumes too much storage
- Memory pressure
// Solution: Use partial indexes, drop unused
```

**Why Edge Cases Matter:**
- Fragmentation degrades performance
- Too many indexes slow writes
- Optimizer may not use index
- Low selectivity wastes space
- Wrong order breaks index usage
- Large indexes cause memory pressure

## Variations / Extensions

### 1. Bitmap Index

```javascript
// For low-cardinality columns
- Efficient for boolean, enum
// Example: gender, status
```

### 2. Full-text Index

```javascript
// For text search
- Inverted index
// Example: search engine
```

### 3. GiST Index

```javascript
// Generalized Search Tree
- Geospatial data
// Example: location queries
```

### 4. Partial Index

```javascript
// Index only subset of rows
- Smaller index
// Example: active users only
```

### 5. Expression Index

```javascript
// Index on computed expression
- Functional index
// Example: LOWER(email)
```

## Optimization Techniques

### 1. Index Statistics

**Update Statistics:**
```javascript
// Keep statistics up to date
- Better optimizer decisions
// Example: ANALYZE command
```

### 2. Index Rebuilding

**Rebuild Fragmented Indexes:**
```javascript
// Rebuild fragmented indexes
- Improve performance
// Example: REINDEX command
```

### 3. Partial Indexes

**Index Subset of Data:**
```javascript
// Index only relevant rows
- Smaller index
- Better performance
```

### 4. Covering Indexes

**Include Query Columns:**
```javascript
// Include all needed columns
- Avoid table lookup
- Faster queries
```

### 5. Trade-offs

**Index Type Comparison:**

| Index Type | Lookup | Range | Use Case |
|------------|--------|-------|----------|
| B-tree | `O(log n)` | Yes | General purpose |
| Hash | `O(1)` | No | Exact matches |
| Bitmap | `O(n)` | No | Low cardinality |
| Full-text | `O(log n)` | No | Text search |

**When to Use Each:**
- B-tree: General purpose, range queries
- Hash: Exact matches, equality checks
- Bitmap: Low cardinality, boolean columns
- Full-text: Text search, content search

## Complexity Analysis

### Time Complexity

**B-tree Lookup: O(log n)**
- n = number of rows
- Tree traversal
- Efficient for large datasets

**Hash Lookup: O(1)**
- Average case
- Hash computation
- Bucket access

**Table Scan: O(n)**
- n = number of rows
- Scan entire table
- No index

### Space Complexity

**Index Storage: O(n)**
- n = number of rows
- Additional storage
- Depends on index type

**Explanation:**
B-tree lookup is O(log n) where n is the number of rows, making it efficient for large datasets. Hash lookup is O(1) on average for exact matches but doesn't support range queries. Table scan is O(n), scanning all rows. Index storage is O(n) where n is the number of rows, requiring additional storage space proportional to the table size. The trade-off is between read performance (faster with indexes) and write performance (slower with indexes due to maintenance overhead).

## Real-world Applications

### 1. User Authentication

**Email Lookup:**
- Index on email column
- Fast login
- Example: User login systems

### 2. E-commerce

**Product Search:**
- Index on category, price
- Fast product search
- Example: Online stores

### 3. Order Management

**Date Range Queries:**
- Index on created_at
- Fast date range queries
- Example: Order history

### 4. Analytics

**Reporting Queries:**
- Index on frequently filtered columns
- Fast analytics
- Example: Business intelligence

### 5. Text Search

**Content Search:**
- Full-text index
- Fast text search
- Example: Search engines

### 6. Geospatial

**Location Queries:**
- GiST index on coordinates
- Fast location queries
- Example: Location-based services

### 7. Social Media

**User Lookup:**
- Index on username
- Fast user lookup
- Example: Social platforms

### 8. Logging

**Log Search:**
- Index on timestamp, level
- Fast log search
- Example: Log analysis

## Common Mistakes

### 1. Indexing Everything

**Mistake:**
```javascript
// Index all columns
// Too many indexes
- Slow writes, high storage
```

**Correct:**
```javascript
// Index only frequently queried columns
- Balance read/write performance
// Monitor index usage
```

**Why It Matters:**
- Too many indexes slow writes
- High storage overhead
- Index maintenance cost

### 2. Wrong Index Type

**Mistake:**
```javascript
// Use hash index for range queries
- Index not used
// Poor performance
```

**Correct:**
```javascript
// Use B-tree for range queries
- Index used
// Better performance
```

**Why It Matters:**
- Wrong type = index not used
- Query optimizer ignores index
- Match type to query pattern

### 3. Ignoring Selectivity

**Mistake:**
```javascript
// Index low-selectivity column
- Index not effective
// Wasted space
```

**Correct:**
```javascript
// Index high-selectivity columns
- Effective index
- Better performance
```

**Why It Matters:**
- Low selectivity = poor index
- Wasted storage space
- High selectivity essential

### 4. Wrong Composite Order

**Mistake:**
```javascript
// Wrong column order in composite index
- Index not used
// Poor performance
```

**Correct:**
```javascript
// Order by selectivity
- Most selective first
// Better index usage
```

**Why It Matters:**
- Wrong order = index not used
- Query optimizer ignores index
- Order by selectivity

### 5. Not Monitoring Usage

**Mistake:**
```javascript
// Don't monitor index usage
- Unused indexes waste space
// Performance degradation
```

**Correct:**
```javascript
// Monitor index usage
- Drop unused indexes
// Better performance
```

**Why It Matters:**
- Unused indexes waste space
- Slow down writes
- Monitoring essential

### 6. Not Updating Statistics

**Mistake:**
```javascript
// Outdated statistics
- Poor optimizer decisions
- Index not used
```

**Correct:**
```javascript
// Update statistics regularly
- Better optimizer decisions
- Index used effectively
```

**Why It Matters:**
- Outdated statistics = poor decisions
- Optimizer may not use index
- Statistics update essential

## Advanced Concepts

### 1. Bitmap Index

**Concept:**
Bitmap for low-cardinality columns.

**Features:**
- Efficient for boolean, enum
- Compressed storage
- Fast AND/OR operations

### 2. Full-text Index

**Concept:**
Inverted index for text search.

**Features:**
- Word-level indexing
- Ranking and relevance
- Phrase search

### 3. GiST Index

**Concept:**
Generalized Search Tree.

**Features:**
- Geospatial data
- Custom data types
- Flexible indexing

### 4. Expression Index

**Concept:**
Index on computed expression.

**Features:**
- Functional index
- Computed columns
- Flexible indexing

## Practice Thinking Guide

### How to Design Database Indexing Strategy

**Key Questions to Ask:**

1. **Which columns to index?**
   - Frequently queried columns
   - High selectivity columns
   - Example: "Index email, username"

2. **Which index type?**
   - B-tree for range queries
   - Hash for exact matches
   - Example: "B-tree for date ranges"

3. **Composite or single?**
   - Multi-column queries
   - Order by selectivity
   - Example: "Composite for (last_name, first_name)"

4. **Covering index needed?**
   - Avoid table lookup
   - Include query columns
   - Example: "INCLUDE customer_id, total"

5. **How to monitor?**
   - Check index usage
   - Monitor performance
   - Example: "Use EXPLAIN ANALYZE"

**Pattern Recognition:**

**Pattern 1: User Lookup**
```
Query: WHERE email = ?
Index: B-tree on email
Solution: Single column B-tree index
```

**Pattern 2: Date Range**
```
Query: WHERE created_at BETWEEN ? AND ?
Index: B-tree on created_at
Solution: B-tree index for range queries
```

**Pattern 3: Multi-column Filter**
```
Query: WHERE last_name = ? AND first_name = ?
Index: Composite on (last_name, first_name)
Solution: Composite B-tree index
```

**Pattern 4: Exact Match**
```
Query: WHERE status = ?
Index: Hash on status
Solution: Hash index for exact match
```

**Pattern 5: Text Search**
```
Query: WHERE content LIKE ?
Index: Full-text on content
Solution: Full-text index for text search
```

**Decision Flowchart:**

```
Indexing Decision:
├─ Query type?
│        ├─ Range queries → B-tree
│        ├─ Exact match → Hash or B-tree
│        └─ Text search → Full-text
├─ Number of columns?
│        ├─ Single → Single column index
│        └─ Multiple → Composite index
├─ Selectivity?
│        ├─ High → Index beneficial
│        └─ Low → Consider bitmap or no index
└─ Query columns?
         ├─ All in index → Covering index
         └─ Need table access → Regular index
```

**Example Analysis:**

**Scenario:** "Design indexing for user table"

**Analysis:**
1. Queries: WHERE email = ?, WHERE username = ?
2. Type: Exact match queries
3. Selectivity: High (unique)
4. Solution: Unique B-tree indexes on email, username

**Scenario:** "Design indexing for orders table"

**Analysis:**
1. Queries: WHERE created_at BETWEEN ? AND ?
2. Type: Range queries
3. Selectivity: Medium
4. Solution: B-tree index on created_at

## Summary

Database indexing creates data structures that improve the speed of data retrieval operations on database tables at the cost of additional writes and storage space. Indexes are like book indexes - they provide a quick way to find data without scanning the entire table. Common index types include B-tree (balanced tree for range queries), Hash (hash table for exact matches), Bitmap (for low-cardinality columns), and Full-text (for text search). Indexes can be single-column, composite, unique, or covering. While indexes dramatically improve read performance (O(log n) or O(1) vs O(n) for table scan), they add overhead for write operations because the index must be maintained. Indexing is essential for large databases and production systems where query performance is critical. The key is to index the right columns with the right index type, monitor index usage, and drop unused indexes to maintain optimal performance.

**Key Takeaways:**
- Indexes dramatically improve query performance
- B-tree for range queries, Hash for exact matches
- Trade-off: read speed vs write speed
- Essential for large databases
- Monitor index usage and drop unused
- Choose appropriate index type
- Composite indexes for multi-column queries
- Covering indexes avoid table lookup

**Mastery Checklist:**
- ✅ Understand index types (B-tree, Hash, Bitmap)
- ✅ Create appropriate indexes
- ✅ Analyze query plans with EXPLAIN
- ✅ Monitor index usage
- ✅ Use composite indexes effectively
- ✅ Implement covering indexes
- ✅ Handle index maintenance
- ✅ Optimize index strategy

