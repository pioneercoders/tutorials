# Fenwick Tree (Binary Indexed Tree)

Fenwick Tree (Binary Indexed Tree) is a data structure that provides efficient methods for calculation and manipulation of prefix sums in an array.

## Introduction

Fenwick Tree, also known as Binary Indexed Tree (BIT), is a data structure that provides efficient methods for calculating and manipulating prefix sums in an array. It supports point updates and prefix sum queries in O(log n) time, which is a significant improvement over the O(n) update time of naive prefix sum arrays. The Fenwick Tree is simpler to implement than a Segment Tree and uses less memory, making it ideal for problems involving dynamic prefix sums, frequency counting, and inversion counting. It was invented by Peter Fenwick in 1994 and is widely used in competitive programming and real-world applications.

**Why Fenwick Tree Exists:**
- Prefix sum queries are O(1) but updates are O(n)
- Fenwick Tree provides O(log n) for both queries and updates
- Simpler implementation than Segment Tree
- Space efficient (O(n))
- Ideal for dynamic prefix sum problems

**Where It Is Used:**
- Range sum queries with updates
- Frequency counting and ranking
- Inversion counting
- Analytics and metrics calculations
- Financial running totals
- Game score tracking
- Database query optimization

## Core Concept Explanation

Fenwick Tree uses a clever indexing scheme where each index stores the sum of a specific range of elements. The key operation is "lowbit" (lowest set bit), which determines the range each index covers. For index i, lowbit(i) gives the number of elements it covers. The tree is built such that index i stores the sum of elements from (i - lowbit(i) + 1) to i. This structure allows us to compute prefix sums by summing specific indices and update elements by updating all indices that include that element. The 1-based indexing is crucial for the lowbit operation to work correctly.

**Step-by-Step Breakdown:**
1. Initialize tree array of size n+1 (1-based)
2. For each index i, tree[i] covers range (i - lowbit(i) + 1) to i
3. To query prefix sum up to i: sum tree[i], then i -= lowbit(i), repeat
4. To update index i by delta: tree[i] += delta, then i += lowbit(i), repeat
5. Range sum query: query(r) - query(l-1)

**Intuition Behind the Concept:**
Think of Fenwick Tree like a hierarchical filing system. Each folder (index) stores the sum of a specific range of documents. When you want the total of documents 1 to 10, you don't count each one - you check folder 10 (which might have documents 9-10), then folder 8 (documents 1-8). When you update document 5, you update all folders that include it (folder 5, 6, 8, 16, etc.). This hierarchical structure makes both queries and updates efficient.

**Visual Thinking:**
```
Array: [1, 2, 3, 4, 5, 6, 7, 8]
Index:  1  2  3  4  5  6  7  8

Fenwick Tree Structure:
tree[1] = arr[1] = 1 (covers 1)
tree[2] = arr[1] + arr[2] = 3 (covers 1-2)
tree[3] = arr[3] = 3 (covers 3)
tree[4] = arr[1] + arr[2] + arr[3] + arr[4] = 10 (covers 1-4)
tree[5] = arr[5] = 5 (covers 5)
tree[6] = arr[5] + arr[6] = 11 (covers 5-6)
tree[7] = arr[7] = 7 (covers 7)
tree[8] = arr[1] + ... + arr[8] = 36 (covers 1-8)

lowbit values:
lowbit(1) = 1 (binary: 001)
lowbit(2) = 2 (binary: 010)
lowbit(3) = 1 (binary: 011)
lowbit(4) = 4 (binary: 100)
lowbit(5) = 1 (binary: 101)
lowbit(6) = 2 (binary: 110)
lowbit(7) = 1 (binary: 111)
lowbit(8) = 8 (binary: 1000)
```

## Internal Working / Logic

Fenwick Tree operates through the lowbit operation, which extracts the lowest set bit of a number. This operation determines the range each index covers and how to navigate the tree. The tree structure is implicit - we don't store actual tree nodes, just use clever indexing.

**Operation 1: Lowbit**
- Extracts lowest set bit: x & (-x)
- Determines range covered by index
- Used for navigation in both directions
- Example: lowbit(6) = 2 (6 in binary: 110, -6: 010, AND: 010 = 2)

**Operation 2: Prefix Sum Query**
- Start at index i
- Add tree[i] to result
- Move to i -= lowbit(i)
- Repeat until i = 0
- Total: O(log n) operations

**Operation 3: Point Update**
- Start at index i
- Add delta to tree[i]
- Move to i += lowbit(i)
- Repeat until i > n
- Total: O(log n) operations

**Operation 4: Range Sum Query**
- Compute prefix sum up to r
- Compute prefix sum up to l-1
- Return difference
- Total: O(log n) operations

**Flow Explanation (Prefix Sum Query):**
1. Start at index i
2. Add tree[i] to result
3. Remove lowest set bit: i = i - lowbit(i)
4. Repeat until i = 0
5. Return result

**Decision Making Logic:**
The key decisions are:
- Use 1-based indexing (required for lowbit)
- Coordinate compression for large value ranges
- Choose Fenwick Tree vs Segment Tree based on operations needed
- Handle overflow in sums (use BigInt if needed)

## Algorithm / Approach

**Build Fenwick Tree Algorithm**

```
1. Initialize tree array of size n+1 with zeros
2. For each element at index i (1-based):
   a. Update tree at i by adding element value
3. Tree is now built
```

**Prefix Sum Query Algorithm**

```
1. Initialize result = 0
2. While i > 0:
   a. Add tree[i] to result
   b. i = i - lowbit(i)
3. Return result
```

**Point Update Algorithm**

```
1. While i <= n:
   a. Add delta to tree[i]
   b. i = i + lowbit(i)
2. Update complete
```

**Range Sum Query Algorithm**

```
1. Compute prefix sum up to r
2. Compute prefix sum up to l-1
3. Return difference
```

**Coordinate Compression Algorithm**

```
1. Collect all unique values
2. Sort unique values
3. Map each value to its rank (1-based)
4. Use ranks as indices in Fenwick Tree
```

## Implementations

### 1. Basic Fenwick Tree

```javascript
class FenwickTree {
  constructor(n) {
    this.n = n;
    this.tree = new Array(n + 1).fill(0);
  }
  
  lowbit(x) {
    return x & (-x);
  }
  
  update(i, delta) {
    while (i <= this.n) {
      this.tree[i] += delta;
      i += this.lowbit(i);
    }
  }
  
  query(i) {
    let result = 0;
    while (i > 0) {
      result += this.tree[i];
      i -= this.lowbit(i);
    }
    return result;
  }
  
  rangeQuery(l, r) {
    return this.query(r) - this.query(l - 1);
  }
}
```

**Advantages:**
- O(log n) query and update
- Simple implementation
- Space efficient

### 2. Range Sum Query - Mutable

```javascript
class NumArray {
  constructor(nums) {
    this.nums = nums;
    this.ft = new FenwickTree(nums.length);
    for (let i = 0; i < nums.length; i++) {
      this.ft.update(i + 1, nums[i]);
    }
  }
  
  update(index, val) {
    const delta = val - this.nums[index];
    this.nums[index] = val;
    this.ft.update(index + 1, delta);
  }
  
  sumRange(left, right) {
    return this.ft.rangeQuery(left + 1, right + 1);
  }
}
```

**Advantages:**
- Dynamic array with updates
- Efficient range sum queries
- Practical application

### 3. Count of Smaller Numbers After Self

```javascript
function countSmaller(nums) {
  // Coordinate compression
  const sortedNums = [...new Set(nums)].sort((a, b) => a - b);
  const rank = new Map();
  sortedNums.forEach((num, i) => rank.set(num, i + 1));
  
  const ft = new FenwickTree(sortedNums.length);
  const result = [];
  
  for (let i = nums.length - 1; i >= 0; i--) {
    const r = rank.get(nums[i]);
    const count = ft.query(r - 1);
    result.push(count);
    ft.update(r, 1);
  }
  
  return result.reverse();
}
```

**Advantages:**
- Inversion counting
- Coordinate compression
- Counting smaller elements

### 4. Reverse Pairs

```javascript
function reversePairs(nums) {
  // Coordinate compression
  const sortedNums = [...new Set(nums)].sort((a, b) => a - b);
  const rank = new Map();
  sortedNums.forEach((num, i) => rank.set(num, i + 1));
  
  const ft = new FenwickTree(sortedNums.length);
  let count = 0;
  
  for (let i = nums.length - 1; i >= 0; i--) {
    const r = rank.get(nums[i]);
    // Count elements > 2 * nums[i]
    const target = 2 * nums[i];
    const targetRank = this.findRank(sortedNums, target);
    if (targetRank > 0) {
      count += ft.query(targetRank);
    }
    ft.update(r, 1);
  }
  
  return count;
}
```

**Advantages:**
- Counts reverse pairs
- Efficient for large arrays
- Coordinate compression

### 5. Create Sorted Array through Instructions

```javascript
function createSortedArray(instructions) {
  const ft = new FenwickTree(10001);
  let result = 0;
  const MOD = 10**9 + 7;
  
  for (const num of instructions) {
    const smaller = ft.query(num);
    const larger = ft.query(10000) - ft.query(num + 1);
    result = (result + Math.min(smaller, larger)) % MOD;
    ft.update(num + 1, 1);
  }
  
  return result;
}
```

**Advantages:**
- Tracks relative ordering
- Efficient insertions
- Cost calculation

## Dry Run

**Example: Build and Query Fenwick Tree**

**Input:**
```
nums = [1, 2, 3, 4, 5]
```

**Step-by-Step Execution:**

```
Initial State:
tree = [0, 0, 0, 0, 0, 0] (indices 0-5)

Update index 1 with value 1:
i = 1, lowbit(1) = 1
tree[1] += 1 → tree[1] = 1
i = 1 + 1 = 2, lowbit(2) = 2
tree[2] += 1 → tree[2] = 1
i = 2 + 2 = 4, lowbit(4) = 4
tree[4] += 1 → tree[4] = 1
i = 4 + 4 = 8 > 5, stop
tree = [0, 1, 1, 0, 1, 0]

Update index 2 with value 2:
i = 2, lowbit(2) = 2
tree[2] += 2 → tree[2] = 3
i = 2 + 2 = 4, lowbit(4) = 4
tree[4] += 2 → tree[4] = 3
i = 4 + 4 = 8 > 5, stop
tree = [0, 1, 3, 0, 3, 0]

Update index 3 with value 3:
i = 3, lowbit(3) = 1
tree[3] += 3 → tree[3] = 3
i = 3 + 1 = 4, lowbit(4) = 4
tree[4] += 3 → tree[4] = 6
i = 4 + 4 = 8 > 5, stop
tree = [0, 1, 3, 3, 6, 0]

Update index 4 with value 4:
i = 4, lowbit(4) = 4
tree[4] += 4 → tree[4] = 10
i = 4 + 4 = 8 > 5, stop
tree = [0, 1, 3, 3, 10, 0]

Update index 5 with value 5:
i = 5, lowbit(5) = 1
tree[5] += 5 → tree[5] = 5
i = 5 + 1 = 6 > 5, stop
tree = [0, 1, 3, 3, 10, 5]

Query prefix sum up to 5:
i = 5, result = 0
result += tree[5] = 5, i = 5 - 1 = 4
result += tree[4] = 10, i = 4 - 4 = 0
Return result = 15

Query range sum from 2 to 5:
query(5) - query(1) = 15 - 1 = 14
```

**Variable Changes Table:**

| Operation | i | lowbit(i) | tree (after) | result |
|-----------|---|-----------|--------------|--------|
| Update(1, 1) | 1 | 1 | [0,1,1,0,1,0] | - |
| Update(2, 2) | 2 | 2 | [0,1,3,0,3,0] | - |
| Update(3, 3) | 3 | 1 | [0,1,3,3,6,0] | - |
| Update(4, 4) | 4 | 4 | [0,1,3,3,10,0] | - |
| Update(5, 5) | 5 | 1 | [0,1,3,3,10,5] | - |
| Query(5) | 5 | 1 | - | 15 |
| Query(1) | 1 | 1 | - | 1 |
| Range(2,5) | - | - | - | 14 |

## Edge Cases

### 1. Empty Array
```javascript
nums = []
FenwickTree(0) → tree = [0]
Handle empty input
```

### 2. Single Element
```javascript
nums = [5]
FenwickTree(1) → tree = [0, 5]
query(1) = 5
Base case
```

### 3. Update to Zero
```javascript
update(3, -5) → Reduces value
Can handle negative deltas
```

### 4. Large Values
```javascript
nums = [1000000, 2000000]
Need coordinate compression
Handle overflow
```

### 5. Duplicate Values
```javascript
nums = [1, 1, 2, 2]
Coordinate compression handles duplicates
```

### 6. Zero-based vs One-based
```javascript
Fenwick Tree uses 1-based indexing
Must convert from 0-based
```

**Why Edge Cases Matter:**
- Empty array needs special handling
- Single element is base case
- Negative deltas are valid
- Large values need compression
- Duplicates handled by compression
- Indexing conversion critical

## Variations / Extensions

### 1. 2D Fenwick Tree

```javascript
class FenwickTree2D {
  constructor(m, n) {
    this.m = m;
    this.n = n;
    this.tree = Array(m + 1).fill(null).map(() => Array(n + 1).fill(0));
  }
  
  update(x, y, delta) {
    for (let i = x; i <= this.m; i += i & (-i)) {
      for (let j = y; j <= this.n; j += j & (-j)) {
        this.tree[i][j] += delta;
      }
    }
  }
  
  query(x, y) {
    let result = 0;
    for (let i = x; i > 0; i -= i & (-i)) {
      for (let j = y; j > 0; j -= j & (-j)) {
        result += this.tree[i][j];
      }
    }
    return result;
  }
}
```

### 2. Fenwick Tree with Range Updates

```javascript
class FenwickTreeRange {
  constructor(n) {
    this.n = n;
    this.tree1 = new Array(n + 2).fill(0);
    this.tree2 = new Array(n + 2).fill(0);
  }
  
  updateRange(l, r, val) {
    this._update(this.tree1, l, val);
    this._update(this.tree1, r + 1, -val);
    this._update(this.tree2, l, val * (l - 1));
    this._update(this.tree2, r + 1, -val * r);
  }
  
  _update(tree, i, val) {
    while (i <= this.n) {
      tree[i] += val;
      i += i & (-i);
    }
  }
  
  query(i) {
    return this._query(this.tree1, i) * i - this._query(this.tree2, i);
  }
  
  _query(tree, i) {
    let result = 0;
    while (i > 0) {
      result += tree[i];
      i -= i & (-i);
    }
    return result;
  }
}
```

### 3. Persistent Fenwick Tree

```javascript
class PersistentFenwickTree {
  constructor(n) {
    this.n = n;
    this.versions = [[0].concat(new Array(n).fill(0))];
  }
  
  update(prevVersion, i, delta) {
    const newVersion = [...this.versions[prevVersion]];
    while (i <= this.n) {
      newVersion[i] += delta;
      i += i & (-i);
    }
    this.versions.push(newVersion);
    return this.versions.length - 1;
  }
  
  query(version, i) {
    const tree = this.versions[version];
    let result = 0;
    while (i > 0) {
      result += tree[i];
      i -= i & (-i);
    }
    return result;
  }
}
```

### 4. Minimum Fenwick Tree

```javascript
class FenwickTreeMin {
  constructor(n) {
    this.n = n;
    this.tree = new Array(n + 1).fill(Infinity);
  }
  
  update(i, val) {
    while (i <= this.n) {
      this.tree[i] = Math.min(this.tree[i], val);
      i += i & (-i);
    }
  }
  
  query(i) {
    let result = Infinity;
    while (i > 0) {
      result = Math.min(result, this.tree[i]);
      i -= i & (-i);
    }
    return result;
  }
}
```

### 5. Frequency Counting

```javascript
function countFrequencies(nums) {
  const sortedNums = [...new Set(nums)].sort((a, b) => a - b);
  const rank = new Map();
  sortedNums.forEach((num, i) => rank.set(num, i + 1));
  
  const ft = new FenwickTree(sortedNums.length);
  const freq = new Map();
  
  for (const num of nums) {
    const r = rank.get(num);
    const count = ft.query(r) - ft.query(r - 1);
    freq.set(num, count + 1);
    ft.update(r, 1);
  }
  
  return freq;
}
```

## Optimization Techniques

### 1. Coordinate Compression

**Handle Large Ranges:**
```javascript
// Map large values to 1..n
// Reduce memory usage
// Essential for large value ranges
```

### 2. Lazy Construction

**Build Efficiently:**
```javascript
// Build in O(n) instead of O(n log n)
// Use prefix sums
// More efficient initialization
```

### 3. Memory Optimization

**Use Smaller Types:**
```javascript
// Use Int32Array for integers
// Reduce memory footprint
// Better cache performance
```

### 4. Batch Updates

**Process Multiple Updates:**
```javascript
// Queue updates
// Process in batches
// Reduce overhead
```

### 5. Trade-offs

**Fenwick Tree vs Segment Tree:**

| Aspect | Fenwick Tree | Segment Tree |
|--------|--------------|--------------|
| Query | `O(log n)` | `O(log n)` |
| Update | `O(log n)` | `O(log n)` |
| Range Update | Difficult | Easy |
| Flexibility | Limited | High |
| Implementation | Simple | Complex |

**When to Use Fenwick Tree:**
- Prefix sum queries
- Point updates
- Frequency counting
- Inversion counting
- Need simple implementation

## Complexity Analysis

### Time Complexity

**Build: O(n log n) or O(n)**
- Standard: O(n log n) with n updates
- Optimized: O(n) with prefix sums
- Example: Building from array

**Point Update: O(log n)**
- Update O(log n) indices
- Each index update is O(1)
- Total: O(log n)

**Prefix Sum Query: O(log n)**
- Sum O(log n) indices
- Each index access is O(1)
- Total: O(log n)

**Range Sum Query: O(log n)**
- Two prefix sum queries
- Each is O(log n)
- Total: O(log n)

### Space Complexity

**Space: O(n)**
- Tree array of size n+1
- No additional space
- Total: O(n)

**Explanation:**
Fenwick Tree achieves O(log n) time complexity for both point updates and prefix sum queries. This is achieved through the clever lowbit operation that determines which indices to visit. Space complexity is O(n) for the tree array, which is optimal for this problem. The key advantage over naive prefix sum arrays is the O(log n) update time compared to O(n).

## Real-world Applications

### 1. Analytics Systems

**Metrics Calculation:**
- Running totals
- Cumulative metrics
- Real-time aggregations
- Example: Google Analytics

### 2. Financial Systems

**Running Totals:**
- Account balances
- Transaction tracking
- Portfolio values
- Example: Banking systems

### 3. Game Development

**Score Tracking:**
- Leaderboard rankings
- Score aggregations
- Achievement tracking
- Example: Online games

### 4. Database Systems

**Query Optimization:**
- Materialized views
- Range sum indexes
- Counting queries
- Example: SQL optimization

### 5. E-commerce

**Sales Aggregation:**
- Daily/weekly sales
- Product rankings
- Inventory tracking
- Example: Amazon sales

### 6. Social Media

**Activity Metrics:**
- Post engagement
- User activity
- Trend analysis
- Example: Facebook metrics

### 7. Network Monitoring

**Traffic Analysis:**
- Bandwidth usage
- Packet counting
- Rate limiting
- Example: Network tools

### 8. Scientific Computing

**Data Analysis:**
- Cumulative distributions
- Statistical calculations
- Signal processing
- Example: Research tools

## Common Mistakes

### 1. Using 0-based Indexing

**Mistake:**
```javascript
// Using 0-based indexing
// lowbit(0) = 0, infinite loop
// Wrong results
```

**Correct:**
```javascript
// Use 1-based indexing
// Convert from 0-based
// Critical for correctness
```

**Why It Matters:**
- lowbit(0) = 0 causes infinite loop
- Fenwick Tree requires 1-based
- Must convert indices

### 2. Incorrect Lowbit Calculation

**Mistake:**
```javascript
// Wrong lowbit formula
// Navigation breaks
// Incorrect results
```

**Correct:**
```javascript
// Use x & (-x)
// Standard formula
// Works correctly
```

**Why It Matters:**
- Lowbit is core operation
- Wrong formula breaks everything
- Must use x & (-x)

### 3. Not Using Coordinate Compression

**Mistake:**
```javascript
// Large values as indices
// Memory overflow
// Slow performance
```

**Correct:**
```javascript
// Compress coordinates
// Map to 1..n
// Essential for large ranges
```

**Why It Matters:**
- Large values cause memory issues
- Compression reduces memory
- Critical for large value ranges

### 4. Off-by-one Errors

**Mistake:**
```javascript
// Wrong index conversion
// Missing +1 or -1
// Incorrect results
```

**Correct:**
```javascript
// Careful with conversions
// Test with examples
// Verify indexing
```

**Why It Matters:**
- Off-by-one errors common
- 1-based vs 0-based confusion
- Critical for correctness

### 5. Not Handling Overflow

**Mistake:**
```javascript
// Sums can overflow
// Wrong results
// Use BigInt if needed
```

**Correct:**
```javascript
// Check for overflow
// Use BigInt for large sums
// Handle appropriately
```

**Why It Matters:**
- Sums can exceed Number.MAX_SAFE_INTEGER
- Overflow causes wrong results
- Must handle large sums

### 6. Wrong Range Query

**Mistake:**
```javascript
// Not using query(r) - query(l-1)
// Wrong calculation
// Incorrect range sum
```

**Correct:**
```javascript
// Use prefix sum difference
// query(r) - query(l-1)
// Correct range sum
```

**Why It Matters:**
- Range sum requires difference
- Wrong formula gives wrong result
- Must use prefix sum difference

## Advanced Concepts

### 1. 2D Fenwick Tree

**Concept:**
Fenwick Tree for 2D arrays.

**Features:**
- Matrix range sum queries
- Point updates in 2D
- O(log m * log n) operations

### 2. Range Update Fenwick Tree

**Concept:**
Support range updates efficiently.

**Features:**
- Update range [l, r] in O(log n)
- Uses two BITs
- Difference array technique

### 3. Persistent Fenwick Tree

**Concept:**
Version control for Fenwick Tree.

**Features:**
- Query any version
- Time travel queries
- O(log n) per operation

### 4. Minimum/Maximum Fenwick Tree

**Concept:**
Store min/max instead of sum.

**Features:**
- Range minimum queries
- Point updates
- Cannot decrease values

## Practice Thinking Guide

### How to Identify When to Use Fenwick Tree

**Key Signals in Problem Statements:**

1. **"Prefix sum" or "cumulative sum"**
   - Fenwick Tree
   - Example: "Prefix sum with updates"

2. **"Range sum query" with updates**
   - Fenwick Tree
   - Example: "Dynamic range sum"

3. **"Count smaller" or "count larger"**
   - Fenwick Tree
   - Example: "Count smaller elements"

4. **"Inversion count"**
   - Fenwick Tree
   - Example: "Count inversions"

5. **"Frequency" or "ranking"**
   - Fenwick Tree
   - Example: "Rank elements"

6. **"Dynamic array" with sum queries**
   - Fenwick Tree
   - Example: "Mutable array sums"

**Pattern Recognition:**

**Pattern 1: Range Sum Query**
```
Problem: Range sum with updates
Solution: Fenwick Tree for dynamic prefix sums
```

**Pattern 2: Count Smaller Elements**
```
Problem: Count smaller elements to the right
Solution: Process from right, use Fenwick Tree
```

**Pattern 3: Inversion Counting**
```
Problem: Count pairs where i < j and nums[i] > nums[j]
Solution: Coordinate compression + Fenwick Tree
```

**Pattern 4: Frequency Counting**
```
Problem: Count frequencies dynamically
Solution: Fenwick Tree with coordinate compression
```

**Pattern 5: Ranking**
```
Problem: Rank elements dynamically
Solution: Fenwick Tree for prefix counts
```

**Decision Flowchart:**

```
Need prefix/range operations?
├─ Yes → Dynamic updates?
│        ├─ Yes → Use Fenwick Tree
│        └─ No → Use prefix sum array
├─ No → Counting problem?
│        ├─ Yes → Use Fenwick Tree with compression
│        └─ No → Consider other
└─ No → Not Fenwick Tree problem
```

**Example Problem Analysis:**

**Problem:** "Range sum query with updates"

**Analysis:**
1. Need range sum queries
2. Array is mutable (updates)
3. Prefix sum array too slow for updates
4. Fenwick Tree perfect fit
5. Solution: Fenwick Tree for dynamic prefix sums

**Problem:** "Count smaller numbers after self"

**Analysis:**
1. Need count of smaller elements to the right
2. Process from right to left
3. Track seen elements
4. Coordinate compression for values
5. Solution: Fenwick Tree with coordinate compression

**Problem:** "Count inversions in array"

**Analysis:**
1. Count pairs where i < j and nums[i] > nums[j]
2. Similar to counting smaller elements
3. Process from left to right
4. Coordinate compression
5. Solution: Fenwick Tree for inversion counting

## Summary

Fenwick Tree (Binary Indexed Tree) is a data structure that provides efficient methods for calculating and manipulating prefix sums in an array. It supports point updates and prefix sum queries in O(log n) time, which is a significant improvement over the O(n) update time of naive prefix sum arrays. The Fenwick Tree is simpler to implement than a Segment Tree and uses less memory, making it ideal for problems involving dynamic prefix sums, frequency counting, and inversion counting. The key operation is lowbit, which determines the range each index covers and enables efficient navigation.

**Key Takeaways:**
- O(log n) query and update
- Uses lowbit operation for navigation
- 1-based indexing required
- Coordinate compression for large values
- Simpler than Segment Tree
- Space efficient (O(n))
- Ideal for prefix sum problems
- Used in counting and ranking

**Mastery Checklist:**
- ✅ Understand lowbit operation
- ✅ Implement basic Fenwick Tree
- ✅ Handle point updates
- ✅ Handle prefix sum queries
- ✅ Handle range sum queries
- ✅ Use coordinate compression
- ✅ Count inversions
- ✅ Know when to use vs Segment Tree
