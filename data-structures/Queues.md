# Queues in Data Structures

Queues are one of the most important linear data structures.

A Queue follows the principle:

```text id="q1"
FIFO → First In First Out
```

The first element inserted is the first one removed.

---

# Real-Life Analogy

Think about:

* Ticket counter line
* Printer queue
* Food delivery orders
* Call center waiting system

```text id="q2"
Front ← [10][20][30] ← Rear
```

* Insert happens at Rear
* Removal happens at Front

---

# Why Queues Matter

Queues are everywhere in real systems:

* Operating systems
* CPU scheduling
* BFS traversal
* Networking
* Databases
* Message brokers
* Streaming systems
* Multiplayer servers

---

# 1. Basic Queues

---

# Core Operations

| Operation      | Description          |
| -------------- | -------------------- |
| enqueue()      | Insert element       |
| dequeue()      | Remove front element |
| front()/peek() | View front element   |
| isEmpty()      | Check empty          |
| size()         | Number of elements   |

---

# Visualization

```text id="q3"
Enqueue 10

Front → [10] ← Rear

Enqueue 20

Front → [10][20] ← Rear

Dequeue

Front → [20] ← Rear
```

---

# Time Complexity

| Operation | Complexity |
| --------- | ---------- |
| Enqueue   | O(1)       |
| Dequeue   | O(1)       |
| Peek      | O(1)       |

---

# JavaScript Queue Example

```js id="q4"
const queue = [];

queue.push(10);
queue.push(20);

console.log(queue.shift());
```

---

# Problem with shift()

JavaScript arrays shift elements internally.

So dequeue becomes:

```text id="q5"
O(n)
```

Efficient implementations avoid this.

---

# Real-Time Applications

| System          | Usage             |
| --------------- | ----------------- |
| Printer systems | Print jobs        |
| Food delivery   | Order processing  |
| Messaging apps  | Message buffering |
| APIs            | Request handling  |

---

# 2. Queue using Arrays

---

# Implementation

```js id="q6"
class Queue {
  constructor() {
    this.items = [];
  }

  enqueue(element) {
    this.items.push(element);
  }

  dequeue() {
    if (this.isEmpty()) {
      return null;
    }

    return this.items.shift();
  }

  peek() {
    return this.items[0];
  }

  isEmpty() {
    return this.items.length === 0;
  }
}
```

---

# Advantages

* Simple
* Easy implementation
* Cache friendly

---

# Disadvantages

* dequeue() expensive in many languages
* Shifting overhead

---

# Optimized Array Queue

Use:

* front index
* rear index

Avoid shifting.

---

# Visualization

```text id="q7"
Index:
0 1 2 3

Front = 1
Rear = 3
```

---

# Real-Time Example

## API Request Queue

Servers queue incoming requests before processing.

---

# 3. Queue using Linked List

More efficient for dynamic operations.

---

# Why Linked List?

No shifting required.

---

# Node Structure

```js id="q8"
class Node {
  constructor(data) {
    this.data = data;
    this.next = null;
  }
}
```

---

# Queue Implementation

```js id="q9"
class Queue {
  constructor() {
    this.front = null;
    this.rear = null;
  }

  enqueue(data) {
    const newNode = new Node(data);

    if (!this.rear) {
      this.front = this.rear = newNode;
      return;
    }

    this.rear.next = newNode;
    this.rear = newNode;
  }

  dequeue() {
    if (!this.front) {
      return null;
    }

    const removed = this.front;
    this.front = this.front.next;

    if (!this.front) {
      this.rear = null;
    }

    return removed.data;
  }
}
```

---

# Complexity

| Operation | Complexity |
| --------- | ---------- |
| Enqueue   | O(1)       |
| Dequeue   | O(1)       |

---

# Array Queue vs Linked List Queue

| Feature        | Array      | Linked List |
| -------------- | ---------- | ----------- |
| Memory         | Contiguous | Dynamic     |
| Resize         | Needed     | Not needed  |
| Cache Locality | Better     | Worse       |
| Flexibility    | Lower      | Higher      |

---

# 4. Advanced Queues

Advanced queue structures solve specialized problems.

Includes:

* Circular Queue
* Deque
* Priority Queue
* Monotonic Queue

---

# 5. Circular Queue

Last position connects back to first.

---

# Why Circular Queue?

Normal queue wastes space after dequeues.

---

# Problem with Normal Queue

```text id="q10"
[ ][ ][30][40]

Front moved ahead,
space wasted.
```

---

# Circular Queue Solution

Reuse empty positions.

---

# Visualization

```text id="q11"
0 → 1 → 2 → 3
↑             ↓
← ← ← ← ← ← ←
```

---

# Formula

```text id="q12"
(nextIndex) % size
```

---

# Circular Queue Implementation

```js id="q13"
class CircularQueue {
  constructor(size) {
    this.queue = new Array(size);
    this.front = -1;
    this.rear = -1;
    this.size = size;
  }
}
```

---

# Real-Time Applications

| System            | Usage            |
| ----------------- | ---------------- |
| CPU scheduling    | Round Robin      |
| Streaming systems | Buffers          |
| Multiplayer games | Turn rotation    |
| Audio processing  | Circular buffers |

---

# 6. Deque (Double Ended Queue)

Supports insertion/deletion from both ends.

---

# Visualization

```text id="q14"
Front ← [10][20][30] → Rear
```

Operations:

* insertFront()
* insertRear()
* deleteFront()
* deleteRear()

---

# Complexity

| Operation               | Complexity |
| ----------------------- | ---------- |
| Insert/Delete both ends | O(1)       |

---

# Real-Time Applications

| System                  | Usage                 |
| ----------------------- | --------------------- |
| Browser history         | Front/back navigation |
| Undo systems            | Bidirectional actions |
| Sliding window problems | Optimization          |

---

# JavaScript Example

```js id="q15"
const deque = [];

deque.unshift(10);
deque.push(20);

deque.shift();
deque.pop();
```

---

# Types of Deque

| Type              | Description     |
| ----------------- | --------------- |
| Input Restricted  | Insert one side |
| Output Restricted | Delete one side |

---

# 7. Priority Queue

Elements processed based on priority.

NOT FIFO.

---

# Example

Hospital emergency room:

```text id="q16"
Critical patient first.
```

---

# Visualization

```text id="q17"
[Priority 1]
[Priority 2]
[Priority 5]
```

Smaller/higher priority processed first.

---

# Internal Implementation

Usually uses:

```text id="q18"
Heap
```

---

# Complexity

| Operation               | Complexity |
| ----------------------- | ---------- |
| Insert                  | O(log n)   |
| Remove Highest Priority | O(log n)   |

---

# JavaScript Example

```js id="q19"
class PriorityQueue {
  constructor() {
    this.items = [];
  }

  enqueue(element, priority) {
    this.items.push({ element, priority });

    this.items.sort((a, b) => a.priority - b.priority);
  }

  dequeue() {
    return this.items.shift();
  }
}
```

---

# Real-Time Applications

| System          | Usage               |
| --------------- | ------------------- |
| OS scheduling   | Process priority    |
| Network routing | Packet priority     |
| AI pathfinding  | Best node selection |
| Task schedulers | Critical jobs       |

---

# 8. Monotonic Queue

Advanced optimization structure.

Maintains:

* Increasing order
  or
* Decreasing order

---

# Why Monotonic Queue?

Efficiently solves:

* Sliding window maximum/minimum

---

# Example

```text id="q20"
[1,3,-1,-3,5]
```

Need maximum in each window.

---

# Complexity

```text id="q21"
O(n)
```

---

# Real-Time Applications

| System              | Usage              |
| ------------------- | ------------------ |
| Stock analysis      | Max price windows  |
| CPU monitoring      | Peak load tracking |
| Streaming analytics | Window statistics  |

---

# 9. BFS Traversal

Breadth First Search uses Queue.

One of the most important graph/tree algorithms.

---

# BFS Idea

Explore level by level.

---

# Visualization

```text id="q22"
      A
    /   \
   B     C
  / \
 D   E
```

Traversal:

```text id="q23"
A B C D E
```

---

# BFS Code

```js id="q24"
function bfs(graph, start) {
  const queue = [start];
  const visited = new Set();

  visited.add(start);

  while (queue.length) {
    const node = queue.shift();

    console.log(node);

    for (const neighbor of graph[node]) {
      if (!visited.has(neighbor)) {
        visited.add(neighbor);
        queue.push(neighbor);
      }
    }
  }
}
```

---

# Complexity

| Complexity | Value    |
| ---------- | -------- |
| Time       | O(V + E) |

---

# Real-Time Applications

| System            | Usage              |
| ----------------- | ------------------ |
| Google Maps       | Shortest routes    |
| Social networks   | Friend suggestions |
| Web crawlers      | Site traversal     |
| Multiplayer games | Path exploration   |

---

# 10. Task Scheduling

Queues are heavily used in scheduling systems.

---

# Examples

| System        | Queue Usage       |
| ------------- | ----------------- |
| CPU scheduler | Process execution |
| Kubernetes    | Pod scheduling    |
| RabbitMQ      | Message queues    |
| Celery        | Background jobs   |

---

# Producer-Consumer Model

Very important system design pattern.

---

# Visualization

```text id="q25"
Producer → Queue → Consumer
```

---

# Example

```text id="q26"
User uploads image
↓
Queue stores task
↓
Worker processes image
```

---

# Why Queues Matter Here

Benefits:

* Decoupling
* Scalability
* Retry mechanisms
* Load balancing

---

# 11. Sliding Window Maximum

Very famous monotonic queue problem.

---

# Problem

```text id="q27"
Array = [1,3,-1,-3,5,3,6,7]
Window size = 3
```

Output:

```text id="q28"
[3,3,5,5,6,7]
```

---

# Brute Force

```text id="q29"
O(n × k)
```

---

# Optimized Monotonic Queue

```text id="q30"
O(n)
```

---

# Key Idea

Maintain decreasing queue.

Front always stores maximum.

---

# Simplified Code

```js id="q31"
function maxSlidingWindow(nums, k) {
  const deque = [];
  const result = [];

  for (let i = 0; i < nums.length; i++) {

    while (
      deque.length &&
      deque[0] <= i - k
    ) {
      deque.shift();
    }

    while (
      deque.length &&
      nums[deque[deque.length - 1]] < nums[i]
    ) {
      deque.pop();
    }

    deque.push(i);

    if (i >= k - 1) {
      result.push(nums[deque[0]]);
    }
  }

  return result;
}
```

---

# Real-Time Applications

| System              | Usage               |
| ------------------- | ------------------- |
| Financial analytics | Moving maximum      |
| Weather systems     | Peak temperatures   |
| AI streaming        | Window computations |

---

# Queue in System Design

Queues are foundational in distributed systems.

---

# Message Queues

Examples:

| Technology   | Usage            |
| ------------ | ---------------- |
| RabbitMQ     | Messaging        |
| Apache Kafka | Event streaming  |
| Amazon SQS   | Cloud queues     |
| Redis        | Queue structures |

---

# Why Distributed Systems Use Queues

Queues help with:

* Scalability
* Fault tolerance
* Async processing
* Load balancing
* Retry handling

---

# Queue Patterns in Interviews

| Problem                | Pattern          |
| ---------------------- | ---------------- |
| BFS Traversal          | Basic queue      |
| Rotten Oranges         | Multi-source BFS |
| Sliding Window Maximum | Monotonic queue  |
| Task Scheduler         | Priority queue   |
| Design Circular Queue  | Circular buffer  |
| Snake Game             | Deque            |

---

# Common Beginner Mistakes

| Mistake                        | Problem             |
| ------------------------------ | ------------------- |
| Using array shift() blindly    | O(n) slowdown       |
| Forgetting circular wraparound | Queue corruption    |
| Wrong dequeue logic            | Empty queue bugs    |
| Ignoring monotonic property    | Missed optimization |
| Infinite BFS loops             | Missing visited set |

---

# Production Engineering Insights

Queues power:

* YouTube video processing
* Uber ride matching
* Instagram notifications
* Payment systems
* Cloud infrastructure
* Real-time analytics

Modern distributed systems are impossible without queues.

---

# Stack vs Queue

| Feature   | Stack          | Queue          |
| --------- | -------------- | -------------- |
| Principle | LIFO           | FIFO           |
| Removal   | Last inserted  | First inserted |
| Usage     | Undo/Recursion | Scheduling/BFS |

---

# Queue vs Deque

| Feature     | Queue      | Deque     |
| ----------- | ---------- | --------- |
| Insert      | Rear only  | Both ends |
| Delete      | Front only | Both ends |
| Flexibility | Lower      | Higher    |

---

# Summary Table

| Topic              | Key Idea                  |
| ------------------ | ------------------------- |
| Basic Queue        | FIFO                      |
| Array Queue        | Simple implementation     |
| Linked List Queue  | Dynamic implementation    |
| Circular Queue     | Efficient reuse           |
| Deque              | Double-ended operations   |
| Priority Queue     | Priority-based processing |
| Monotonic Queue    | Window optimization       |
| BFS                | Level-order traversal     |
| Task Scheduling    | Async systems             |
| Sliding Window Max | Monotonic optimization    |

---
