# Prefix Sum

Prefix Sum is a technique that precomputes cumulative sums of array elements to answer range sum queries in O(1) time.

## Introduction

Prefix Sum is a preprocessing technique that computes cumulative sums of array elements, enabling O(1) time complexity for range sum queries. Instead of recalculating the sum for each query, we precompute prefix sums once and use them to answer any range sum query instantly. This is particularly useful when dealing with multiple range queries on the same array.

**Why Prefix Sum Exists:**
- Naive range sum: O(n) per query (sum from l to r)
- With prefix sum: O(1) per query after O(n) preprocessing
- Dramatic improvement for multiple queries
- Essential for subarray sum problems
- Foundation for many advanced algorithms

**Where It Is Used:**
- Range sum queries on arrays
- Subarray sum problems
- Equilibrium index finding
- 2D matrix range queries
- Time-series data analysis
- Financial calculations
- Image processing operations
- Game board calculations

## Core Concept Explanation

Prefix sum works by precomputing an array where each element at index i represents the sum of all elements from the start (index 0) to index i in the original array. This allows us to compute any range sum [l, r] by subtracting prefix[l-1] from prefix[r].

**Step-by-Step Breakdown:**
1. Create prefix array of size n+1 (with 0 at index 0)
2. For each element in original array:
   a. Add it to running sum
   b. Store running sum in prefix array
3. To find sum from l to r: prefix[r+1] - prefix[l]
4. This works because prefix[r+1] includes all elements up to r
5. Subtracting prefix[l] removes elements before l

**Intuition Behind the Concept:**
Think of measuring distance along a road. If you mark the distance at each kilometer marker (0km, 1km, 2km, etc.), you can find the distance between any two points by subtracting their markers. You don't need to measure the distance each time - just read the markers and subtract.

**Visual Thinking:**
```
Original Array: [2, 4, 1, 5, 3]
Index:          0  1  2  3  4

Prefix Array:  [0, 2, 6, 7, 12, 15]
Index:         0  1  2  3  4  5

prefix[0] = 0 (base case)
prefix[1] = 0 + 2 = 2
prefix[2] = 2 + 4 = 6
prefix[3] = 6 + 1 = 7
prefix[4] = 7 + 5 = 12
prefix[5] = 12 + 3 = 15

Range Sum [1, 3] = arr[1] + arr[2] + arr[3] = 4 + 1 + 5 = 10
Using prefix: prefix[4] - prefix[1] = 12 - 2 = 10 ✓

Range Sum [2, 4] = arr[2] + arr[3] + arr[4] = 1 + 5 + 3 = 9
Using prefix: prefix[5] - prefix[2] = 15 - 6 = 9 ✓
```

## Internal Working / Logic

Prefix sum operates through a single preprocessing pass followed by constant-time queries.

**Phase 1: Preprocessing**
- Initialize prefix array with 0 at index 0
- Iterate through original array
- Maintain running sum
- Store running sum at each index
- Time: O(n), Space: O(n)

**Phase 2: Query**
- To find sum from l to r:
- Return prefix[r+1] - prefix[l]
- This subtracts sum of elements before l
- Time: O(1), Space: O(1)

**Flow Explanation (Preprocessing):**
1. Initialize prefix = [0]
2. Initialize runningSum = 0
3. For each element in array:
   a. runningSum += element
   b. prefix.push(runningSum)
4. Return prefix

**Flow Explanation (Query):**
1. Given range [l, r]
2. Check if l == 0: return prefix[r+1]
3. Else: return prefix[r+1] - prefix[l]
4. Return result

**Decision Making Logic:**
The key decision is whether to use prefix sum:
- Use when multiple range sum queries on same array
- Use when finding subarrays with specific sum
- Don't use for single query (overhead not worth it)
- Don't use when array changes frequently (need to recompute)

## Algorithm / Approach

**1D Prefix Sum Algorithm**

```
1. Initialize prefix array with 0 at index 0
2. Initialize runningSum = 0
3. For i from 0 to n-1:
   a. runningSum += arr[i]
   b. prefix[i+1] = runningSum
4. Return prefix
```

**Range Sum Query Algorithm**

```
1. Given range [l, r]
2. If l == 0: return prefix[r+1]
3. Else: return prefix[r+1] - prefix[l]
4. Return result
```

**2D Prefix Sum Algorithm**

```
1. Create prefix matrix of size (m+1) x (n+1)
2. Initialize all to 0
3. For i from 1 to m:
   For j from 1 to n:
     prefix[i][j] = matrix[i-1][j-1] + 
                    prefix[i-1][j] + 
                    prefix[i][j-1] - 
                    prefix[i-1][j-1]
4. Return prefix
```

**2D Range Sum Query Algorithm**

```
1. Given rectangle (row1, col1) to (row2, col2)
2. sum = prefix[row2+1][col2+1] - 
3.        prefix[row1][col2+1] - 
4.        prefix[row2+1][col1] + 
5.        prefix[row1][col1]
6. Return sum
```

## Implementations

### 1. Basic Prefix Sum

```javascript
function prefixSum(arr) {
  const prefix = [0];
  let runningSum = 0;
  
  for (let i = 0; i < arr.length; i++) {
    runningSum += arr[i];
    prefix.push(runningSum);
  }
  
  return prefix;
}

function rangeSum(prefix, l, r) {
  return prefix[r + 1] - prefix[l];
}
```

**Advantages:**
- O(n) preprocessing, O(1) per query
- Simple to implement
- Handles any numeric array

### 2. Subarray Sum Equals K

```javascript
function subarraySumEqualsK(arr, k) {
  let count = 0;
  let prefixSum = 0;
  const sumMap = new Map([[0, 1]]);
  
  for (const num of arr) {
    prefixSum += num;
    
    if (sumMap.has(prefixSum - k)) {
      count += sumMap.get(prefixSum - k);
    }
    
    sumMap.set(prefixSum, (sumMap.get(prefixSum) || 0) + 1);
  }
  
  return count;
}
```

**State Definition:**
- Track running prefix sum
- Use hash map to store prefix sum frequencies
- If (prefixSum - k) exists, subarray with sum k exists

### 3. Find Pivot Index

```javascript
function pivotIndex(nums) {
  const totalSum = nums.reduce((a, b) => a + b, 0);
  let leftSum = 0;
  
  for (let i = 0; i < nums.length; i++) {
    if (leftSum === totalSum - leftSum - nums[i]) {
      return i;
    }
    leftSum += nums[i];
  }
  
  return -1;
}
```

**Advantages:**
- O(n) time, O(1) space
- Single pass through array
- No extra prefix array needed

### 4. 2D Prefix Sum

```javascript
function prefixSum2D(matrix) {
  const m = matrix.length;
  const n = matrix[0].length;
  const prefix = Array(m + 1).fill().map(() => Array(n + 1).fill(0));
  
  for (let i = 1; i <= m; i++) {
    for (let j = 1; j <= n; j++) {
      prefix[i][j] = matrix[i - 1][j - 1] + 
                      prefix[i - 1][j] + 
                      prefix[i][j - 1] - 
                      prefix[i - 1][j - 1];
    }
  }
  
  return prefix;
}

function rangeSum2D(prefix, row1, col1, row2, col2) {
  return prefix[row2 + 1][col2 + 1] - 
         prefix[row1][col2 + 1] - 
         prefix[row2 + 1][col1] + 
         prefix[row1][col1];
}
```

**Advantages:**
- O(mn) preprocessing, O(1) per query
- Handles 2D range queries efficiently
- Used in image processing, game boards

### 5. Product of Array Except Self

```javascript
function productExceptSelf(nums) {
  const n = nums.length;
  const left = new Array(n);
  const right = new Array(n);
  const result = new Array(n);
  
  // Left prefix products
  left[0] = 1;
  for (let i = 1; i < n; i++) {
    left[i] = left[i - 1] * nums[i - 1];
  }
  
  // Right prefix products
  right[n - 1] = 1;
  for (let i = n - 2; i >= 0; i--) {
    right[i] = right[i + 1] * nums[i + 1];
  }
  
  // Result
  for (let i = 0; i < n; i++) {
    result[i] = left[i] * right[i];
  }
  
  return result;
}
```

### 6. Maximum Size Subarray Sum Equals K

```javascript
function maxSubArrayLen(nums, k) {
  const sumMap = new Map([[0, -1]]);
  let maxLen = 0;
  let prefixSum = 0;
  
  for (let i = 0; i < nums.length; i++) {
    prefixSum += nums[i];
    
    if (sumMap.has(prefixSum - k)) {
      maxLen = Math.max(maxLen, i - sumMap.get(prefixSum - k));
    }
    
    if (!sumMap.has(prefixSum)) {
      sumMap.set(prefixSum, i);
    }
  }
  
  return maxLen;
}
```

## Dry Run

**Example: Basic Prefix Sum**

**Input:**
```
arr = [2, 4, 1, 5, 3]
```

**Step-by-Step Execution:**

```
Initial State:
prefix = [0]
runningSum = 0

Iteration 1 (i = 0):
arr[0] = 2
runningSum = 0 + 2 = 2
prefix.push(2)
prefix = [0, 2]

Iteration 2 (i = 1):
arr[1] = 4
runningSum = 2 + 4 = 6
prefix.push(6)
prefix = [0, 2, 6]

Iteration 3 (i = 2):
arr[2] = 1
runningSum = 6 + 1 = 7
prefix.push(7)
prefix = [0, 2, 6, 7]

Iteration 4 (i = 3):
arr[3] = 5
runningSum = 7 + 5 = 12
prefix.push(12)
prefix = [0, 2, 6, 7, 12]

Iteration 5 (i = 4):
arr[4] = 3
runningSum = 12 + 3 = 15
prefix.push(15)
prefix = [0, 2, 6, 7, 12, 15]

Query: sum from index 1 to 3
rangeSum(prefix, 1, 3) = prefix[4] - prefix[1] = 12 - 2 = 10
Verify: arr[1] + arr[2] + arr[3] = 4 + 1 + 5 = 10 ✓
```

**Variable Changes Table:**

| Iteration | i | arr[i] | runningSum | prefix (after) |
|-----------|---|---------|------------|----------------|
| Initial | - | - | 0 | [0] |
| 1 | 0 | 2 | 2 | [0, 2] |
| 2 | 1 | 4 | 6 | [0, 2, 6] |
| 3 | 2 | 1 | 7 | [0, 2, 6, 7] |
| 4 | 3 | 5 | 12 | [0, 2, 6, 7, 12] |
| 5 | 4 | 3 | 15 | [0, 2, 6, 7, 12, 15] |

## Edge Cases

### 1. Empty Array
```javascript
arr = []
prefix = [0]
rangeSum(prefix, 0, 0) = prefix[1] - prefix[0] = 0 - 0 = 0
```

### 2. Single Element
```javascript
arr = [5]
prefix = [0, 5]
rangeSum(prefix, 0, 0) = prefix[1] - prefix[0] = 5 - 0 = 5
```

### 3. Negative Numbers
```javascript
arr = [-2, 3, -1, 4]
prefix = [0, -2, 1, 0, 4]
rangeSum(prefix, 1, 2) = prefix[3] - prefix[1] = 0 - (-2) = 2
Verify: arr[1] + arr[2] = 3 + (-1) = 2 ✓
```

### 4. All Zeros
```javascript
arr = [0, 0, 0, 0]
prefix = [0, 0, 0, 0, 0]
All range sums are 0
```

### 5. Large Numbers (Overflow)
```javascript
arr = [Number.MAX_SAFE_INTEGER, 1]
prefix = [0, MAX, MAX+1] (overflow!)
Use BigInt or modular arithmetic
```

### 6. Query Out of Bounds
```javascript
prefix = [0, 2, 6, 7]
rangeSum(prefix, 0, 5) → Index out of bounds
Must validate indices before query
```

**Why Edge Cases Matter:**
- Empty arrays prevent index errors
- Single elements test boundary conditions
- Negative numbers test algorithm correctness
- Large numbers test overflow handling
- Out of bounds queries need validation

## Variations / Extensions

### 1. Difference Array

```javascript
class DifferenceArray {
  constructor(arr) {
    this.diff = new Array(arr.length + 1).fill(0);
    this.diff[0] = arr[0];
    for (let i = 1; i < arr.length; i++) {
      this.diff[i] = arr[i] - arr[i - 1];
    }
  }
  
  update(l, r, val) {
    this.diff[l] += val;
    this.diff[r + 1] -= val;
  }
  
  getResult() {
    const result = new Array(this.diff.length - 1);
    result[0] = this.diff[0];
    for (let i = 1; i < result.length; i++) {
      result[i] = result[i - 1] + this.diff[i];
    }
    return result;
  }
}
```

### 2. Prefix Sum with Modulo

```javascript
function prefixSumMod(arr, mod) {
  const prefix = [0];
  let runningSum = 0;
  
  for (const num of arr) {
    runningSum = (runningSum + num) % mod;
    prefix.push(runningSum);
  }
  
  return prefix;
}
```

### 3. Prefix XOR

```javascript
function prefixXOR(arr) {
  const prefix = [0];
  let runningXOR = 0;
  
  for (const num of arr) {
    runningXOR ^= num;
    prefix.push(runningXOR);
  }
  
  return prefix;
}

function rangeXOR(prefix, l, r) {
  return prefix[r + 1] ^ prefix[l];
}
```

### 4. Prefix Minimum/Maximum

```javascript
function prefixMin(arr) {
  const prefix = [arr[0]];
  for (let i = 1; i < arr.length; i++) {
    prefix.push(Math.min(prefix[i - 1], arr[i]));
  }
  return prefix;
}

function prefixMax(arr) {
  const prefix = [arr[0]];
  for (let i = 1; i < arr.length; i++) {
    prefix.push(Math.max(prefix[i - 1], arr[i]));
  }
  return prefix;
}
```

### 5. Running Average

```javascript
function runningAverage(arr, k) {
  const result = [];
  let windowSum = 0;
  
  for (let i = 0; i < arr.length; i++) {
    windowSum += arr[i];
    
    if (i >= k - 1) {
      result.push(windowSum / k);
      windowSum -= arr[i - k + 1];
    }
  }
  
  return result;
}
```

## Optimization Techniques

### 1. Space Optimization

**In-Place Prefix Sum:**
```javascript
// Use input array for prefix sum
for (let i = 1; i < arr.length; i++) {
  arr[i] += arr[i - 1];
}
// arr now contains prefix sums
```

### 2. Time Optimization

**Lazy Computation:**
```javascript
// Only compute prefix sums when needed
// Cache results for repeated queries
```

### 3. Trade-offs

**Prefix Sum vs Brute Force:**

| Aspect | Prefix Sum | Brute Force |
|--------|------------|-------------|
| Preprocessing | `O(n)` | `O(1)` |
| Per Query | `O(1)` | `O(n)` |
| Space | `O(n)` | `O(1)` |
| Best For | Multiple queries | Single query |
| Dynamic Updates | `O(n)` to update | `O(1)` |

**When to Use Brute Force Instead:**
- Single query only
- Array changes frequently
- Memory constraints
- Small array size

## Complexity Analysis

### Time Complexity

**Preprocessing: O(n)**
- Single pass through array
- Each element processed once
- Example: Building prefix array

**Query: O(1)**
- Constant time subtraction
- No traversal needed
- Example: Range sum query

**Multiple Queries: O(n + q)**
- n = array size, q = number of queries
- O(n) preprocessing + O(q) queries
- Much better than O(nq) brute force

**Update: O(n)**
- Need to recompute prefix array
- Affects all subsequent indices
- Example: Updating array element

### Space Complexity

**1D Prefix Sum: O(n)**
- Store n+1 prefix values
- Linear space overhead
- Example: Standard prefix array

**2D Prefix Sum: O(mn)**
- Store (m+1) x (n+1) prefix matrix
- Quadratic space overhead
- Example: Matrix prefix sum

**In-Place: O(1)**
- Modify input array
- No extra space
- Example: In-place prefix sum

**Explanation:**
Prefix sum trades O(n) space for O(1) query time. This is beneficial when multiple queries are needed. Space is linear for 1D, quadratic for 2D. In-place optimization can reduce space to O(1).

## Real-world Applications

### 1. Financial Analysis

**Transaction Summaries:**
- Calculate total over time periods
- Daily/weekly/monthly totals
- Example: Banking transactions

### 2. Time-Series Data

**Data Aggregation:**
- Calculate running totals
- Moving averages
- Example: Stock prices, sensor data

### 3. Log Analysis

**Error Counting:**
- Count errors in time windows
- Aggregate statistics
- Example: Server logs, application logs

### 4. Image Processing

**Region Sum Calculation:**
- Sum pixel values in regions
- Image filters
- Example: Computer vision applications

### 5. Game Development

**Board Calculations:**
- Calculate scores in regions
- Pathfinding costs
- Example: Strategy games, puzzles

### 6. Network Monitoring

**Bandwidth Usage:**
- Calculate total data transfer
- Time-window statistics
- Example: Network traffic analysis

### 7. Scientific Computing

**Data Integration:**
- Numerical integration
- Cumulative calculations
- Example: Physics simulations

### 8. Database Systems

**Range Queries:**
- Efficient range sum queries
- OLAP operations
- Example: Data warehousing

## Common Mistakes

### 1. Off-by-One Errors

**Mistake:**
```javascript
// Wrong indexing
prefix[i] = prefix[i-1] + arr[i]; // Missing +1
```

**Correct:**
```javascript
// Correct indexing
prefix[i+1] = prefix[i] + arr[i];
```

**Why It Matters:**
- Off-by-one causes wrong results
- Range queries return incorrect sums
- Must be careful with indices

### 2. Not Handling Empty Array

**Mistake:**
```javascript
// Not checking for empty array
for (let i = 0; i < arr.length; i++) { // May not execute
```

**Correct:**
```javascript
// Handle empty array
if (arr.length === 0) return [0];
```

**Why It Matters:**
- Empty arrays cause edge cases
- Must handle gracefully
- Prevents index errors

### 3. Integer Overflow

**Mistake:**
```javascript
// Not handling overflow
runningSum += num; // May overflow
```

**Correct:**
```javascript
// Use BigInt or modular arithmetic
runningSum = (runningSum + num) % MOD;
```

**Why It Matters:**
- Large numbers cause overflow
- Results become incorrect
- Must handle appropriately

### 4. Wrong 2D Formula

**Mistake:**
```javascript
// Wrong 2D prefix sum formula
prefix[i][j] = matrix[i][j] + prefix[i-1][j] + prefix[i][j-1];
```

**Correct:**
```javascript
// Correct 2D prefix sum formula
prefix[i][j] = matrix[i-1][j-1] + 
                prefix[i-1][j] + 
                prefix[i][j-1] - 
                prefix[i-1][j-1];
```

**Why It Matters:**
- Wrong formula gives incorrect results
- Must subtract overlap twice
- Critical for 2D queries

### 5. Not Recomputing After Update

**Mistake:**
```javascript
// Not recomputing after array update
arr[0] = 100;
// prefix array is now stale!
```

**Correct:**
```javascript
// Recompute prefix after update
arr[0] = 100;
prefix = prefixSum(arr);
```

**Why It Matters:**
- Prefix becomes stale after update
- Queries return wrong results
- Must recompute after changes

### 6. Using for Single Query

**Mistake:**
```javascript
// Using prefix sum for single query
prefix = prefixSum(arr);
sum = rangeSum(prefix, l, r); // Overkill
```

**Correct:**
```javascript
// Direct sum for single query
sum = 0;
for (let i = l; i <= r; i++) {
  sum += arr[i];
}
```

**Why It Matters:**
- O(n) overhead for single query
- Not worth the preprocessing cost
- Use only for multiple queries

## Advanced Concepts

### 1. Fenwick Tree (Binary Indexed Tree)

**Concept:**
Data structure for efficient prefix sums and updates.

**Features:**
- O(log n) updates and queries
- Better than prefix sum for dynamic arrays
- Used in competitive programming

### 2. Segment Tree

**Concept:**
Tree structure for range queries and updates.

**Features:**
- O(log n) updates and queries
- Supports range minimum/maximum
- More flexible than prefix sum

### 3. Sparse Table

**Concept:**
Precompute answers for all ranges of size 2^k.

**Features:**
- O(1) range minimum queries
- O(n log n) preprocessing
- Static arrays only

### 4. Mo's Algorithm

**Concept:**
Process range queries in optimal order.

**Features:**
- O((n+q)√n) for offline queries
- Used for complex range queries
- Minimizes pointer movement

## Practice Thinking Guide

### How to Identify When to Use Prefix Sum

**Key Signals in Problem Statements:**

1. **"Sum of elements from l to r"**
   - Multiple range sum queries
   - Example: "Range sum query"

2. **"Subarray with sum K"**
   - Find subarrays with specific sum
   - Example: "Subarray sum equals K"

3. **"Equilibrium index"**
   - Index where left sum equals right sum
   - Example: "Find pivot index"

4. **"Product except self"**
   - Product of all elements except current
   - Example: "Product of array except self"

5. **"Matrix region sum"**
   - Sum of elements in matrix region
   - Example: "Range sum query 2D"

6. **"Running total/average"**
   - Calculate running statistics
   - Example: "Moving average"

**Pattern Recognition:**

**Pattern 1: Range Sum**
```
Problem: Sum of elements in range
Solution: 1D prefix sum
```

**Pattern 2: Subarray Sum**
```
Problem: Subarray with specific sum
Solution: Prefix sum with hash map
```

**Pattern 3: Equilibrium**
```
Problem: Balance point in array
Solution: Total sum - left sum
```

**Pattern 4: Matrix Region**
```
Problem: Sum in matrix region
Solution: 2D prefix sum
```

**Pattern 5: Product Except Self**
```
Problem: Product except current
Solution: Left and right prefix products
```

**Decision Flowchart:**

```
Need range sum queries?
├─ Yes → Multiple queries on same array?
│        ├─ Yes → Use prefix sum
│        └─ No → Use direct sum
├─ No → Need subarray with sum K?
│        ├─ Yes → Prefix sum + hash map
│        └─ No → Consider other approach
└─ No → Not prefix sum problem
```

**Example Problem Analysis:**

**Problem:** "Sum of elements from index l to r"

**Analysis:**
1. Need range sum queries
2. Multiple queries expected
3. Prefix sum provides O(1) per query
4. O(n) preprocessing acceptable
5. Solution: 1D prefix sum

**Problem:** "Find subarray with sum K"

**Analysis:**
1. Need to find subarray with specific sum
2. Use prefix sum to track running sum
3. If (prefixSum - K) exists, subarray exists
4. Use hash map to store prefix sums
5. Solution: Prefix sum with hash map

**Problem:** "Sum of elements in matrix region"

**Analysis:**
1. Need 2D range sum
2. Multiple queries expected
3. 2D prefix sum provides O(1) per query
4. O(mn) preprocessing acceptable
5. Solution: 2D prefix sum

## Summary

Prefix Sum is a powerful preprocessing technique that enables O(1) range sum queries after O(n) preprocessing. It's essential for problems involving multiple range queries, subarray sums, and equilibrium indices. Understanding the formula and handling edge cases is crucial for correct implementation.

**Key Takeaways:**
- O(n) preprocessing, O(1) per query
- Trade space for time efficiency
- Handle off-by-one errors carefully
- Works with 1D and 2D arrays
- Use hash map for subarray sum problems
- Recompute after array updates
- Not worth it for single query

**Mastery Checklist:**
- ✅ Understand prefix sum formula
- ✅ Implement 1D prefix sum
- ✅ Implement 2D prefix sum
- ✅ Solve subarray sum with hash map
- ✅ Find equilibrium index
- ✅ Handle off-by-one errors
- ✅ Use prefix products/XOR
- ✅ Choose appropriate data structure

