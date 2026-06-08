# Advanced Trees

Advanced Trees are specialized tree data structures designed for:

* High performance
* Fast searching
* Efficient updates
* Scalable storage
* Range queries
* Database indexing
* String processing

These structures power:

* Google Search
* Databases
* Redis
* Linux Kernel
* File systems
* AI systems
* Search engines

---

# Why Advanced Trees Exist

Normal BSTs can become skewed.

Example:

```text id="at1"
10
 \
  20
    \
     30
```

Searching becomes:

```text id="at2"
O(n)
```

Advanced trees solve:

* Balancing
* Range queries
* Massive storage
* Prefix matching
* Streaming updates

---

# 1. AVL Trees

AVL Tree is a:

```text id="at3"
Self-balancing Binary Search Tree
```

Invented by:

* Adelson-Velsky
* Landis

---

# AVL Property

For every node:

|\text{Height(Left)} - \text{Height(Right)}| \leq 1

---

# Why AVL?

Keeps tree balanced,
guaranteeing:

```text id="at4"
O(log n)
```

operations.

---

# Example Balanced Tree

```text id="at5"
        30
       /  \
     20    40
```

---

# Example Unbalanced Tree

```text id="at6"
10
 \
  20
    \
     30
```

Requires balancing.

---

# AVL Node Structure

```js id="at7"
class AVLNode {
  constructor(data) {
    this.data = data;
    this.left = null;
    this.right = null;
    this.height = 1;
  }
}
```

---

# Complexity

| Operation | Complexity |
| --------- | ---------- |
| Insert    | O(log n)   |
| Delete    | O(log n)   |
| Search    | O(log n)   |

---

# Real-Time Applications

| System              | Usage            |
| ------------------- | ---------------- |
| In-memory databases | Fast lookup      |
| Gaming engines      | Spatial indexing |
| Scheduling systems  | Ordered data     |

---

# 2. Rotations in AVL Trees

Rotations restore balance.

Most important AVL concept.

---

# Types of Rotations

| Rotation       | Case        |
| -------------- | ----------- |
| Left Rotation  | Right-heavy |
| Right Rotation | Left-heavy  |
| Left-Right     | Mixed       |
| Right-Left     | Mixed       |

---

# Right Rotation

Before:

```text id="at8"
      30
     /
   20
  /
10
```

After:

```text id="at9"
      20
     /  \
   10   30
```

---

# Left Rotation

Before:

```text id="at10"
10
 \
  20
    \
     30
```

After:

```text id="at11"
      20
     /  \
   10   30
```

---

# Why Rotations Matter

They maintain:

```text id="at12"
Balanced height
```

without breaking BST property.

---

# Rotation Complexity

```text id="at13"
O(1)
```

Very efficient.

---

# 3. Balancing in AVL Trees

After insertion/deletion:

* Calculate balance factor
* Apply rotations if needed

---

# Balance Factor

\text{Balance Factor} = \text{Height(Left)} - \text{Height(Right)}

---

# Cases

| Balance   | Meaning    |
| --------- | ---------- |
| 0         | Perfect    |
| ±1        | Balanced   |
| >1 or <-1 | Unbalanced |

---

# Why AVL Trees are Fast

Height remains logarithmic.

---

# AVL Height Property

\text{Height} = O(\log n)

---

# 4. Red-Black Trees

Another self-balancing BST.

Very important in production systems.

Used more often than AVL in practice.

---

# Why Red-Black Trees?

AVL:

* More strict balancing

Red-Black:

* Faster insertion/deletion

---

# Node Colors

Each node:

* Red
  or
* Black

---

# Coloring Rules

---

# Rule 1

Root must be black.

---

# Rule 2

Red node cannot have red child.

---

# Rule 3

Every path from root to null
must have same number of black nodes.

---

# Example

```text id="at14"
       (B)20
       /    \
    (R)10  (R)30
```

---

# Why Colors?

Colors help maintain:

```text id="at15"
Approximate balance
```

---

# Complexity

| Operation | Complexity |
| --------- | ---------- |
| Search    | O(log n)   |
| Insert    | O(log n)   |
| Delete    | O(log n)   |

---

# Real-Time Applications

| System       | Usage              |
| ------------ | ------------------ |
| Linux Kernel | Process scheduling |
| Java TreeMap | Ordered maps       |
| C++ STL map  | Balanced storage   |

---

# Rotations in Red-Black Trees

Uses:

* Left rotation
* Right rotation

plus:

* Recoloring

---

# Why Rotations Matter

Prevent skewed trees.

---

# AVL vs Red-Black Tree

| Feature          | AVL    | Red-Black       |
| ---------------- | ------ | --------------- |
| Balancing        | Strict | Relaxed         |
| Search           | Faster | Slightly slower |
| Insert/Delete    | Slower | Faster          |
| Production Usage | Less   | More            |

---

# 5. Segment Trees

Very powerful range-query data structure.

---

# Why Segment Trees?

Efficiently answer:

* Range sum
* Range minimum
* Range maximum
* Updates

---

# Brute Force Problem

Range query repeatedly:

```text id="at16"
O(n)
```

too slow.

---

# Segment Tree Solution

Supports:

| Operation   | Complexity |
| ----------- | ---------- |
| Range Query | O(log n)   |
| Update      | O(log n)   |

---

# Example

Array:

```text id="at17"
[1,3,5,7,9,11]
```

Query:

```text id="at18"
sum(1,4)
```

---

# Visualization

```text id="at19"
             [1-6]
            /     \
         [1-3]   [4-6]
```

---

# Real-Time Applications

| System            | Usage            |
| ----------------- | ---------------- |
| Gaming            | Score ranges     |
| Financial systems | Stock intervals  |
| Analytics         | Range statistics |

---

# Segment Tree Complexity

Build:

```text id="at20"
O(n)
```

Query:

```text id="at21"
O(log n)
```

---

# 6. Lazy Propagation

Advanced Segment Tree optimization.

---

# Problem

Updating large ranges repeatedly becomes expensive.

---

# Lazy Propagation Idea

Delay updates until necessary.

---

# Example

Instead of updating:

```text id="at22"
Entire subtree immediately
```

Store:

```text id="at23"
Pending update
```

---

# Benefits

Huge optimization for:

* Massive updates
* Competitive programming
* Real-time analytics

---

# Complexity

Range updates:

```text id="at24"
O(log n)
```

---

# Real-Time Applications

| System               | Usage            |
| -------------------- | ---------------- |
| Analytics dashboards | Batch updates    |
| Financial systems    | Interval changes |
| Streaming systems    | Window updates   |

---

# 7. Fenwick Tree (Binary Indexed Tree)

Simpler alternative to Segment Tree.

Used for:

* Prefix sums
* Updates

---

# Why Fenwick Tree?

Efficient:

* Memory usage
* Simpler implementation

---

# Complexity

| Operation    | Complexity |
| ------------ | ---------- |
| Prefix Query | O(log n)   |
| Update       | O(log n)   |

---

# Fenwick Tree Idea

Store cumulative contributions efficiently.

---

# Prefix Query Example

```text id="at25"
sum(1 to i)
```

---

# Update Example

```text id="at26"
Add value at index
```

---

# Fenwick Tree Code

```js id="at27"
class BIT {
  constructor(size) {
    this.tree = Array(size + 1).fill(0);
  }
}
```

---

# Segment Tree vs Fenwick Tree

| Feature        | Segment Tree | Fenwick Tree |
| -------------- | ------------ | ------------ |
| Flexibility    | High         | Medium       |
| Memory         | More         | Less         |
| Implementation | Complex      | Simpler      |

---

# Real-Time Applications

| System            | Usage           |
| ----------------- | --------------- |
| Analytics         | Prefix metrics  |
| Leaderboards      | Running totals  |
| Financial systems | Cumulative sums |

---

# 8. Trie

Very important string tree.

Used for:

* Prefix matching
* Autocomplete
* Search engines

---

# Trie Structure

```text id="at28"
       root
      /    \
     c      d
    /        \
   a          o
  /            \
 t              g
```

Words:

* cat
* dog

---

# Why Trie?

Searching character-by-character is efficient.

---

# Complexity

| Operation     | Complexity |
| ------------- | ---------- |
| Insert        | O(length)  |
| Search        | O(length)  |
| Prefix Search | O(length)  |

---

# Trie Node

```js id="at29"
class TrieNode {
  constructor() {
    this.children = {};
    this.isEnd = false;
  }
}
```

---

# 9. Prefix Matching

Very important real-world application.

---

# Example

Search:

```text id="at30"
"app"
```

Matches:

* apple
* application
* appstore

---

# Why Trie is Efficient

Avoids scanning all strings.

---

# Real-Time Applications

| System        | Usage             |
| ------------- | ----------------- |
| Google Search | Suggestions       |
| IDEs          | Code autocomplete |
| Keyboards     | Word prediction   |

---

# 10. Autocomplete Systems

One of the most practical Trie applications.

---

# Workflow

User types:

```text id="at31"
"rea"
```

Trie returns:

* react
* read
* real
* reason

---

# Additional Optimizations

Production systems combine:

* Trie
* Ranking
* Frequency analysis
* AI models

---

# Real-Time Systems

| Company           | Usage                |
| ----------------- | -------------------- |
| Google            | Search autocomplete  |
| Microsoft VS Code | IntelliSense         |
| Apple             | Keyboard suggestions |

---

# 11. B Trees / B+ Trees

Extremely important database topic.

---

# Why Normal BSTs Fail for Databases

Disk access is expensive.

Need:

* Fewer disk reads
* High branching factor

---

# B-Tree Idea

Each node stores:

* Multiple keys
* Multiple children

---

# Visualization

```text id="at32"
[10 | 20 | 30]
 /    |    |   \
```

---

# Advantages

| Benefit             | Why Important     |
| ------------------- | ----------------- |
| Fewer disk accesses | Faster DB queries |
| Balanced height     | Efficient lookup  |
| Large branching     | Better storage    |

---

# B+ Tree

Most databases use:

```text id="at33"
B+ Trees
```

instead of B-Trees.

---

# Why B+ Trees?

Leaf nodes linked sequentially.

Better for:

* Range queries
* Sequential access

---

# Real-Time Applications

| System       | Usage              |
| ------------ | ------------------ |
| MySQL        | Database indexing  |
| PostgreSQL   | Query optimization |
| File systems | Metadata indexing  |

---

# 12. Database Indexing

One of the most important real-world applications.

---

# Without Index

Database scans every row:

```text id="at34"
O(n)
```

---

# With B+ Tree Index

Search becomes:

```text id="at35"
O(log n)
```

---

# Example

Query:

```sql id="at36"
SELECT * FROM users
WHERE id = 100;
```

Uses index tree internally.

---

# Why Indexes Matter

Indexes power:

* Fast search
* Sorting
* Range queries
* Joins

---

# 13. Suffix Trees

Advanced string-processing tree.

---

# Purpose

Efficient substring searching.

---

# Example

String:

```text id="at37"
banana
```

Suffixes:

* banana
* anana
* nana
* ana
* na
* a

---

# Why Suffix Trees?

Fast substring operations.

---

# Complexity

| Operation | Complexity |
| --------- | ---------- |
| Build     | O(n)       |
| Search    | O(m)       |

---

# Real-Time Applications

| System              | Usage             |
| ------------------- | ----------------- |
| DNA sequencing      | Pattern search    |
| Search engines      | Fast matching     |
| Compression systems | Repeated patterns |

---

# 14. String Processing with Trees

Advanced trees optimize:

* Pattern matching
* Autocomplete
* Compression
* Similarity search

---

# Important Structures

| Structure    | Purpose                        |
| ------------ | ------------------------------ |
| Trie         | Prefix matching                |
| Suffix Tree  | Substring matching             |
| Suffix Array | Memory-efficient suffix search |

---

# Advanced Tree Interview Problems

| Problem           | Structure        |
| ----------------- | ---------------- |
| Range Sum Query   | Segment Tree     |
| Prefix Search     | Trie             |
| Kth Smallest      | Balanced BST     |
| Interval Updates  | Lazy Propagation |
| Autocomplete      | Trie             |
| Median in Stream  | Balanced Trees   |
| Database Indexing | B+ Trees         |

---

# Common Beginner Mistakes

| Mistake                          | Problem               |
| -------------------------------- | --------------------- |
| Forgetting rotations             | Unbalanced trees      |
| Wrong balance factor             | AVL errors            |
| Confusing AVL/RB Trees           | Incorrect assumptions |
| Using Segment Tree unnecessarily | Overengineering       |
| Wrong Trie traversal             | Prefix bugs           |

---

# Production Engineering Insights

Advanced trees power:

* Google indexing
* Linux schedulers
* MySQL/PostgreSQL indexing
* Redis sorted structures
* AI autocomplete systems
* Kubernetes scheduling

These are foundational in large-scale systems.

---

# Summary Table

| Topic            | Key Idea              |
| ---------------- | --------------------- |
| AVL Tree         | Strict balancing      |
| Rotations        | Restore balance       |
| Red-Black Tree   | Relaxed balancing     |
| Segment Tree     | Range queries         |
| Lazy Propagation | Delayed updates       |
| Fenwick Tree     | Prefix sums           |
| Trie             | Prefix matching       |
| B+ Tree          | Database indexing     |
| Suffix Tree      | Fast substring search |

---
