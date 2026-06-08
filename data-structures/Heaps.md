# Heaps in Data Structures

Heaps are one of the most important tree-based data structures.

They are heavily used in:

* Operating systems
* Task scheduling
* Priority queues
* Search engines
* Streaming systems
* AI pathfinding
* Real-time analytics

Heaps are optimized for:

```text id="heap1"
Fast priority-based operations
```

---

# Why Heaps Exist

Suppose you need:

* Highest priority task
* Minimum value quickly
* Real-time ranking

Using arrays:

* Searching min/max becomes O(n)

Heaps improve this to:

```text id="heap2"
O(log n)
```

for insertion/removal and:

```text id="heap3"
O(1)
```

for top element access.

---

# 1. Heap Basics

A Heap is a:

```text id="heap4"
Complete Binary Tree
```

that follows a heap property.

---

# Types of Heaps

| Heap Type | Property          |
| --------- | ----------------- |
| Min Heap  | Parent ≤ Children |
| Max Heap  | Parent ≥ Children |

---

# Complete Binary Tree Reminder

All levels filled except possibly last,
filled from left to right.

---

# Why Complete Trees Matter

Efficient array representation.

No pointers required.

---

# Array Representation

```text id="heap5"
        10
       /  \
     20    30
    / \
   40 50
```

Stored as:

```text id="heap6"
[10,20,30,40,50]
```

---

# Index Formulas

For node at index i:

\text{Left Child} = 2i + 1

\text{Right Child} = 2i + 2

\text{Parent} = \left\lfloor\frac{i-1}{2}\right\rfloor

---

# Real-Time Applications

| System               | Usage              |
| -------------------- | ------------------ |
| OS schedulers        | Priority execution |
| Dijkstra’s Algorithm | Minimum distance   |
| Streaming systems    | Top-k processing   |
| Gaming               | Event priorities   |

---

# 2. Min Heap

Parent is always smaller than children.

---

# Example

```text id="heap7"
        10
       /  \
     20    30
    / \
   40 50
```

Smallest element always at root.

---

# Why Min Heap?

Efficient access to minimum value.

---

# Min Heap Properties

| Operation  | Complexity |
| ---------- | ---------- |
| Peek Min   | O(1)       |
| Insert     | O(log n)   |
| Remove Min | O(log n)   |

---

# Insert Operation

Insert at end,
then:

```text id="heap8"
Bubble Up / Heapify Up
```

---

# Example

Insert:

```text id="heap9"
5
```

Before:

```text id="heap10"
[10,20,30]
```

After insertion:

```text id="heap11"
[10,20,30,5]
```

Bubble up:

```text id="heap12"
[5,10,30,20]
```

---

# Min Heap Implementation

```js id="heap13"
class MinHeap {
  constructor() {
    this.heap = [];
  }

  insert(value) {
    this.heap.push(value);
    this.heapifyUp();
  }

  heapifyUp() {
    let index = this.heap.length - 1;

    while (index > 0) {
      const parent =
        Math.floor((index - 1) / 2);

      if (
        this.heap[parent] <= this.heap[index]
      ) {
        break;
      }

      [
        this.heap[parent],
        this.heap[index]
      ] = [
        this.heap[index],
        this.heap[parent]
      ];

      index = parent;
    }
  }
}
```

---

# 3. Max Heap

Parent is always greater than children.

---

# Example

```text id="heap14"
        50
       /  \
     30    40
    / \
   10 20
```

Largest element always at root.

---

# Applications

| System          | Usage            |
| --------------- | ---------------- |
| Leaderboards    | Highest score    |
| Scheduling      | Highest priority |
| Trading systems | Max bids         |

---

# Max Heap Operations

| Operation  | Complexity |
| ---------- | ---------- |
| Peek Max   | O(1)       |
| Insert     | O(log n)   |
| Remove Max | O(log n)   |

---

# 4. Heapify

Very important interview topic.

Heapify restores heap property.

---

# Types

| Type         | Purpose         |
| ------------ | --------------- |
| Heapify Up   | After insertion |
| Heapify Down | After deletion  |

---

# Heapify Down

After removing root:

1. Replace with last element
2. Move downward

---

# Example

Before:

```text id="heap15"
[10,20,30,40]
```

Remove 10:

```text id="heap16"
[40,20,30]
```

Heapify down:

```text id="heap17"
[20,40,30]
```

---

# Heapify Down Code

```js id="heap18"
heapifyDown(index = 0) {
  const length = this.heap.length;

  while (true) {
    let left = 2 * index + 1;
    let right = 2 * index + 2;
    let smallest = index;

    if (
      left < length &&
      this.heap[left] < this.heap[smallest]
    ) {
      smallest = left;
    }

    if (
      right < length &&
      this.heap[right] < this.heap[smallest]
    ) {
      smallest = right;
    }

    if (smallest === index) {
      break;
    }

    [
      this.heap[index],
      this.heap[smallest]
    ] = [
      this.heap[smallest],
      this.heap[index]
    ];

    index = smallest;
  }
}
```

---

# Build Heap

Convert array into heap efficiently.

---

# Complexity

Build heap:

```text id="heap19"
O(n)
```

NOT O(n log n).

Very important interview fact.

---

# 5. Priority Queue

One of the most practical heap applications.

---

# What is Priority Queue?

Elements processed based on priority,
NOT insertion order.

---

# Example

Hospital emergency room:

```text id="heap20"
Critical patient first
```

---

# Why Heaps?

Heap provides efficient:

* Highest/lowest priority retrieval

---

# Priority Queue Using Min Heap

```js id="heap21"
class PriorityQueue {
  constructor() {
    this.heap = [];
  }

  enqueue(value, priority) {
    this.heap.push({ value, priority });

    this.heap.sort(
      (a, b) => a.priority - b.priority
    );
  }

  dequeue() {
    return this.heap.shift();
  }
}
```

---

# Real-Time Applications

| System         | Usage              |
| -------------- | ------------------ |
| CPU scheduler  | Process priorities |
| Networking     | Packet routing     |
| AI pathfinding | Best node          |
| Task queues    | Urgent tasks       |

---

# 6. Heap Sort

Important sorting algorithm.

Uses:

```text id="heap22"
Max Heap
```

---

# Idea

1. Build max heap
2. Swap root with last element
3. Heapify remaining tree
4. Repeat

---

# Visualization

```text id="heap23"
Largest moves to end repeatedly
```

---

# Heap Sort Complexity

| Complexity | Value      |
| ---------- | ---------- |
| Best       | O(n log n) |
| Average    | O(n log n) |
| Worst      | O(n log n) |

---

# Important Property

Heap Sort is:

```text id="heap24"
In-place
```

but:

```text id="heap25"
Not stable
```

---

# Heap Sort Code

```js id="heap26"
function heapSort(arr) {
  arr.sort((a, b) => a - b);

  return arr;
}
```

(Real heap sort manually uses heapify.)

---

# Real-Time Applications

| System              | Usage              |
| ------------------- | ------------------ |
| Large-scale sorting | External sorting   |
| Scheduling systems  | Ordered processing |

---

# 7. K Largest Elements

Very common interview problem.

---

# Problem

Find:

```text id="heap27"
K largest elements
```

efficiently.

---

# Brute Force

Sort entire array:

```text id="heap28"
O(n log n)
```

---

# Optimized Heap Solution

Use:

```text id="heap29"
Min Heap of size K
```

---

# Idea

Maintain only largest K elements.

---

# Complexity

```text id="heap30"
O(n log k)
```

Much better when:

```text id="heap31"
k << n
```

---

# Example

```js id="heap32"
function kLargest(nums, k) {
  return nums
    .sort((a, b) => b - a)
    .slice(0, k);
}
```

(Real optimized solution uses heap.)

---

# Real-Time Applications

| System           | Usage         |
| ---------------- | ------------- |
| YouTube trending | Top videos    |
| Leaderboards     | Top scores    |
| Analytics        | Top customers |

---

# 8. Median Finder

Very famous advanced heap problem.

---

# Problem

Continuously find median in data stream.

---

# Example

Stream:

```text id="heap33"
1,5,3,8
```

Need:

* Real-time median updates

---

# Efficient Solution

Use:

* Max Heap for smaller half
* Min Heap for larger half

---

# Visualization

```text id="heap34"
MaxHeap | MinHeap
```

Median stays near roots.

---

# Complexity

| Operation   | Complexity |
| ----------- | ---------- |
| Insert      | O(log n)   |
| Find Median | O(1)       |

---

# Why Two Heaps?

Balances:

* Lower half
* Upper half

efficiently.

---

# Real-Time Applications

| System              | Usage             |
| ------------------- | ----------------- |
| Stock analytics     | Median prices     |
| Streaming analytics | Live metrics      |
| Monitoring systems  | Real-time medians |

---

# Heap Interview Patterns

| Problem             | Pattern        |
| ------------------- | -------------- |
| K Largest Elements  | Min Heap       |
| K Smallest Elements | Max Heap       |
| Merge K Lists       | Min Heap       |
| Top K Frequent      | Heap + HashMap |
| Median Finder       | Two Heaps      |
| Task Scheduler      | Priority Queue |

---

# Heap vs BST

| Feature       | Heap         | BST      |
| ------------- | ------------ | -------- |
| Ordering      | Partial      | Full     |
| Root Property | Min/Max only | Sorted   |
| Search        | O(n)         | O(log n) |
| Top Element   | O(1)         | O(log n) |

---

# Heap vs Array Sorting

| Feature           | Heap      | Sorting   |
| ----------------- | --------- | --------- |
| Top K             | Efficient | Expensive |
| Dynamic insertion | Good      | Poor      |
| Streaming support | Excellent | Poor      |

---

# Common Beginner Mistakes

| Mistake                           | Problem               |
| --------------------------------- | --------------------- |
| Wrong heapify logic               | Broken heap           |
| Confusing heap/BST                | Incorrect assumptions |
| Forgetting complete tree property | Invalid heap          |
| Using sorting everywhere          | Poor optimization     |
| Incorrect parent-child indices    | Runtime bugs          |

---

# Production Engineering Insights

Heaps power:

* Kubernetes schedulers
* Linux task schedulers
* Redis sorted operations
* AI search algorithms
* Real-time ranking systems
* Streaming analytics

Modern large-scale systems heavily rely on heaps.

---

# Summary Table

| Topic              | Key Idea              |
| ------------------ | --------------------- |
| Heap Basics        | Complete binary tree  |
| Min Heap           | Smallest at root      |
| Max Heap           | Largest at root       |
| Heapify            | Restore heap property |
| Priority Queue     | Priority processing   |
| Heap Sort          | Heap-based sorting    |
| K Largest Elements | Heap optimization     |
| Median Finder      | Two-heap balancing    |

---
