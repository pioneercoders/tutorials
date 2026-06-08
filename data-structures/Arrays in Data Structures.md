# Arrays in Data Structures

Arrays are the backbone of almost every data structure and algorithm.

Most advanced structures internally rely on arrays:

* Hash Tables
* Heaps
* Dynamic Arrays
* Matrices
* Buffers
* CPU caches

Mastering arrays builds the foundation for solving coding interviews and designing efficient systems.

---

# 1. Introduction to Arrays

An **Array** is a collection of elements stored in contiguous memory locations.

```text id="5m4g0f"
Index:   0   1   2   3
Value:  10  20  30  40
```

Each element is accessed using an index.

---

# Characteristics of Arrays

| Feature           | Description             |
| ----------------- | ----------------------- |
| Ordered           | Elements maintain order |
| Indexed           | Access via index        |
| Contiguous Memory | Stored continuously     |
| Fast Access       | O(1) indexing           |

---

# Real-Time Examples

| Application       | Usage                   |
| ----------------- | ----------------------- |
| Images            | Pixels stored in arrays |
| Audio processing  | Sound samples           |
| Game boards       | Grid systems            |
| Databases         | Internal page storage   |
| Browser rendering | DOM node collections    |

---

# Basic Array Example

```js id="f4n5rx"
const numbers = [10, 20, 30, 40];

console.log(numbers[0]); // 10
console.log(numbers[2]); // 30
```

---

# Why Arrays are Fast

Because arrays use contiguous memory.

Address calculation:

```text id="c3xut7"
Address = Base + (Index × Size)
```

This allows instant access.

---

# Time Complexity of Array Operations

| Operation           | Complexity |
| ------------------- | ---------- |
| Access              | O(1)       |
| Search              | O(n)       |
| Insert at End       | O(1)       |
| Insert at Beginning | O(n)       |
| Delete              | O(n)       |

---

# Memory Representation

```text id="eg3vij"
Address: 100 104 108 112
Value:    5   8  12  20
```

Each integer takes 4 bytes.

---

# 2. Static Arrays

Static arrays have fixed size.

Size cannot change after creation.

---

# Example

```js id="6e1rpb"
const arr = new Array(5);

arr[0] = 10;
arr[1] = 20;
```

---

# Characteristics

| Feature     | Value        |
| ----------- | ------------ |
| Size        | Fixed        |
| Memory      | Preallocated |
| Speed       | Fast         |
| Flexibility | Low          |

---

# Real-Time Example

## Student Roll Numbers

Suppose:

* Maximum students = 100

A static array can store fixed entries efficiently.

---

# Advantages

* Fast indexing
* Better cache performance
* Simpler implementation

---

# Disadvantages

* Wasted memory
* Cannot grow dynamically

---

# Problem Example

```js id="j3ox5j"
const arr = new Array(2);

arr[0] = 1;
arr[1] = 2;

// Need more space later
```

Cannot expand efficiently.

---

# 3. Dynamic Arrays

Dynamic arrays resize automatically.

Examples:

* JavaScript Arrays
* Python Lists
* Java ArrayList
* C++ Vector

---

# How Dynamic Arrays Work

When capacity is full:

1. Create bigger array
2. Copy old elements
3. Insert new element

---

# Visualization

```text id="9w7kcu"
Capacity = 2

[10, 20]

Insert 30

↓

New Capacity = 4

[10, 20, 30]
```

---

# Example

```js id="zjtt4w"
const arr = [];

arr.push(10);
arr.push(20);
arr.push(30);
```

---

# Internal Growth Strategy

Most languages double capacity.

```text id="40v4b2"
2 → 4 → 8 → 16 → 32
```

This keeps insertion efficient.

---

# Amortized Complexity

Appending:

* Average: O(1)
* Worst-case resize: O(n)

---

# Real-Time Example

## Instagram Infinite Feed

Posts dynamically grow while scrolling.

Dynamic arrays efficiently handle:

* Expansion
* Appending
* Iteration

---

# 4. Multi-Dimensional Arrays

Arrays inside arrays.

Used for:

* Matrices
* Games
* Images
* Graphs

---

# 2D Array Example

```js id="lk70ph"
const matrix = [
  [1, 2, 3],
  [4, 5, 6],
  [7, 8, 9]
];

console.log(matrix[1][2]); // 6
```

---

# Visualization

```text id="lknl2v"
1 2 3
4 5 6
7 8 9
```

---

# Real-Time Applications

| System           | Usage                |
| ---------------- | -------------------- |
| Chess game       | Board representation |
| Image processing | Pixel matrices       |
| AI/ML            | Tensors              |
| Excel sheets     | Grid data            |

---

# Traversing 2D Arrays

```js id="g3uk0g"
for (let row = 0; row < matrix.length; row++) {
  for (let col = 0; col < matrix[row].length; col++) {
    console.log(matrix[row][col]);
  }
}
```

---

# Complexity

For matrix of rows × cols:

Time Complexity:

* O(rows × cols)

---

# 5. Array Operations

---

# Traversal

```js id="jlwm9r"
const arr = [10, 20, 30];

for (let i = 0; i < arr.length; i++) {
  console.log(arr[i]);
}
```

Complexity:

* O(n)

---

# Insertion

```js id="rn5wqz"
arr.push(40);
```

Average:

* O(1)

---

# Insert at Beginning

```js id="gzk0m9"
arr.unshift(5);
```

Complexity:

* O(n)

Because all elements shift.

---

# Deletion

```js id="rlv67g"
arr.pop();
```

Complexity:

* O(1)

---

# Delete from Middle

```js id="yjzyl5"
arr.splice(1, 1);
```

Complexity:

* O(n)

---

# Searching

## Linear Search

```js id="m1a8vj"
function search(arr, target) {
  for (let i = 0; i < arr.length; i++) {
    if (arr[i] === target) {
      return i;
    }
  }

  return -1;
}
```

Complexity:

* O(n)

---

# Binary Search

Requires sorted array.

Complexity:

* O(log n)

---

# 6. Prefix Sum

A powerful optimization technique.

Used for:

* Range sum queries
* Competitive programming
* Analytics systems

---

# Idea

Store cumulative sums.

---

# Example

Array:

```text id="jrd5mf"
[1, 2, 3, 4]
```

Prefix Sum:

```text id="z6v5c6"
[1, 3, 6, 10]
```

---

# Formula

```text id="rk08rm"
prefix[i] = prefix[i - 1] + arr[i]
```

---

# Code

```js id="8e5t4j"
const arr = [1, 2, 3, 4];
const prefix = [];

prefix[0] = arr[0];

for (let i = 1; i < arr.length; i++) {
  prefix[i] = prefix[i - 1] + arr[i];
}

console.log(prefix);
```

---

# Range Sum Query

```text id="1z8nzy"
Sum(L, R) = prefix[R] - prefix[L - 1]
```

---

# Real-Time Example

## Analytics Dashboard

Suppose:

* Need sum of website visitors between dates repeatedly

Prefix sums avoid recalculating every time.

---

# Complexity

| Operation       | Complexity |
| --------------- | ---------- |
| Build Prefix    | O(n)       |
| Query Range Sum | O(1)       |

---

# 7. Sliding Window Technique

One of the most important array optimization techniques.

Used heavily in:

* Streaming systems
* Real-time analytics
* Subarray problems

---

# Problem Example

Find maximum sum of subarray of size k.

---

# Brute Force

```js id="dt1y2z"
function maxSum(arr, k) {
  let max = 0;

  for (let i = 0; i <= arr.length - k; i++) {
    let sum = 0;

    for (let j = i; j < i + k; j++) {
      sum += arr[j];
    }

    max = Math.max(max, sum);
  }

  return max;
}
```

Complexity:

* O(n × k)

---

# Optimized Sliding Window

```js id="vc8zn5"
function maxSum(arr, k) {
  let windowSum = 0;

  for (let i = 0; i < k; i++) {
    windowSum += arr[i];
  }

  let maxSum = windowSum;

  for (let i = k; i < arr.length; i++) {
    windowSum += arr[i] - arr[i - k];
    maxSum = Math.max(maxSum, windowSum);
  }

  return maxSum;
}
```

Complexity:

* O(n)

---

# Visualization

```text id="b4ktc6"
[1 2 3] 4 5
1 [2 3 4] 5
1 2 [3 4 5]
```

Window slides efficiently.

---

# Real-Time Example

## Network Monitoring

Track:

* Average traffic in last 5 minutes
* CPU usage windows
* Stock market moving averages

---

# 8. Two Pointer Technique

Uses two indices to optimize traversal.

---

# Common Use Cases

* Sorted arrays
* Pair problems
* Palindrome checking
* Duplicate removal

---

# Example Problem

Find pair with target sum.

```js id="h7r3lq"
function hasPair(arr, target) {
  let left = 0;
  let right = arr.length - 1;

  while (left < right) {
    const sum = arr[left] + arr[right];

    if (sum === target) {
      return true;
    }

    if (sum < target) {
      left++;
    } else {
      right--;
    }
  }

  return false;
}
```

---

# Complexity

| Method      | Complexity |
| ----------- | ---------- |
| Brute Force | O(n²)      |
| Two Pointer | O(n)       |

---

# Real-Time Example

## Fraud Detection Systems

Finding suspicious transaction pairs efficiently.

---

# 9. Kadane’s Algorithm

Find maximum subarray sum efficiently.

One of the most famous interview algorithms.

---

# Problem

```text id="7c7q8e"
[-2,1,-3,4,-1,2,1,-5,4]
```

Maximum subarray:

```text id="gmlp6d"
[4,-1,2,1]
```

Sum:

* 6

---

# Brute Force Complexity

O(n²)

---

# Optimized Kadane’s Algorithm

```js id="j1jcv5"
function kadane(arr) {
  let maxCurrent = arr[0];
  let maxGlobal = arr[0];

  for (let i = 1; i < arr.length; i++) {
    maxCurrent = Math.max(arr[i], maxCurrent + arr[i]);

    if (maxCurrent > maxGlobal) {
      maxGlobal = maxCurrent;
    }
  }

  return maxGlobal;
}
```

---

# Complexity

| Complexity Type | Value |
| --------------- | ----- |
| Time            | O(n)  |
| Space           | O(1)  |

---

# Real-Time Example

## Stock Trading Systems

Finding:

* Best profit streak
* Maximum revenue window

---

# 10. Sparse Arrays

Sparse arrays contain many empty/default values.

---

# Example

```text id="2jlwm1"
[0, 0, 0, 0, 1000, 0, 0]
```

Most values are empty.

---

# Problem

Wasted memory.

---

# Optimized Representation

Store only non-zero values.

```js id="5ps4ja"
const sparse = {
  4: 1000
};
```

---

# Real-Time Applications

| System                 | Usage              |
| ---------------------- | ------------------ |
| Search engines         | Huge matrices      |
| AI systems             | Sparse vectors     |
| Recommendation systems | User-item matrices |

---

# Advantages

* Saves memory
* Faster processing

---

# 11. Circular Arrays

Last element connects back to first.

---

# Visualization

```text id="9hndt7"
1 → 2 → 3 → 4
↑         ↓
← ← ← ← ←
```

---

# Circular Traversal

```js id="xqvqvn"
const arr = [1, 2, 3, 4];

for (let i = 0; i < 8; i++) {
  console.log(arr[i % arr.length]);
}
```

---

# Real-Time Applications

| System            | Usage          |
| ----------------- | -------------- |
| CPU scheduling    | Round Robin    |
| Music playlists   | Loop playback  |
| Buffers           | Circular queue |
| Multiplayer games | Turn rotation  |

---

# Circular Queue Example

```js id="zc4ph0"
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

# Important Interview Patterns from Arrays

| Pattern        | Usage                 |
| -------------- | --------------------- |
| Sliding Window | Subarray optimization |
| Two Pointer    | Sorted array problems |
| Prefix Sum     | Range queries         |
| Kadane’s       | Maximum subarray      |
| Binary Search  | Fast searching        |

---

# Common Array Interview Problems

1. Two Sum
2. Maximum Subarray
3. Move Zeroes
4. Merge Intervals
5. Product Except Self
6. Trapping Rain Water
7. Rotate Array
8. Longest Substring
9. Container With Most Water
10. Best Time to Buy/Sell Stock

---

# Common Beginner Mistakes

| Mistake                     | Issue                 |
| --------------------------- | --------------------- |
| Ignoring bounds             | Runtime errors        |
| Nested loops everywhere     | Poor performance      |
| Using brute force first     | Inefficient solutions |
| Forgetting edge cases       | Bugs                  |
| Confusing shallow/deep copy | Unexpected behavior   |

---

# Production Engineering Insights

Arrays are heavily used in:

* Databases
* Search engines
* Browsers
* Game engines
* AI systems
* Operating systems

Because arrays provide:

* Cache-friendly access
* Fast iteration
* Efficient memory usage

---

# Summary Table

| Concept           | Key Idea            |
| ----------------- | ------------------- |
| Static Array      | Fixed size          |
| Dynamic Array     | Resizable           |
| Multi-Dimensional | Matrix/grid         |
| Prefix Sum        | Fast range queries  |
| Sliding Window    | Efficient subarrays |
| Two Pointer       | Optimized traversal |
| Kadane’s          | Max subarray        |
| Sparse Array      | Memory optimization |
| Circular Array    | Loop structure      |

---
