# Introduction to Data Structures

Data Structures are one of the most important foundations in Computer Science and Software Engineering.

Every application you use today — from Instagram feeds to Google Search to WhatsApp chats — relies heavily on Data Structures internally.

---

# 1. What are Data Structures?

A **Data Structure** is a way of organizing, storing, and managing data efficiently so that operations can be performed effectively.

Think of it like organizing items in real life.

### Real-Life Examples

| Real Life           | Data Structure Idea |
| ------------------- | ------------------- |
| Books on shelves    | Array               |
| Train compartments  | Linked List         |
| Browser back button | Stack               |
| Printer queue       | Queue               |
| Google Maps routes  | Graph               |
| Folder system in OS | Tree                |

---

## Why Data Structures Matter

Without proper data structures:

* Applications become slow
* Memory usage increases
* Searching becomes inefficient
* Scaling becomes difficult

### Example

Imagine storing 10 million users.

If data is not organized properly:

* Searching may take minutes

With efficient data structures:

* Searching happens in milliseconds

---

# 2. Types of Data Structures

Data Structures are broadly divided into two categories:

```text
Data Structures
│
├── Primitive
│   ├── int
│   ├── char
│   ├── float
│   └── boolean
│
└── Non-Primitive
    ├── Linear
    └── Non-Linear
```

---

# Primitive Data Structures

These are built-in basic data types provided by programming languages.

Examples:

* Integer
* Float
* Character
* Boolean

```js
let age = 25;
let price = 99.99;
let isLoggedIn = true;
```

---

# Non-Primitive Data Structures

These are more complex structures built using primitive data types.

Examples:

* Arrays
* Linked Lists
* Trees
* Graphs
* Hash Tables

---

# 3. Linear vs Non-Linear Data Structures

# Linear Data Structures

Elements are arranged sequentially.

```text
10 → 20 → 30 → 40
```

Examples:

* Array
* Linked List
* Stack
* Queue

---

## Characteristics

* Easy traversal
* Single-level organization
* Memory efficient for sequential operations

---

## Real-Time Examples

| Application       | Data Structure |
| ----------------- | -------------- |
| Music playlist    | Linked List    |
| Browser history   | Stack          |
| Call center queue | Queue          |

---

# Non-Linear Data Structures

Elements are connected hierarchically or network-wise.

```text
        A
      /   \
     B     C
    / \
   D   E
```

Examples:

* Trees
* Graphs
* Heap
* Trie

---

## Characteristics

* Complex relationships
* Faster searching in many scenarios
* Used in AI, networking, databases

---

## Real-Time Examples

| Application       | Data Structure |
| ----------------- | -------------- |
| File system       | Tree           |
| Social networks   | Graph          |
| GPS navigation    | Graph          |
| Database indexing | B-Tree         |

---

# Comparison Table

| Feature    | Linear       | Non-Linear           |
| ---------- | ------------ | -------------------- |
| Structure  | Sequential   | Hierarchical/Network |
| Traversal  | Single path  | Multiple paths       |
| Complexity | Simpler      | More complex         |
| Examples   | Array, Stack | Tree, Graph          |

---

# 4. Static vs Dynamic Data Structures

# Static Data Structures

Size is fixed during compile time or initialization.

Example:

* Array

```js
const arr = new Array(5);
```

Memory is allocated beforehand.

---

## Advantages

* Faster access
* Simpler implementation
* Better cache locality

---

## Disadvantages

* Memory wastage
* Fixed size limitation

---

## Real-Time Example

### Classroom Bench Allocation

If classroom has only 40 seats:

* Fixed structure
* Cannot expand dynamically

---

# Dynamic Data Structures

Size can grow or shrink during runtime.

Examples:

* Linked List
* Dynamic Array
* Trees
* Graphs

```js
const arr = [];
arr.push(10);
arr.push(20);
```

---

## Advantages

* Flexible memory usage
* Efficient for unpredictable data

---

## Disadvantages

* Extra memory overhead
* Complex implementation

---

## Real-Time Example

### Instagram Feed

Posts load dynamically:

* Infinite scrolling
* Data keeps growing

Dynamic structures handle this efficiently.

---

# Static vs Dynamic Comparison

| Feature  | Static        | Dynamic            |
| -------- | ------------- | ------------------ |
| Size     | Fixed         | Flexible           |
| Memory   | Pre-allocated | Runtime allocation |
| Speed    | Faster        | Slightly slower    |
| Examples | Array         | Linked List        |

---

# 5. Time Complexity Basics

Time Complexity measures:

> How execution time grows as input size increases.

---

# Why Time Complexity Matters

Suppose:

```js
for (let i = 0; i < n; i++) {
  console.log(i);
}
```

If:

* n = 10 → 10 operations
* n = 1,000,000 → 1 million operations

Performance becomes critical.

---

# Common Time Complexities

| Complexity | Name         | Example             |
| ---------- | ------------ | ------------------- |
| O(1)       | Constant     | Array access        |
| O(log n)   | Logarithmic  | Binary Search       |
| O(n)       | Linear       | Linear Search       |
| O(n log n) | Linearithmic | Merge Sort          |
| O(n²)      | Quadratic    | Bubble Sort         |
| O(2ⁿ)      | Exponential  | Recursive Fibonacci |

---

# Example: O(1)

```js
const arr = [10, 20, 30];

console.log(arr[1]);
```

Accessing an index takes constant time.

---

# Example: O(n)

```js
for (let i = 0; i < n; i++) {
  console.log(i);
}
```

Execution grows linearly.

---

# Example: O(n²)

```js
for (let i = 0; i < n; i++) {
  for (let j = 0; j < n; j++) {
    console.log(i, j);
  }
}
```

Nested loops create quadratic complexity.

---

# Real-Time Engineering Example

## Search Systems

### Linear Search

```text
1 → 2 → 3 → 4 → 5
```

Worst-case:

* Check every element

Complexity:

* O(n)

---

### Binary Search

```text
Middle → Left/Right halves
```

Complexity:

* O(log n)

Used in:

* Databases
* Search engines
* File systems

---

# Performance Comparison

| Input Size | O(n)      | O(log n) |
| ---------- | --------- | -------- |
| 1,000      | 1,000 ops | ~10 ops  |
| 1,000,000  | 1M ops    | ~20 ops  |

Huge difference in production systems.

---

# 6. Space Complexity Basics

Space Complexity measures:

> How much memory an algorithm uses.

Includes:

* Variables
* Data structures
* Function calls
* Recursion stack

---

# Example: O(1) Space

```js
function sum(a, b) {
  return a + b;
}
```

Uses fixed memory.

---

# Example: O(n) Space

```js
function createArray(n) {
  let arr = [];

  for (let i = 0; i < n; i++) {
    arr.push(i);
  }

  return arr;
}
```

Memory grows with input size.

---

# Recursive Space Example

```js
function factorial(n) {
  if (n === 1) return 1;

  return n * factorial(n - 1);
}
```

Recursive calls use stack memory.

Space Complexity:

* O(n)

---

# Real-Time Example

## Video Streaming Platforms

Netflix/YouTube optimize:

* Memory usage
* Cache size
* Buffer storage

Efficient space complexity improves performance.

---

# 7. Big-O Notation

Big-O describes the upper bound of algorithm growth.

It helps predict scalability.

---

# Common Big-O Orders

```text
Best Performance
O(1)

O(log n)

O(n)

O(n log n)

O(n²)

O(2ⁿ)

Worst Performance
```

---

# Example

```js
function findUser(users, target) {
  for (const user of users) {
    if (user === target) {
      return true;
    }
  }

  return false;
}
```

Worst-case:

* Search entire array

Big-O:

* O(n)

---

# Big-O Rules

---

## Rule 1: Drop Constants

```js
O(2n) → O(n)
```

Because growth matters more than constants.

---

## Rule 2: Drop Smaller Terms

```js
O(n² + n) → O(n²)
```

Dominant term matters.

---

# Real-Time Big-O in Production

| System         | Important Complexity |
| -------------- | -------------------- |
| Google Search  | O(log n) indexing    |
| Instagram Feed | O(1) cache lookup    |
| Uber Maps      | Graph algorithms     |
| Databases      | B-Tree search        |

---

# 8. Memory Representation

Understanding memory is crucial for mastering DSA.

---

# Computer Memory Basics

Memory stores data in bytes.

Each memory location has:

* Address
* Value

Example:

| Address | Value |
| ------- | ----- |
| 100     | 10    |
| 101     | 20    |
| 102     | 30    |

---

# Array Memory Representation

Arrays use contiguous memory.

```text
Index:    0   1   2
Value:   10  20  30
Address:100 104 108
```

Advantages:

* Fast indexing

Formula:

```text
Address = Base + (Index × Size)
```

---

# Why Array Access is O(1)

Because address calculation is direct.

```js
arr[2]
```

Computer instantly calculates memory location.

---

# Linked List Memory Representation

Linked Lists are non-contiguous.

```text
[10 | * ] → [20 | * ] → [30 | null]
```

Each node contains:

* Data
* Pointer

---

# Real-Time Memory Usage

## Browser Tabs

Modern browsers internally use:

* Linked structures
* Trees
* Hash Maps

to manage:

* Tabs
* Cache
* Sessions

---

# Stack Memory vs Heap Memory

# Stack Memory

Stores:

* Function calls
* Local variables

Fast but limited.

---

# Heap Memory

Stores:

* Dynamic objects
* Dynamic arrays
* Linked structures

Flexible but slower.

---

# Example

```js
let a = 10;
```

Stored in stack.

---

```js
let arr = [1, 2, 3];
```

Reference stored in stack,
actual array stored in heap.

---

# Real-Time Interview Insight

Interviewers often ask:

> Why are arrays faster than linked lists for indexing?

Answer:

* Arrays use contiguous memory
* Direct address calculation
* O(1) access

Linked lists require traversal:

* O(n)

---

# Common Beginner Mistakes

| Mistake                 | Problem                  |
| ----------------------- | ------------------------ |
| Ignoring complexity     | Slow applications        |
| Using arrays everywhere | Inefficient memory usage |
| Confusing stack vs heap | Memory bugs              |
| Ignoring scalability    | System crashes           |

---

# Production Engineering Perspective

In real systems:

* Choosing wrong data structure can cost millions
* Databases heavily depend on Trees
* Caches use Hash Maps
* Messaging systems use Queues
* OS schedulers use Priority Queues

---

# Summary

| Concept               | Key Idea                    |
| --------------------- | --------------------------- |
| Data Structure        | Organizing data efficiently |
| Linear DS             | Sequential arrangement      |
| Non-Linear DS         | Hierarchical/network        |
| Static DS             | Fixed size                  |
| Dynamic DS            | Runtime growth              |
| Time Complexity       | Execution growth            |
| Space Complexity      | Memory growth               |
| Big-O                 | Scalability measurement     |
| Memory Representation | How data lives in memory    |

---

# What You Should Learn Next

Recommended order:

1. Arrays
2. Strings
3. Linked Lists
4. Stack
5. Queue
6. Hashing
7. Trees
8. Heap
9. Graphs
10. Advanced Algorithms

---

# Mini Practice Questions

1. Difference between Array and Linked List?
2. Why is Binary Search faster?
3. Explain O(1) with examples.
4. What is contiguous memory?
5. Difference between stack and heap memory?
6. Real-world examples of Trees and Graphs?
7. Why are dynamic structures important?

---

# Mini Assignment

Implement in JavaScript:

1. Linear Search
2. Dynamic Array behavior using push()
3. Stack using Array
4. Queue using Array

---

# Final Real-World Takeaway

Data Structures are everywhere.

Whenever you:

* Scroll Instagram
* Search Google
* Watch YouTube
* Book Uber
* Send WhatsApp messages

You are indirectly interacting with advanced Data Structures designed for:

* Speed
* Scalability
* Memory efficiency
* Reliability
