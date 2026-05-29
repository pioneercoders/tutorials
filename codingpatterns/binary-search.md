# Binary Search

Binary Search is an efficient algorithm used to find a target element within a sorted collection by repeatedly dividing the search space into halves.

## Introduction

Binary Search is a divide-and-conquer algorithm that searches for a target value in a sorted array by repeatedly dividing the search interval in half. If the target value is less than the middle element, the search continues in the lower half; otherwise, it continues in the upper half. This process repeats until the target is found or the search space is exhausted.

**Why Binary Search Exists:**
- Linear search is O(n) which is inefficient for large datasets
- Binary search reduces time complexity to O(log n)
- Essential for performance-critical applications
- Foundation for many advanced algorithms

**Where It Is Used:**
- Database indexing (B-tree, B+ tree)
- Search engines (inverted indices)
- Version control systems (git bisect)
- File systems (directory searches)
- Load balancers (consistent hashing)
- Pagination in web applications

## Core Concept Explanation

Binary search works on the principle of elimination. Instead of checking every element, it intelligently eliminates half of the remaining elements in each step.

**Step-by-Step Breakdown:**
1. Start with the entire sorted array
2. Find the middle element
3. Compare middle element with target
4. If match found, return index
5. If target is smaller, discard right half
6. If target is larger, discard left half
7. Repeat until found or search space empty

**Intuition Behind the Concept:**
Think of searching for a word in a dictionary. You don't start from the first page and check every word. Instead, you open the dictionary somewhere in the middle, check if your word comes before or after that page, and then narrow down to that half. This is exactly how binary search works.

**Visual Thinking:**
```
Array: [1, 3, 5, 7, 9, 11, 13, 15]
Target: 7

Step 1: Entire array
        [1, 3, 5, 7, 9, 11, 13, 15]
         ↑        mid         ↑
        left              right

Step 2: Compare arr[mid] = 9 with target = 7
        7 < 9, so search left half
        [1, 3, 5, 7]
         ↑  mid  ↑
        left   right

Step 3: Compare arr[mid] = 3 with target = 7
        7 > 3, so search right half
           [5, 7]
            ↑mid↑
           left right

Step 4: Compare arr[mid] = 5 with target = 7
        7 > 5, so search right half
              [7]
              ↑mid
             left=right

Step 5: arr[mid] = 7 == target, found!
```

## Internal Working / Logic

Binary search maintains two pointers that define the current search space: `left` (start) and `right` (end). In each iteration, it calculates the middle index and compares the middle element with the target.

**Flow Explanation:**
1. Initialize `left = 0` and `right = n - 1`
2. Calculate `mid = (left + right) / 2`
3. Compare `arr[mid]` with `target`
4. If equal: return `mid` (target found)
5. If `arr[mid] < target`: target is in right half, set `left = mid + 1`
6. If `arr[mid] > target`: target is in left half, set `right = mid - 1`
7. Repeat until `left > right` (target not found)

**Decision Making Logic:**
The key decision is which half to discard. This decision is based on the sorted property of the array:
- If array is sorted in ascending order and `arr[mid] < target`, the target must be in the right half
- If array is sorted in ascending order and `arr[mid] > target`, the target must be in the left half
- For descending order, the logic is reversed

## Algorithm / Approach

**Step-by-Step Algorithm:**

```
1. Initialize left = 0, right = n - 1
2. While left <= right:
   a. Calculate mid = (left + right) / 2
   b. If arr[mid] == target:
      Return mid (target found)
   c. If arr[mid] < target:
      left = mid + 1 (search right half)
   d. Else:
      right = mid - 1 (search left half)
3. Return -1 (target not found)
```

**Pseudocode:**

```
function binarySearch(arr, target):
    left = 0
    right = length(arr) - 1
    
    while left <= right:
        mid = floor((left + right) / 2)
        
        if arr[mid] == target:
            return mid
        else if arr[mid] < target:
            left = mid + 1
        else:
            right = mid - 1
    
    return -1
```

## Implementations

### Iterative Approach

```javascript
function binarySearch(arr, target) {
  let left = 0, right = arr.length - 1;

  while (left <= right) {
    let mid = Math.floor((left + right) / 2);

    if (arr[mid] === target) return mid;

    if (arr[mid] < target) left = mid + 1;
    else right = mid - 1;
  }

  return -1;
}
```

**Advantages:**
- O(1) space complexity
- No stack overflow risk
- Generally faster due to no function call overhead

### Recursive Approach

```javascript
function binarySearch(arr, target, left = 0, right = arr.length - 1) {
  if (left > right) return -1;

  let mid = Math.floor((left + right) / 2);

  if (arr[mid] === target) return mid;

  if (arr[mid] < target)
    return binarySearch(arr, target, mid + 1, right);
  else
    return binarySearch(arr, target, left, mid - 1);
}
```

**Advantages:**
- More elegant and readable
- Natural divide-and-conquer expression
- Easier to understand for some

**Disadvantages:**
- O(log n) space complexity due to call stack
- Risk of stack overflow for very large arrays

### Optimized Approach (Safe Mid Calculation)

```javascript
function binarySearch(arr, target) {
  let left = 0, right = arr.length - 1;

  while (left <= right) {
    // Safe mid calculation to prevent integer overflow
    let mid = left + Math.floor((right - left) / 2);

    if (arr[mid] === target) return mid;

    if (arr[mid] < target) left = mid + 1;
    else right = mid - 1;
  }

  return -1;
}
```

**Why This Optimization Matters:**
- In languages with fixed-size integers (like C++, Java), `left + right` can overflow
- `left + (right - left) / 2` is mathematically equivalent but overflow-safe
- Critical for production code handling large arrays

## Dry Run

**Example Input:**
```
arr = [2, 5, 8, 12, 16, 23, 38, 56, 72, 91]
target = 23
```

**Step-by-Step Execution:**

```
Initial State:
left = 0, right = 9
arr = [2, 5, 8, 12, 16, 23, 38, 56, 72, 91]
       0  1  2   3   4   5   6   7   8   9

Iteration 1:
mid = (0 + 9) / 2 = 4
arr[mid] = arr[4] = 16
16 < 23, so target is in right half
left = mid + 1 = 5
right = 9

Iteration 2:
left = 5, right = 9
mid = (5 + 9) / 2 = 7
arr[mid] = arr[7] = 56
56 > 23, so target is in left half
left = 5
right = mid - 1 = 6

Iteration 3:
left = 5, right = 6
mid = (5 + 6) / 2 = 5
arr[mid] = arr[5] = 23
23 == 23, target found!
Return 5
```

**Variable Changes Table:**

| Iteration | left | right | mid | arr[mid] | Comparison | Action |
|-----------|------|-------|-----|----------|------------|--------|
| 1 | 0 | 9 | 4 | 16 | 16 < 23 | left = 5 |
| 2 | 5 | 9 | 7 | 56 | 56 > 23 | right = 6 |
| 3 | 5 | 6 | 5 | 23 | 23 == 23 | return 5 |

## Edge Cases

### 1. Empty Array
```javascript
arr = [], target = 5
left = 0, right = -1
Condition left <= right is false immediately
Return -1
```

### 2. Single Element - Target Present
```javascript
arr = [5], target = 5
left = 0, right = 0
mid = 0, arr[mid] = 5 == target
Return 0
```

### 3. Single Element - Target Absent
```javascript
arr = [5], target = 3
left = 0, right = 0
mid = 0, arr[mid] = 5 > 3
right = -1
Condition left <= right is false
Return -1
```

### 4. Target at First Position
```javascript
arr = [1, 2, 3, 4, 5], target = 1
Will find in log₂(5) ≈ 3 steps
```

### 5. Target at Last Position
```javascript
arr = [1, 2, 3, 4, 5], target = 5
Will find in log₂(5) ≈ 3 steps
```

### 6. Duplicate Values
```javascript
arr = [1, 2, 2, 2, 3], target = 2
Standard binary search may return any index with value 2
Need modified logic for first/last occurrence
```

### 7. All Elements Same
```javascript
arr = [5, 5, 5, 5, 5], target = 5
Will find quickly but may not be first/last
```

### 8. Target Not in Array
```javascript
arr = [1, 3, 5, 7, 9], target = 4
Will exhaust search space and return -1
```

**Why Edge Cases Matter:**
- Empty arrays prevent index out of bounds errors
- Single elements test boundary conditions
- Duplicates require special handling for exact position
- Not-found cases must be handled gracefully
- Production code must handle all edge cases

## Variations / Extensions

### 1. First Occurrence (Lower Bound)

Find the first index where target appears in array with duplicates.

```javascript
function firstOccurrence(arr, target) {
  let left = 0, right = arr.length - 1;
  let result = -1;

  while (left <= right) {
    let mid = left + Math.floor((right - left) / 2);

    if (arr[mid] === target) {
      result = mid;
      right = mid - 1; // Continue searching left
    } else if (arr[mid] < target) {
      left = mid + 1;
    } else {
      right = mid - 1;
    }
  }

  return result;
}
```

**Use Case:** Finding the first occurrence of a user ID in logs.

### 2. Last Occurrence (Upper Bound)

Find the last index where target appears in array with duplicates.

```javascript
function lastOccurrence(arr, target) {
  let left = 0, right = arr.length - 1;
  let result = -1;

  while (left <= right) {
    let mid = left + Math.floor((right - left) / 2);

    if (arr[mid] === target) {
      result = mid;
      left = mid + 1; // Continue searching right
    } else if (arr[mid] < target) {
      left = mid + 1;
    } else {
      right = mid - 1;
    }
  }

  return result;
}
```

**Use Case:** Finding the last occurrence of an error code in logs.

### 3. Lower Bound (First Element >= Target)

Find the first element greater than or equal to target.

```javascript
function lowerBound(arr, target) {
  let left = 0, right = arr.length;

  while (left < right) {
    let mid = left + Math.floor((right - left) / 2);

    if (arr[mid] < target) {
      left = mid + 1;
    } else {
      right = mid;
    }
  }

  return left;
}
```

**Use Case:** Insert position in sorted array, finding ceiling element.

### 4. Upper Bound (First Element > Target)

Find the first element strictly greater than target.

```javascript
function upperBound(arr, target) {
  let left = 0, right = arr.length;

  while (left < right) {
    let mid = left + Math.floor((right - left) / 2);

    if (arr[mid] <= target) {
      left = mid + 1;
    } else {
      right = mid;
    }
  }

  return left;
}
```

**Use Case:** Finding floor element, counting elements less than target.

### 5. Binary Search on Answer

Instead of searching in an array, search for an optimal value in a range.

**Example: Minimum Speed to Eat Bananas**

```javascript
function minEatingSpeed(piles, h) {
  let left = 1, right = Math.max(...piles);

  while (left < right) {
    let mid = left + Math.floor((right - left) / 2);
    
    // Calculate hours needed at speed = mid
    let hours = piles.reduce((sum, pile) => sum + Math.ceil(pile / mid), 0);
    
    if (hours <= h) {
      right = mid; // Try slower speed
    } else {
      left = mid + 1; // Need faster speed
    }
  }

  return left;
}
```

**Use Cases:**
- Finding minimum/maximum capacity
- Optimizing threshold values
- Resource allocation problems
- Search space problems

### 6. Binary Search in 2D Matrix

Search in a row-wise and column-wise sorted matrix.

```javascript
function searchMatrix(matrix, target) {
  if (!matrix.length || !matrix[0].length) return false;

  let row = 0, col = matrix[0].length - 1;

  while (row < matrix.length && col >= 0) {
    if (matrix[row][col] === target) return true;
    if (matrix[row][col] > target) col--;
    else row++;
  }

  return false;
}
```

## Optimization Techniques

### 1. Time Optimization

**Branch Prediction Optimization:**
```javascript
// Less predictable branches
if (arr[mid] < target) left = mid + 1;
else right = mid - 1;

// More predictable (arr[mid] == target is rare)
if (arr[mid] === target) return mid;
if (arr[mid] < target) left = mid + 1;
else right = mid - 1;
```

**Cache-Friendly Access:**
- Binary search has poor cache locality (jumps around)
- For small arrays, linear search might be faster due to cache
- Hybrid approach: linear search for small arrays, binary for large

### 2. Space Optimization

**Iterative vs Recursive:**
- Iterative: O(1) space
- Recursive: O(log n) space
- Always prefer iterative for production code

### 3. Trade-offs

**Binary Search vs Linear Search:**

| Aspect | Binary Search | Linear Search |
|--------|---------------|---------------|
| Time Complexity | `O(log n)` | `O(n)` |
| Space Complexity | `O(1)` iterative, `O(log n)` recursive | `O(1)` |
| Prerequisite | Sorted array | None |
| Cache Locality | Poor | Excellent |
| Best For | Large sorted datasets | Small or unsorted data |

**When to Use Linear Search Instead:**
- Array size is small (n < 20)
- Data is not sorted
- Cache locality is critical
- Search is done only once

## Complexity Analysis

### Time Complexity

**Best Case: O(1)**
- Target is at the middle element in the first comparison
- Rare but possible

**Average Case: O(log n)**
- Each iteration halves the search space
- Number of iterations = log₂(n)
- For n = 1,000,000: ~20 comparisons
- For n = 1,000,000,000: ~30 comparisons

**Worst Case: O(log n)**
- Target is not present or at the ends
- Same as average case due to halving property

**Explanation:**
The logarithmic complexity comes from the halving property. Each comparison eliminates half of the remaining elements. The number of elements reduces as: n → n/2 → n/4 → n/8 → ... → 1. This takes log₂(n) steps.

### Space Complexity

**Iterative Implementation: O(1)**
- Only uses a few variables (left, right, mid)
- Constant space regardless of input size

**Recursive Implementation: O(log n)**
- Each recursive call adds to the call stack
- Maximum depth = log₂(n)
- For n = 1,000,000: ~20 stack frames

**Explanation:**
Space complexity depends on implementation. Iterative uses constant space. Recursive uses stack space proportional to recursion depth, which is log₂(n).

## Real-world Applications

### 1. Database Indexing

**B-Tree and B+ Tree:**
- Databases use B-trees for indexing
- B-tree is a generalization of binary search
- Each node can have multiple children
- Enables efficient range queries

**Example:**
```sql
-- Binary search on indexed column
SELECT * FROM users WHERE id = 12345;
-- Uses B-tree index, O(log n) lookup
```

### 2. Search Engines

**Inverted Index:**
- Search engines maintain sorted lists of document IDs
- Binary search finds documents containing a term
- Used in Google, Elasticsearch, Solr

**Example:**
- Term "binary" → [doc1, doc5, doc10, doc20, ...]
- Binary search to find intersection of multiple terms

### 3. Version Control Systems

**Git Bisect:**
- Uses binary search to find buggy commit
- Tests middle commit, discards half based on result
- Dramatically reduces debugging time

**Example:**
```bash
git bisect start
git bisect bad HEAD
git bisect good v1.0
# Git uses binary search to find bad commit
```

### 4. File Systems

**Directory Searches:**
- File systems maintain sorted directory entries
- Binary search for file lookup
- Used in NTFS, ext4, APFS

**Example:**
- Searching for "document.txt" in directory with 10,000 files
- Binary search reduces comparisons from 10,000 to ~14

### 5. Load Balancing

**Consistent Hashing:**
- Uses binary search on hash ring
- Maps requests to servers
- Used in distributed systems

**Example:**
- Hash ring: [0, 100, 200, 300, ...]
- Request hash = 150
- Binary search to find server 200

### 6. Pagination

**Offset-Based Pagination:**
- Database queries with OFFSET/LIMIT
- Binary search to find optimal page size
- Used in web applications

**Example:**
```sql
-- Binary search to find optimal LIMIT
SELECT * FROM products ORDER BY id OFFSET 10000 LIMIT 100;
```

### 7. Game Development

**Collision Detection:**
- Spatial partitioning using binary search
- Octree/Quadtree data structures
- Efficient object lookup in game world

### 8. Financial Systems

**Stock Price Lookup:**
- Time-series data stored in sorted order
- Binary search for historical prices
- Used in trading platforms

## Common Mistakes

### 1. Off-by-One Errors

**Mistake:**
```javascript
while (left < right) {  // Wrong condition
  // ...
}
```

**Correct:**
```javascript
while (left <= right) {  // Correct condition
  // ...
}
```

**Why It Matters:**
- `left < right` misses the last element
- When left == right, there's still one element to check
- Can cause target not found when it exists

### 2. Infinite Loops

**Mistake:**
```javascript
while (left <= right) {
  let mid = (left + right) / 2;
  if (arr[mid] < target) left = mid;  // Wrong: should be mid + 1
  else right = mid;  // Wrong: should be mid - 1
}
```

**Correct:**
```javascript
while (left <= right) {
  let mid = (left + right) / 2;
  if (arr[mid] < target) left = mid + 1;
  else right = mid - 1;
}
```

**Why It Matters:**
- If left = mid and arr[mid] < target, left doesn't change
- Infinite loop when target is in right half
- Must exclude mid from next search space

### 3. Integer Overflow

**Mistake:**
```javascript
let mid = (left + right) / 2;  // Can overflow
```

**Correct:**
```javascript
let mid = left + (right - left) / 2;  // Overflow-safe
```

**Why It Matters:**
- In languages with fixed-size integers (C++, Java)
- left + right can exceed maximum integer value
- Causes undefined behavior or incorrect results

### 4. Wrong Assumption About Sorted Order

**Mistake:**
```javascript
// Assuming ascending order when array is descending
if (arr[mid] < target) left = mid + 1;
```

**Correct:**
```javascript
// Check array order first
if (isAscending) {
  if (arr[mid] < target) left = mid + 1;
  else right = mid - 1;
} else {
  if (arr[mid] > target) left = mid + 1;
  else right = mid - 1;
}
```

**Why It Matters:**
- Binary search only works on sorted data
- Wrong sort order gives incorrect results
- Must verify sorted order before applying

### 5. Not Handling Duplicates

**Mistake:**
```javascript
// Standard binary search returns any occurrence
// When you need first/last occurrence
```

**Correct:**
```javascript
// Use modified binary search for first/last
function firstOccurrence(arr, target) {
  // Continue searching left after finding match
}
```

**Why It Matters:**
- Standard binary search may not return expected index
- Important for applications needing exact position
- Range queries need first/last occurrence

### 6. Incorrect Mid Calculation

**Mistake:**
```javascript
let mid = Math.floor((left + right) / 2);  // Always floor
```

**Issue:**
- Always flooring can bias search
- For some variations, ceiling might be needed

**Correct:**
```javascript
let mid = left + Math.floor((right - left) / 2);  // Standard
// Or use ceiling for specific cases
let mid = Math.ceil((left + right) / 2);
```

## Advanced Concepts

### 1. Binary Search on Answer

**Concept:**
Instead of searching for a value in an array, search for an optimal value in a continuous range.

**When to Use:**
- Problem asks for minimum/maximum value
- There's a monotonic predicate (true/false property)
- Can test if a value is "good enough"

**Example: Koko Eating Bananas**

**Problem:**
- Koko can eat k bananas per hour from a pile
- Each pile must be finished before moving to next
- Find minimum k to finish all piles in h hours

**Approach:**
```
1. Search space: k from 1 to max(piles)
2. Predicate: canFinish(k) = (hours needed <= h)
3. If canFinish(k) is true, try smaller k
4. If canFinish(k) is false, try larger k
5. Binary search for minimum k where canFinish(k) is true
```

**Implementation:**
```javascript
function minEatingSpeed(piles, h) {
  let left = 1, right = Math.max(...piles);

  while (left < right) {
    let mid = left + Math.floor((right - left) / 2);
    
    let hours = piles.reduce((sum, pile) => 
      sum + Math.ceil(pile / mid), 0);
    
    if (hours <= h) {
      right = mid;  // Try slower
    } else {
      left = mid + 1;  // Need faster
    }
  }

  return left;
}
```

### 2. Exponential Search

**Concept:**
Combines exponential search with binary search for unbounded/infinite arrays.

**When to Use:**
- Array size is unknown or infinite
- Target is likely near the beginning
- Better than binary search when target is close to start

**Algorithm:**
```
1. Start with range [0, 1]
2. Double range until arr[high] >= target
3. Apply binary search in [low, high]
```

**Implementation:**
```javascript
function exponentialSearch(arr, target) {
  if (arr[0] === target) return 0;

  let i = 1;
  while (i < arr.length && arr[i] <= target) {
    i *= 2;
  }

  return binarySearch(arr, target, i / 2, Math.min(i, arr.length - 1));
}
```

### 3. Interpolation Search

**Concept:**
Improves on binary search by using value distribution to estimate position.

**When to Use:**
- Array is uniformly distributed
- Values are numeric and evenly spaced
- Can achieve O(log log n) average case

**Algorithm:**
```
pos = low + ((target - arr[low]) * (high - low)) / (arr[high] - arr[low])
```

**Implementation:**
```javascript
function interpolationSearch(arr, target) {
  let left = 0, right = arr.length - 1;

  while (left <= right && target >= arr[left] && target <= arr[right]) {
    if (left === right) {
      if (arr[left] === target) return left;
      return -1;
    }

    let pos = left + Math.floor(
      ((target - arr[left]) * (right - left)) / (arr[right] - arr[left])
    );

    if (arr[pos] === target) return pos;
    if (arr[pos] < target) left = pos + 1;
    else right = pos - 1;
  }

  return -1;
}
```

### 4. Ternary Search

**Concept:**
Divides array into three parts instead of two.

**When to Use:**
- Searching for maximum/minimum in unimodal function
- Peak finding problems

**Algorithm:**
```
1. Divide array into three parts using two midpoints
2. Discard one-third based on comparison
3. Repeat in remaining two-thirds
```

**Implementation:**
```javascript
function ternarySearch(arr, target) {
  let left = 0, right = arr.length - 1;

  while (left <= right) {
    let mid1 = left + Math.floor((right - left) / 3);
    let mid2 = right - Math.floor((right - left) / 3);

    if (arr[mid1] === target) return mid1;
    if (arr[mid2] === target) return mid2;

    if (target < arr[mid1]) right = mid1 - 1;
    else if (target > arr[mid2]) left = mid2 + 1;
    else {
      left = mid1 + 1;
      right = mid2 - 1;
    }
  }

  return -1;
}
```

### 5. Fractional Cascading

**Concept:**
Optimizes binary search across multiple sorted arrays.

**When to Use:**
- Searching in multiple related sorted arrays
- Computational geometry problems
- Range queries

**Benefit:**
- Reduces search time from O(k log n) to O(log n + k)
- Where k is number of arrays, n is array size

## Practice Thinking Guide

### How to Identify When to Use Binary Search

**Key Signals in Problem Statements:**

1. **"Find X in sorted array/list"**
   - Direct signal for binary search
   - Example: "Find target in sorted array"

2. **"Minimum/Maximum value to achieve something"**
   - Binary search on answer
   - Example: "Minimum speed to finish task"

3. **"First/last occurrence of X"**
   - Modified binary search
   - Example: "Find first occurrence of element"

4. **"Search in range [low, high]"**
   - Binary search on answer
   - Example: "Find optimal capacity"

5. **"O(log n) time complexity required"**
   - Binary search is likely solution
   - Example: "Find in O(log n) time"

6. **"Sorted data" mentioned**
   - Binary search is applicable
   - Example: "Given sorted array..."

**Pattern Recognition:**

**Pattern 1: Exact Match in Sorted Array**
```
Problem: Find if target exists in sorted array
Solution: Standard binary search
```

**Pattern 2: First/Last Occurrence**
```
Problem: Find first/last index of target in sorted array with duplicates
Solution: Modified binary search (continue searching after match)
```

**Pattern 3: Insert Position**
```
Problem: Find where to insert target in sorted array
Solution: Lower bound binary search
```

**Pattern 4: Binary Search on Answer**
```
Problem: Find minimum/maximum value satisfying condition
Solution: Binary search on value range, test predicate
```

**Pattern 5: Peak Finding**
```
Problem: Find peak element in array
Solution: Binary search (compare mid with neighbors)
```

**Pattern 6: Rotated Sorted Array**
```
Problem: Search in rotated sorted array
Solution: Modified binary search (find rotation point first)
```

**Decision Flowchart:**

```
Is data sorted?
├─ Yes → Can we use standard binary search?
│        ├─ Yes → Use standard binary search
│        └─ No → Need modified binary search?
│                 ├─ Yes → First/last occurrence, bounds
│                 └─ No → Binary search on answer?
└─ No → Can we sort first?
         ├─ Yes → Sort + binary search (if allowed)
         └─ No → Binary search on answer?
                  ├─ Yes → Search in value range
                  └─ No → Consider other algorithms
```

**Example Problem Analysis:**

**Problem:** "Find the minimum speed to eat all bananas in h hours"

**Analysis:**
1. Not searching in array → not standard binary search
2. Looking for minimum value → binary search on answer
3. Search space: speed from 1 to max(piles)
4. Predicate: canFinish(speed) `=` (hours `<=` h)
5. Monotonic: higher speed always helps
6. Solution: Binary search on speed range

**Problem:** "Find first occurrence of target in sorted array with duplicates"

**Analysis:**
1. Data is sorted → binary search applicable
2. Need first occurrence → modified binary search
3. When found, continue searching left
4. Solution: First occurrence binary search

**Problem:** "Search in rotated sorted array"

**Analysis:**
1. Data is sorted but rotated
2. Can find rotation point with binary search
3. Then search in appropriate half
4. Solution: Modified binary search

## Summary

Binary Search is a fundamental algorithm that reduces search time from O(n) to O(log n) by repeatedly dividing the search space in half. It requires sorted data and is essential for performance-critical applications.

**Key Takeaways:**
- Always verify data is sorted before applying
- Use iterative approach for O(1) space
- Handle edge cases (empty, single element, duplicates)
- Use safe mid calculation to prevent overflow
- Understand variations (first/last, bounds, on answer)
- Recognize when to use binary search in problems
- Be aware of common mistakes (off-by-one, infinite loops)
- Consider trade-offs with linear search for small arrays

**Mastery Checklist:**
- ✅ Understand core concept and intuition
- ✅ Implement iterative and recursive versions
- ✅ Handle all edge cases correctly
- ✅ Know variations and when to use them
- ✅ Apply binary search on answer
- ✅ Recognize binary search problems
- ✅ Avoid common mistakes
- ✅ Understand complexity analysis
