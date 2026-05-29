# Bitmask Dynamic Programming

Bitmask Dynamic Programming uses bitmasks to represent subsets of elements, enabling efficient state representation and transitions for subset-based problems.

## Introduction

Bitmask Dynamic Programming is a powerful technique that uses bitmasks (binary representations) to efficiently represent subsets of elements. Each bit in an integer represents whether a particular element is included (1) or excluded (0) from the subset. This allows us to represent `2^n` possible subsets using integers from 0 to `2^n` - 1. Combined with dynamic programming, we can solve complex subset-based optimization problems by caching results and avoiding recomputation. This technique is essential for problems like the Traveling Salesman Problem, partition problems, and team selection where we need to optimize over all possible subsets.

**Why Bitmask DP Exists:**
- Subset enumeration is `O(2^n)` with brute force
- Bitmask representation is compact and efficient
- DP avoids recomputation of overlapping subproblems
- Bit operations are extremely fast
- Elegant state representation for subset problems

**Where It Is Used:**
- Traveling Salesman Problem (route optimization)
- Partition to K Equal Sum Subsets (resource allocation)
- Smallest Sufficient Team (team selection)
- Letter Tile Possibilities (combinatorial counting)
- Job scheduling (task assignment)
- Resource allocation (subset selection)
- Combinatorial optimization (complex selections)

## Core Concept Explanation

Bitmask DP leverages the fact that a subset of n elements can be represented as an n-bit integer. For example, with 3 elements, the subset {0, 2} is represented as 101 in binary (5 in decimal). Bit 0 being 1 means element 0 is included, bit 1 being 0 means element 1 is excluded, and bit 2 being 1 means element 2 is included. This representation allows us to efficiently iterate through all subsets, check element inclusion using bitwise AND, add elements using bitwise OR, and remove elements using bitwise AND with complement. The DP state typically has the form DP[mask] or DP[mask][i] where mask represents the subset and i represents additional state like the last visited city.

**Step-by-Step Breakdown:**
1. Represent each subset as a bitmask (integer)
2. Define DP state based on problem requirements
3. Iterate through all masks from 0 to `2^n` - 1
4. For each mask, compute transitions by adding/removing elements
5. Cache results to avoid recomputation
6. Extract answer from final DP state

**Intuition Behind the Concept:**
Think of bitmask DP like having n light switches, each representing an item. When a switch is on (1), the item is selected; when off (0), it's not selected. Instead of listing all items in a subset, we just record which switches are on. This compact representation lets us efficiently explore all combinations while DP remembers which combinations we've already solved, avoiding redundant work.

**Visual Thinking:**
```
Bitmask Representation for 3 elements:

Element:    2   1   0
            |   |   |
Subset `{}`:  0   0   0  `=` 0 (decimal)
Subset `{0}`: 0   0   1  `=` 1
Subset `{1}`: 0   1   0  `=` 2
Subset `{0,1}`: 0  1   1  `=` 3
Subset `{2}`: 1   0   0  `=` 4
Subset `{0,2}`: 1  0   1  `=` 5
Subset `{1,2}`: 1  1   0  `=` 6
Subset `{0,1,2}`: 1 1   1  `=` 7

Bit Operations:
Add element i: mask | `(1 << i)`
Remove element i: mask & `~(1 << i)`
Check element i: mask & `(1 << i)`
Count elements: countSetBits(mask)
```

## Internal Working / Logic

Bitmask DP operates by treating each subset as a state and using DP to compute optimal values for each state. The key is defining the DP state correctly and efficiently transitioning between states by adding or removing elements.

**Operation 1: Bitmask Representation**
- Each bit represents element inclusion
- Bit i `=` 1 means element i is in subset
- Bit i `=` 0 means element i is not in subset
- Total of `2^n` possible subsets

**Operation 2: State Definition**
- DP[mask] `=` optimal value for subset represented by mask
- DP[mask][i] `=` optimal value ending at element i
- Depends on problem requirements
- Must capture all necessary information

**Operation 3: State Transitions**
- Add element: newMask `=` mask | `(1 << i)`
- Remove element: newMask `=` mask & `~(1 << i)`
- Check inclusion: if (mask & `(1 << i)`)
- Iterate through all valid transitions

**Operation 4: Memoization**
- Cache computed states
- Avoid recomputation
- Use hash map or array
- Critical for efficiency

**Flow Explanation (TSP):**
1. DP[mask][i] `=` min cost to visit cities in mask ending at i
2. Initialize DP[1][0] `=` 0 (start at city 0)
3. For each mask, for each city i in mask:
   - For each city j not in mask:
     - Update DP[mask | `(1 << j)`][j] `=` min(DP[mask][i] + cost[i][j])
4. Answer `=` min(DP[fullMask][i] + cost[i][0]) for all i

**Decision Making Logic:**
The key decisions are:
- State definition (what does DP[mask] represent?)
- Transition logic (how do we move between states?)
- Base cases (what are the initial values?)
- Answer extraction (how do we get the final answer?)

## Algorithm / Approach

**Subset Sum Algorithm**

```
1. Initialize DP array of size `2^n`
2. DP[0] `=` True (empty subset)
3. For each mask from 0 to `2^n` - 1:
   a. If DP[mask] is True:
      i. Calculate sum of elements in mask
      ii. If sum equals target, return True
4. Return False
```

**Traveling Salesman Algorithm**

```
1. Initialize DP[mask][i] `=` infinity
2. DP[1][0] `=` 0 (start at city 0)
3. For each mask from 0 to `2^n` - 1:
   a. For each city i in mask:
      i. For each city j not in mask:
         - newMask `=` mask | `(1 << j)`
         - DP[newMask][j] `=` min(DP[newMask][j], DP[mask][i] + cost[i][j])
4. Return min(DP[fullMask][i] + cost[i][0]) for all i
```

**Partition to K Equal Sum Subsets Algorithm**

```
1. Calculate total sum, check if divisible by k
2. Target `=` total / k
3. Use backtracking with bitmask:
   a. Track used elements with mask
   b. Track current sum for current subset
   c. Track remaining subsets to form
   d. Memoize results by mask
4. Return True if all subsets formed
```

**Smallest Sufficient Team Algorithm**

```
1. Map each person to skills they have
2. DP[mask] `=` minimum team to achieve skills in mask
3. Initialize DP[0] `=` []
4. For each mask, for each person:
   a. newMask `=` mask | personSkills
   b. If DP[newMask] is empty or smaller, update
5. Return DP[fullSkillMask]
```

## Implementations

### 1. Subset Sum

```javascript
function subsetSum(nums, target) {
  const n = nums.length;
  const dp = new Array(1 << n).fill(false);
  dp[0] = true;
  
  for (let mask = 0; mask < (1 << n); mask++) {
    if (dp[mask]) {
      let currentSum = 0;
      for (let i = 0; i < n; i++) {
        if (mask & (1 << i)) {
          currentSum += nums[i];
        }
      }
      if (currentSum === target) return true;
    }
  }
  
  return false;
}
```

**Advantages:**
- Simple bitmask representation
- Checks all subsets
- Easy to understand

### 2. Traveling Salesman Problem

```javascript
function travelingSalesman(graph) {
  const n = graph.length;
  const dp = Array(1 << n).fill(null).map(() => Array(n).fill(Infinity));
  dp[1][0] = 0; // Start at city 0
  
  for (let mask = 0; mask < (1 << n); mask++) {
    for (let i = 0; i < n; i++) {
      if (mask & (1 << i)) {
        for (let j = 0; j < n; j++) {
          if (!(mask & (1 << j))) {
            const newMask = mask | (1 << j);
            dp[newMask][j] = Math.min(dp[newMask][j], dp[mask][i] + graph[i][j]);
          }
        }
      }
    }
  }
  
  // Return to start
  const fullMask = (1 << n) - 1;
  let result = Infinity;
  for (let i = 1; i < n; i++) {
    result = Math.min(result, dp[fullMask][i] + graph[i][0]);
  }
  return result;
}
```

**Advantages:**
- Optimal solution for small n
- Finds minimum cost tour
- Classic TSP application

### 3. Partition to K Equal Sum Subsets

```javascript
function canPartitionKSubsets(nums, k) {
  const total = nums.reduce((a, b) => a + b, 0);
  if (total % k !== 0) return false;
  const target = total / k;
  const n = nums.length;
  const dp = new Map();
  
  function backtrack(mask, currentSum, remaining) {
    if (remaining === 0) return true;
    if (dp.has(mask)) return dp.get(mask);
    
    for (let i = 0; i < n; i++) {
      if (!(mask & (1 << i)) && currentSum + nums[i] <= target) {
        if (currentSum + nums[i] === target) {
          if (backtrack(mask | (1 << i), 0, remaining - 1)) {
            dp.set(mask, true);
            return true;
          }
        } else {
          if (backtrack(mask | (1 << i), currentSum + nums[i], remaining)) {
            dp.set(mask, true);
            return true;
          }
        }
      }
    }
    
    dp.set(mask, false);
    return false;
  }
  
  return backtrack(0, 0, k);
}
```

**Advantages:**
- Handles partitioning problems
- Memoization avoids recomputation
- Practical application

### 4. Smallest Sufficient Team

```javascript
function smallestSufficientTeam(reqSkills, people) {
  const skillToIndex = {};
  reqSkills.forEach((skill, i) => skillToIndex[skill] = i);
  
  const peopleSkills = people.map(person => {
    let mask = 0;
    person.forEach(skill => {
      if (skill in skillToIndex) {
        mask |= 1 << skillToIndex[skill];
      }
    });
    return mask;
  });
  
  const n = reqSkills.length;
  const dp = new Map();
  dp.set(0, []);
  
  for (let mask = 0; mask < (1 << n); mask++) {
    if (!dp.has(mask)) continue;
    
    for (let i = 0; i < people.length; i++) {
      const newMask = mask | peopleSkills[i];
      if (!dp.has(newMask) || dp.get(newMask).length > dp.get(mask).length + 1) {
        dp.set(newMask, [...dp.get(mask), i]);
      }
    }
  }
  
  return dp.get((1 << n) - 1);
}
```

**Advantages:**
- Team selection optimization
- Skill-based matching
- Minimum team size

### 5. Letter Tile Possibilities

```javascript
function numTilePossibilities(tiles) {
  const count = {};
  for (const tile of tiles) {
    count[tile] = (count[tile] || 0) + 1;
  }
  
  const letters = Object.keys(count);
  const n = letters.length;
  
  function backtrack(mask) {
    let result = 1; // Count current sequence
    
    for (let i = 0; i < n; i++) {
      if (count[letters[i]] > 0) {
        count[letters[i]]--;
        result += backtrack(mask | (1 << i));
        count[letters[i]]++;
      }
    }
    
    return result;
  }
  
  return backtrack(0) - 1; // Subtract 1 for empty sequence
}
```

**Advantages:**
- Counts all possible sequences
- Handles duplicate letters
- Combinatorial counting

## Dry Run

**Example: Subset Sum**

**Input:**
```
nums `=` [1, 2, 3]
target `=` 4
```

**Step-by-Step Execution:**

```
n `=` 3, `2^n` `=` 8
dp `=` [false, false, false, false, false, false, false, false]
dp[0] `=` true

mask `=` 0 (binary: 000)
dp[0] `=` true
currentSum `=` 0
target `=` 4, not equal

mask `=` 1 (binary: 001, subset: `{0}`)
dp[1] `=` false, skip

mask `=` 2 (binary: 010, subset: `{1}`)
dp[2] `=` false, skip

mask `=` 3 (binary: 011, subset: `{0,1}`)
dp[3] `=` false, skip

mask `=` 4 (binary: 100, subset: `{2}`)
dp[4] `=` false, skip

mask `=` 5 (binary: 101, subset: `{0,2}`)
dp[5] `=` false, skip

mask `=` 6 (binary: 110, subset: `{1,2}`)
dp[6] `=` false, skip

mask `=` 7 (binary: 111, subset: `{0,1,2}`)
dp[7] `=` false, skip

First pass complete, no subsets found
Need to propagate from dp[0]

After propagation:
dp[1] `=` true (add element 0)
dp[2] `=` true (add element 1)
dp[4] `=` true (add element 2)
dp[3] `=` true (sum `=` 1+2 `=` 3)
dp[5] `=` true (sum `=` 1+3 `=` 4) → FOUND!
```

**Variable Changes Table:**

| mask | binary | subset | sum | dp[mask] | equals target? |
|------|--------|--------|-----|---------|----------------|
| 0 | 000 | `{}` | 0 | true | No |
| 1 | 001 | `{0}` | 1 | true | No |
| 2 | 010 | `{1}` | 2 | true | No |
| 3 | 011 | `{0,1}` | 3 | true | No |
| 4 | 100 | `{2}` | 3 | true | No |
| 5 | 101 | `{0,2}` | 4 | true | Yes |
| 6 | 110 | `{1,2}` | 5 | true | No |
| 7 | 111 | `{0,1,2}` | 6 | true | No |

## Edge Cases

### 1. Empty Array
```javascript
nums `=` []
target `=` 0
subsetSum([], 0) → true (empty subset)
Handle empty input
```

### 2. Single Element
```javascript
nums `=` [5]
target `=` 5
subsetSum([5], 5) → true
Base case
```

### 3. No Valid Subset
```javascript
nums `=` [1, 2, 3]
target `=` 10
subsetSum([1, 2, 3], 10) → false
No subset equals target
```

### 4. All Elements Sum
```javascript
nums `=` [1, 2, 3]
target `=` 6
subsetSum([1, 2, 3], 6) → true
Full subset
```

### 5. Zero Target
```javascript
nums `=` [1, 2, 3]
target `=` 0
subsetSum([1, 2, 3], 0) → true (empty subset)
Edge case
```

### 6. Large n
```javascript
n `=` 20
`2^20` `=` 1,048,576 states
Memory intensive
```

**Why Edge Cases Matter:**
- Empty array needs special handling
- Single element is base case
- No valid subset should return false
- Full subset is valid
- Zero target is edge case
- Large n causes memory issues

## Variations / Extensions

### 1. Count Subsets with Given Sum

```javascript
function countSubsets(nums, target) {
  const n = nums.length;
  const dp = new Array(1 << n).fill(0);
  dp[0] = 1;
  
  for (let mask = 0; mask < (1 << n); mask++) {
    if (dp[mask] > 0) {
      for (let i = 0; i < n; i++) {
        if (!(mask & (1 << i))) {
          const newMask = mask | (1 << i);
          dp[newMask] += dp[mask];
        }
      }
    }
  }
  
  let count = 0;
  for (let mask = 0; mask < (1 << n); mask++) {
    let sum = 0;
    for (let i = 0; i < n; i++) {
      if (mask & (1 << i)) sum += nums[i];
    }
    if (sum === target) count += dp[mask];
  }
  
  return count;
}
```

### 2. Maximum Size Subset with Given Sum

```javascript
function maxSizeSubset(nums, target) {
  const n = nums.length;
  const dp = new Array(1 << n).fill(-1);
  dp[0] = 0;
  
  for (let mask = 0; mask < (1 << n); mask++) {
    if (dp[mask] >= 0) {
      for (let i = 0; i < n; i++) {
        if (!(mask & (1 << i))) {
          const newMask = mask | (1 << i);
          dp[newMask] = Math.max(dp[newMask], dp[mask] + 1);
        }
      }
    }
  }
  
  let maxSize = 0;
  for (let mask = 0; mask < (1 << n); mask++) {
    let sum = 0;
    for (let i = 0; i < n; i++) {
      if (mask & (1 << i)) sum += nums[i];
    }
    if (sum === target) maxSize = Math.max(maxSize, dp[mask]);
  }
  
  return maxSize;
}
```

### 3. Minimum Subset Sum Difference

```javascript
function minSubsetSumDiff(nums) {
  const n = nums.length;
  const total = nums.reduce((a, b) => a + b, 0);
  const dp = new Array(1 << n).fill(0);
  
  for (let mask = 0; mask < (1 << n); mask++) {
    for (let i = 0; i < n; i++) {
      if (mask & (1 << i)) {
        dp[mask] += nums[i];
      }
    }
  }
  
  let minDiff = Infinity;
  for (let mask = 0; mask < (1 << n); mask++) {
    const sum1 = dp[mask];
    const sum2 = total - sum1;
    minDiff = Math.min(minDiff, Math.abs(sum1 - sum2));
  }
  
  return minDiff;
}
```

### 4. Hamiltonian Path

```javascript
function hamiltonianPath(graph) {
  const n = graph.length;
  const dp = Array(1 << n).fill(null).map(() => Array(n).fill(false));
  
  for (let i = 0; i < n; i++) {
    dp[1 << i][i] = true;
  }
  
  for (let mask = 0; mask < (1 << n); mask++) {
    for (let i = 0; i < n; i++) {
      if (dp[mask][i]) {
        for (let j = 0; j < n; j++) {
          if (graph[i][j] && !(mask & (1 << j))) {
            dp[mask | (1 << j)][j] = true;
          }
        }
      }
    }
  }
  
  const fullMask = (1 << n) - 1;
  for (let i = 0; i < n; i++) {
    if (dp[fullMask][i]) return true;
  }
  
  return false;
}
```

### 5. Bitmask DP for Longest Path in DAG

```javascript
function longestPathDAG(graph) {
  const n = graph.length;
  const dp = new Array(1 << n).fill(0);
  
  for (let mask = 0; mask < (1 << n); mask++) {
    for (let i = 0; i < n; i++) {
      if (mask & (1 << i)) {
        for (const j of graph[i]) {
          if (!(mask & (1 << j))) {
            dp[mask | (1 << j)] = Math.max(dp[mask | (1 << j)], dp[mask] + 1);
          }
        }
      }
    }
  }
  
  return Math.max(...dp);
}
```

## Optimization Techniques

### 1. Memoization

**Cache DP States:**
```javascript
// Use hash map or array
// Avoid recomputation
// Critical for efficiency
```

### 2. Bit Tricks

**Efficient Operations:**
```javascript
// Count set bits efficiently
// Iterate through set bits only
// Use built-in bit functions
```

### 3. State Compression

**Reduce State Space:**
```javascript
// Only store necessary information
// Use smaller data types
// Compress when possible
```

### 4. Pruning

**Skip Invalid States:**
```javascript
// Skip states that can't lead to solution
// Early termination
// Reduce search space
```

### 5. Trade-offs

**Bitmask DP vs Brute Force:**

| Aspect | Bitmask DP | Brute Force |
|--------|------------|-------------|
| Time | `O(n * 2^n)` | `O(n * 2^n)` |
| Space | `O(n * 2^n)` | `O(1)` |
| Optimization | Yes | No |
| Best For | Small n, optimization | Very small n |

**When to Use Bitmask DP:**
- n ≤ 20 (`2^n` is manageable)
- Subset-based optimization
- Need optimal solution
- DP has overlapping subproblems

## Complexity Analysis

### Time Complexity

**Subset Sum: `O(n * 2^n)`**
- `2^n` subsets
- `O(n)` to calculate sum per subset
- Total: `O(n * 2^n)`

**TSP: `O(n^2 * 2^n)`**
- `2^n` masks
- n cities per mask
- n transitions per city
- Total: `O(n^2 * 2^n)`

**Partition K Subsets: `O(k * 2^n)`**
- `2^n` masks
- k subsets
- Memoization reduces work
- Total: `O(k * 2^n)`

### Space Complexity

**Space: `O(n * 2^n)`**
- DP array of size `2^n`
- Each entry may store `O(n)` information
- Total: `O(n * 2^n)`

**Explanation:**
Bitmask DP has exponential time and space complexity due to the `2^n` possible subsets. However, for small n (typically n ≤ 20), this is manageable. The key insight is that we're trading exponential complexity for optimal solutions to NP-hard problems. Memoization is critical to avoid recomputation and make the approach feasible.

## Real-world Applications

### 1. Route Optimization

**Delivery Planning:**
- Optimize delivery routes
- Minimize travel time/cost
- Visit multiple locations
- Example: Amazon delivery

### 2. Resource Allocation

**Team Selection:**
- Select minimum team with required skills
- Optimize resource usage
- Skill-based matching
- Example: Project teams

### 3. Job Scheduling

**Task Assignment:**
- Assign tasks to workers
- Optimize completion time
- Handle constraints
- Example: Manufacturing

### 4. Combinatorial Optimization

**Complex Selections:**
- Optimize over subsets
- Handle constraints
- Find optimal configuration
- Example: Portfolio optimization

### 5. Network Design

**Infrastructure Planning:**
- Optimize network layout
- Minimize cost
- Connect all nodes
- Example: Telecommunications

### 6. DNA Sequencing

**Bioinformatics:**
- Optimize sequence assembly
- Find optimal ordering
- Handle constraints
- Example: Genome analysis

### 7. Game AI

**Strategy Games:**
- Optimize unit selection
- Plan optimal moves
- Resource management
- Example: Strategy games

### 8. Compiler Optimization

**Code Generation:**
- Optimize instruction selection
- Minimize execution time
- Handle dependencies
- Example: JIT compilers

## Common Mistakes

### 1. Ignoring Exponential Complexity

**Mistake:**
```javascript
// Not checking n size
// May cause memory overflow
// `2^20` = 1M, `2^25` = 33M
```

**Correct:**
```javascript
// Check n before using
// Limit to n ≤ 20
// Use heuristics for larger n
```

**Why It Matters:**
- Exponential grows very fast
- Memory overflow possible
- Must validate input size

### 2. Incorrect Bitmask Operations

**Mistake:**
```javascript
// Wrong bit operations
// Off-by-one errors
// Incorrect transitions
```

**Correct:**
```javascript
// Use correct bit operations
// Test with small examples
// Verify transitions
```

**Why It Matters:**
- Bit operations are tricky
- Off-by-one errors common
- Critical for correctness

### 3. Not Using Memoization

**Mistake:**
```javascript
// Recomputing states
// Exponential blowup
// Time limit exceeded
```

**Correct:**
```javascript
// Cache all states
// Use hash map or array
// Avoid recomputation
```

**Why It Matters:**
- Without memoization, exponential
- DP relies on caching
- Critical for efficiency

### 4. Wrong State Definition

**Mistake:**
```javascript
// State doesn't capture all info
// Can't reconstruct solution
// Incorrect transitions
```

**Correct:**
```javascript
// State must be complete
- Capture all necessary info
- Allow reconstruction
```

**Why It Matters:**
- State definition is key
- Incomplete state fails
- Must capture all info

### 5. Not Handling Base Cases

**Mistake:**
```javascript
// Missing base cases
// Incorrect initialization
// Wrong answer
```

**Correct:**
```javascript
// Initialize base cases
// Handle empty subset
// Set correct initial values
```

**Why It Matters:**
- Base cases are foundation
- Wrong initialization propagates
- Critical for correctness

### 6. Memory Overflow

**Mistake:**
```javascript
// Allocating too much memory
// `2^n` * n can be huge
// Runtime error
```

**Correct:**
```javascript
// Check memory requirements
// Use space optimization
- Limit problem size
```

**Why It Matters:**
- Memory is limited
- `2^n` grows fast
- Must manage memory

## Advanced Concepts

### 1. Meet-in-the-Middle

**Concept:**
Split problem in half, solve each half, combine results.

**Features:**
- Reduces `2^n` to `2^(n/2)`
- Handles larger n
- More complex implementation

### 2. Branch and Bound

**Concept:**
Prune search space using bounds.

**Features:**
- Skip impossible branches
- Reduces search space
- Heuristic-based

### 3. Approximation Algorithms

**Concept:**
Find near-optimal solutions for large instances.

**Features:**
- Polynomial time
- Guaranteed approximation ratio
- Used for large n

### 4. State Compression

**Concept:**
Compress state representation.

**Features:**
- Reduce memory usage
- More complex encoding
- Trade-off with speed

## Practice Thinking Guide

### How to Identify When to Use Bitmask DP

**Key Signals in Problem Statements:**

1. **"Subset" or "combination"**
   - Bitmask DP
   - Example: "Select subset of items"

2. **"Visit all" or "cover all"**
   - Bitmask DP
   - Example: "Visit all cities"

3. **"Partition" or "divide"**
   - Bitmask DP
   - Example: "Partition into k subsets"

4. **"Team" or "group" selection**
   - Bitmask DP
   - Example: "Select minimum team"

5. **"Permutation" with optimization**
   - Bitmask DP
   - Example: "Optimal ordering"

6. **"Small n" (n ≤ 20)**
   - Bitmask DP
   - Example: "n ≤ 15"

**Pattern Recognition:**

**Pattern 1: Subset Sum**
```
Problem: Find subset with given sum
Solution: Iterate all masks, check sum
```

**Pattern 2: TSP**
```
Problem: Visit all cities with minimum cost
Solution: DP[mask][i] `=` min cost to visit mask ending at i
```

**Pattern 3: Partition K Subsets**
```
Problem: Partition into k equal sum subsets
Solution: Backtrack with bitmask, memoize
```

**Pattern 4: Team Selection**
```
Problem: Select minimum team with required skills
Solution: DP[mask] `=` minimum team for skills in mask
```

**Pattern 5: Hamiltonian Path**
```
Problem: Find path visiting all nodes
Solution: DP[mask][i] `=` can reach mask ending at i
```

**Decision Flowchart:**

```
Subset-based problem?
├─ Yes → n ≤ 20?
│        ├─ Yes → Use Bitmask DP
│        └─ No → Use heuristics/approximation
├─ No → Permutation with optimization?
│        ├─ Yes → Use Bitmask DP
│        └─ No → Consider other
└─ No → Not Bitmask DP problem
```

**Example Problem Analysis:**

**Problem:** "Partition array into k equal sum subsets"

**Analysis:**
1. Need to partition into k subsets
2. Each subset must have equal sum
3. Track used elements with bitmask
4. Backtrack with memoization
5. Solution: Bitmask DP with backtracking

**Problem:** "Find minimum cost to visit all cities"

**Analysis:**
1. Need to visit all cities
2. Minimize total cost
3. Order matters (permutation)
4. TSP problem
5. Solution: DP[mask][i] for TSP

**Problem:** "Select minimum team with required skills"

**Analysis:**
1. Need to select people with skills
2. Minimize team size
3. Each person has specific skills
4. Subset selection problem
5. Solution: DP[mask] for skill coverage

## Summary

Bitmask Dynamic Programming is a powerful technique that uses bitmasks to represent subsets of elements efficiently. Each bit in an integer represents whether an element is included (1) or excluded (0) from the subset. Combined with dynamic programming, we can solve complex subset-based optimization problems by caching results and avoiding recomputation. This technique is essential for problems like the Traveling Salesman Problem, partition problems, and team selection where we need to optimize over all possible subsets. The key is defining the DP state correctly and efficiently transitioning between states.

**Key Takeaways:**
- Bitmask represents subset as integer
- `2^n` possible subsets for n elements
- DP caches results to avoid recomputation
- State definition is critical
- Bit operations are fast and efficient
- Limited to small n (n ≤ 20)
- `O(n * 2^n)` time complexity
- Essential for subset optimization

**Mastery Checklist:**
- ✅ Understand bitmask representation
- ✅ Implement subset sum
- ✅ Implement TSP
- ✅ Implement partition k subsets
- ✅ Use bit operations correctly
- ✅ Define DP state properly
- ✅ Handle memoization
- ✅ Know when to use
