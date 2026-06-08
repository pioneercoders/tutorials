# Hashing & Hash Tables

Hashing is one of the most powerful concepts in Computer Science.

Modern systems heavily depend on hashing for:

* Databases
* Caching
* Authentication
* Distributed systems
* Search engines
* Blockchain
* AI systems

Hash tables provide near:

```text id="h1"
O(1)
```

average-time complexity for:

* Insert
* Search
* Delete

This makes them one of the fastest data structures ever created.

---

# 1. What is Hashing?

Hashing is the process of converting data into a fixed-size value called:

```text id="h2"
Hash Code / Hash Value
```

using a:

```text id="h3"
Hash Function
```

---

# Real-Life Analogy

Imagine a library.

Instead of searching every shelf:

* Book ID determines exact location.

That mapping process is hashing.

---

# Hash Table Structure

```text id="h4"
Key → Hash Function → Index
```

---

# Example

```js id="h5"
const map = {
  name: "Gowtham"
};
```

Internally:

* `"name"` gets hashed
* Stored at computed index

---

# Why Hashing Matters

Without hashing:

* Searching may take O(n)

With hashing:

* Average lookup becomes O(1)

---

# Real-Time Applications

| System           | Usage                  |
| ---------------- | ---------------------- |
| Google           | Search indexing        |
| Redis            | Key-value storage      |
| Databases        | Fast lookup            |
| Password systems | Secure hashing         |
| Blockchain       | Integrity verification |

---

# 2. Hash Functions

A Hash Function converts input into array index.

---

# Formula

```text id="h6"
index = hash(key) % tableSize
```

---

# Example

```text id="h7"
hash("cat") = 3456

3456 % 10 = 6
```

Store at index 6.

---

# Good Hash Function Properties

| Property             | Why Important            |
| -------------------- | ------------------------ |
| Fast                 | Efficient computation    |
| Deterministic        | Same input → same output |
| Uniform distribution | Avoid collisions         |
| Minimal clustering   | Better performance       |

---

# Bad Hash Function Example

```text id="h8"
Always returns 1
```

Everything collides.

Performance becomes:

```text id="h9"
O(n)
```

---

# Simple Hash Function

```js id="h10"
function hash(key, size) {
  let total = 0;

  for (const char of key) {
    total += char.charCodeAt(0);
  }

  return total % size;
}
```

---

# Real-Time Example

## Password Storage

Passwords are hashed before storing.

NOT stored directly.

---

# Example

```text id="h11"
password123
↓
hashed value
↓
9f86d081884...
```

---

# Important Note

Password systems use:

* Cryptographic hashing

Examples:

* SHA-256
* bcrypt
* Argon2

NOT regular hash tables.

---

# 3. Collision Handling

A collision occurs when:

* Two keys map to same index.

---

# Example

```text id="h12"
hash("abc") = 5
hash("xyz") = 5
```

Both collide at index 5.

---

# Why Collisions Matter

Collisions reduce performance.

Efficient handling is critical.

---

# Main Collision Handling Techniques

1. Chaining
2. Open Addressing

---

# 4. Chaining

Each bucket stores multiple values.

Usually using:

* Linked Lists
* Dynamic arrays

---

# Visualization

```text id="h13"
Index 5:
["cat"] → ["dog"] → ["bird"]
```

---

# Example

```js id="h14"
class HashTable {
  constructor(size) {
    this.table = new Array(size);
  }

  set(key, value) {
    const index = hash(key, this.table.length);

    if (!this.table[index]) {
      this.table[index] = [];
    }

    this.table[index].push([key, value]);
  }
}
```

---

# Complexity

| Case    | Complexity |
| ------- | ---------- |
| Average | O(1)       |
| Worst   | O(n)       |

---

# Advantages

* Simple
* Easy deletion
* Handles many collisions

---

# Disadvantages

* Extra memory
* Cache inefficiency

---

# Real-Time Applications

Used internally in:

* Older hash maps
* Symbol tables
* Caches

---

# 5. Open Addressing

Instead of linked lists:

* Find another empty slot.

---

# Types

| Type              | Formula     |
| ----------------- | ----------- |
| Linear Probing    | i + 1       |
| Quadratic Probing | i²          |
| Double Hashing    | second hash |

---

# Linear Probing Example

```text id="h15"
Collision at 5
↓
Try 6
↓
Try 7
```

---

# Visualization

```text id="h16"
Index:
0 1 2 3 4 5 6 7

           X X
```

---

# Advantages

* Better cache locality
* Memory efficient

---

# Disadvantages

* Clustering
* More complex deletion

---

# Real-Time Applications

Used in:

* Modern CPUs
* High-performance systems
* Embedded systems

---

# 6. HashMap Internals

One of the most important interview topics.

---

# What is HashMap?

Stores:

```text id="h17"
key → value
```

pairs.

---

# Example

```js id="h18"
const map = new Map();

map.set("name", "Gowtham");

console.log(map.get("name"));
```

---

# Internal Components

| Component          | Purpose           |
| ------------------ | ----------------- |
| Array              | Buckets           |
| Hash function      | Index computation |
| Collision handling | Resolve conflicts |

---

# Internal Workflow

```text id="h19"
Key
↓
Hash Function
↓
Bucket Index
↓
Store/Retrieve Value
```

---

# Java HashMap Insight

Java internally uses:

* Array
* Linked List
* Red-Black Tree (large collisions)

---

# Why Tree?

If collisions become large:

* Linked list becomes slow.

Tree improves:

```text id="h20"
O(n) → O(log n)
```

---

# Complexity

| Operation | Average | Worst |
| --------- | ------- | ----- |
| Insert    | O(1)    | O(n)  |
| Search    | O(1)    | O(n)  |
| Delete    | O(1)    | O(n)  |

---

# Real-Time Applications

| System    | Usage           |
| --------- | --------------- |
| Redis     | Key-value store |
| Caches    | Fast retrieval  |
| APIs      | Session storage |
| Databases | Indexing        |

---

# 7. HashSet

Stores only unique values.

---

# Example

```js id="h21"
const set = new Set();

set.add(10);
set.add(10);

console.log(set);
```

Only one 10 stored.

---

# Use Cases

| Problem            | Usage            |
| ------------------ | ---------------- |
| Duplicate removal  | Unique elements  |
| Membership testing | Fast lookup      |
| Cycle detection    | Visited tracking |

---

# Complexity

| Operation | Complexity |
| --------- | ---------- |
| Add       | O(1)       |
| Search    | O(1)       |
| Delete    | O(1)       |

---

# Real-Time Applications

| System                 | Usage               |
| ---------------------- | ------------------- |
| Graph algorithms       | Visited nodes       |
| Search systems         | Unique indexing     |
| Recommendation systems | Duplicate filtering |

---

# 8. Rehashing

When hash table becomes crowded:

* Resize table
* Recompute indices

---

# Why Rehash?

Too many collisions reduce performance.

---

# Visualization

Before:

```text id="h22"
Size = 4
```

After resize:

```text id="h23"
Size = 8
```

---

# Process

1. Create larger table
2. Rehash all keys
3. Insert again

---

# Complexity

Rehash operation:

```text id="h24"
O(n)
```

But infrequent.

---

# Real-Time Example

## Dynamic HashMap Growth

Most languages:

* Double table size automatically.

---

# 9. Load Factor

Measures fullness of hash table.

---

# Formula

\text{Load Factor} = \frac{\text{Number of Elements}}{\text{Table Size}}

---

# Example

```text id="h25"
Elements = 6
Table Size = 10

Load Factor = 0.6
```

---

# Why Load Factor Matters

Higher load factor:

* More collisions
* Slower operations

---

# Typical Threshold

Most systems rehash around:

```text id="h26"
0.75
```

---

# Real-Time Example

## Java HashMap

Default load factor:

```text id="h27"
0.75
```

Balances:

* Memory
* Performance

---

# 10. Consistent Hashing

Advanced distributed systems concept.

Extremely important in:

* System Design
* Distributed Databases
* Cloud Infrastructure

---

# Problem with Normal Hashing

Suppose:

```text id="h28"
hash(key) % servers
```

If servers change:

* Most keys remap.

Huge problem.

---

# Example

Before:

```text id="h29"
4 servers
```

After adding server:

```text id="h30"
5 servers
```

Almost everything moves.

---

# Consistent Hashing Solution

Maps:

* Servers
* Keys

onto a circular ring.

---

# Visualization

```text id="h31"
        Server A
      /         \
Key               Server B
      \         /
        Server C
```

---

# Benefits

| Benefit           | Why Important           |
| ----------------- | ----------------------- |
| Minimal remapping | Better scalability      |
| Fault tolerance   | Server failure handling |
| Load balancing    | Distributed traffic     |

---

# Real-Time Applications

| System           | Usage                |
| ---------------- | -------------------- |
| Amazon DynamoDB  | Data partitioning    |
| Apache Cassandra | Distributed storage  |
| Redis            | Cluster sharding     |
| CDNs             | Traffic distribution |

---

# 11. Bloom Filters

Probabilistic data structure.

Checks whether element:

* Possibly exists
* Definitely does NOT exist

---

# Key Property

```text id="h32"
False positives possible
False negatives impossible
```

---

# Why Bloom Filters?

Very memory efficient.

---

# Visualization

```text id="h33"
Element
↓
Multiple hash functions
↓
Bit array positions set
```

---

# Example Workflow

Insert:

```text id="h34"
"cat"
↓
hash1 → bit 2
hash2 → bit 8
hash3 → bit 15
```

Set bits.

---

# Search

If any bit = 0:

```text id="h35"
Definitely absent
```

If all bits = 1:

```text id="h36"
Possibly present
```

---

# Complexity

| Operation | Complexity |
| --------- | ---------- |
| Insert    | O(k)       |
| Search    | O(k)       |

Where:

```text id="h37"
k = number of hash functions
```

---

# Real-Time Applications

| System        | Usage                   |
| ------------- | ----------------------- |
| Google Chrome | Safe browsing           |
| Databases     | Query optimization      |
| Web crawlers  | Duplicate URL detection |
| Redis         | Membership testing      |

---

# Important Interview Problems

| Problem                      | Pattern              |
| ---------------------------- | -------------------- |
| Two Sum                      | HashMap              |
| Longest Consecutive Sequence | HashSet              |
| Group Anagrams               | Hashing              |
| LRU Cache                    | HashMap + DLL        |
| Top K Frequent               | Heap + HashMap       |
| Subarray Sum Equals K        | Prefix sum + HashMap |

---

# Common Beginner Mistakes

| Mistake                  | Problem          |
| ------------------------ | ---------------- |
| Poor hash function       | Heavy collisions |
| Ignoring load factor     | Performance drop |
| Wrong collision handling | Data loss        |
| Forgetting rehashing     | Slow lookups     |
| Assuming O(1) always     | Worst-case O(n)  |

---

# Production Engineering Insights

Hashing powers:

* Google indexing
* Redis caching
* Blockchain
* URL shortening
* Session management
* Distributed databases
* Password security

Modern internet infrastructure heavily relies on hashing.

---

# HashMap vs TreeMap

| Feature     | HashMap    | TreeMap        |
| ----------- | ---------- | -------------- |
| Ordering    | No         | Sorted         |
| Complexity  | O(1) avg   | O(log n)       |
| Internal DS | Hash table | Red-Black Tree |

---

# HashSet vs Array

| Feature            | HashSet     | Array             |
| ------------------ | ----------- | ----------------- |
| Search             | O(1)        | O(n)              |
| Duplicate handling | Unique only | Allows duplicates |

---

# Summary Table

| Topic              | Key Idea              |
| ------------------ | --------------------- |
| Hashing            | Key → index mapping   |
| Hash Functions     | Generate bucket index |
| Collisions         | Same index conflict   |
| Chaining           | Linked-list buckets   |
| Open Addressing    | Alternate slots       |
| HashMap            | Key-value structure   |
| HashSet            | Unique elements       |
| Rehashing          | Resize table          |
| Load Factor        | Fullness measure      |
| Consistent Hashing | Distributed scaling   |
| Bloom Filters      | Probabilistic lookup  |

---
