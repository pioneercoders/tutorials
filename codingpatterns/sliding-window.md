# Sliding Window

Sliding Window is a technique that processes a subset of data (a "window") as it slides through an array or string. Instead of recalculating everything for each position, we reuse computations from the previous window.

## Introduction

Sliding Window is an optimization technique that reduces time complexity from O(n²) to O(n) for problems involving contiguous subarrays or substrings. Instead of recalculating the result for every possible subarray, we maintain a "window" of elements and update it incrementally as it slides through the data.

**Why Sliding Window Exists:**
- Brute force checks every subarray/substring → O(n²)
- Many subarrays/substrings overlap significantly
- We can reuse computations from overlapping portions
- Reduces redundant calculations dramatically
- Essential for streaming data and real-time processing

**Where It Is Used:**
- Finding maximum/minimum in subarrays
- Longest substring with constraints
- Counting subarrays with specific properties
- Rate limiting and throttling
- Network traffic analysis
- Time-series data processing
- Pattern matching in strings
- DNA sequence analysis

## Core Concept Explanation

Sliding window works by maintaining a window (range) of elements defined by two pointers: `left` and `right`. As we process the data, we slide this window by moving the pointers, updating the window state incrementally instead of recalculating from scratch.

**Step-by-Step Breakdown:**
1. Initialize window with first k elements (for fixed-size) or empty (for dynamic)
2. Calculate initial window state (sum, count, etc.)
3. Slide window by moving right pointer
4. Add new element to window state
5. Remove old element from window state (if fixed-size)
6. Update result based on new window state
7. Repeat until right pointer reaches end

**Intuition Behind the Concept:**
Think of looking through a small window as you walk past a long fence. You don't need to remember everything you've seen - just what's currently visible through the window. As you move, the view changes slightly, but most of what you see remains the same. You only need to note what enters and leaves the window.

**Visual Thinking:**
```
Array: [1, 2, 3, 4, 5, 6, 7, 8, 9]
Window Size: 3

Initial Window:
[1, 2, 3, 4, 5, 6, 7, 8, 9]
 ↑↑↑
Window: [1, 2, 3], Sum = 6

Slide Right:
[1, 2, 3, 4, 5, 6, 7, 8, 9]
   ↑↑↑
Window: [2, 3, 4], Sum = 9
Update: Sum = 6 - 1 + 4 = 9

Slide Right:
[1, 2, 3, 4, 5, 6, 7, 8, 9]
      ↑↑↑
Window: [3, 4, 5], Sum = 12
Update: Sum = 9 - 2 + 5 = 12
```

## Internal Working / Logic

Sliding window operates in two main patterns, each with different movement logic:

**Pattern 1: Fixed-Size Window**
- Window size remains constant (k elements)
- Initialize with first k elements
- Slide by removing leftmost, adding rightmost
- Used for: maximum/minimum sum, average, etc.

**Pattern 2: Dynamic-Size Window**
- Window size expands/contracts based on conditions
- Start with empty or minimal window
- Expand right until condition met
- Shrink left when condition violated
- Used for: longest/shortest substring with constraints

**Flow Explanation (Fixed-Size):**
1. Initialize `left = 0`, `right = k - 1`
2. Calculate initial window state (sum, count, etc.)
3. While `right < n - 1`:
   a. Remove element at `left` from state
   b. Move `left` right: `left = left + 1`
   c. Move `right` right: `right = right + 1`
   d. Add element at `right` to state
   e. Update result based on new state
4. Return result

**Flow Explanation (Dynamic-Size):**
1. Initialize `left = 0`, `right = 0`
2. While `right < n`:
   a. Add element at `right` to window state
   b. While condition is violated:
      i. Remove element at `left` from state
      ii. Move `left` right: `left = left + 1`
   c. Update result based on current window
   d. Move `right` right: `right = right + 1`
3. Return result

**Decision Making Logic:**
The key decision is when to shrink the window:
- For fixed-size: shrink every step (remove leftmost)
- For dynamic-size: shrink when condition violated
- Condition violation depends on problem (duplicate, sum > target, etc.)

## Algorithm / Approach

**Pattern 1: Fixed-Size Window Algorithm**

```
1. If array length < k, return invalid
2. Initialize window state with first k elements
3. Set result = initial window state
4. For right from k to n-1:
   a. Remove arr[right - k] from state
   b. Add arr[right] to state
   c. Update result based on new state
5. Return result
```

**Pattern 2: Dynamic-Size Window Algorithm**

```
1. Initialize left = 0, right = 0
2. Initialize window state (empty)
3. While right < n:
   a. Add arr[right] to window state
   b. While condition is violated:
      i. Remove arr[left] from window state
      ii. left = left + 1
   c. Update result based on window [left, right]
   d. right = right + 1
4. Return result
```

## Implementations

### 1. Maximum Sum Subarray of Size K (Fixed-Size)

```javascript
function maxSumSubarray(arr, k) {
  if (arr.length < k) return 0;
  
  // Initialize window with first k elements
  let windowSum = 0;
  for (let i = 0; i < k; i++) {
    windowSum += arr[i];
  }
  
  let maxSum = windowSum;
  
  // Slide window
  for (let i = k; i < arr.length; i++) {
    // Remove leftmost, add new rightmost
    windowSum += arr[i] - arr[i - k];
    maxSum = Math.max(maxSum, windowSum);
  }
  
  return maxSum;
}
```

**Advantages:**
- O(n) time, O(1) space
- No nested loops
- Reuses previous computation

### 2. Longest Substring Without Repeating Characters (Dynamic-Size)

```javascript
function longestSubstring(s) {
  const charIndex = new Map();
  let maxLength = 0, left = 0;
  
  for (let right = 0; right < s.length; right++) {
    const char = s[right];
    
    // If char seen and within current window, shrink
    if (charIndex.has(char) && charIndex.get(char) >= left) {
      left = charIndex.get(char) + 1;
    }
    
    charIndex.set(char, right);
    maxLength = Math.max(maxLength, right - left + 1);
  }
  
  return maxLength;
}
```

**Advantages:**
- O(n) time, O(min(n, alphabet)) space
- Single pass through string
- Handles all edge cases

### 3. Minimum Window Substring (Dynamic-Size)

```javascript
function minWindow(s, t) {
  const need = new Map();
  for (const char of t) {
    need.set(char, (need.get(char) || 0) + 1);
  }
  
  let left = 0, minLen = Infinity, minLeft = 0;
  let missing = t.length;
  
  for (let right = 0; right < s.length; right++) {
    const char = s[right];
    
    if (need.has(char)) {
      if (need.get(char) > 0) missing--;
      need.set(char, need.get(char) - 1);
    }
    
    // When all characters found, try to shrink
    while (missing === 0) {
      if (right - left + 1 < minLen) {
        minLen = right - left + 1;
        minLeft = left;
      }
      
      const leftChar = s[left];
      if (need.has(leftChar)) {
        need.set(leftChar, need.get(leftChar) + 1);
        if (need.get(leftChar) > 0) missing++;
      }
      left++;
    }
  }
  
  return minLen === Infinity ? '' : s.substring(minLeft, minLeft + minLen);
}
```

**Advantages:**
- O(n) time, O(alphabet) space
- Finds minimum window containing all characters
- Handles duplicates correctly

### 4. Count Subarrays with Sum Less Than K

```javascript
function countSubarrays(arr, k) {
  let count = 0, sum = 0, left = 0;
  
  for (let right = 0; right < arr.length; right++) {
    sum += arr[right];
    
    // Shrink while sum >= k
    while (sum >= k && left <= right) {
      sum -= arr[left];
      left++;
    }
    
    // All subarrays ending at right with start >= left are valid
    count += right - left + 1;
  }
  
  return count;
}
```

**Advantages:**
- O(n) time, O(1) space
- Counts all valid subarrays efficiently
- Uses mathematical insight for counting

### 5. Maximum Average Subarray of Size K

```javascript
function findMaxAverage(arr, k) {
  if (arr.length < k) return 0;
  
  let windowSum = 0;
  for (let i = 0; i < k; i++) {
    windowSum += arr[i];
  }
  
  let maxSum = windowSum;
  
  for (let i = k; i < arr.length; i++) {
    windowSum += arr[i] - arr[i - k];
    maxSum = Math.max(maxSum, windowSum);
  }
  
  return maxSum / k;
}
```

**Advantages:**
- O(n) time, O(1) space
- Avoids floating-point precision issues
- Reuses sum calculation

## Dry Run

**Example: Maximum Sum Subarray of Size K**

**Input:**
```
arr = [2, 1, 5, 1, 3, 2]
k = 3
```

**Step-by-Step Execution:**

```
Initial State:
left = 0, right = 2
arr = [2, 1, 5, 1, 3, 2]
       0  1  2  3  4  5
Window: [2, 1, 5]
windowSum = 2 + 1 + 5 = 8
maxSum = 8

Iteration 1:
right = 3
Remove arr[0] = 2 from window
Add arr[3] = 1 to window
windowSum = 8 - 2 + 1 = 7
maxSum = max(8, 7) = 8
Window: [1, 5, 1]

Iteration 2:
right = 4
Remove arr[1] = 1 from window
Add arr[4] = 3 to window
windowSum = 7 - 1 + 3 = 9
maxSum = max(8, 9) = 9
Window: [5, 1, 3]

Iteration 3:
right = 5
Remove arr[2] = 5 from window
Add arr[5] = 2 to window
windowSum = 9 - 5 + 2 = 6
maxSum = max(9, 6) = 9
Window: [1, 3, 2]

Final: maxSum = 9
```

**Variable Changes Table:**

| Iteration | right | Window | windowSum | maxSum | Action |
|-----------|-------|--------|-----------|--------|--------|
| Initial | 2 | [2,1,5] | 8 | 8 | Initialize |
| 1 | 3 | [1,5,1] | 7 | 8 | -2+1 |
| 2 | 4 | [5,1,3] | 9 | 9 | -1+3 |
| 3 | 5 | [1,3,2] | 6 | 9 | -5+2 |

## Edge Cases

### 1. Empty Array
```javascript
arr = [], k = 3
arr.length < k, return 0 or handle appropriately
```

### 2. Window Size Larger Than Array
```javascript
arr = [1, 2], k = 5
arr.length < k, return 0 or handle appropriately
```

### 3. Single Element
```javascript
arr = [5], k = 1
windowSum = 5, maxSum = 5
Return 5
```

### 4. All Identical Elements
```javascript
arr = [3, 3, 3, 3], k = 2
Every window has sum = 6
Return 6
```

### 5. Negative Numbers
```javascript
arr = [-1, -2, -3, -4], k = 2
windowSum = -3, -5, -7
maxSum = -3 (least negative)
```

### 6. Window Size Equals Array Length
```javascript
arr = [1, 2, 3, 4], k = 4
windowSum = 10, no sliding
Return 10
```

### 7. No Valid Window (Dynamic)
```javascript
s = "abc", t = "xyz"
No characters match
Return ""
```

**Why Edge Cases Matter:**
- Empty/large windows prevent index errors
- Single elements test boundary conditions
- Negative numbers test algorithm correctness
- No valid windows must return appropriate values
- Edge window sizes test initialization logic

## Variations / Extensions

### 1. Sliding Window Maximum (Monotonic Queue)

Use deque for O(1) max/min operations.

```javascript
function maxSlidingWindow(nums, k) {
  const result = [];
  const deque = []; // stores indices
  
  for (let i = 0; i < nums.length; i++) {
    // Remove indices outside window
    while (deque.length > 0 && deque[0] <= i - k) {
      deque.shift();
    }
    
    // Remove smaller elements from back
    while (deque.length > 0 && nums[deque[deque.length - 1]] < nums[i]) {
      deque.pop();
    }
    
    deque.push(i);
    
    // Add max to result when window is formed
    if (i >= k - 1) {
      result.push(nums[deque[0]]);
    }
  }
  
  return result;
}
```

### 2. Subarray Product Less Than K

```javascript
function numSubarrayProductLessThanK(nums, k) {
  if (k <= 1) return 0;
  
  let product = 1, count = 0, left = 0;
  
  for (let right = 0; right < nums.length; right++) {
    product *= nums[right];
    
    while (product >= k) {
      product /= nums[left];
      left++;
    }
    
    count += right - left + 1;
  }
  
  return count;
}
```

### 3. Longest Subarray with Absolute Difference

```javascript
function longestSubarray(nums, limit) {
  const maxDeque = [], minDeque = [];
  let left = 0, maxLength = 0;
  
  for (let right = 0; right < nums.length; right++) {
    // Maintain max deque (decreasing)
    while (maxDeque.length > 0 && nums[maxDeque[maxDeque.length - 1]] < nums[right]) {
      maxDeque.pop();
    }
    maxDeque.push(right);
    
    // Maintain min deque (increasing)
    while (minDeque.length > 0 && nums[minDeque[minDeque.length - 1]] > nums[right]) {
      minDeque.pop();
    }
    minDeque.push(right);
    
    // Shrink if difference exceeds limit
    while (nums[maxDeque[0]] - nums[minDeque[0]] > limit) {
      left++;
      if (maxDeque[0] < left) maxDeque.shift();
      if (minDeque[0] < left) minDeque.shift();
    }
    
    maxLength = Math.max(maxLength, right - left + 1);
  }
  
  return maxLength;
}
```

### 4. Permutation in String

Check if one string is permutation of substring in another.

```javascript
function checkInclusion(s1, s2) {
  if (s1.length > s2.length) return false;
  
  const count = new Array(26).fill(0);
  
  for (let i = 0; i < s1.length; i++) {
    count[s1.charCodeAt(i) - 97]++;
    count[s2.charCodeAt(i) - 97]--;
  }
  
  if (count.every(c => c === 0)) return true;
  
  for (let i = s1.length; i < s2.length; i++) {
    count[s2.charCodeAt(i) - 97]--;
    count[s2.charCodeAt(i - s1.length) - 97]++;
    
    if (count.every(c => c === 0)) return true;
  }
  
  return false;
}
```

### 5. Fixed-Size Window with Hash Map

Count distinct elements in each window.

```javascript
function countDistinct(arr, k) {
  const result = [];
  const freq = new Map();
  
  // Initialize first window
  for (let i = 0; i < k; i++) {
    freq.set(arr[i], (freq.get(arr[i]) || 0) + 1);
  }
  result.push(freq.size);
  
  // Slide window
  for (let i = k; i < arr.length; i++) {
    // Remove leftmost
    freq.set(arr[i - k], freq.get(arr[i - k]) - 1);
    if (freq.get(arr[i - k]) === 0) freq.delete(arr[i - k]);
    
    // Add new rightmost
    freq.set(arr[i], (freq.get(arr[i]) || 0) + 1);
    
    result.push(freq.size);
  }
  
  return result;
}
```

## Optimization Techniques

### 1. Time Optimization

**Early Termination:**
```javascript
// Stop if maximum possible window found
if (maxLength === arr.length) return maxLength;
```

**Monotonic Queues:**
```javascript
// Use deque for O(1) max/min operations
// Instead of O(k) for each window
```

### 2. Space Optimization

**Fixed-Size Arrays:**
```javascript
// Use array instead of hash map for known alphabet
const count = new Array(26).fill(0); // For lowercase letters
```

**Two Pointers Only:**
```javascript
// For simple sums, no additional data structures needed
// Just maintain running sum
```

### 3. Trade-offs

**Sliding Window vs Brute Force:**

| Aspect | Sliding Window | Brute Force |
|--------|----------------|-------------|
| Time Complexity | `O(n)` | `O(n²)` |
| Space Complexity | `O(k)` or `O(1)` | `O(1)` |
| Reuses Computation | Yes | No |
| Best For | Contiguous subarrays | Any subarrays |
| Complexity | Medium | Simple |

**When to Use Brute Force Instead:**
- Non-contiguous subarrays
- Very small input size
- Simple implementation needed
- No overlapping computations

## Complexity Analysis

### Time Complexity

**Fixed-Size Window: O(n)**
- Each element added once, removed once
- Total operations: 2n = O(n)
- Example: Maximum sum subarray

**Dynamic-Size Window: O(n)**
- Each element added once, removed at most once
- Total operations: 2n = O(n)
- Example: Longest substring without repeats

**With Monotonic Queue: O(n)**
- Each element added once, removed once from deque
- Total operations: 2n = O(n)
- Example: Sliding window maximum

### Space Complexity

**Fixed-Size Window: O(1)**
- Only stores sum, count, or simple state
- Constant space regardless of input
- Example: Maximum sum subarray

**Dynamic-Size Window: O(k) or O(alphabet)**
- Stores hash map of window elements
- k = window size, alphabet = character set
- Example: Longest substring without repeats

**With Monotonic Queue: O(k)**
- Deque stores at most k elements
- k = window size
- Example: Sliding window maximum

**Explanation:**
Sliding window achieves O(n) time by reusing computations. Each element is processed a constant number of times (added once, removed once). Space depends on whether we need to track window contents (hash map) or just aggregate values (sum, count).

## Real-world Applications

### 1. Rate Limiting

**Sliding Window Rate Limiter:**
- Track requests in time window
- Allow requests if count < limit
- Used in APIs, web servers

**Example:**
```javascript
class RateLimiter {
  constructor(limit, window) {
    this.limit = limit;
    this.window = window;
    this.requests = [];
  }
  
  allow() {
    const now = Date.now();
    this.requests = this.requests.filter(t => t > now - this.window);
    
    if (this.requests.length < this.limit) {
      this.requests.push(now);
      return true;
    }
    return false;
  }
}
```

### 2. Network Traffic Analysis

**Bandwidth Monitoring:**
- Monitor traffic in time windows
- Detect anomalies, DDoS attacks
- Used in network security

### 3. Stock Market Analysis

**Moving Averages:**
- Calculate moving averages over time windows
- Identify trends, support/resistance
- Used in trading algorithms

### 4. Video Streaming

**Buffer Management:**
- Monitor buffer levels in time windows
- Adjust quality based on buffer
- Used in adaptive streaming

### 5. Log Analysis

**Error Rate Monitoring:**
- Count errors in time windows
- Trigger alerts if threshold exceeded
- Used in monitoring systems

### 6. DNA Sequence Analysis

**Pattern Matching:**
- Find DNA patterns in sequences
- Sliding window over genome
- Used in bioinformatics

### 7. Image Processing

**Convolution Operations:**
- Apply filters using sliding window
- Edge detection, blurring
- Used in computer vision

### 8. Time-Series Forecasting

**Trend Analysis:**
- Analyze trends in time windows
- Smooth out noise
- Used in financial forecasting

## Common Mistakes

### 1. Not Initializing Window Correctly

**Mistake:**
```javascript
// Not initializing first window
for (let i = 0; i < arr.length; i++) {
  // Sliding logic
}
```

**Correct:**
```javascript
// Initialize first window
let windowSum = 0;
for (let i = 0; i < k; i++) {
  windowSum += arr[i];
}
// Then slide
```

**Why It Matters:**
- First window must be calculated separately
- Sliding logic assumes window exists
- Incorrect initialization gives wrong results

### 2. Wrong Window Update Order

**Mistake:**
```javascript
// Wrong order: add before remove
windowSum += arr[i];
windowSum -= arr[i - k];
```

**Correct:**
```javascript
// Correct order: remove before add
windowSum -= arr[i - k];
windowSum += arr[i];
```

**Why It Matters:**
- Order affects intermediate state
- Can cause incorrect calculations
- Must remove old before adding new

### 3. Not Checking Window Bounds

**Mistake:**
```javascript
// Not checking if window is valid
if (windowSum > target) {
  // Process
}
```

**Correct:**
```javascript
// Check window size before processing
if (right - left + 1 >= k && windowSum > target) {
  // Process
}
```

**Why It Matters:**
- Processing incomplete windows gives wrong results
- Must ensure window is fully formed
- Critical for fixed-size windows

### 4. Incorrect Shrinking Logic

**Mistake:**
```javascript
// Shrinking too much
while (sum > target) {
  sum -= arr[left];
  left++;
}
```

**Correct:**
```javascript
// Shrink only while condition violated
while (sum > target && left <= right) {
  sum -= arr[left];
  left++;
}
```

**Why It Matters:**
- Can shrink window to invalid state
- Must check bounds while shrinking
- Prevents index errors

### 5. Not Handling Empty Results

**Mistake:**
```javascript
// Assuming result always exists
return result;
```

**Correct:**
```javascript
// Handle case where no valid window exists
if (minLen === Infinity) return '';
return s.substring(minLeft, minLeft + minLen);
```

**Why It Matters:**
- No valid window is possible in some cases
- Must return appropriate default value
- Prevents undefined behavior

### 6. Using Wrong Data Structure

**Mistake:**
```javascript
// Using array for character counting
const count = [];
count[char] = (count[char] || 0) + 1;
```

**Correct:**
```javascript
// Use hash map for character counting
const count = new Map();
count.set(char, (count.get(char) || 0) + 1);
```

**Why It Matters:**
- Arrays have fixed size and sparse indices
- Hash maps are more efficient for sparse data
- Affects both time and space complexity

## Advanced Concepts

### 1. At Most K Distinct Characters

**Concept:**
Find longest substring with at most K distinct characters.

```javascript
function lengthOfLongestSubstringKDistinct(s, k) {
  const charCount = new Map();
  let left = 0, maxLength = 0;
  
  for (let right = 0; right < s.length; right++) {
    const char = s[right];
    charCount.set(char, (charCount.get(char) || 0) + 1);
    
    while (charCount.size > k) {
      const leftChar = s[left];
      charCount.set(leftChar, charCount.get(leftChar) - 1);
      if (charCount.get(leftChar) === 0) {
        charCount.delete(leftChar);
      }
      left++;
    }
    
    maxLength = Math.max(maxLength, right - left + 1);
  }
  
  return maxLength;
}
```

### 2. Minimum Window Subsequence

**Concept:**
Find minimum window containing subsequence (not substring).

```javascript
function minWindowSubsequence(s, t) {
  let minLen = Infinity, minLeft = -1;
  
  for (let i = 0; i < s.length; i++) {
    if (s[i] === t[0]) {
      let tIndex = 0, sIndex = i;
      
      while (sIndex < s.length && tIndex < t.length) {
        if (s[sIndex] === t[tIndex]) {
          tIndex++;
        }
        sIndex++;
      }
      
      if (tIndex === t.length) {
        // Found match, now find best start
        tIndex = t.length - 1;
        sIndex = sIndex - 1;
        
        while (tIndex >= 0) {
          if (s[sIndex] === t[tIndex]) {
            tIndex--;
          }
          sIndex--;
        }
        
        const windowLen = sIndex - i + 2;
        if (windowLen < minLen) {
          minLen = windowLen;
          minLeft = i;
        }
      }
    }
  }
  
  return minLeft === -1 ? '' : s.substring(minLeft, minLeft + minLen);
}
```

### 3. Sliding Window with Two Pointers

**Concept:**
Combine sliding window with two pointers for complex problems.

**Example: Longest Repeating Character Replacement**

```javascript
function characterReplacement(s, k) {
  const count = new Array(26).fill(0);
  let maxCount = 0, maxLength = 0, left = 0;
  
  for (let right = 0; right < s.length; right++) {
    const index = s.charCodeAt(right) - 65;
    count[index]++;
    maxCount = Math.max(maxCount, count[index]);
    
    // If window needs more than k replacements, shrink
    while (right - left + 1 - maxCount > k) {
      const leftIndex = s.charCodeAt(left) - 65;
      count[leftIndex]--;
      left++;
    }
    
    maxLength = Math.max(maxLength, right - left + 1);
  }
  
  return maxLength;
}
```

### 4. Sliding Window Median

**Concept:**
Find median of each window using two heaps.

```javascript
function medianSlidingWindow(nums, k) {
  const result = [];
  // Implementation using two heaps (min-heap and max-heap)
  // This is complex and requires careful balancing
  // O(n log k) time complexity
  return result;
}
```

## Practice Thinking Guide

### How to Identify When to Use Sliding Window

**Key Signals in Problem Statements:**

1. **"Maximum/minimum in subarray of size K"**
   - Fixed-size sliding window
   - Example: "Maximum sum subarray of size K"

2. **"Longest/shortest substring with condition"**
   - Dynamic-size sliding window
   - Example: "Longest substring without repeating characters"

3. **"Contiguous subarray with sum X"**
   - Sliding window or prefix sum
   - Example: "Subarray sum equals K"

4. **"At most K distinct characters"**
   - Dynamic-size with hash map
   - Example: "Longest substring with at most K distinct"

5. **"Count subarrays with property"**
   - Sliding window with counting
   - Example: "Count subarrays with sum less than K"

6. **"Permutation in string"**
   - Fixed-size with frequency map
   - Example: "Check if s2 contains permutation of s1"

**Pattern Recognition:**

**Pattern 1: Fixed-Size Window**
```
Problem: Find max/min in subarray of size K
Solution: Fixed-size sliding window
```

**Pattern 2: Dynamic-Size Window**
```
Problem: Find longest/shortest with condition
Solution: Dynamic-size sliding window
```

**Pattern 3: Counting Subarrays**
```
Problem: Count subarrays with property
Solution: Sliding window with mathematical counting
```

**Pattern 4: Frequency-Based**
```
Problem: Track character/element frequencies
Solution: Sliding window with hash map
```

**Pattern 5: Constraint-Based**
```
Problem: Maintain constraint (sum < K, distinct < K)
Solution: Dynamic-size window with shrinking
```

**Decision Flowchart:**

```
Is window size fixed?
├─ Yes → Fixed-size sliding window
│        ├─ Simple aggregate (sum, count)
│        └─ Complex (max/min) → Monotonic queue
└─ No → Dynamic-size sliding window
         ├─ Simple condition → Expand/shrink
         ├─ Frequency-based → Hash map
         └─ Counting subarrays → Mathematical insight
```

**Example Problem Analysis:**

**Problem:** "Find the longest substring without repeating characters"

**Analysis:**
1. Need longest substring → dynamic-size window
2. Condition: no repeating characters
3. Use hash map to track last seen position
4. Shrink when duplicate found
5. Solution: Dynamic-size sliding window with hash map

**Problem:** "Maximum sum subarray of size K"

**Analysis:**
1. Window size is fixed (K)
2. Need maximum sum
3. Can reuse previous sum
4. Solution: Fixed-size sliding window

**Problem:** "Count subarrays with sum less than K"

**Analysis:**
1. Need to count all valid subarrays
2. Condition: sum < K
3. Use mathematical insight for counting
4. Solution: Dynamic-size sliding window with counting

## Summary

Sliding Window is a powerful optimization technique that reduces time complexity from O(n²) to O(n) for problems involving contiguous subarrays or substrings. It reuses computations from overlapping portions of the data, making it essential for streaming data and real-time processing.

**Key Takeaways:**
- Two main patterns: fixed-size and dynamic-size
- O(n) time, O(k) or O(1) space
- Reuses computations from overlapping windows
- Essential for contiguous subarray/substring problems
- Use hash maps for frequency-based problems
- Use monotonic queues for max/min operations
- Watch for edge cases (empty, window size bounds)
- Understand when to shrink the window

**Mastery Checklist:**
- ✅ Understand fixed-size vs dynamic-size windows
- ✅ Implement window initialization correctly
- ✅ Handle window shrinking logic
- ✅ Use hash maps for frequency tracking
- ✅ Apply monotonic queues for max/min
- ✅ Handle all edge cases
- ✅ Recognize sliding window problems
- ✅ Optimize space usage
