
# Greedy Algorithms

Greedy algorithms make locally optimal choices at each step with the hope of finding a global optimum. They don't reconsider previous decisions.

## Introduction

Greedy algorithms are a class of algorithms that make locally optimal choices at each step with the hope of finding a global optimum. Unlike dynamic programming, which considers all possible subproblems, greedy algorithms make a single choice at each step and never reconsider that choice. This makes them simpler and often faster, but they don't always produce optimal solutions. Greedy algorithms work best for problems with optimal substructure and the greedy choice property, where making a locally optimal choice leads to a globally optimal solution.

**Why Greedy Algorithms Exist:**
- Simpler and faster than dynamic programming
- Often produce optimal solutions for specific problems
- Easy to implement and understand
- No need to store subproblem solutions
- Natural for many optimization problems

**Where It Is Used:**
- Activity selection and scheduling
- Huffman coding for data compression
- Minimum spanning trees (Prim's, Kruskal's)
- Shortest path (Dijkstra's algorithm)
- Fractional knapsack problem
- Coin change problem (with canonical coin systems)
- Interval scheduling
- Job sequencing

## Core Concept Explanation

Greedy algorithms work by making the best possible choice at each step, assuming that this local choice will lead to a global optimum. The key insight is that for some problems, if you always make the locally optimal choice, you'll end up with the globally optimal solution. This is called the "greedy choice property." Additionally, the problem must have "optimal substructure," meaning an optimal solution to the problem contains optimal solutions to subproblems.

**Step-by-Step Breakdown:**
1. Identify the greedy choice (what to optimize at each step)
2. Prove the greedy choice property (local optimal leads to global optimal)
3. Verify optimal substructure (subproblems are independent)
4. Make the greedy choice at each step
5. Never reconsider previous choices
6. Continue until problem is solved

**Intuition Behind the Concept:**
Think of climbing a mountain. A greedy approach would be to always take the steepest path upward at each step. This might get you to the peak quickly, but it could also lead you to a local maximum that's not the true peak. For some problems (like certain mountain shapes), the greedy approach works perfectly. For others, it fails.

**Visual Thinking:**
```
Greedy vs Non-Greedy:

Problem: Make change for amount 11 with coins [1, 5, 10]

Greedy Approach (always take largest coin):
11 - 10 = 1 (take 10)
1 - 1 = 0 (take 1)
Result: [10, 1] = 2 coins ✓ Optimal

Problem: Make change for amount 6 with coins [1, 3, 4]

Greedy Approach:
6 - 4 = 2 (take 4)
2 - 1 = 1 (take 1)
1 - 1 = 0 (take 1)
Result: [4, 1, 1] = 3 coins ✗ Not optimal!

Optimal Approach:
6 - 3 = 3 (take 3)
3 - 3 = 0 (take 3)
Result: [3, 3] = 2 coins ✓ Optimal

This shows greedy doesn't always work!
```

## Internal Working / Logic

Greedy algorithms operate through a simple iterative process: at each step, make the locally optimal choice based on the current state, and never revisit that choice. The algorithm maintains the current solution state and updates it incrementally.

**Phase 1: Problem Analysis**
- Identify if greedy choice property holds
- Verify optimal substructure
- Determine the greedy choice criterion
- Prove correctness (or find counterexample)

**Phase 2: Preprocessing**
- Sort input if needed (common for greedy)
- Build auxiliary data structures
- Initialize solution state

**Phase 3: Greedy Selection**
- At each step, make the greedy choice
- Update solution state
- Continue until termination condition

**Phase 4: Solution Construction**
- Assemble final solution from choices
- Return result

**Flow Explanation (Activity Selection):**
1. Sort activities by end time (greedy criterion)
2. Select first activity (earliest ending)
3. For each subsequent activity:
   - If it starts after last selected ends, select it
   - Otherwise, skip it
4. Return selected activities

**Decision Making Logic:**
The key decision is the greedy criterion:
- For activity selection: earliest end time
- For fractional knapsack: highest value-to-weight ratio
- For Huffman coding: lowest frequency
- For Dijkstra: shortest distance
- Wrong criterion leads to suboptimal solutions

## Algorithm / Approach

**General Greedy Algorithm**

```
1. Identify greedy choice criterion
2. Sort/preprocess input if needed
3. Initialize solution state
4. While not done:
   a. Make greedy choice based on criterion
   b. Update solution state
   c. Remove used elements from consideration
5. Return solution
```

**Activity Selection Algorithm**

```
1. Sort activities by end time
2. Select first activity
3. For each remaining activity:
   a. If starts after last selected ends:
      i. Select it
   b. Otherwise:
      i. Skip it
4. Return selected activities
```

**Fractional Knapsack Algorithm**

```
1. Sort items by value-to-weight ratio (descending)
2. Initialize remaining capacity
3. For each item:
   a. If item fits completely:
      i. Take it all
   b. Otherwise:
      i. Take fraction that fits
4. Return total value
```

**Huffman Coding Algorithm**

```
1. Count character frequencies
2. Create leaf nodes for each character
3. Build min-heap of nodes
4. While heap has more than 1 node:
   a. Extract two minimum frequency nodes
   b. Create new node with sum of frequencies
   c. Add new node to heap
5. Last node is root of Huffman tree
6. Assign codes based on tree traversal
```

## Implementations

### 1. Activity Selection

```javascript
function activitySelection(activities) {
  // Sort by end time (greedy criterion)
  activities.sort((a, b) => a[1] - b[1]);
  
  const selected = [];
  let lastEnd = -Infinity;
  
  for (const [start, end] of activities) {
    if (start >= lastEnd) {
      selected.push([start, end]);
      lastEnd = end;
    }
  }
  
  return selected;
}
```

**Advantages:**
- O(n log n) time due to sorting
- O(1) space (excluding output)
- Proven optimal for this problem

### 2. Jump Game

```javascript
function canJump(nums) {
  let maxReach = 0;
  
  for (let i = 0; i < nums.length; i++) {
    if (i > maxReach) return false;
    maxReach = Math.max(maxReach, i + nums[i]);
  }
  
  return true;
}
```

**Advantages:**
- O(n) time, O(1) space
- Greedy: always extend max reach
- Proven optimal

### 3. Jump Game II

```javascript
function jumpGameII(nums) {
  let jumps = 0;
  let currentEnd = 0;
  let farthest = 0;
  
  for (let i = 0; i < nums.length - 1; i++) {
    farthest = Math.max(farthest, i + nums[i]);
    if (i === currentEnd) {
      jumps++;
      currentEnd = farthest;
    }
  }
  
  return jumps;
}
```

**Advantages:**
- O(n) time, O(1) space
- Greedy: jump at boundary of current range
- Optimal for minimum jumps

### 4. Partition Labels

```javascript
function partitionLabels(s) {
  const lastOccurrence = {};
  for (let i = 0; i < s.length; i++) {
    lastOccurrence[s[i]] = i;
  }
  
  const result = [];
  let start = 0, end = 0;
  
  for (let i = 0; i < s.length; i++) {
    end = Math.max(end, lastOccurrence[s[i]]);
    if (i === end) {
      result.push(end - start + 1);
      start = i + 1;
    }
  }
  
  return result;
}
```

**Advantages:**
- O(n) time, O(1) space (26 letters)
- Greedy: extend partition as needed
- Optimal partition

### 5. Fractional Knapsack

```javascript
function fractionalKnapsack(items, capacity) {
  // Sort by value-to-weight ratio (descending)
  items.sort((a, b) => (b.value / b.weight) - (a.value / a.weight));
  
  let totalValue = 0;
  let remainingCapacity = capacity;
  
  for (const item of items) {
    if (item.weight <= remainingCapacity) {
      totalValue += item.value;
      remainingCapacity -= item.weight;
    } else {
      const fraction = remainingCapacity / item.weight;
      totalValue += item.value * fraction;
      remainingCapacity = 0;
      break;
    }
  }
  
  return totalValue;
}
```

**Advantages:**
- O(n log n) time due to sorting
- Greedy: highest ratio first
- Optimal for fractional knapsack

### 6. Minimum Number of Arrows to Burst Balloons

```javascript
function findMinArrowShots(points) {
  if (points.length === 0) return 0;
  
  // Sort by end coordinate
  points.sort((a, b) => a[1] - b[1]);
  
  let arrows = 1;
  let end = points[0][1];
  
  for (let i = 1; i < points.length; i++) {
    const [start, currentEnd] = points[i];
    if (start > end) {
      arrows++;
      end = currentEnd;
    }
  }
  
  return arrows;
}
```

## Dry Run

**Example: Activity Selection**

**Input:**
```
activities = [[1, 4], [3, 5], [0, 6], [5, 7], [3, 9], [5, 9], [6, 10], [8, 11], [8, 12], [2, 14], [12, 16]]
```

**Step-by-Step Execution:**

```
Initial State:
activities = [[1, 4], [3, 5], [0, 6], [5, 7], [3, 9], [5, 9], [6, 10], [8, 11], [8, 12], [2, 14], [12, 16]]

Step 1: Sort by end time
activities = [[1, 4], [3, 5], [0, 6], [5, 7], [3, 9], [5, 9], [6, 10], [8, 11], [8, 12], [2, 14], [12, 16]]

Step 2: Select activities
selected = []
lastEnd = -Infinity

Iteration 1: [1, 4]
start = 1 >= lastEnd = -Infinity ✓
selected = [[1, 4]]
lastEnd = 4

Iteration 2: [3, 5]
start = 3 < lastEnd = 4 ✗
Skip

Iteration 3: [0, 6]
start = 0 < lastEnd = 4 ✗
Skip

Iteration 4: [5, 7]
start = 5 >= lastEnd = 4 ✓
selected = [[1, 4], [5, 7]]
lastEnd = 7

Iteration 5: [3, 9]
start = 3 < lastEnd = 7 ✗
Skip

Iteration 6: [5, 9]
start = 5 < lastEnd = 7 ✗
Skip

Iteration 7: [6, 10]
start = 6 < lastEnd = 7 ✗
Skip

Iteration 8: [8, 11]
start = 8 >= lastEnd = 7 ✓
selected = [[1, 4], [5, 7], [8, 11]]
lastEnd = 11

Iteration 9: [8, 12]
start = 8 < lastEnd = 11 ✗
Skip

Iteration 10: [2, 14]
start = 2 < lastEnd = 11 ✗
Skip

Iteration 11: [12, 16]
start = 12 >= lastEnd = 11 ✓
selected = [[1, 4], [5, 7], [8, 11], [12, 16]]
lastEnd = 16

Final: selected = [[1, 4], [5, 7], [8, 11], [12, 16]]
Count: 4 activities
```

**Variable Changes Table:**

| Iteration | Activity | start | lastEnd | Action | selected (after) |
|-----------|----------|-------|---------|--------|------------------|
| 1 | [1, 4] | 1 | -∞ | Select | [[1, 4]] |
| 2 | [3, 5] | 3 | 4 | Skip | [[1, 4]] |
| 3 | [0, 6] | 0 | 4 | Skip | [[1, 4]] |
| 4 | [5, 7] | 5 | 4 | Select | [[1, 4], [5, 7]] |
| 5 | [3, 9] | 3 | 7 | Skip | [[1, 4], [5, 7]] |
| 6 | [5, 9] | 5 | 7 | Skip | [[1, 4], [5, 7]] |
| 7 | [6, 10] | 6 | 7 | Skip | [[1, 4], [5, 7]] |
| 8 | [8, 11] | 8 | 7 | Select | [[1, 4], [5, 7], [8, 11]] |
| 9 | [8, 12] | 8 | 11 | Skip | [[1, 4], [5, 7], [8, 11]] |
| 10 | [2, 14] | 2 | 11 | Skip | [[1, 4], [5, 7], [8, 11]] |
| 11 | [12, 16] | 12 | 11 | Select | [[1, 4], [5, 7], [8, 11], [12, 16]] |

## Edge Cases

### 1. Empty Input
```javascript
activities = []
activitySelection([]) → []
Handle empty input gracefully
```

### 2. Single Activity
```javascript
activities = [[1, 4]]
activitySelection([[1, 4]]) → [[1, 4]]
Only one activity, select it
```

### 3. All Overlapping
```javascript
activities = [[1, 5], [2, 6], [3, 7]]
activitySelection([[1, 5], [2, 6], [3, 7]]) → [[1, 5]]
Only first activity selected
```

### 4. No Overlapping
```javascript
activities = [[1, 2], [3, 4], [5, 6]]
activitySelection([[1, 2], [3, 4], [5, 6]]) → [[1, 2], [3, 4], [5, 6]]
All activities selected
```

### 5. Zero Capacity
```javascript
fractionalKnapsack(items, 0) → 0
No capacity, no value
```

### 6. Greedy Fails
```javascript
coins = [1, 3, 4], amount = 6
Greedy: [4, 1, 1] = 3 coins
Optimal: [3, 3] = 2 coins
Greedy doesn't always work!
```

**Why Edge Cases Matter:**
- Empty input tests boundary
- Single element tests base case
- All overlapping tests worst case
- No overlapping tests best case
- Zero capacity tests edge
- Greedy failure shows limitations

## Variations / Extensions

### 1. Maximum Number of Events That Can Be Attended

```javascript
function maxEvents(events) {
  events.sort((a, b) => a[1] - b[1]);
  const attended = new Set();
  
  for (const [start, end] of events) {
    for (let day = start; day <= end; day++) {
      if (!attended.has(day)) {
        attended.add(day);
        break;
      }
    }
  }
  
  return attended.size;
}
```

### 2. Task Scheduler

```javascript
function leastInterval(tasks, n) {
  const freq = {};
  for (const task of tasks) {
    freq[task] = (freq[task] || 0) + 1;
  }
  
  const sorted = Object.values(freq).sort((a, b) => b - a);
  const maxFreq = sorted[0];
  const maxCount = sorted.filter(f => f === maxFreq).length;
  
  const partCount = maxFreq - 1;
  const partLength = n - (maxCount - 1);
  const emptySlots = partCount * partLength;
  const availableTasks = tasks.length - maxFreq * maxCount;
  const idles = Math.max(0, emptySlots - availableTasks);
  
  return tasks.length + idles;
}
```

### 3. Reorganize String

```javascript
function reorganizeString(s) {
  const freq = {};
  for (const char of s) {
    freq[char] = (freq[char] || 0) + 1;
  }
  
  const maxHeap = Object.entries(freq).map(([char, count]) => ({ char, count }));
  maxHeap.sort((a, b) => b.count - a.count);
  
  let result = '';
  let prev = null;
  
  while (maxHeap.length > 0) {
    const current = maxHeap.shift();
    result += current.char;
    current.count--;
    
    if (prev && prev.count > 0) {
      maxHeap.push(prev);
      maxHeap.sort((a, b) => b.count - a.count);
    }
    
    prev = current;
  }
  
  return result.length === s.length ? result : '';
}
```

### 4. Minimum Platforms Required

```javascript
function minPlatforms(arrivals, departures) {
  arrivals.sort((a, b) => a - b);
  departures.sort((a, b) => a - b);
  
  let platforms = 0;
  let maxPlatforms = 0;
  let i = 0, j = 0;
  
  while (i < arrivals.length && j < departures.length) {
    if (arrivals[i] <= departures[j]) {
      platforms++;
      i++;
      maxPlatforms = Math.max(maxPlatforms, platforms);
    } else {
      platforms--;
      j++;
    }
  }
  
  return maxPlatforms;
}
```

### 5. Candy Distribution

```javascript
function candy(ratings) {
  const n = ratings.length;
  const candies = new Array(n).fill(1);
  
  // Left to right
  for (let i = 1; i < n; i++) {
    if (ratings[i] > ratings[i - 1]) {
      candies[i] = candies[i - 1] + 1;
    }
  }
  
  // Right to left
  for (let i = n - 2; i >= 0; i--) {
    if (ratings[i] > ratings[i + 1]) {
      candies[i] = Math.max(candies[i], candies[i + 1] + 1);
    }
  }
  
  return candies.reduce((sum, c) => sum + c, 0);
}
```

## Optimization Techniques

### 1. Sorting

**Pre-sort Input:**
```javascript
// Sort by greedy criterion
// Enables greedy selection
// O(n log n) preprocessing
```

### 2. Priority Queue

**Efficient Selection:**
```javascript
// Use heap for greedy selection
// O(log n) per selection
// Better than linear scan
```

### 3. Trade-offs

**Greedy vs Dynamic Programming:**

| Aspect | Greedy | Dynamic Programming |
|--------|--------|---------------------|
| Time | Often `O(n log n)` | `O(n²)` or more |
| Space | `O(1)` or `O(n)` | `O(n)` table |
| Optimality | Not guaranteed | Guaranteed |
| Simplicity | Simple | Complex |
| Best For | Specific problems | General problems |

**When to Use DP Instead:**
- Greedy doesn't guarantee optimality
- Overlapping subproblems exist
- Need to consider all possibilities
- Counterexample to greedy exists

## Complexity Analysis

### Time Complexity

**Activity Selection: O(n log n)**
- Sorting: O(n log n)
- Selection: O(n)
- Dominated by sorting

**Jump Game: O(n)**
- Single pass through array
- O(1) work per element
- Linear time

**Fractional Knapsack: O(n log n)**
- Sorting: O(n log n)
- Selection: O(n)
- Dominated by sorting

**Huffman Coding: O(n log n)**
- Building heap: O(n)
- Each extraction: O(log n)
- Total: O(n log n)

### Space Complexity

**Activity Selection: O(1)**
- Only store last end time
- Constant space (excluding output)

**Jump Game: O(1)**
- Only store max reach
- Constant space

**Fractional Knapsack: O(1)**
- Only store total value and capacity
- Constant space

**Huffman Coding: O(n)**
- Store heap of n nodes
- Linear space

**Explanation:**
Greedy algorithms are often O(n log n) due to sorting preprocessing. Selection phase is usually O(n). Space is typically O(1) or O(n) depending on whether we need auxiliary data structures.

## Real-world Applications

### 1. Task Scheduling

**Job Scheduling:**
- Schedule jobs to maximize profit
- Meet deadlines
- Example: CPU scheduling

### 2. Resource Allocation

**Resource Management:**
- Allocate resources optimally
- Maximize utilization
- Example: Cloud resource allocation

### 3. Network Routing

**Path Finding:**
- Find shortest path
- Dijkstra's algorithm
- Example: Network routing protocols

### 4. Data Compression

**Huffman Coding:**
- Compress data efficiently
- Variable-length codes
- Example: ZIP compression

### 5. Delivery Optimization

**Route Planning:**
- Optimize delivery routes
- Minimize distance
- Example: Delivery truck routing

### 6. Cache Management

**Cache Replacement:**
- Evict least recently used
- Optimize cache hits
- Example: LRU cache

### 7. Image Processing

**Image Compression:**
- Compress image data
- Huffman coding
- Example: JPEG compression

### 8. Finance

**Portfolio Optimization:**
- Maximize returns
- Minimize risk
- Example: Investment portfolio

## Common Mistakes

### 1. Assuming Greedy Always Works

**Mistake:**
```javascript
// Assuming greedy always optimal
// Doesn't verify greedy choice property
```

**Correct:**
```javascript
// Prove greedy choice property
// Find counterexample if needed
// Use DP if greedy fails
```

**Why It Matters:**
- Greedy doesn't always work
- Must prove correctness
- Counterexamples exist

### 2. Wrong Greedy Criterion

**Mistake:**
```javascript
// Wrong sorting criterion
activities.sort((a, b) => a[0] - b[0]); // Sort by start time (wrong!)
```

**Correct:**
```javascript
// Correct sorting criterion
activities.sort((a, b) => a[1] - b[1]); // Sort by end time (correct)
```

**Why It Matters:**
- Wrong criterion leads to suboptimal
- Must choose correct greedy choice
- Critical for correctness

### 3. Not Sorting

**Mistake:**
```javascript
// Not sorting before greedy
// Greedy selection won't work
```

**Correct:**
```javascript
// Sort before greedy selection
activities.sort((a, b) => a[1] - b[1]);
// Then apply greedy
```

**Why It Matters:**
- Greedy often requires sorted input
- Without sorting, algorithm fails
- Preprocessing is essential

### 4. Integer vs Fractional Knapsack

**Mistake:**
```javascript
// Using greedy for 0/1 knapsack
// Greedy doesn't work for 0/1 knapsack
```

**Correct:**
```javascript
// Use DP for 0/1 knapsack
// Use greedy only for fractional knapsack
```

**Why It Matters:**
- Greedy works for fractional, not 0/1
- 0/1 knapsack requires DP
- Must know which variant

### 5. Not Handling Edge Cases

**Mistake:**
```javascript
// Not handling empty input
// Not handling single element
```

**Correct:**
```javascript
// Handle all edge cases
if (activities.length === 0) return [];
if (activities.length === 1) return activities;
```

**Why It Matters:**
- Edge cases cause errors
- Must handle gracefully
- Robust code needed

### 6. Ignoring Proof of Correctness

**Mistake:**
```javascript
// Not proving greedy choice property
// Assuming it works without proof
```

**Correct:**
```javascript
// Prove greedy choice property
// Use exchange argument
// Verify with examples
```

**Why It Matters:**
- Greedy needs proof
- Without proof, may be wrong
- Critical for correctness

## Advanced Concepts

### 1. Matroid Theory

**Concept:**
Mathematical framework for greedy algorithms.

**Features:**
- Independent sets
- Greedy works on matroids
- Used in optimization

### 2. Exchange Argument

**Concept:**
Prove greedy optimality by exchange.

**Features:**
- Show any solution can be transformed
- Transform to greedy solution
- Standard proof technique

### 3. Approximation Algorithms

**Concept:**
Greedy as approximation for NP-hard problems.

**Features:**
- Guaranteed approximation ratio
- Used when exact solution is hard
- Vertex cover, set cover

### 4. Online Algorithms

**Concept:**
Greedy decisions with incomplete information.

**Features:**
- No future knowledge
- Competitive analysis
- Used in scheduling

## Practice Thinking Guide

### How to Identify When to Use Greedy

**Key Signals in Problem Statements:**

1. **"Maximum/minimum number of"**
   - Optimization problem
   - Example: "Maximum activities"

2. **"Earliest/latest"**
   - Time-based optimization
   - Example: "Earliest finish time"

3. **"Sort by"**
   - Sorting suggests greedy
   - Example: "Sort by end time"

4. **"Fractional"**
   - Fractional knapsack
   - Example: "Fractional knapsack"

5. **"Shortest/longest"**
   - Path optimization
   - Example: "Shortest path"

6. **"Can be divided"**
   - Partition problem
   - Example: "Partition labels"

**Pattern Recognition:**

**Pattern 1: Interval Scheduling**
```
Problem: Maximum non-overlapping intervals
Solution: Sort by end time, select greedily
```

**Pattern 2: Fractional Knapsack**
```
Problem: Maximize value with weight limit
Solution: Sort by value-to-weight ratio
```

**Pattern 3: Jump Game**
```
Problem: Can reach end / minimum jumps
Solution: Greedy extend max reach
```

**Pattern 4: Partition Labels**
```
Problem: Partition string
Solution: Extend partition greedily
```

**Pattern 5: Huffman Coding**
```
Problem: Optimal prefix codes
Solution: Greedy merge lowest frequency
```

**Decision Flowchart:**

```
Has optimal substructure?
├─ Yes → Has greedy choice property?
│        ├─ Yes → Use greedy
│        └─ No → Use DP
├─ No → Is problem NP-hard?
│        ├─ Yes → Greedy approximation
│        └─ No → Consider other
└─ No → Not greedy problem
```

**Example Problem Analysis:**

**Problem:** "Maximum number of non-overlapping activities"

**Analysis:**
1. Need to maximize count
2. Optimal substructure: optimal for n includes optimal for n-1
3. Greedy choice: earliest finishing activity
4. Proof: exchange argument
5. Solution: Sort by end time, select greedily

**Problem:** "Can jump to end of array"

**Analysis:**
1. Need to determine if reachable
2. Greedy: extend max reach
3. If current position exceeds max reach, impossible
4. O(n) time, O(1) space
5. Solution: Greedy max reach

**Problem:** "Fractional knapsack"

**Analysis:**
1. Need to maximize value with weight limit
2. Can take fractions of items
3. Greedy: highest value-to-weight ratio first
4. Take fraction if item doesn't fit
5. Solution: Sort by ratio, take greedily

## Summary

Greedy algorithms make locally optimal choices at each step to find a global optimum. They're simple, efficient, and work well for problems with the greedy choice property and optimal substructure. However, they don't always produce optimal solutions, so proof of correctness is essential.

**Key Takeaways:**
- Make locally optimal choices
- Never reconsider previous choices
- Prove greedy choice property
- Verify optimal substructure
- Sorting often required
- O(n log n) time with sorting
- Not always optimal
- Use DP if greedy fails

**Mastery Checklist:**
- ✅ Understand greedy choice property
- ✅ Identify optimal substructure
- ✅ Prove greedy correctness
- ✅ Implement activity selection
- ✅ Implement jump game
- ✅ Implement fractional knapsack
- ✅ Know when greedy fails
- ✅ Choose greedy vs DP

