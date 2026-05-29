# Heap / Priority Queue

Heap is a specialized tree-based data structure that satisfies the heap property. Priority Queue is an abstract data type implemented using heaps to efficiently access the highest/lowest priority element.

## Introduction

Heap is a complete binary tree data structure that satisfies the heap property: in a min-heap, every parent node is less than or equal to its children; in a max-heap, every parent node is greater than or equal to its children. This structure enables efficient access to the minimum or maximum element, making it ideal for implementing priority queues where elements are processed based on their priority.

**Why Heap Exists:**
- Arrays provide O(1) access but O(n) for min/max operations
- Sorted arrays provide O(1) min/max but O(n) insertion
- Heaps provide O(1) min/max access and O(log n) insertion/deletion
- Essential for priority-based processing
- Foundation for many algorithms (Dijkstra, Prim's, Huffman coding)

**Where It Is Used:**
- Priority queues (task scheduling, event processing)
- Finding top/bottom k elements
- Merging sorted streams
- Graph algorithms (shortest path, MST)
- Data compression (Huffman coding)
- Load balancing systems
- Search result ranking
- Real-time analytics

## Core Concept Explanation

Heap is a complete binary tree stored in an array, where the parent-child relationship is determined by index calculations. The heap property ensures that the root is always the minimum (min-heap) or maximum (max-heap) element.

**Step-by-Step Breakdown:**
1. Store elements in array representing complete binary tree
2. For index i: parent = floor((i-1)/2), left = 2i+1, right = 2i+2
3. Maintain heap property through bubble-up (insertion) and bubble-down (deletion)
4. Root always contains min/max element
5. O(log n) operations due to tree height

**Intuition Behind the Concept:**
Think of a tournament bracket where the winner (min or max) is always at the top. When a new player enters, they climb up the bracket by challenging opponents (bubble-up). When the winner leaves, the remaining players compete to determine the new winner (bubble-down). This ensures the best player is always accessible in O(1) time.

**Visual Thinking:**
```
Array Representation:
Index:  0   1   2   3   4   5   6
Value:  1   3   2   5   4   6   7

Tree Representation (Min-Heap):
         1
       /   \
      3     2
     / \   / \
    5   4 6   7

Heap Property: Parent <= Children
1 <= 3, 1 <= 2
3 <= 5, 3 <= 4
2 <= 6, 2 <= 7

Index Calculations:
- Parent of index 3: floor((3-1)/2) = 1
- Left child of index 1: 2*1+1 = 3
- Right child of index 1: 2*1+2 = 4
```

## Internal Working / Logic

Heap operates through two primary operations that maintain the heap property:

**Operation 1: Bubble-Up (Heapify-Up)**
- Used when inserting a new element
- Start at the inserted position
- Compare with parent, swap if heap property violated
- Continue until heap property satisfied or root reached
- Time: O(log n) - height of tree

**Operation 2: Bubble-Down (Heapify-Down)**
- Used when removing root element
- Replace root with last element
- Compare with children, swap with smaller/larger child
- Continue until heap property satisfied or leaf reached
- Time: O(log n) - height of tree

**Flow Explanation (Insertion):**
1. Add new element at end of array
2. Set current index to new element's position
3. While current index > 0:
   a. Calculate parent index
   b. If heap property satisfied, break
   c. Swap current element with parent
   d. Set current index to parent index
4. Heap property now satisfied

**Flow Explanation (Deletion):**
1. Remove root element (min/max)
2. Move last element to root position
3. Set current index to root (0)
4. While current index has children:
   a. Find smallest/largest child
   b. If heap property satisfied, break
   c. Swap current element with child
   d. Set current index to child index
5. Heap property now satisfied

**Decision Making Logic:**
The key decision is which child to swap with during bubble-down:
- For min-heap: swap with smaller child
- For max-heap: swap with larger child
- If both children equal, can swap with either
- If only one child exists, swap with that child

## Algorithm / Approach

**Insert Algorithm (Bubble-Up)**

```
1. Add element to end of heap array
2. Set index = heap.length - 1
3. While index > 0:
   a. parent = floor((index - 1) / 2)
   b. If heap[parent] <= heap[index] (min-heap): break
   c. Swap heap[parent] and heap[index]
   d. index = parent
4. Return
```

**Delete Algorithm (Bubble-Down)**

```
1. If heap empty: return null
2. If heap has one element: remove and return
3. Save root value
4. Move last element to root
5. Remove last element
6. index = 0
7. While true:
   a. left = 2*index + 1, right = 2*index + 2
   b. Find smallest/largest child
   c. If heap property satisfied: break
   d. Swap with child
   e. index = child index
8. Return saved root value
```

**Heapify Algorithm (Build from Array)**

```
1. Start from last non-leaf node (floor(n/2) - 1)
2. For each node from last to first:
   a. Apply bubble-down at this node
3. Complete heap formed in O(n) time
```

## Implementations

### 1. Min-Heap Implementation

```javascript
class MinHeap {
  constructor() {
    this.heap = [];
  }
  
  push(val) {
    this.heap.push(val);
    this._bubbleUp(this.heap.length - 1);
  }
  
  pop() {
    if (this.heap.length === 0) return null;
    if (this.heap.length === 1) return this.heap.pop();
    
    const min = this.heap[0];
    this.heap[0] = this.heap.pop();
    this._bubbleDown(0);
    return min;
  }
  
  peek() {
    return this.heap[0] || null;
  }
  
  size() {
    return this.heap.length;
  }
  
  isEmpty() {
    return this.heap.length === 0;
  }
  
  _bubbleUp(index) {
    while (index > 0) {
      const parent = Math.floor((index - 1) / 2);
      if (this.heap[parent] <= this.heap[index]) break;
      [this.heap[parent], this.heap[index]] = [this.heap[index], this.heap[parent]];
      index = parent;
    }
  }
  
  _bubbleDown(index) {
    while (true) {
      const left = 2 * index + 1;
      const right = 2 * index + 2;
      let smallest = index;
      
      if (left < this.heap.length && this.heap[left] < this.heap[smallest]) {
        smallest = left;
      }
      if (right < this.heap.length && this.heap[right] < this.heap[smallest]) {
        smallest = right;
      }
      
      if (smallest === index) break;
      [this.heap[index], this.heap[smallest]] = [this.heap[smallest], this.heap[index]];
      index = smallest;
    }
  }
}
```

**Advantages:**
- O(log n) insert and delete
- O(1) peek at min element
- Efficient for priority-based operations

### 2. Max-Heap Implementation

```javascript
class MaxHeap {
  constructor() {
    this.heap = [];
  }
  
  push(val) {
    this.heap.push(val);
    this._bubbleUp(this.heap.length - 1);
  }
  
  pop() {
    if (this.heap.length === 0) return null;
    if (this.heap.length === 1) return this.heap.pop();
    
    const max = this.heap[0];
    this.heap[0] = this.heap.pop();
    this._bubbleDown(0);
    return max;
  }
  
  peek() {
    return this.heap[0] || null;
  }
  
  _bubbleUp(index) {
    while (index > 0) {
      const parent = Math.floor((index - 1) / 2);
      if (this.heap[parent] >= this.heap[index]) break;
      [this.heap[parent], this.heap[index]] = [this.heap[index], this.heap[parent]];
      index = parent;
    }
  }
  
  _bubbleDown(index) {
    while (true) {
      const left = 2 * index + 1;
      const right = 2 * index + 2;
      let largest = index;
      
      if (left < this.heap.length && this.heap[left] > this.heap[largest]) {
        largest = left;
      }
      if (right < this.heap.length && this.heap[right] > this.heap[largest]) {
        largest = right;
      }
      
      if (largest === index) break;
      [this.heap[index], this.heap[largest]] = [this.heap[largest], this.heap[index]];
      index = largest;
    }
  }
}
```

### 3. Kth Largest Element

```javascript
function kthLargest(nums, k) {
  const minHeap = new MinHeap();
  
  for (const num of nums) {
    minHeap.push(num);
    if (minHeap.size() > k) {
      minHeap.pop();
    }
  }
  
  return minHeap.peek();
}
```

**State Definition:**
- Maintain min-heap of size k
- Heap contains k largest elements seen so far
- Root is kth largest element

### 4. Top K Frequent Elements

```javascript
function topKFrequent(nums, k) {
  const freq = new Map();
  for (const num of nums) {
    freq.set(num, (freq.get(num) || 0) + 1);
  }
  
  const minHeap = new MinHeap();
  
  for (const [num, count] of freq) {
    minHeap.push({ num, count });
    if (minHeap.size() > k) {
      minHeap.pop();
    }
  }
  
  // Custom comparator for min-heap
  minHeap._bubbleUp = function(index) {
    while (index > 0) {
      const parent = Math.floor((index - 1) / 2);
      if (this.heap[parent].count <= this.heap[index].count) break;
      [this.heap[parent], this.heap[index]] = [this.heap[index], this.heap[parent]];
      index = parent;
    }
  };
  
  return minHeap.heap.map(item => item.num);
}
```

### 5. Merge K Sorted Lists

```javascript
function mergeKLists(lists) {
  const minHeap = new MinHeap();
  
  // Custom comparator for linked list nodes
  minHeap._bubbleUp = function(index) {
    while (index > 0) {
      const parent = Math.floor((index - 1) / 2);
      if (this.heap[parent].val <= this.heap[index].val) break;
      [this.heap[parent], this.heap[index]] = [this.heap[index], this.heap[parent]];
      index = parent;
    }
  };
  
  minHeap._bubbleDown = function(index) {
    while (true) {
      const left = 2 * index + 1;
      const right = 2 * index + 2;
      let smallest = index;
      
      if (left < this.heap.length && this.heap[left].val < this.heap[smallest].val) {
        smallest = left;
      }
      if (right < this.heap.length && this.heap[right].val < this.heap[smallest].val) {
        smallest = right;
      }
      
      if (smallest === index) break;
      [this.heap[index], this.heap[smallest]] = [this.heap[smallest], this.heap[index]];
      index = smallest;
    }
  };
  
  // Push first node of each list
  for (const list of lists) {
    if (list) {
      minHeap.push(list);
    }
  }
  
  const dummy = { val: 0, next: null };
  let current = dummy;
  
  while (!minHeap.isEmpty()) {
    const node = minHeap.pop();
    current.next = node;
    current = current.next;
    
    if (node.next) {
      minHeap.push(node.next);
    }
  }
  
  return dummy.next;
}
```

## Dry Run

**Example: Insertion in Min-Heap**

**Input:**
```
Insert: 5, 3, 8, 1, 2
```

**Step-by-Step Execution:**

```
Initial: heap = []

Insert 5:
heap = [5]
Bubble-up: index 0 (root), no parent
heap = [5]

Insert 3:
heap = [5, 3]
Bubble-up: index 1, parent = 0
3 < 5, swap
heap = [3, 5]

Insert 8:
heap = [3, 5, 8]
Bubble-up: index 2, parent = 0
8 >= 3, stop
heap = [3, 5, 8]

Insert 1:
heap = [3, 5, 8, 1]
Bubble-up: index 3, parent = 1
1 < 5, swap
heap = [3, 1, 8, 5]
Bubble-up: index 1, parent = 0
1 < 3, swap
heap = [1, 3, 8, 5]

Insert 2:
heap = [1, 3, 8, 5, 2]
Bubble-up: index 4, parent = 1
2 < 3, swap
heap = [1, 2, 8, 5, 3]
Bubble-up: index 1, parent = 0
2 >= 1, stop
heap = [1, 2, 8, 5, 3]

Final: heap = [1, 2, 8, 5, 3]
Tree:
       1
     /   \
    2     8
   / \
  5   3
```

**Variable Changes Table:**

| Operation | Heap Array | Action | Result |
|-----------|------------|--------|--------|
| Insert 5 | [5] | Add to end | [5] |
| Insert 3 | [5, 3] | Swap 3,5 | [3, 5] |
| Insert 8 | [3, 5, 8] | No swap | [3, 5, 8] |
| Insert 1 | [3, 5, 8, 1] | Swap 1,5,3 | [1, 3, 8, 5] |
| Insert 2 | [1, 3, 8, 5, 2] | Swap 2,3 | [1, 2, 8, 5, 3] |

## Edge Cases

### 1. Empty Heap Operations
```javascript
heap = []
heap.pop() → null
heap.peek() → null
heap.isEmpty() → true
```

### 2. Single Element
```javascript
heap = [5]
heap.pop() → 5
heap = []
```

### 3. Duplicate Elements
```javascript
heap = [1, 1, 1]
All duplicates allowed
Heap property maintained
```

### 4. Large Number of Elements
```javascript
n = 1000000
Operations still O(log n)
Memory: O(n)
```

### 5. Custom Object Comparison
```javascript
heap = [{val: 5, priority: 2}, {val: 3, priority: 1}]
Need custom comparator
Compare by priority, not value
```

### 6. Negative Numbers
```javascript
heap = [-5, -3, -1]
Min-heap: [-5, -3, -1]
Max-heap: [-1, -3, -5]
```

**Why Edge Cases Matter:**
- Empty operations prevent null pointer errors
- Single element tests boundary conditions
- Duplicates test heap property maintenance
- Large inputs test performance
- Custom objects test comparator logic

## Variations / Extensions

### 1. Max-Heap for Kth Smallest

```javascript
function kthSmallest(nums, k) {
  const maxHeap = new MaxHeap();
  
  for (const num of nums) {
    maxHeap.push(num);
    if (maxHeap.size() > k) {
      maxHeap.pop();
    }
  }
  
  return maxHeap.peek();
}
```

### 2. Median Finder

```javascript
class MedianFinder {
  constructor() {
    this.maxHeap = new MaxHeap(); // Lower half
    this.minHeap = new MinHeap(); // Upper half
  }
  
  addNum(num) {
    if (this.maxHeap.isEmpty() || num <= this.maxHeap.peek()) {
      this.maxHeap.push(num);
    } else {
      this.minHeap.push(num);
    }
    
    // Balance heaps
    if (this.maxHeap.size() > this.minHeap.size() + 1) {
      this.minHeap.push(this.maxHeap.pop());
    } else if (this.minHeap.size() > this.maxHeap.size()) {
      this.maxHeap.push(this.minHeap.pop());
    }
  }
  
  findMedian() {
    if (this.maxHeap.size() > this.minHeap.size()) {
      return this.maxHeap.peek();
    }
    return (this.maxHeap.peek() + this.minHeap.peek()) / 2;
  }
}
```

### 3. Heap Sort

```javascript
function heapSort(arr) {
  const n = arr.length;
  
  // Build max-heap
  for (let i = Math.floor(n / 2) - 1; i >= 0; i--) {
    heapify(arr, n, i);
  }
  
  // Extract elements one by one
  for (let i = n - 1; i > 0; i--) {
    [arr[0], arr[i]] = [arr[i], arr[0]];
    heapify(arr, i, 0);
  }
  
  return arr;
}

function heapify(arr, n, i) {
  let largest = i;
  const left = 2 * i + 1;
  const right = 2 * i + 2;
  
  if (left < n && arr[left] > arr[largest]) {
    largest = left;
  }
  if (right < n && arr[right] > arr[largest]) {
    largest = right;
  }
  
  if (largest !== i) {
    [arr[i], arr[largest]] = [arr[largest], arr[i]];
    heapify(arr, n, largest);
  }
}
```

### 4. Priority Queue with Custom Comparator

```javascript
class PriorityQueue {
  constructor(comparator = (a, b) => a < b) {
    this.heap = [];
    this.comparator = comparator;
  }
  
  push(val) {
    this.heap.push(val);
    this._bubbleUp(this.heap.length - 1);
  }
  
  pop() {
    if (this.heap.length === 0) return null;
    if (this.heap.length === 1) return this.heap.pop();
    
    const top = this.heap[0];
    this.heap[0] = this.heap.pop();
    this._bubbleDown(0);
    return top;
  }
  
  _bubbleUp(index) {
    while (index > 0) {
      const parent = Math.floor((index - 1) / 2);
      if (this.comparator(this.heap[parent], this.heap[index])) break;
      [this.heap[parent], this.heap[index]] = [this.heap[index], this.heap[parent]];
      index = parent;
    }
  }
  
  _bubbleDown(index) {
    while (true) {
      const left = 2 * index + 1;
      const right = 2 * index + 2;
      let target = index;
      
      if (left < this.heap.length && this.comparator(this.heap[left], this.heap[target])) {
        target = left;
      }
      if (right < this.heap.length && this.comparator(this.heap[right], this.heap[target])) {
        target = right;
      }
      
      if (target === index) break;
      [this.heap[index], this.heap[target]] = [this.heap[target], this.heap[index]];
      index = target;
    }
  }
}
```

### 5. Sliding Window Maximum

```javascript
function maxSlidingWindow(nums, k) {
  const result = [];
  const maxHeap = new PriorityQueue((a, b) => a.val > b.val);
  
  for (let i = 0; i < nums.length; i++) {
    maxHeap.push({ val: nums[i], index: i });
    
    // Remove elements outside window
    while (maxHeap.heap[0].index <= i - k) {
      maxHeap.pop();
    }
    
    if (i >= k - 1) {
      result.push(maxHeap.heap[0].val);
    }
  }
  
  return result;
}
```

## Optimization Techniques

### 1. Heapify Optimization

**Build Heap in O(n):**
```javascript
// Instead of inserting n elements (O(n log n))
// Build heap from array in O(n)
function heapify(arr) {
  for (let i = Math.floor(arr.length / 2) - 1; i >= 0; i--) {
    _bubbleDown(arr, i, arr.length);
  }
}
```

### 2. Space Optimization

**In-Place Heap Sort:**
```javascript
// Use input array as heap
// No extra space needed
// O(1) additional space
```

### 3. Trade-offs

**Heap vs Sorted Array:**

| Aspect | Heap | Sorted Array |
|--------|------|--------------|
| Insert | `O(log n)` | `O(n)` |
| Delete Min/Max | `O(log n)` | `O(1)` or `O(n)` |
| Peek Min/Max | `O(1)` | `O(1)` |
| Search | `O(n)` | `O(log n)` |
| Space | `O(n)` | `O(n)` |
| Best For | Dynamic data | Static data |

**When to Use Sorted Array Instead:**
- Data is static (no insertions/deletions)
- Need to search for arbitrary elements
- Need to access elements in order
- Simpler implementation needed

## Complexity Analysis

### Time Complexity

**Insert (Push): O(log n)**
- Bubble-up operation
- Height of tree = log n
- Each step: O(1) comparison and swap

**Delete (Pop): O(log n)**
- Bubble-down operation
- Height of tree = log n
- Each step: O(1) comparison and swap

**Peek: O(1)**
- Direct access to root
- No traversal needed

**Build Heap (Heapify): O(n)**
- Start from last non-leaf node
- Each bubble-down is O(log n)
- Total: O(n) due to amortized analysis

**Search: O(n)**
- Must traverse entire heap
- No binary search property
- Linear scan required

### Space Complexity

**Heap Storage: O(n)**
- Store n elements in array
- No additional space for tree structure
- Array representation is compact

**Heap Sort: O(1)**
- In-place sorting
- No additional arrays needed
- Uses input array as heap

**Priority Queue: O(n)**
- Same as heap storage
- May store additional metadata
- Depends on implementation

**Explanation:**
Heap achieves O(log n) operations by maintaining a balanced tree structure. The array representation is space-efficient, requiring no pointers. Building a heap from an array is O(n) due to the bottom-up approach.

## Real-world Applications

### 1. Task Scheduling

**Priority-Based Task Queue:**
- High-priority tasks execute first
- Used in operating systems
- Example: Process scheduling in OS

### 2. Event Processing

**Event Simulation:**
- Process events in chronological order
- Used in discrete event simulation
- Example: Network simulation

### 3. Resource Allocation

**Load Balancing:**
- Allocate resources based on priority
- Used in cloud computing
- Example: Server load distribution

### 4. Search Ranking

**Search Results:**
- Rank results by relevance score
- Used in search engines
- Example: Google search ranking

### 5. Recommendation Systems

**Content Ranking:**
- Recommend top-k items
- Used in e-commerce, streaming
- Example: Netflix recommendations

### 6. Graph Algorithms

**Dijkstra's Shortest Path:**
- Use min-heap for distance updates
- Efficient shortest path finding
- Used in GPS navigation

### 7. Data Compression

**Huffman Coding:**
- Build optimal prefix codes
- Use min-heap for tree construction
- Used in ZIP compression

### 8. Real-Time Analytics

**Stream Processing:**
- Find top-k elements in stream
- Used in monitoring systems
- Example: Real-time error tracking

## Common Mistakes

### 1. Wrong Parent/Child Index Calculation

**Mistake:**
```javascript
// Wrong index calculation
const parent = index / 2; // Should be floor((index - 1) / 2)
const left = 2 * index; // Should be 2 * index + 1
```

**Correct:**
```javascript
// Correct index calculation
const parent = Math.floor((index - 1) / 2);
const left = 2 * index + 1;
const right = 2 * index + 2;
```

**Why It Matters:**
- Wrong indices break heap structure
- Incorrect parent-child relationships
- Heap property not maintained

### 2. Not Handling Empty Heap

**Mistake:**
```javascript
// Not checking if empty
const min = heap.pop(); // May return undefined
```

**Correct:**
```javascript
// Check before operations
if (heap.isEmpty()) return null;
const min = heap.pop();
```

**Why It Matters:**
- Accessing empty heap causes errors
- Must handle edge cases
- Prevents undefined behavior

### 3. Wrong Comparison for Min/Max Heap

**Mistake:**
```javascript
// Using wrong comparison
if (this.heap[parent] < this.heap[index]) break; // Wrong for max-heap
```

**Correct:**
```javascript
// Use correct comparison for heap type
if (this.heap[parent] >= this.heap[index]) break; // For max-heap
```

**Why It Matters:**
- Wrong comparison breaks heap property
- Min-heap vs max-heap logic differs
- Affects correctness of operations

### 4. Not Maintaining Heap Size

**Mistake:**
```javascript
// Not limiting heap size for top-k
minHeap.push(num); // Should check size
```

**Correct:**
```javascript
// Maintain heap size for top-k problems
minHeap.push(num);
if (minHeap.size() > k) {
  minHeap.pop();
}
```

**Why It Matters:**
- Unbounded heap uses O(n) space
- Top-k requires O(k) space
- Affects memory efficiency

### 5. Inefficient Build Heap

**Mistake:**
```javascript
// Inserting one by one (O(n log n))
for (const num of arr) {
  heap.push(num);
}
```

**Correct:**
```javascript
// Build heap in O(n)
heap.heap = [...arr];
for (let i = Math.floor(arr.length / 2) - 1; i >= 0; i--) {
  heap._bubbleDown(i);
}
```

**Why It Matters:**
- Insertion is O(n log n)
- Heapify is O(n)
- Significant performance difference

### 6. Not Using Built-in Heap

**Mistake:**
```javascript
// Implementing custom heap when built-in available
class MinHeap { /* ... */ }
```

**Correct:**
```javascript
// Use built-in when available (language-specific)
// Python: heapq, Java: PriorityQueue, C++: priority_queue
```

**Why It Matters:**
- Built-in is optimized
- Less error-prone
- Better performance

## Advanced Concepts

### 1. Fibonacci Heap

**Concept:**
Advanced heap with amortized O(1) insert and O(log n) delete-min.

**Features:**
- Collection of trees (not single tree)
- Lazy merging
- Amortized better time complexity
- Complex implementation

### 2. Binomial Heap

**Concept:**
Heap similar to binary heap but with better merge operation.

**Features:**
- Collection of binomial trees
- O(log n) merge operation
- Used in advanced algorithms
- More complex than binary heap

### 3. Pairing Heap

**Concept:**
Simpler alternative to Fibonacci heap with good performance.

**Features:**
- Multi-way tree structure
- Simple implementation
- Good amortized performance
- Used in practice

### 4. Leftist Heap

**Concept:**
Heap with efficient merge operation using rank property.

**Features:**
- O(log n) merge
- Priority queue with merge
- Used in functional programming
- Good for persistent data structures

## Practice Thinking Guide

### How to Identify When to Use Heap

**Key Signals in Problem Statements:**

1. **"Find kth largest/smallest element"**
   - Use heap to maintain top/bottom k
   - Example: "Kth largest element in array"

2. **"Top k frequent elements"**
   - Use heap with frequency count
   - Example: "Top K frequent words"

3. **"Merge k sorted lists/arrays"**
   - Use min-heap to merge efficiently
   - Example: "Merge k sorted linked lists"

4. **"Find median from data stream"**
   - Use two heaps (max and min)
   - Example: "Median finder"

5. **"Priority-based processing"**
   - Use priority queue
   - Example: "Task scheduler"

6. **"Sliding window maximum/minimum"**
   - Use heap or deque
   - Example: "Sliding window maximum"

**Pattern Recognition:**

**Pattern 1: Top/Bottom K**
```
Problem: Find top/bottom k elements
Solution: Maintain heap of size k
```

**Pattern 2: Merge Sorted Streams**
```
Problem: Merge multiple sorted sequences
Solution: Min-heap for efficient merge
```

**Pattern 3: Frequency-Based Selection**
```
Problem: Select based on frequency
Solution: Heap with frequency count
```

**Pattern 4: Median Maintenance**
```
Problem: Find median dynamically
Solution: Two heaps (max + min)
```

**Pattern 5: Priority Processing**
```
Problem: Process by priority
Solution: Priority queue (heap)
```

**Decision Flowchart:**

```
Need to find min/max efficiently?
├─ Yes → Need to maintain top/bottom k?
│        ├─ Yes → Use heap of size k
│        └─ No → Use full heap
├─ No → Need to merge sorted streams?
│        ├─ Yes → Use min-heap
│        └─ No → Consider other approach
└─ No → Not heap problem
```

**Example Problem Analysis:**

**Problem:** "Find kth largest element in array"

**Analysis:**
1. Need kth largest → top-k problem
2. Maintain min-heap of size k
3. Push all elements, pop when size > k
4. Root is kth largest
5. Solution: Min-heap of size k

**Problem:** "Merge k sorted linked lists"

**Analysis:**
1. Need to merge sorted lists
2. Always pick smallest available head
3. Min-heap provides O(1) access to smallest
4. Push next node after popping
5. Solution: Min-heap with list nodes

**Problem:** "Find median from data stream"

**Analysis:**
1. Need median dynamically
2. Median splits data into two halves
3. Use max-heap for lower half, min-heap for upper half
4. Balance heaps to maintain median
5. Solution: Two heaps

## Summary

Heap is a powerful data structure that provides efficient access to the minimum or maximum element. It's essential for priority-based operations and forms the foundation for many algorithms including Dijkstra's shortest path, Prim's MST, and Huffman coding.

**Key Takeaways:**
- Complete binary tree stored in array
- O(log n) insert and delete, O(1) peek
- Min-heap for smallest, max-heap for largest
- Essential for top-k problems and priority queues
- Build heap in O(n) from array
- Not fully ordered (only min/max at root)
- Use built-in heap when available

**Mastery Checklist:**
- ✅ Understand heap property and structure
- ✅ Implement bubble-up and bubble-down
- ✅ Calculate parent/child indices correctly
- ✅ Solve top-k problems with heaps
- ✅ Merge sorted streams with heaps
- ✅ Implement median finder with two heaps
- ✅ Choose min-heap vs max-heap appropriately
- ✅ Optimize heap operations

