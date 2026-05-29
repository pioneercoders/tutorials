# Two Pointers

Two Pointers is a technique where two pointers traverse a data structure simultaneously, often from opposite ends or at different speeds. This avoids nested loops, reducing time complexity from O(n²) to O(n).

## Introduction

Two Pointers is a powerful algorithmic technique that uses two pointers to traverse a data structure simultaneously. Instead of using nested loops (which gives O(n²) complexity), two pointers can often solve the same problem in O(n) time by intelligently moving the pointers based on the problem constraints.

**Why Two Pointers Exists:**
- Nested loops are inefficient for large datasets (O(n²))
- Many problems can be solved with a single pass using two pointers
- Enables in-place operations without extra space
- Essential for memory-constrained environments
- Foundation for many advanced algorithms

**Where It Is Used:**
- Finding pairs/triplets with specific sums
- Removing duplicates from sorted arrays
- Detecting cycles in linked lists
- Merging sorted arrays/lists
- Finding subarrays with specific properties
- Partitioning arrays (quick sort)
- Palindrome checking
- Sliding window problems

## Core Concept Explanation

Two pointers work by maintaining two indices that move through the data structure based on specific conditions. The key insight is that we can often eliminate large portions of the search space by moving one or both pointers intelligently.

**Step-by-Step Breakdown:**
1. Initialize two pointers at specific positions
2. Process elements at both pointer positions
3. Compare or combine elements based on problem requirements
4. Move one or both pointers based on the result
5. Repeat until pointers meet or condition is satisfied

**Intuition Behind the Concept:**
Think of searching for a pair of numbers that sum to a target in a sorted array. Instead of checking every pair (nested loops), you can start with the smallest and largest numbers. If their sum is too small, you need a larger sum, so move the left pointer right. If their sum is too large, move the right pointer left. This way, you eliminate half the possibilities in each step.

**Visual Thinking:**
```
Array: [1, 2, 3, 4, 5, 6, 7, 8, 9]
Target: 10

Opposite Direction Pointers:
[1, 2, 3, 4, 5, 6, 7, 8, 9]
 ↑                   ↑
left               right

Sum = 1 + 9 = 10, found!

Same Direction Pointers (Slow-Fast):
[1, 2, 2, 3, 3, 4, 5]
 ↑  ↑
slow fast

If arr[fast] != arr[slow], move slow, copy value
[1, 2, 2, 3, 3, 4, 5]
    ↑     ↑
   slow  fast
```

## Internal Working / Logic

Two pointers can operate in three main patterns, each with different movement logic:

**Pattern 1: Opposite Direction Pointers**
- Start with `left = 0` and `right = n - 1`
- Move pointers toward each other
- Stop when `left >= right`
- Used for: finding pairs, checking palindromes, container problems

**Pattern 2: Same Direction Pointers (Fast-Slow)**
- Start both at same position or different positions
- Fast pointer moves faster (2 steps vs 1 step)
- Used for: cycle detection, finding middle element
- Stop when fast reaches end or meets slow

**Pattern 3: Same Direction Pointers (Slow-Fast for In-Place)**
- Slow pointer tracks valid position
- Fast pointer scans ahead
- Used for: removing duplicates, partitioning
- Stop when fast reaches end

**Flow Explanation (Opposite Direction):**
1. Initialize `left = 0`, `right = n - 1`
2. Calculate value using `arr[left]` and `arr[right]`
3. Compare with target or condition
4. If condition met: process and move both pointers
5. If value too small: move `left` right (increase value)
6. If value too large: move `right` left (decrease value)
7. Repeat until `left >= right`

**Decision Making Logic:**
The key decision is which pointer to move. This depends on:
- For sorted arrays: move based on whether current value is too small or too large
- For in-place operations: move fast always, move slow only when condition met
- For cycle detection: move fast 2 steps, slow 1 step until they meet

## Algorithm / Approach

**Pattern 1: Opposite Direction Algorithm**

```
1. Initialize left = 0, right = n - 1
2. While left < right:
   a. Calculate value = f(arr[left], arr[right])
   b. If value == target:
      Process result
      Move both pointers
   c. If value < target:
      left = left + 1 (increase value)
   d. If value > target:
      right = right - 1 (decrease value)
3. Return result
```

**Pattern 2: Fast-Slow Algorithm**

```
1. Initialize slow = head, fast = head
2. While fast and fast.next:
   a. slow = slow.next
   b. fast = fast.next.next
   c. If slow == fast:
      Return true (cycle detected)
3. Return false (no cycle)
```

**Pattern 3: In-Place Algorithm**

```
1. Initialize slow = 0
2. For fast from 1 to n-1:
   a. If condition(arr[fast], arr[slow]) is true:
      slow = slow + 1
      arr[slow] = arr[fast]
3. Return slow + 1 (new length)
```

## Implementations

### 1. Two Sum II - Sorted Array (Opposite Direction)

```javascript
function twoSumSorted(arr, target) {
  let left = 0, right = arr.length - 1;
  
  while (left < right) {
    const sum = arr[left] + arr[right];
    
    if (sum === target) {
      return [left + 1, right + 1]; // 1-indexed
    } else if (sum < target) {
      left++;
    } else {
      right--;
    }
  }
  
  return [];
}
```

**Advantages:**
- O(n) time, O(1) space
- No hash map needed
- Works with sorted input

### 2. Remove Duplicates from Sorted Array (In-Place)

```javascript
function removeDuplicates(arr) {
  if (arr.length === 0) return 0;
  
  let slow = 0;
  for (let fast = 1; fast < arr.length; fast++) {
    if (arr[fast] !== arr[slow]) {
      slow++;
      arr[slow] = arr[fast];
    }
  }
  
  return slow + 1;
}
```

**Advantages:**
- O(n) time, O(1) space
- In-place modification
- Preserves order

### 3. Detect Cycle in Linked List (Fast-Slow)

```javascript
function hasCycle(head) {
  let slow = head, fast = head;
  
  while (fast && fast.next) {
    slow = slow.next;
    fast = fast.next.next;
    
    if (slow === fast) {
      return true; // Cycle detected
    }
  }
  
  return false; // No cycle
}
```

**Advantages:**
- O(n) time, O(1) space
- No extra memory needed
- Floyd's cycle detection algorithm

### 4. Container With Most Water (Opposite Direction)

```javascript
function maxArea(height) {
  let left = 0, right = height.length - 1;
  let maxArea = 0;
  
  while (left < right) {
    const width = right - left;
    const h = Math.min(height[left], height[right]);
    maxArea = Math.max(maxArea, width * h);
    
    // Move the pointer with smaller height
    if (height[left] < height[right]) {
      left++;
    } else {
      right--;
    }
  }
  
  return maxArea;
}
```

**Advantages:**
- O(n) time, O(1) space
- Greedy approach works
- Eliminates unnecessary checks

### 5. 3Sum (Combination of Sort + Two Pointers)

```javascript
function threeSum(nums) {
  nums.sort((a, b) => a - b);
  const result = [];
  
  for (let i = 0; i < nums.length - 2; i++) {
    // Skip duplicates for first element
    if (i > 0 && nums[i] === nums[i - 1]) continue;
    
    let left = i + 1, right = nums.length - 1;
    
    while (left < right) {
      const sum = nums[i] + nums[left] + nums[right];
      
      if (sum === 0) {
        result.push([nums[i], nums[left], nums[right]]);
        
        // Skip duplicates
        while (left < right && nums[left] === nums[left + 1]) left++;
        while (left < right && nums[right] === nums[right - 1]) right--;
        
        left++;
        right--;
      } else if (sum < 0) {
        left++;
      } else {
        right--;
      }
    }
  }
  
  return result;
}
```

**Advantages:**
- O(n²) time, O(1) space (excluding output)
- Better than O(n³) brute force
- Handles duplicates correctly

## Dry Run

**Example: Two Sum in Sorted Array**

**Input:**
```
arr = [2, 7, 11, 15]
target = 9
```

**Step-by-Step Execution:**

```
Initial State:
left = 0, right = 3
arr = [2, 7, 11, 15]
       0  1   2   3

Iteration 1:
arr[left] = arr[0] = 2
arr[right] = arr[3] = 15
sum = 2 + 15 = 17
17 > 9, so move right left
right = 2

Iteration 2:
left = 0, right = 2
arr[left] = arr[0] = 2
arr[right] = arr[2] = 11
sum = 2 + 11 = 13
13 > 9, so move right left
right = 1

Iteration 3:
left = 0, right = 1
arr[left] = arr[0] = 2
arr[right] = arr[1] = 7
sum = 2 + 7 = 9
9 == 9, found!
Return [0, 1]
```

**Variable Changes Table:**

| Iteration | left | right | arr[left] | arr[right] | sum | Comparison | Action |
|-----------|------|-------|-----------|------------|-----|------------|--------|
| 1 | 0 | 3 | 2 | 15 | 17 | 17 > 9 | right = 2 |
| 2 | 0 | 2 | 2 | 11 | 13 | 13 > 9 | right = 1 |
| 3 | 0 | 1 | 2 | 7 | 9 | 9 == 9 | return [0,1] |

## Edge Cases

### 1. Empty Array
```javascript
arr = [], target = 5
left = 0, right = -1
Condition left < right is false immediately
Return []
```

### 2. Single Element
```javascript
arr = [5], target = 10
left = 0, right = 0
Condition left < right is false immediately
Return []
```

### 3. No Valid Solution
```javascript
arr = [1, 2, 3], target = 100
Will exhaust all possibilities
Return []
```

### 4. All Identical Elements
```javascript
arr = [5, 5, 5, 5], target = 10
Will find first pair (0, 3)
Need to handle duplicates if unique pairs required
```

### 5. Negative Numbers
```javascript
arr = [-5, -3, 0, 2, 4], target = -1
Algorithm works correctly with negatives
Will find (-5, 4) or (-3, 2)
```

### 6. Target at Edges
```javascript
arr = [1, 2, 3, 4, 5], target = 6
Will find (1, 5) or (2, 4)
```

### 7. Duplicates in 3Sum
```javascript
arr = [-1, -1, 0, 1, 1]
Must skip duplicates to avoid duplicate triplets
```

**Why Edge Cases Matter:**
- Empty/single element arrays prevent index errors
- No solution cases must return appropriate values
- Duplicates require special handling for unique results
- Negative numbers test algorithm correctness
- Edge targets test boundary conditions

## Variations / Extensions

### 1. Valid Palindrome (Opposite Direction)

Check if string reads same forwards and backwards.

```javascript
function isPalindrome(s) {
  let left = 0, right = s.length - 1;
  
  while (left < right) {
    // Skip non-alphanumeric
    while (left < right && !isAlphaNumeric(s[left])) left++;
    while (left < right && !isAlphaNumeric(s[right])) right--;
    
    if (s[left].toLowerCase() !== s[right].toLowerCase()) {
      return false;
    }
    
    left++;
    right--;
  }
  
  return true;
}
```

### 2. Merge Sorted Arrays (Same Direction)

Merge two sorted arrays into one sorted array.

```javascript
function mergeArrays(arr1, arr2) {
  const result = [];
  let i = 0, j = 0;
  
  while (i < arr1.length && j < arr2.length) {
    if (arr1[i] <= arr2[j]) {
      result.push(arr1[i++]);
    } else {
      result.push(arr2[j++]);
    }
  }
  
  // Add remaining elements
  while (i < arr1.length) result.push(arr1[i++]);
  while (j < arr2.length) result.push(arr2[j++]);
  
  return result;
}
```

### 3. Find Middle of Linked List (Fast-Slow)

```javascript
function findMiddle(head) {
  let slow = head, fast = head;
  
  while (fast && fast.next) {
    slow = slow.next;
    fast = fast.next.next;
  }
  
  return slow; // Middle node
}
```

### 4. Partition Array (Dutch National Flag)

Partition array around a pivot value.

```javascript
function partition(arr, pivot) {
  let left = 0, right = arr.length - 1;
  
  while (left <= right) {
    while (left <= right && arr[left] < pivot) left++;
    while (left <= right && arr[right] >= pivot) right--;
    
    if (left <= right) {
      [arr[left], arr[right]] = [arr[right], arr[left]];
      left++;
      right--;
    }
  }
  
  return left; // Partition point
}
```

### 5. Move Zeroes (In-Place)

Move all zeroes to end while maintaining order.

```javascript
function moveZeroes(arr) {
  let slow = 0;
  
  for (let fast = 0; fast < arr.length; fast++) {
    if (arr[fast] !== 0) {
      [arr[slow], arr[fast]] = [arr[fast], arr[slow]];
      slow++;
    }
  }
}
```

### 6. Find Cycle Start Point

After detecting a cycle, find where it starts.

```javascript
function findCycleStart(head) {
  let slow = head, fast = head;
  
  // Detect cycle
  while (fast && fast.next) {
    slow = slow.next;
    fast = fast.next.next;
    if (slow === fast) break;
  }
  
  if (!fast || !fast.next) return null; // No cycle
  
  // Find start
  slow = head;
  while (slow !== fast) {
    slow = slow.next;
    fast = fast.next;
  }
  
  return slow;
}
```

## Optimization Techniques

### 1. Time Optimization

**Early Termination:**
```javascript
// Stop early if target found
while (left < right) {
  if (arr[left] + arr[right] === target) {
    return [left, right]; // Early return
  }
  // ...
}
```

**Skip Duplicates:**
```javascript
// Skip duplicate values to avoid redundant work
while (left < right && nums[left] === nums[left + 1]) left++;
while (left < right && nums[right] === nums[right - 1]) right--;
```

### 2. Space Optimization

**In-Place Operations:**
- Use slow-fast pattern for in-place modifications
- Avoid creating new arrays when possible
- Reuse input array for output

### 3. Trade-offs

**Two Pointers vs Hash Map:**

| Aspect | Two Pointers | Hash Map |
|--------|--------------|----------|
| Time Complexity | `O(n)` or `O(n log n)` with sort | `O(n)` |
| Space Complexity | `O(1)` | `O(n)` |
| Requires Sorting | Often yes | No |
| Preserves Order | Yes | No |
| Best For | Sorted data, in-place ops | Unsorted data, frequency counting |

**When to Use Hash Map Instead:**
- Data is unsorted and sorting is expensive
- Need frequency counts
- Need to store additional information
- Order doesn't matter

## Complexity Analysis

### Time Complexity

**Opposite Direction: O(n)**
- Each pointer moves at most n times
- Total operations: 2n = O(n)
- Example: Two Sum, Container With Most Water

**Fast-Slow: O(n)**
- Fast pointer moves 2n times, slow moves n times
- Total operations: 3n = O(n)
- Example: Cycle detection, Find middle

**In-Place: O(n)**
- Fast pointer traverses once, slow moves at most n times
- Total operations: 2n = O(n)
- Example: Remove duplicates, Move zeroes

**With Sorting: O(n log n)**
- Sorting dominates: O(n log n)
- Two pointers: O(n)
- Total: O(n log n) + O(n) = O(n log n)
- Example: 3Sum, 4Sum

### Space Complexity

**Iterative: O(1)**
- Only uses a few pointer variables
- Constant space regardless of input size
- Most two pointer solutions are O(1)

**With Sorting: O(n) or O(log n)**
- Depends on sorting algorithm
- Quick sort: O(log n) stack space
- Merge sort: O(n) auxiliary space
- In-place sort: O(1) or O(log n)

**Explanation:**
Two pointers excel in space efficiency because they only maintain indices, not additional data structures. This makes them ideal for memory-constrained environments.

## Real-world Applications

### 1. Database Operations

**Merge Join:**
- Databases use two pointers to merge sorted tables
- Used in SQL join operations
- More efficient than nested loop joins for large datasets

**Example:**
```sql
-- Merge join uses two-pointer technique
SELECT * FROM orders o, customers c
WHERE o.customer_id = c.id
-- Both tables sorted by customer_id
```

### 2. Data Compression

**Run-Length Encoding:**
- Use two pointers to count consecutive identical elements
- Used in image compression, file compression
- Reduces storage requirements

### 3. Network Protocols

**Sliding Window Protocol:**
- Two pointers track send and receive windows
- Used in TCP for flow control
- Ensures reliable data transmission

### 4. Image Processing

**Edge Detection:**
- Two pointers scan image in different directions
- Used in computer vision applications
- Identifies boundaries in images

### 5. Financial Systems

**Stock Trading:**
- Find buy-sell pairs for maximum profit
- Two pointers track low and high points
- Used in algorithmic trading

### 6. Text Processing

**Spell Checking:**
- Compare words with dictionary using two pointers
- Used in word processors, search engines
- Efficient string matching

### 7. Version Control

**Diff Algorithm:**
- Compare two versions of a file
- Two pointers find differences efficiently
- Used in git, svn

### 8. Game Development

**Collision Detection:**
- Two pointers check for object overlaps
- Used in physics engines
- Efficient spatial queries

## Common Mistakes

### 1. Wrong Loop Condition

**Mistake:**
```javascript
while (left <= right) {  // Wrong for opposite direction
  // ...
}
```

**Correct:**
```javascript
while (left < right) {  // Correct for opposite direction
  // ...
}
```

**Why It Matters:**
- `left <= right` checks same element twice
- Can cause duplicate results or incorrect answers
- For opposite direction, stop when pointers meet

### 2. Not Moving Both Pointers

**Mistake:**
```javascript
if (sum === target) {
  return [left, right];  // Only one solution
}
```

**Correct:**
```javascript
if (sum === target) {
  result.push([left, right]);
  left++;  // Move both to find more solutions
  right--;
}
```

**Why It Matters:**
- May miss multiple valid solutions
- Important for problems like 3Sum, 4Sum
- Need to continue searching after finding a match

### 3. Not Handling Duplicates

**Mistake:**
```javascript
// No duplicate handling
for (let i = 0; i < nums.length; i++) {
  // ...
}
```

**Correct:**
```javascript
// Skip duplicates
for (let i = 0; i < nums.length; i++) {
  if (i > 0 && nums[i] === nums[i - 1]) continue;
  // ...
}
```

**Why It Matters:**
- Can produce duplicate results
- Important for problems requiring unique solutions
- Affects correctness and efficiency

### 4. Incorrect Pointer Movement

**Mistake:**
```javascript
// Moving wrong pointer
if (sum < target) {
  right--;  // Wrong: should move left
}
```

**Correct:**
```javascript
// Move correct pointer
if (sum < target) {
  left++;  // Correct: need larger sum
}
```

**Why It Matters:**
- Wrong movement leads to incorrect results
- Must understand which pointer to move based on condition
- Critical for sorted array problems

### 5. Not Checking Bounds

**Mistake:**
```javascript
while (fast.next) {  // Missing fast check
  fast = fast.next.next;
}
```

**Correct:**
```javascript
while (fast && fast.next) {  // Check both
  fast = fast.next.next;
}
```

**Why It Matters:**
- Can cause null pointer errors
- Fast pointer can reach null before slow
- Must check both fast and fast.next

### 6. Forgetting to Sort

**Mistake:**
```javascript
// Not sorting before two pointers
function twoSum(arr, target) {
  // Two pointers on unsorted array
}
```

**Correct:**
```javascript
// Sort first
function twoSum(arr, target) {
  arr.sort((a, b) => a - b);
  // Then use two pointers
}
```

**Why It Matters:**
- Two pointers often require sorted input
- Unsorted input gives incorrect results
- Must sort or use alternative approach

## Advanced Concepts

### 1. Three Pointers

**Concept:**
Use three pointers for more complex problems.

**Example: Sort Colors (Dutch National Flag)**

```javascript
function sortColors(nums) {
  let low = 0, mid = 0, high = nums.length - 1;
  
  while (mid <= high) {
    if (nums[mid] === 0) {
      [nums[low], nums[mid]] = [nums[mid], nums[low]];
      low++;
      mid++;
    } else if (nums[mid] === 1) {
      mid++;
    } else {
      [nums[mid], nums[high]] = [nums[high], nums[mid]];
      high--;
    }
  }
}
```

### 2. Sliding Window with Two Pointers

**Concept:**
Two pointers define a dynamic window that expands/contracts.

**Example: Minimum Window Substring**

```javascript
function minWindow(s, t) {
  if (!s.length || !t.length) return "";
  
  const need = new Map();
  for (const char of t) {
    need.set(char, (need.get(char) || 0) + 1);
  }
  
  let left = 0, right = 0;
  let required = need.size;
  let formed = 0;
  let windowCounts = new Map();
  let result = [-1, 0, 0]; // [length, left, right]
  
  while (right < s.length) {
    const char = s[right];
    windowCounts.set(char, (windowCounts.get(char) || 0) + 1);
    
    if (need.has(char) && windowCounts.get(char) === need.get(char)) {
      formed++;
    }
    
    while (left <= right && formed === required) {
      if (result[0] === -1 || right - left + 1 < result[0]) {
        result = [right - left + 1, left, right];
      }
      
      const leftChar = s[left];
      windowCounts.set(leftChar, windowCounts.get(leftChar) - 1);
      if (need.has(leftChar) && windowCounts.get(leftChar) < need.get(leftChar)) {
        formed--;
      }
      left++;
    }
    
    right++;
  }
  
  return result[0] === -1 ? "" : s.slice(result[1], result[2] + 1);
}
```

### 3. Binary Search + Two Pointers

**Concept:**
Combine binary search with two pointers for optimization.

**Example: 4Sum**

```javascript
function fourSum(nums, target) {
  nums.sort((a, b) => a - b);
  const result = [];
  
  for (let i = 0; i < nums.length - 3; i++) {
    if (i > 0 && nums[i] === nums[i - 1]) continue;
    
    for (let j = i + 1; j < nums.length - 2; j++) {
      if (j > i + 1 && nums[j] === nums[j - 1]) continue;
      
      let left = j + 1, right = nums.length - 1;
      
      while (left < right) {
        const sum = nums[i] + nums[j] + nums[left] + nums[right];
        
        if (sum === target) {
          result.push([nums[i], nums[j], nums[left], nums[right]]);
          while (left < right && nums[left] === nums[left + 1]) left++;
          while (left < right && nums[right] === nums[right - 1]) right--;
          left++;
          right--;
        } else if (sum < target) {
          left++;
        } else {
          right--;
        }
      }
    }
  }
  
  return result;
}
```

### 4. Two Pointers on Strings

**Concept:**
Apply two pointers to string manipulation problems.

**Example: Longest Palindromic Substring**

```javascript
function longestPalindrome(s) {
  let start = 0, maxLength = 1;
  
  for (let i = 0; i < s.length; i++) {
    // Odd length palindrome
    expandAroundCenter(s, i, i);
    // Even length palindrome
    expandAroundCenter(s, i, i + 1);
  }
  
  function expandAroundCenter(s, left, right) {
    while (left >= 0 && right < s.length && s[left] === s[right]) {
      if (right - left + 1 > maxLength) {
        start = left;
        maxLength = right - left + 1;
      }
      left--;
      right++;
    }
  }
  
  return s.substring(start, start + maxLength);
}
```

## Practice Thinking Guide

### How to Identify When to Use Two Pointers

**Key Signals in Problem Statements:**

1. **"Find pair/triplet with sum X"**
   - Two pointers if sorted
   - Hash map if unsorted
   - Example: "Two Sum", "3Sum"

2. **"Remove duplicates from sorted array"**
   - Slow-fast pattern
   - In-place operation
   - Example: "Remove Duplicates"

3. **"Check if palindrome"**
   - Opposite direction pointers
   - Compare from both ends
   - Example: "Valid Palindrome"

4. **"Find middle of linked list"**
   - Fast-slow pointers
   - O(n) time, O(1) space
   - Example: "Middle of Linked List"

5. **"Detect cycle in linked list"**
   - Floyd's algorithm
   - Fast-slow pointers
   - Example: "Linked List Cycle"

6. **"Merge sorted arrays/lists"**
   - Same direction pointers
   - Compare and merge
   - Example: "Merge Sorted Array"

7. **"Maximum/minimum container/trapping"**
   - Opposite direction
   - Greedy approach
   - Example: "Container With Most Water"

**Pattern Recognition:**

**Pattern 1: Pair Sum in Sorted Array**
```
Problem: Find two numbers that sum to target
Solution: Opposite direction pointers
```

**Pattern 2: In-Place Array Modification**
```
Problem: Modify array without extra space
Solution: Slow-fast pointers
```

**Pattern 3: Cycle Detection**
```
Problem: Detect cycle in linked list
Solution: Fast-slow pointers (Floyd's)
```

**Pattern 4: Sorted Array Processing**
```
Problem: Process sorted array efficiently
Solution: Same direction pointers
```

**Pattern 5: String Palindrome**
```
Problem: Check if string is palindrome
Solution: Opposite direction pointers
```

**Decision Flowchart:**

```
Is data sorted?
├─ Yes → Need to find pairs/triplets?
│        ├─ Yes → Opposite direction pointers
│        └─ No → Need in-place modification?
│                 ├─ Yes → Slow-fast pointers
│                 └─ No → Same direction pointers
└─ No → Can we sort first?
         ├─ Yes → Sort + two pointers
         └─ No → Consider hash map or other approach
```

**Example Problem Analysis:**

**Problem:** "Find all triplets that sum to zero"

**Analysis:**
1. Need to find triplets → 3Sum problem
2. Can sort array → O(n log n)
3. Fix one element, use two pointers for remaining two
4. Solution: Sort + two pointers (opposite direction)

**Problem:** "Remove duplicates from sorted array"

**Analysis:**
1. Array is sorted
2. Need in-place modification
3. Keep unique elements at front
4. Solution: Slow-fast pointers

**Problem:** "Detect cycle in linked list"

**Analysis:**
1. Linked list structure
2. Need to detect cycle
3. Cannot use hash map (space constraint)
4. Solution: Fast-slow pointers (Floyd's algorithm)

## Summary

Two Pointers is a versatile technique that reduces time complexity from O(n²) to O(n) by using two indices to traverse data structures intelligently. It's essential for memory-efficient solutions and forms the foundation for many advanced algorithms.

**Key Takeaways:**
- Requires sorted data for opposite direction pattern
- O(n) time, O(1) space for most problems
- Three main patterns: opposite, fast-slow, slow-fast
- Essential for in-place operations
- Watch for edge cases and duplicates
- Understand which pointer to move and when
- Combine with sorting for unsorted data
- Can be extended to three or more pointers

**Mastery Checklist:**
- ✅ Understand all three pointer patterns
- ✅ Know when to use each pattern
- ✅ Handle edge cases correctly
- ✅ Implement in-place operations
- ✅ Detect cycles in linked lists
- ✅ Solve pair/triplet sum problems
- ✅ Handle duplicates appropriately
- ✅ Combine with sorting when needed

