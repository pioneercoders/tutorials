# Linked Lists in Data Structures

Linked Lists are one of the most fundamental dynamic data structures.

Unlike arrays:

* Linked lists do not require contiguous memory.
* Elements are connected using pointers/references.

They are heavily used in:

* Operating systems
* Browsers
* Databases
* Memory management
* Caches
* Music playlists
* Undo/Redo systems

---

# Why Linked Lists Exist

Arrays have limitations:

* Fixed size (static arrays)
* Expensive insertions/deletions in middle
* Memory resizing overhead

Linked Lists solve these problems using dynamic memory allocation.

---

# Real-World Analogy

Imagine train compartments.

```text id="x8dwh2"
[Engine] → [Compartment] → [Compartment]
```

Each compartment stores:

* Data
* Link to next compartment

That is exactly how a linked list works.

---

# 1. Singly Linked List

Each node contains:

1. Data
2. Pointer to next node

---

# Structure

```text id="czfhme"
[10 | * ] → [20 | * ] → [30 | null]
```

---

# Node Structure

```js id="gr2u5s"
class Node {
  constructor(data) {
    this.data = data;
    this.next = null;
  }
}
```

---

# Linked List Structure

```js id="3u90nj"
class LinkedList {
  constructor() {
    this.head = null;
  }
}
```

---

# Creating Nodes

```js id="rfczw4"
const first = new Node(10);
const second = new Node(20);
const third = new Node(30);

first.next = second;
second.next = third;
```

---

# Visualization

```text id="grd1pz"
Head
 ↓
10 → 20 → 30 → null
```

---

# Time Complexity

| Operation       | Complexity |
| --------------- | ---------- |
| Insert at Head  | O(1)       |
| Insert at Tail  | O(n)       |
| Search          | O(n)       |
| Delete          | O(n)       |
| Access by Index | O(n)       |

---

# Real-Time Applications

| Application          | Usage                 |
| -------------------- | --------------------- |
| Music playlists      | Sequential navigation |
| Browser history      | Navigation chain      |
| Hash tables          | Collision handling    |
| OS memory allocation | Free lists            |

---

# 2. Insertion in Singly Linked List

---

# Insert at Beginning

Fastest insertion operation.

---

# Visualization

Before:

```text id="fjlwm8"
10 → 20 → 30
```

Insert 5:

```text id="j7m17r"
5 → 10 → 20 → 30
```

---

# Code

```js id="x92g8k"
insertAtHead(data) {
  const newNode = new Node(data);

  newNode.next = this.head;
  this.head = newNode;
}
```

---

# Complexity

```text id="q8n3ku"
O(1)
```

---

# Insert at End

---

# Code

```js id="c3z5fg"
insertAtTail(data) {
  const newNode = new Node(data);

  if (!this.head) {
    this.head = newNode;
    return;
  }

  let current = this.head;

  while (current.next) {
    current = current.next;
  }

  current.next = newNode;
}
```

---

# Complexity

```text id="jjjlwm"
O(n)
```

Unless tail pointer is maintained.

---

# Insert at Position

```js id="o6l8jw"
insertAtPosition(data, position) {
  const newNode = new Node(data);

  if (position === 0) {
    newNode.next = this.head;
    this.head = newNode;
    return;
  }

  let current = this.head;

  for (let i = 0; i < position - 1; i++) {
    current = current.next;
  }

  newNode.next = current.next;
  current.next = newNode;
}
```

---

# 3. Deletion in Singly Linked List

---

# Delete Head

```js id="0gxjlwm"
deleteHead() {
  if (!this.head) return;

  this.head = this.head.next;
}
```

---

# Complexity

```text id="q6lm1j"
O(1)
```

---

# Delete by Value

```js id="lq2ewx"
delete(value) {
  if (!this.head) return;

  if (this.head.data === value) {
    this.head = this.head.next;
    return;
  }

  let current = this.head;

  while (current.next && current.next.data !== value) {
    current = current.next;
  }

  if (current.next) {
    current.next = current.next.next;
  }
}
```

---

# Visualization

Before:

```text id="1mp6fs"
10 → 20 → 30
```

Delete 20:

```text id="m2clvm"
10 → 30
```

---

# 4. Traversal

Traversal means visiting all nodes.

---

# Code

```js id="5r7x5h"
traverse() {
  let current = this.head;

  while (current) {
    console.log(current.data);
    current = current.next;
  }
}
```

---

# Complexity

```text id="s39hh0"
O(n)
```

---

# Real-Time Example

## Spotify Playlist Navigation

Songs are traversed sequentially.

---

# 5. Reverse Linked List

One of the most important interview problems.

---

# Visualization

Before:

```text id="p3pjlwm"
10 → 20 → 30 → null
```

After:

```text id="d07z2w"
30 → 20 → 10 → null
```

---

# Iterative Solution

```js id="6n91gx"
reverse() {
  let prev = null;
  let current = this.head;

  while (current) {
    let next = current.next;

    current.next = prev;
    prev = current;
    current = next;
  }

  this.head = prev;
}
```

---

# Complexity

| Type  | Complexity |
| ----- | ---------- |
| Time  | O(n)       |
| Space | O(1)       |

---

# Real-Time Applications

| System          | Usage              |
| --------------- | ------------------ |
| Browser history | Reverse navigation |
| Undo operations | State reversal     |
| Media playback  | Reverse traversal  |

---

# 6. Doubly Linked List

Each node contains:

1. Previous pointer
2. Data
3. Next pointer

---

# Structure

```text id="sjlwm8"
null ← 10 ⇄ 20 ⇄ 30 → null
```

---

# Node Structure

```js id="5m1h3y"
class DoublyNode {
  constructor(data) {
    this.data = data;
    this.prev = null;
    this.next = null;
  }
}
```

---

# Advantages

| Feature                 | Benefit                |
| ----------------------- | ---------------------- |
| Bidirectional traversal | Move both ways         |
| Faster deletion         | Easier pointer updates |
| Better navigation       | Browser history        |

---

# Disadvantages

* Extra memory
* More pointer management

---

# Real-Time Applications

| Application       | Usage            |
| ----------------- | ---------------- |
| Browser history   | Back/Forward     |
| Music players     | Previous/Next    |
| Undo/Redo systems | State navigation |

---

# 7. Bidirectional Traversal

---

# Forward Traversal

```js id="vv2lax"
let current = head;

while (current) {
  console.log(current.data);
  current = current.next;
}
```

---

# Backward Traversal

```js id="jjpjlwm"
let current = tail;

while (current) {
  console.log(current.data);
  current = current.prev;
}
```

---

# Why This Matters

Arrays support random access.

Singly linked lists do not.

Doubly linked lists partially solve navigation limitations.

---

# 8. Insert/Delete Operations in Doubly Linked List

---

# Insert

```js id="33nq8h"
newNode.next = current.next;
newNode.prev = current;

current.next.prev = newNode;
current.next = newNode;
```

---

# Delete

```js id="1p9t0q"
current.prev.next = current.next;
current.next.prev = current.prev;
```

---

# Complexity

| Operation     | Complexity |
| ------------- | ---------- |
| Insert/Delete | O(1)       |
| Search        | O(n)       |

---

# 9. Circular Linked List

Last node points back to head.

---

# Structure

```text id="jlwmqt"
10 → 20 → 30
↑         ↓
← ← ← ← ←
```

---

# Why Circular?

No null termination.

Useful for:

* Round-robin scheduling
* Cyclic systems
* Multiplayer turns

---

# Circular Traversal

```js id="jbw2cd"
traverseCircular() {
  if (!this.head) return;

  let current = this.head;

  do {
    console.log(current.data);
    current = current.next;
  } while (current !== this.head);
}
```

---

# Real-Time Applications

| System            | Usage             |
| ----------------- | ----------------- |
| CPU scheduling    | Round Robin       |
| Multiplayer games | Turn rotation     |
| Circular buffers  | Streaming systems |

---

# 10. Josephus Problem

Classic circular linked list problem.

---

# Problem

People stand in a circle.

Every kth person gets eliminated.

Find survivor.

---

# Visualization

```text id="nmjlwm"
1 → 2 → 3 → 4 → 5
```

Eliminate every 2nd person.

---

# Real-Time Analogy

Used in:

* Scheduling systems
* Distributed elimination algorithms

---

# 11. Detect Cycle in Linked List

Very famous interview problem.

---

# Problem

```text id="q5j6jk"
10 → 20 → 30
      ↑    ↓
      ← ← ←
```

List loops infinitely.

---

# Floyd’s Cycle Detection Algorithm

Also called:

```text id="k1jlwm"
Tortoise and Hare Algorithm
```

---

# Idea

Use:

* Slow pointer
* Fast pointer

If they meet:

* Cycle exists

---

# Code

```js id="frjlwm"
function hasCycle(head) {
  let slow = head;
  let fast = head;

  while (fast && fast.next) {
    slow = slow.next;
    fast = fast.next.next;

    if (slow === fast) {
      return true;
    }
  }

  return false;
}
```

---

# Complexity

| Type  | Complexity |
| ----- | ---------- |
| Time  | O(n)       |
| Space | O(1)       |

---

# Real-Time Applications

| System                | Usage                    |
| --------------------- | ------------------------ |
| OS process scheduling | Loop detection           |
| Networking            | Packet routing cycles    |
| Graph systems         | Infinite loop prevention |

---

# 12. Merge Linked Lists

---

# Merge Sorted Lists

```js id="u4kjlwm"
function merge(l1, l2) {
  const dummy = new Node(0);
  let current = dummy;

  while (l1 && l2) {
    if (l1.data < l2.data) {
      current.next = l1;
      l1 = l1.next;
    } else {
      current.next = l2;
      l2 = l2.next;
    }

    current = current.next;
  }

  current.next = l1 || l2;

  return dummy.next;
}
```

---

# Complexity

```text id="yjlwmx"
O(n + m)
```

---

# Real-Time Applications

* Merge sort
* Database merging
* Streaming systems

---

# 13. Clone Linked List

Advanced interview problem.

---

# Problem

Clone:

* Data
* Next pointers
* Random pointers

---

# Real-Time Use Case

Deep copying complex structures:

* Browser tabs
* Undo systems
* Game states

---

# Key Idea

Use:

* HashMap
  or
* Interweaving nodes

---

# Complexity

| Method    | Complexity       |
| --------- | ---------------- |
| HashMap   | O(n) space       |
| Optimized | O(1) extra space |

---

# 14. LRU Cache Design

One of the most important system design interview problems.

---

# What is LRU?

```text id="gj0jlwm"
Least Recently Used Cache
```

Removes least recently accessed item.

---

# Why LRU Exists

Memory is limited.

Need efficient cache eviction.

---

# Real-Time Applications

| System            | Usage             |
| ----------------- | ----------------- |
| Browsers          | Cache tabs        |
| Databases         | Query cache       |
| Redis             | In-memory caching |
| Operating systems | Page replacement  |

---

# LRU Requirements

Operations must be:

* O(1) get
* O(1) put

---

# Data Structures Used

| Structure          | Purpose                |
| ------------------ | ---------------------- |
| HashMap            | Fast lookup            |
| Doubly Linked List | Fast removal/insertion |

---

# Architecture

```text id="ywp4gf"
HashMap + Doubly Linked List
```

---

# Visualization

Most Recently Used near head.

```text id="jlwm0m"
HEAD ⇄ A ⇄ B ⇄ C ⇄ TAIL
```

Least recently used near tail.

---

# Simplified LRU Design

```js id="jlwmkc"
class LRUCache {
  constructor(capacity) {
    this.capacity = capacity;
    this.cache = new Map();
  }
}
```

---

# Why Doubly Linked List?

Need:

* O(1) deletion
* O(1) insertion

Singly linked list cannot delete efficiently without previous node.

---

# Important Linked List Interview Problems

| Problem           | Pattern              |
| ----------------- | -------------------- |
| Reverse List      | Pointer manipulation |
| Detect Cycle      | Fast/Slow pointers   |
| Merge Lists       | Two pointers         |
| Palindrome List   | Reverse + middle     |
| Remove Nth Node   | Two pointers         |
| Clone Random List | Hashing              |
| LRU Cache         | DLL + HashMap        |

---

# Common Beginner Mistakes

| Mistake               | Problem                  |
| --------------------- | ------------------------ |
| Losing head pointer   | Memory leak              |
| Wrong pointer updates | Broken list              |
| Infinite traversal    | Cycles                   |
| Null pointer access   | Runtime crash            |
| Forgetting edge cases | Empty/single node issues |

---

# Production Engineering Insights

Linked Lists are heavily used internally in:

* Redis
* Linux Kernel
* Browsers
* Memory allocators
* Networking systems
* LRU caches
* Database engines

---

# Linked List vs Array

| Feature        | Array      | Linked List |
| -------------- | ---------- | ----------- |
| Memory         | Contiguous | Dynamic     |
| Access         | O(1)       | O(n)        |
| Insert/Delete  | Expensive  | Efficient   |
| Cache locality | Better     | Worse       |
| Dynamic growth | Difficult  | Easy        |

---

# Summary Table

| Topic                | Key Idea              |
| -------------------- | --------------------- |
| Singly Linked List   | One-way traversal     |
| Doubly Linked List   | Two-way traversal     |
| Circular Linked List | Cyclic structure      |
| Reverse List         | Pointer reversal      |
| Detect Cycle         | Fast/slow pointers    |
| Merge Lists          | Sequential merging    |
| Clone List           | Deep copying          |
| LRU Cache            | Cache eviction design |

---
