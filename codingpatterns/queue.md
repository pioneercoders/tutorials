# Queue

Queue is a linear data structure that follows First-In-First-Out (FIFO) principle. Elements are added at the rear and removed from the front.

## Introduction

Queue is a linear data structure that follows the First-In-First-Out (FIFO) principle, meaning the first element added is the first one to be removed. Think of it like a line of people at a ticket counter: the first person in line is the first to be served. This makes queues ideal for processing elements in order of arrival, implementing breadth-first traversal, task scheduling, and producer-consumer patterns.

**Why Queue Exists:**
- FIFO behavior is needed for many problems
- Natural for processing in order of arrival
- Essential for breadth-first traversal (BFS)
- Used in task scheduling and buffering
- Foundation for producer-consumer patterns

**Where It Is Used:**
- Task scheduling in operating systems
- Message queues in distributed systems
- Request throttling and rate limiting
- Buffer management in I/O operations
- Printer job queues
- BFS graph traversal
- Producer-consumer patterns
- Level order tree traversal

## Core Concept Explanation

Queue operates on the FIFO principle: the first element enqueued is the first one dequeued. This is implemented using two primary operations: enqueue (add to rear) and dequeue (remove from front). Additional operations include peek (view front without removing), isEmpty (check if empty), and size (number of elements).

**Step-by-Step Breakdown:**
1. Initialize empty queue
2. Enqueue elements at rear (they accumulate)
3. Dequeue elements from front (removed in order of arrival)
4. Peek to view front element without removing
5. Check if empty before dequeuing
6. All operations should be O(1) time complexity

**Intuition Behind the Concept:**
Think of a line of people waiting at a bank. The first person who joined the line is the first to be served. If people A, B, C join the line in that order, they will be served in the same order: A, B, C. This is exactly how a queue data structure works.

**Visual Thinking:**
```
Queue Operations:

Initial: []
Enqueue(5): [5]
Enqueue(3): [5, 3]
Enqueue(7): [5, 3, 7]
Peek():      5 (front element)
Dequeue():   5 → [3, 7]
Dequeue():   3 → [7]
Enqueue(2): [7, 2]
Dequeue():   7 → [2]
Dequeue():   2 → []
isEmpty():  true

Visual Representation:
Front → [5, 3, 7] ← Rear
          ↑         ↑
       Dequeue   Enqueue
```

## Internal Working / Logic

Queue operates through a simple mechanism where elements are added at the rear and removed from the front. The underlying implementation can use an array, linked list, or circular buffer, but the operations remain the same.

**Operation 1: Enqueue**
- Add element to the rear of the queue
- Increment size
- Time: O(1) amortized (array may need resizing)

**Operation 2: Dequeue**
- Remove element from the front of the queue
- Decrement size
- Return removed element
- Time: O(1) with deque, O(n) with array shift

**Operation 3: Peek**
- Return element at the front of the queue
- Don't remove it
- Time: O(1)

**Operation 4: isEmpty**
- Check if size is 0
- Return boolean
- Time: O(1)

**Flow Explanation (Enqueue):**
1. Check if queue needs resizing (array implementation)
2. Add element to rear of queue
3. Increment size
4. Return

**Flow Explanation (Dequeue):**
1. Check if queue is empty
2. If empty, return null or throw error
3. Remove element from front of queue
4. Decrement size
5. Return removed element

**Decision Making Logic:**
The key decision is the underlying implementation:
- Array: Simple, O(n) dequeue (shift), may need resizing
- Linked list: O(1) enqueue/dequeue, more memory overhead
- Circular buffer: O(1) operations, fixed size
- Deque: O(1) operations at both ends

## Algorithm / Approach

**Enqueue Algorithm**

```
1. Check if queue needs resizing (array implementation)
2. Add element to rear of queue
3. Increment size
4. Return
```

**Dequeue Algorithm**

```
1. Check if queue is empty
2. If empty: return null or throw error
3. Remove element from front of queue
4. Decrement size
5. Return removed element
```

**Peek Algorithm**

```
1. Check if queue is empty
2. If empty: return null or throw error
3. Return element at front of queue
4. Don't remove it
```

**isEmpty Algorithm**

```
1. Check if size is 0
2. Return true if empty, false otherwise
```

## Implementations

### 1. Basic Queue Implementation

```javascript
class Queue {
  constructor() {
    this.items = [];
  }
  
  enqueue(item) {
    this.items.push(item);
  }
  
  dequeue() {
    if (!this.isEmpty()) {
      return this.items.shift();
    }
    return null;
  }
  
  peek() {
    if (!this.isEmpty()) {
      return this.items[0];
    }
    return null;
  }
  
  isEmpty() {
    return this.items.length === 0;
  }
  
  size() {
    return this.items.length;
  }
  
  clear() {
    this.items = [];
  }
}
```

**Advantages:**
- Simple to implement
- Uses array for storage
- O(1) enqueue, O(n) dequeue

**Disadvantages:**
- Dequeue is O(n) due to shift
- May need array resizing

### 2. Circular Buffer Queue

```javascript
class CircularQueue {
  constructor(capacity) {
    this.capacity = capacity;
    this.queue = new Array(capacity);
    this.front = 0;
    this.rear = -1;
    this.size = 0;
  }
  
  enqueue(item) {
    if (this.isFull()) {
      throw new Error('Queue overflow');
    }
    this.rear = (this.rear + 1) % this.capacity;
    this.queue[this.rear] = item;
    this.size++;
  }
  
  dequeue() {
    if (this.isEmpty()) {
      throw new Error('Queue underflow');
    }
    const item = this.queue[this.front];
    this.front = (this.front + 1) % this.capacity;
    this.size--;
    return item;
  }
  
  peek() {
    if (this.isEmpty()) {
      throw new Error('Queue is empty');
    }
    return this.queue[this.front];
  }
  
  isEmpty() {
    return this.size === 0;
  }
  
  isFull() {
    return this.size === this.capacity;
  }
}
```

**Advantages:**
- O(1) enqueue and dequeue
- Fixed size, no resizing
- Efficient memory usage

### 3. Level Order Traversal (BFS)

```javascript
function levelOrder(root) {
  if (!root) return [];
  
  const result = [];
  const queue = [root];
  
  while (queue.length > 0) {
    const level = [];
    const levelSize = queue.length;
    
    for (let i = 0; i < levelSize; i++) {
      const node = queue.shift();
      level.push(node.val);
      if (node.left) queue.push(node.left);
      if (node.right) queue.push(node.right);
    }
    
    result.push(level);
  }
  
  return result;
}
```

**Advantages:**
- O(n) time, O(n) space
- Level-by-level traversal
- Classic BFS application

### 4. Implement Queue using Stacks

```javascript
class MyQueue {
  constructor() {
    this.inStack = [];
    this.outStack = [];
  }
  
  push(x) {
    this.inStack.push(x);
  }
  
  pop() {
    this._transfer();
    return this.outStack.pop();
  }
  
  peek() {
    this._transfer();
    return this.outStack[this.outStack.length - 1];
  }
  
  empty() {
    return this.inStack.length === 0 && this.outStack.length === 0;
  }
  
  _transfer() {
    if (this.outStack.length === 0) {
      while (this.inStack.length > 0) {
        this.outStack.push(this.inStack.pop());
      }
    }
  }
}
```

**Advantages:**
- Amortized O(1) time
- Demonstrates stack usage
- Two-stack implementation

### 5. Sliding Window Maximum

```javascript
function maxSlidingWindow(nums, k) {
  const result = [];
  const deque = [];
  
  for (let i = 0; i < nums.length; i++) {
    // Remove elements outside window
    while (deque.length > 0 && deque[0] <= i - k) {
      deque.shift();
    }
    
    // Remove smaller elements
    while (deque.length > 0 && nums[deque[deque.length - 1]] < nums[i]) {
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

**Advantages:**
- O(n) time, O(k) space
- Monotonic deque pattern
- Efficient sliding window

### 6. Binary Tree Level Order

```javascript
function levelOrderTraversal(root) {
  if (!root) return [];
  
  const result = [];
  const queue = [root];
  
  while (queue.length > 0) {
    const node = queue.shift();
    result.push(node.val);
    
    if (node.left) queue.push(node.left);
    if (node.right) queue.push(node.right);
  }
  
  return result;
}
```

## Dry Run

**Example: Level Order Traversal**

**Input:**
```
    1
   / \
  2   3
 / \
4   5
```

**Step-by-Step Execution:**

```
Initial State:
queue = [1]
result = []

Iteration 1:
node = queue.shift() = 1
result.push(1) → [1]
queue.push(2), queue.push(3)
queue = [2, 3]

Iteration 2:
node = queue.shift() = 2
result.push(2) → [1, 2]
queue.push(4), queue.push(5)
queue = [3, 4, 5]

Iteration 3:
node = queue.shift() = 3
result.push(3) → [1, 2, 3]
queue = [4, 5]

Iteration 4:
node = queue.shift() = 4
result.push(4) → [1, 2, 3, 4]
queue = [5]

Iteration 5:
node = queue.shift() = 5
result.push(5) → [1, 2, 3, 4, 5]
queue = []

Final: result = [1, 2, 3, 4, 5]
```

**Variable Changes Table:**

| Iteration | node | result (after) | queue (after) |
|-----------|------|---------------|--------------|
| 1 | 1 | [1] | [2, 3] |
| 2 | 2 | [1, 2] | [3, 4, 5] |
| 3 | 3 | [1, 2, 3] | [4, 5] |
| 4 | 4 | [1, 2, 3, 4] | [5] |
| 5 | 5 | [1, 2, 3, 4, 5] | [] |

## Edge Cases

### 1. Empty Queue Operations
```javascript
queue = []
queue.dequeue() → null
queue.peek() → null
queue.isEmpty() → true
```

### 2. Single Element
```javascript
queue = [5]
queue.dequeue() → 5
queue = []
queue.isEmpty() → true
```

### 3. Queue Overflow
```javascript
Circular queue with capacity 3
Enqueue 4 elements → overflow
Must check isFull() before enqueue
```

### 4. Null Root
```javascript
levelOrder(null) → []
Handle null input gracefully
```

### 5. Invalid Window Size
```javascript
maxSlidingWindow(nums, 0) → []
maxSlidingWindow(nums, nums.length + 1) → []
Validate window size
```

### 6. Empty Array
```javascript
maxSlidingWindow([], 3) → []
Handle empty input
```

**Why Edge Cases Matter:**
- Empty operations prevent errors
- Single element tests boundaries
- Overflow tests resilience
- Null input needs validation
- Invalid parameters need checking

## Variations / Extensions

### 1. Priority Queue

```javascript
class PriorityQueue {
  constructor() {
    this.items = [];
  }
  
  enqueue(item, priority) {
    const element = { item, priority };
    let added = false;
    
    for (let i = 0; i < this.items.length; i++) {
      if (element.priority < this.items[i].priority) {
        this.items.splice(i, 0, element);
        added = true;
        break;
      }
    }
    
    if (!added) {
      this.items.push(element);
    }
  }
  
  dequeue() {
    return this.items.shift();
  }
}
```

### 2. Deque (Double-Ended Queue)

```javascript
class Deque {
  constructor() {
    this.items = [];
  }
  
  addFront(item) {
    this.items.unshift(item);
  }
  
  addRear(item) {
    this.items.push(item);
  }
  
  removeFront() {
    return this.items.shift();
  }
  
  removeRear() {
    return this.items.pop();
  }
}
```

### 3. Circular Queue with Dynamic Resizing

```javascript
class DynamicCircularQueue {
  constructor(initialCapacity = 10) {
    this.capacity = initialCapacity;
    this.queue = new Array(this.capacity);
    this.front = 0;
    this.rear = -1;
    this.size = 0;
  }
  
  _resize() {
    const newCapacity = this.capacity * 2;
    const newQueue = new Array(newCapacity);
    
    for (let i = 0; i < this.size; i++) {
      newQueue[i] = this.queue[(this.front + i) % this.capacity];
    }
    
    this.queue = newQueue;
    this.capacity = newCapacity;
    this.front = 0;
    this.rear = this.size - 1;
  }
  
  enqueue(item) {
    if (this.isFull()) {
      this._resize();
    }
    this.rear = (this.rear + 1) % this.capacity;
    this.queue[this.rear] = item;
    this.size++;
  }
}
```

### 4. Linked List Queue

```javascript
class Node {
  constructor(value) {
    this.value = value;
    this.next = null;
  }
}

class LinkedListQueue {
  constructor() {
    this.front = null;
    this.rear = null;
    this.size = 0;
  }
  
  enqueue(value) {
    const newNode = new Node(value);
    if (this.rear) {
      this.rear.next = newNode;
    }
    this.rear = newNode;
    if (!this.front) {
      this.front = newNode;
    }
    this.size++;
  }
  
  dequeue() {
    if (!this.front) return null;
    const value = this.front.value;
    this.front = this.front.next;
    if (!this.front) {
      this.rear = null;
    }
    this.size--;
    return value;
  }
}
```

### 5. Blocking Queue

```javascript
class BlockingQueue {
  constructor(capacity) {
    this.capacity = capacity;
    this.queue = [];
  }
  
  async enqueue(item) {
    while (this.queue.length >= this.capacity) {
      await new Promise(resolve => setTimeout(resolve, 100));
    }
    this.queue.push(item);
  }
  
  async dequeue() {
    while (this.queue.length === 0) {
      await new Promise(resolve => setTimeout(resolve, 100));
    }
    return this.queue.shift();
  }
}
```

## Optimization Techniques

### 1. Use Deque

**Double-Ended Queue:**
```javascript
// O(1) operations at both ends
// Better than array shift
// Use for sliding window
```

### 2. Circular Buffer

**Fixed Size Optimization:**
```javascript
// No resizing overhead
// O(1) enqueue/dequeue
// Efficient memory usage
```

### 3. Trade-offs

**Array vs Linked List vs Circular Buffer:**

| Aspect | Array | Linked List | Circular Buffer |
|--------|-------|-------------|----------------|
| Enqueue | `O(1)` | `O(1)` | `O(1)` |
| Dequeue | `O(n)` | `O(1)` | `O(1)` |
| Memory | Contiguous | Scattered | Contiguous |
| Resizing | May need | No need | Fixed size |
| Cache | Better | Worse | Better |

**When to Use Circular Buffer:**
- Fixed size is acceptable
- Need O(1) operations
- Memory efficiency is important

## Complexity Analysis

### Time Complexity

**Enqueue: O(1) amortized**
- Add to end of array
- May need to resize (rare)
- Amortized constant time

**Dequeue: O(1) with deque/circular buffer**
- Remove from front
- O(n) with array shift
- O(1) with proper implementation

**Peek: O(1)**
- Access front element
- No removal
- Constant time

**isEmpty: O(1)**
- Check size
- Constant time

### Space Complexity

**Storage: O(n)**
- Store n elements
- Array or linked list
- Linear space

**Circular Buffer: O(capacity)**
- Fixed size
- No resizing
- Constant space

**Explanation:**
Queue operations should be O(1) time with proper implementation. Array shift makes dequeue O(n), so use deque or circular buffer for O(1) operations. Space is O(n) for dynamic queues, O(capacity) for fixed-size.

## Real-world Applications

### 1. Task Scheduling

**Operating Systems:**
- Process scheduling
- CPU task queue
- Example: OS scheduler

### 2. Message Queues

**Distributed Systems:**
- Asynchronous communication
- Decouple services
- Example: RabbitMQ, Kafka

### 3. Request Throttling

**Rate Limiting:**
- Limit request rate
- Token bucket algorithm
- Example: API rate limiting

### 4. Buffer Management

**I/O Operations:**
- Buffer data between processes
- Smooth data flow
- Example: Keyboard buffer

### 5. Printer Queues

**Print Spooling:**
- Queue print jobs
- Process in order
- Example: Print spooler

### 6. BFS Graph Traversal

**Graph Algorithms:**
- Shortest path
- Level-order traversal
- Example: Social network analysis

### 7. Producer-Consumer

**Concurrency:**
- Buffer between producers/consumers
- Synchronize access
- Example: Thread pools

### 8. Call Center

**Customer Service:**
- Queue incoming calls
- Assign to agents
- Example: Call routing systems

## Common Mistakes

### 1. Not Checking Empty Before Dequeue

**Mistake:**
```javascript
// Not checking if empty
queue.dequeue(); // May return undefined
```

**Correct:**
```javascript
// Check before dequeuing
if (!queue.isEmpty()) {
  queue.dequeue();
}
```

**Why It Matters:**
- Dequeuing empty queue causes errors
- Must check before operations
- Prevents undefined behavior

### 2. Using Array Shift for Large Queues

**Mistake:**
```javascript
// O(n) dequeue
dequeue() {
  return this.items.shift(); // Shifts all elements!
}
```

**Correct:**
```javascript
// Use deque or circular buffer
dequeue() {
  if (this.isEmpty()) return null;
  const item = this.items[this.front];
  this.front = (this.front + 1) % this.capacity;
  return item;
}
```

**Why It Matters:**
- Array shift is O(n)
- Degrades performance
- Use O(1) implementation

### 3. Not Handling Circular Buffer Wraparound

**Mistake:**
```javascript
// Not using modulo
this.rear++; // May exceed capacity
```

**Correct:**
```javascript
// Use modulo for wraparound
this.rear = (this.rear + 1) % this.capacity;
```

**Why It Matters:**
- Must wrap around circular buffer
- Otherwise index out of bounds
- Critical for correctness

### 4. Not Checking Full Before Enqueue

**Mistake:**
```javascript
// Not checking if full
enqueue(item) {
  this.queue.push(item); // May overflow
}
```

**Correct:**
```javascript
// Check capacity
enqueue(item) {
  if (this.isFull()) {
    throw new Error('Queue overflow');
  }
  this.queue.push(item);
}
```

**Why It Matters:**
- Overflow causes errors
- Must check capacity
- Prevents crashes

### 5. Using Queue When Stack Needed

**Mistake:**
```javascript
// Using queue for LIFO
queue.enqueue(1);
queue.enqueue(2);
queue.dequeue(); // Returns 1, not 2!
```

**Correct:**
```javascript
// Use stack for LIFO
stack.push(1);
stack.push(2);
stack.pop(); // Returns 2
```

**Why It Matters:**
- Queue is FIFO, stack is LIFO
- Wrong choice gives wrong order
- Must choose correct structure

### 6. Not Handling Null Root

**Mistake:**
```javascript
// Not checking null
levelOrder(null) // Error!
```

**Correct:**
```javascript
// Handle null input
if (!root) return [];
```

**Why It Matters:**
- Null input causes errors
- Must handle gracefully
- Prevents crashes

## Advanced Concepts

### 1. Monotonic Queue

**Concept:**
Maintain queue in monotonic order (increasing or decreasing).

**Features:**
- Efficient for sliding window
- O(n) time for many problems
- Used in sliding window maximum/minimum

### 2. Priority Queue

**Concept:**
Elements have priorities, dequeue based on priority.

**Features:**
- Not strictly FIFO
- Implemented with heap
- Used in Dijkstra's algorithm

### 3. Lock-Free Queue

**Concept:**
Concurrent queue without locks using atomic operations.

**Features:**
- Thread-safe without locks
- Better performance
- Complex implementation

### 4. Bounded Queue

**Concept:**
Queue with fixed capacity, blocks when full.

**Features:**
- Backpressure handling
- Producer-consumer pattern
- Used in concurrent systems

## Practice Thinking Guide

### How to Identify When to Use Queue

**Key Signals in Problem Statements:**

1. **"First-in-first-out"**
   - Need FIFO behavior
   - Example: "Process in order"

2. **"Level order/breadth-first"**
   - BFS traversal
   - Example: "Level order traversal"

3. **"Sliding window"**
   - Process windows
   - Example: "Sliding window maximum"

4. **"Task scheduling"**
   - Process tasks in order
   - Example: "Task scheduler"

5. **"Buffer"**
   - Buffer between processes
   - Example: "Producer-consumer"

6. **"Shortest path"**
   - BFS for unweighted graphs
   - Example: "Shortest path in unweighted graph"

**Pattern Recognition:**

**Pattern 1: BFS Traversal**
```
Problem: Level order traversal
Solution: Queue for BFS
```

**Pattern 2: Sliding Window**
```
Problem: Sliding window maximum
Solution: Monotonic deque
```

**Pattern 3: Task Scheduling**
```
Problem: Process tasks in order
Solution: Queue for scheduling
```

**Pattern 4: Producer-Consumer**
```
Problem: Buffer between processes
Solution: Queue for buffering
```

**Pattern 5: Shortest Path**
```
Problem: BFS shortest path
Solution: Queue for BFS
```

**Decision Flowchart:**

```
Need FIFO behavior?
├─ Yes → Need to process levels?
│        ├─ Yes → Use queue (BFS)
│        └─ No → Use queue (general)
├─ No → Need sliding window?
│        ├─ Yes → Use deque
│        └─ No → Consider other
└─ No → Not queue problem
```

**Example Problem Analysis:**

**Problem:** "Level order traversal of binary tree"

**Analysis:**
1. Need to process tree level by level
2. BFS naturally uses queue
3. Enqueue root, then children
4. Process in order of arrival
5. Solution: Queue for BFS

**Problem:** "Sliding window maximum"

**Analysis:**
1. Need to find max in each window
2. Maintain decreasing order in deque
3. Remove elements outside window
4. O(n) time, O(k) space
5. Solution: Monotonic deque

**Problem:** "Task scheduler with cooldown"

**Analysis:**
1. Need to schedule tasks with cooldown
2. Queue to track cooldown
3. Process tasks in order
4. O(n) time, O(n) space
5. Solution: Queue for scheduling

## Summary

Queue is a fundamental data structure that follows the FIFO principle. It's essential for processing elements in order of arrival, implementing BFS, task scheduling, and producer-consumer patterns. Understanding queue operations and implementations is crucial for solving many algorithmic problems.

**Key Takeaways:**
- FIFO principle (first-in-first-out)
- O(1) enqueue, O(1) dequeue with proper implementation
- O(n) space for storage
- Essential for BFS algorithms
- Used in task scheduling and buffering
- Circular buffer for fixed-size efficiency
- Deque for O(1) operations at both ends
- Check empty before dequeue

**Mastery Checklist:**
- ✅ Understand FIFO principle
- ✅ Implement basic queue operations
- ✅ Use circular buffer for efficiency
- ✅ Implement BFS with queue
- ✅ Use monotonic deque for sliding window
- ✅ Implement queue using stacks
- ✅ Choose appropriate implementation
- ✅ Handle edge cases

