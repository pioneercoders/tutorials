# Dynamic Programming

Dynamic Programming is an optimization technique that solves complex problems by breaking them into simpler subproblems and storing their results to avoid redundant computations.

## Introduction

Dynamic Programming (DP) is a powerful algorithmic paradigm that solves complex problems by breaking them down into simpler overlapping subproblems. Instead of solving the same subproblem multiple times, DP stores the results and reuses them, dramatically improving efficiency. It's particularly useful for optimization problems where we need to find the best solution among many possibilities.

**Why Dynamic Programming Exists:**
- Recursive solutions often recompute the same subproblems exponentially
- Storing subproblem results reduces exponential time to polynomial
- Essential for optimization problems (min/max, count, etc.)
- Foundation for many advanced algorithms
- Critical for competitive programming and interviews

**Where It Is Used:**
- Fibonacci numbers and similar sequences
- Pathfinding and shortest path problems
- Resource allocation and scheduling
- String matching and editing distance
- Knapsack and subset problems
- Game theory and AI decision making
- DNA sequence alignment in bioinformatics
- Financial portfolio optimization

## Core Concept Explanation

Dynamic Programming is based on two fundamental properties that must be present for DP to be applicable:

**1. Overlapping Subproblems:**
The same subproblems are solved multiple times in the recursive solution. Instead of recomputing, we store and reuse results.

**2. Optimal Substructure:**
The optimal solution to the problem can be constructed from optimal solutions to its subproblems.

**Step-by-Step Breakdown:**
1. Identify that the problem can be broken into subproblems
2. Recognize that subproblems overlap (same computations repeated)
3. Define a recurrence relation (how to build solution from subproblems)
4. Store subproblem results (memoization or tabulation)
5. Build the solution using stored results
6. Return the final answer

**Intuition Behind the Concept:**
Think of solving a maze. If you explore every path from the start, you'll visit the same intersections many times. Instead, you could mark each intersection you've visited and the shortest path to reach it. When you reach that intersection again, you already know the best way to get there. This is exactly what DP does - it "remembers" solutions to subproblems.

**Visual Thinking:**
```
Fibonacci without DP (exponential):
fib(5)
├─ fib(4)
│  ├─ fib(3)
│  │  ├─ fib(2)
│  │  │  ├─ fib(1) = 1
│  │  │  └─ fib(0) = 0
│  │  └─ fib(1) = 1
│  └─ fib(2)
│     ├─ fib(1) = 1
│     └─ fib(0) = 0
└─ fib(3)
   ├─ fib(2)
   │  ├─ fib(1) = 1
   │  └─ fib(0) = 0
   └─ fib(1) = 1

fib(2) computed 3 times! (redundant)

Fibonacci with DP (linear):
fib(5) = fib(4) + fib(3)
fib(4) = fib(3) + fib(2)
fib(3) = fib(2) + fib(1)
fib(2) = fib(1) + fib(0)
fib(1) = 1, fib(0) = 0

Each value computed once, stored, reused!
```

## Internal Working / Logic

Dynamic Programming operates in two main approaches, each with different execution flow:

**Approach 1: Top-Down (Memoization)**
- Start from the main problem
- Recursively break into subproblems
- Store results in a cache (hash map or array)
- Check cache before computing
- Used for: intuitive recursive solutions

**Approach 2: Bottom-Up (Tabulation)**
- Start from smallest subproblems
- Build up solutions iteratively
- Fill a table (array) with results
- Use previous values to compute current
- Used for: space-efficient solutions

**Flow Explanation (Top-Down):**
1. Define function with memo parameter
2. Check if result in memo: return if yes
3. Solve subproblems recursively
4. Store result in memo
5. Return result
6. Memo prevents redundant computations

**Flow Explanation (Bottom-Up):**
1. Identify base cases
2. Create DP table (array)
3. Fill base cases in table
4. Iterate through states in order
5. Use recurrence to fill each state
6. Return final state

**Decision Making Logic:**
The key decision is which approach to use:
- Top-Down: Easier to implement, intuitive, uses recursion stack
- Bottom-Up: More space-efficient, no recursion overhead, iterative
- Choose based on problem constraints and personal preference

## Algorithm / Approach

**Top-Down (Memoization) Algorithm**

```
1. Define function with memo parameter (hash map or array)
2. If n in memo: return memo[n]
3. If base case: return base value
4. Recursively solve subproblems
5. Store result: memo[n] = result
6. Return result
```

**Bottom-Up (Tabulation) Algorithm**

```
1. Identify base cases and recurrence relation
2. Create DP table of appropriate size
3. Initialize base cases in table
4. For each state from small to large:
   a. Compute using recurrence relation
   b. Store in table
5. Return final state
```

**DP State Definition Algorithm**

```
1. What do we need to track? (index, sum, etc.)
2. How many dimensions? (1D, 2D, 3D)
3. What is the range of each dimension?
4. Define dp[i] or dp[i][j] meaning
5. Write recurrence relation
6. Identify base cases
```

## Implementations

### 1. Fibonacci - Top-Down (Memoization)

```javascript
function fibonacci(n, memo = {}) {
  if (n in memo) return memo[n];
  if (n <= 1) return n;
  
  memo[n] = fibonacci(n - 1, memo) + fibonacci(n - 2, memo);
  return memo[n];
}
```

**Advantages:**
- Intuitive, mirrors mathematical definition
- Easy to implement
- Only computes needed states

**Disadvantages:**
- Recursion stack overhead
- Risk of stack overflow for large n
- Slightly slower than bottom-up

### 2. Fibonacci - Bottom-Up (Tabulation)

```javascript
function fibonacci(n) {
  if (n <= 1) return n;
  
  const dp = [0, 1];
  for (let i = 2; i <= n; i++) {
    dp[i] = dp[i - 1] + dp[i - 2];
  }
  return dp[n];
}
```

**Advantages:**
- No recursion overhead
- Iterative, faster execution
- No risk of stack overflow

**Disadvantages:**
- Must compute all states
- Less intuitive
- Uses O(n) space

### 3. Fibonacci - Space Optimized

```javascript
function fibonacci(n) {
  if (n <= 1) return n;
  
  let prev2 = 0, prev1 = 1;
  for (let i = 2; i <= n; i++) {
    [prev2, prev1] = [prev1, prev2 + prev1];
  }
  return prev1;
}
```

**Advantages:**
- O(1) space
- O(n) time
- Most efficient

### 4. Climbing Stairs

```javascript
function climbStairs(n) {
  if (n <= 2) return n;
  
  let prev2 = 1, prev1 = 2;
  for (let i = 3; i <= n; i++) {
    [prev2, prev1] = [prev1, prev2 + prev1];
  }
  return prev1;
}
```

**State Definition:**
- dp[i] = number of ways to reach step i
- Recurrence: dp[i] = dp[i-1] + dp[i-2]
- Base: dp[1] = 1, dp[2] = 2

### 5. 0/1 Knapsack

```javascript
function knapsack(weights, values, capacity) {
  const n = weights.length;
  const dp = Array(capacity + 1).fill(0);
  
  for (let i = 0; i < n; i++) {
    for (let w = capacity; w >= weights[i]; w--) {
      dp[w] = Math.max(dp[w], dp[w - weights[i]] + values[i]);
    }
  }
  
  return dp[capacity];
}
```

**State Definition:**
- dp[w] = max value with capacity w
- Recurrence: dp[w] = max(dp[w], dp[w-weight[i]] + value[i])
- Base: dp[0] = 0

### 6. Longest Common Subsequence

```javascript
function longestCommonSubsequence(text1, text2) {
  const m = text1.length, n = text2.length;
  const dp = Array(m + 1).fill().map(() => Array(n + 1).fill(0));
  
  for (let i = 1; i <= m; i++) {
    for (let j = 1; j <= n; j++) {
      if (text1[i - 1] === text2[j - 1]) {
        dp[i][j] = dp[i - 1][j - 1] + 1;
      } else {
        dp[i][j] = Math.max(dp[i - 1][j], dp[i][j - 1]);
      }
    }
  }
  
  return dp[m][n];
}
```

**State Definition:**
- dp[i][j] = LCS length of text1[0..i-1] and text2[0..j-1]
- Recurrence: match = dp[i-1][j-1] + 1, else max(dp[i-1][j], dp[i][j-1])
- Base: dp[0][j] = 0, dp[i][0] = 0

### 7. Coin Change

```javascript
function coinChange(coins, amount) {
  const dp = Array(amount + 1).fill(Infinity);
  dp[0] = 0;
  
  for (const coin of coins) {
    for (let i = coin; i <= amount; i++) {
      dp[i] = Math.min(dp[i], dp[i - coin] + 1);
    }
  }
  
  return dp[amount] === Infinity ? -1 : dp[amount];
}
```

**State Definition:**
- dp[i] = min coins to make amount i
- Recurrence: dp[i] = min(dp[i], dp[i-coin] + 1)
- Base: dp[0] = 0

## Dry Run

**Example: Fibonacci (Bottom-Up)**

**Input:**
```
n = 5
```

**Step-by-Step Execution:**

```
Initial State:
dp = [0, 1]

Iteration 1 (i = 2):
dp[2] = dp[1] + dp[0] = 1 + 0 = 1
dp = [0, 1, 1]

Iteration 2 (i = 3):
dp[3] = dp[2] + dp[1] = 1 + 1 = 2
dp = [0, 1, 1, 2]

Iteration 3 (i = 4):
dp[4] = dp[3] + dp[2] = 2 + 1 = 3
dp = [0, 1, 1, 2, 3]

Iteration 4 (i = 5):
dp[5] = dp[4] + dp[3] = 3 + 2 = 5
dp = [0, 1, 1, 2, 3, 5]

Final: dp[5] = 5
```

**Variable Changes Table:**

| Iteration | i | dp[i-2] | dp[i-1] | dp[i] | dp Array |
|-----------|---|---------|---------|-------|----------|
| Initial | - | - | - | - | [0,1] |
| 1 | 2 | 0 | 1 | 1 | [0,1,1] |
| 2 | 3 | 1 | 1 | 2 | [0,1,1,2] |
| 3 | 4 | 1 | 2 | 3 | [0,1,1,2,3] |
| 4 | 5 | 2 | 3 | 5 | [0,1,1,2,3,5] |

## Edge Cases

### 1. Base Case (n = 0 or n = 1)
```javascript
n = 0
fib(0) = 0 (base case)
n = 1
fib(1) = 1 (base case)
```

### 2. Small Input
```javascript
n = 2
fib(2) = fib(1) + fib(0) = 1 + 0 = 1
```

### 3. No Solution Possible
```javascript
coins = [2], amount = 3
dp[3] = Infinity (no solution)
Return -1
```

### 4. Empty Input
```javascript
weights = [], capacity = 10
dp[10] = 0 (no items to choose)
```

### 5. Large Capacity
```javascript
capacity = 10000, weights = [1, 2, 3]
DP table size = 10001
May need space optimization
```

### 6. Negative Values
```javascript
values = [-5, 10], capacity = 10
Need to handle negative values appropriately
May need to adjust recurrence
```

**Why Edge Cases Matter:**
- Base cases prevent infinite recursion
- No solution cases must return appropriate values
- Empty inputs test initialization logic
- Large inputs test space optimization
- Negative values test algorithm correctness

## Variations / Extensions

### 1. Longest Increasing Subsequence

```javascript
function lengthOfLIS(nums) {
  const dp = new Array(nums.length).fill(1);
  
  for (let i = 1; i < nums.length; i++) {
    for (let j = 0; j < i; j++) {
      if (nums[j] < nums[i]) {
        dp[i] = Math.max(dp[i], dp[j] + 1);
      }
    }
  }
  
  return Math.max(...dp);
}
```

### 2. Edit Distance

```javascript
function minDistance(word1, word2) {
  const m = word1.length, n = word2.length;
  const dp = Array(m + 1).fill().map(() => Array(n + 1).fill(0));
  
  for (let i = 0; i <= m; i++) dp[i][0] = i;
  for (let j = 0; j <= n; j++) dp[0][j] = j;
  
  for (let i = 1; i <= m; i++) {
    for (let j = 1; j <= n; j++) {
      if (word1[i - 1] === word2[j - 1]) {
        dp[i][j] = dp[i - 1][j - 1];
      } else {
        dp[i][j] = 1 + Math.min(
          dp[i - 1][j],      // delete
          dp[i][j - 1],      // insert
          dp[i - 1][j - 1]   // replace
        );
      }
    }
  }
  
  return dp[m][n];
}
```

### 3. Partition Equal Subset Sum

```javascript
function canPartition(nums) {
  const sum = nums.reduce((a, b) => a + b, 0);
  if (sum % 2 !== 0) return false;
  
  const target = sum / 2;
  const dp = new Array(target + 1).fill(false);
  dp[0] = true;
  
  for (const num of nums) {
    for (let i = target; i >= num; i--) {
      dp[i] = dp[i] || dp[i - num];
    }
  }
  
  return dp[target];
}
```

### 4. Unique Paths

```javascript
function uniquePaths(m, n) {
  const dp = Array(m).fill().map(() => Array(n).fill(1));
  
  for (let i = 1; i < m; i++) {
    for (let j = 1; j < n; j++) {
      dp[i][j] = dp[i - 1][j] + dp[i][j - 1];
    }
  }
  
  return dp[m - 1][n - 1];
}
```

### 5. Maximum Subarray

```javascript
function maxSubArray(nums) {
  const dp = new Array(nums.length);
  dp[0] = nums[0];
  let maxSum = nums[0];
  
  for (let i = 1; i < nums.length; i++) {
    dp[i] = Math.max(nums[i], dp[i - 1] + nums[i]);
    maxSum = Math.max(maxSum, dp[i]);
  }
  
  return maxSum;
}
```

### 6. Palindromic Substrings

```javascript
function countSubstrings(s) {
  const n = s.length;
  const dp = Array(n).fill().map(() => Array(n).fill(false));
  let count = 0;
  
  for (let i = 0; i < n; i++) {
    dp[i][i] = true;
    count++;
  }
  
  for (let len = 2; len <= n; len++) {
    for (let i = 0; i <= n - len; i++) {
      const j = i + len - 1;
      if (len === 2) {
        dp[i][j] = s[i] === s[j];
      } else {
        dp[i][j] = s[i] === s[j] && dp[i + 1][j - 1];
      }
      if (dp[i][j]) count++;
    }
  }
  
  return count;
}
```

## Optimization Techniques

### 1. Space Optimization

**1D DP from 2D:**
```javascript
// 2D version
const dp = Array(m).fill().map(() => Array(n).fill(0));

// 1D optimized version
const dp = Array(n).fill(0);
for (let i = 0; i < m; i++) {
  for (let j = n - 1; j >= 0; j--) {
    dp[j] = /* recurrence using dp[j] and dp[j-1] */;
  }
}
```

**O(1) Space:**
```javascript
// Only keep previous values
let prev = 0, curr = 1;
for (let i = 2; i <= n; i++) {
  [prev, curr] = [curr, prev + curr];
}
```

### 2. Time Optimization

**Early Termination:**
```javascript
// Stop if target reached
if (dp[target] !== Infinity) return dp[target];
```

**State Pruning:**
```javascript
// Only compute necessary states
// Use BFS/DFS with memoization instead of full table
```

### 3. Trade-offs

**Top-Down vs Bottom-Up:**

| Aspect | Top-Down | Bottom-Up |
|--------|----------|-----------|
| Intuition | High | Medium |
| Space | `O(n)` stack + memo | `O(n)` table |
| Overhead | Function calls | Loop overhead |
| Best For | Sparse states | Dense states |
| Debugging | Easier | Harder |

**When to Use Top-Down:**
- Problem has natural recursive structure
- Only need some states computed
- Easier to understand and debug

**When to Use Bottom-Up:**
- Need all states computed
- Space optimization is critical
- No recursion stack available

## Complexity Analysis

### Time Complexity

**1D DP: O(n)**
- Single loop through states
- Each state computed in O(1)
- Example: Fibonacci, Climbing Stairs

**2D DP: O(n × m)**
- Nested loops through two dimensions
- Each state computed in O(1)
- Example: Unique Paths, LCS

**Knapsack: O(n × capacity)**
- Loop through items and capacity
- Each state computed in O(1)
- Example: 0/1 Knapsack, Coin Change

**General: O(number of states × transitions)**
- Depends on state definition
- Each state may have multiple transitions
- Example: Complex DP problems

### Space Complexity

**Without Optimization: O(number of states)**
- Store all states in table
- 1D: O(n), 2D: O(n × m)
- Example: Standard tabulation

**With Space Optimization: O(n) or O(1)**
- Only keep necessary previous states
- 1D: O(1), 2D: O(n)
- Example: Fibonacci O(1), LCS O(n)

**Memoization: O(n) + stack space**
- Hash map for memo + recursion stack
- Stack space: O(n) worst case
- Example: Top-down Fibonacci

**Explanation:**
DP time complexity depends on the number of states and transitions. Space complexity can often be optimized by only keeping necessary states. Top-down uses stack space, bottom-up uses table space.

## Real-world Applications

### 1. Resource Allocation

**Knapsack Problem:**
- Allocate limited resources to maximize value
- Used in project selection, budget allocation
- Example: Choose projects with max ROI under budget

### 2. Inventory Management

**Production Planning:**
- Optimize production schedules
- Minimize costs while meeting demand
- Used in supply chain management

### 3. Route Optimization

**Shortest Path:**
- Find optimal routes in networks
- Used in GPS, logistics
- Example: Dijkstra's algorithm (DP variant)

### 4. Text Comparison

**Diff Tools:**
- Compare two versions of a file
- Find minimum edit distance
- Used in git, version control

### 5. DNA Sequence Alignment

**Bioinformatics:**
- Align DNA sequences
- Find similarities/differences
- Used in genetic research

### 6. Game Theory

**AI Decision Making:**
- Optimal strategies in games
- Minimax with memoization
- Used in chess engines, game AI

### 7. Financial Portfolio

**Investment Optimization:**
- Maximize returns under constraints
- Risk management
- Used in financial planning

### 8. Image Processing

**Image Segmentation:**
- Find optimal segmentation
- Used in computer vision
- Medical imaging analysis

## Common Mistakes

### 1. Not Identifying Overlapping Subproblems

**Mistake:**
```javascript
// Using recursion without memoization
function fib(n) {
  if (n <= 1) return n;
  return fib(n - 1) + fib(n - 2); // Exponential!
}
```

**Correct:**
```javascript
// Add memoization
function fib(n, memo = {}) {
  if (n in memo) return memo[n];
  if (n <= 1) return n;
  memo[n] = fib(n - 1, memo) + fib(n - 2, memo);
  return memo[n];
}
```

**Why It Matters:**
- Without memoization, exponential time
- Same subproblems computed repeatedly
- DP is specifically for overlapping subproblems

### 2. Wrong Base Cases

**Mistake:**
```javascript
// Missing or incorrect base cases
dp[0] = 0; // Might be wrong for some problems
```

**Correct:**
```javascript
// Define correct base cases
dp[0] = 1; // Depends on problem
dp[1] = 1;
```

**Why It Matters:**
- Base cases are foundation of DP
- Wrong base cases propagate errors
- Must carefully analyze problem

### 3. Incorrect Recurrence Relation

**Mistake:**
```javascript
// Wrong recurrence
dp[i] = dp[i - 1] + dp[i - 3]; // Missing dp[i - 2]
```

**Correct:**
```javascript
// Correct recurrence
dp[i] = dp[i - 1] + dp[i - 2] + dp[i - 3];
```

**Why It Matters:**
- Recurrence defines solution
- Wrong recurrence gives wrong answer
- Must derive from problem logic

### 4. Not Considering Order of Computation

**Mistake:**
```javascript
// Wrong order for bottom-up
for (let i = n; i >= 0; i--) { // Wrong direction
  dp[i] = dp[i + 1] + dp[i + 2];
}
```

**Correct:**
```javascript
// Correct order
for (let i = 2; i <= n; i++) {
  dp[i] = dp[i - 1] + dp[i - 2];
}
```

**Why It Matters:**
- Dependencies must be computed first
- Wrong order uses uninitialized values
- Must analyze dependency graph

### 5. Integer Overflow

**Mistake:**
```javascript
// Not handling large numbers
dp[i] = dp[i - 1] + dp[i - 2]; // Can overflow
```

**Correct:**
```javascript
// Use modulo or big integers
dp[i] = (dp[i - 1] + dp[i - 2]) % MOD;
```

**Why It Matters:**
- Fibonacci grows exponentially
- Can exceed integer limits
- Must handle large numbers appropriately

### 6. Not Optimizing Space

**Mistake:**
```javascript
// Using full 2D table when 1D suffices
const dp = Array(m).fill().map(() => Array(n).fill(0));
```

**Correct:**
```javascript
// Use 1D when possible
const dp = Array(n).fill(0);
```

**Why It Matters:**
- Space optimization is often required
- 2D tables can be memory-intensive
- Must analyze if full table needed

## Advanced Concepts

### 1. Bitmask DP

**Concept:**
Use bitmask to represent subsets in DP state.

**Example: Traveling Salesman Problem**

```javascript
function tsp(graph) {
  const n = graph.length;
  const dp = Array(1 << n).fill().map(() => Array(n).fill(Infinity));
  
  for (let i = 0; i < n; i++) {
    dp[1 << i][i] = graph[0][i];
  }
  
  for (let mask = 1; mask < (1 << n); mask++) {
    for (let last = 0; last < n; last++) {
      if (!(mask & (1 << last))) continue;
      
      for (let next = 0; next < n; next++) {
        if (mask & (1 << next)) continue;
        
        const newMask = mask | (1 << next);
        dp[newMask][next] = Math.min(
          dp[newMask][next],
          dp[mask][last] + graph[last][next]
        );
      }
    }
  }
  
  return Math.min(...dp[(1 << n) - 1]);
}
```

### 2. DP on Trees

**Concept:**
Apply DP on tree structures using post-order traversal.

**Example: Maximum Path Sum**

```javascript
function maxPathSum(root) {
  let maxSum = -Infinity;
  
  function dfs(node) {
    if (!node) return 0;
    
    const left = Math.max(0, dfs(node.left));
    const right = Math.max(0, dfs(node.right));
    
    maxSum = Math.max(maxSum, left + right + node.val);
    
    return node.val + Math.max(left, right);
  }
  
  dfs(root);
  return maxSum;
}
```

### 3. DP with Divide and Conquer

**Concept:**
Combine DP with divide and conquer for optimization.

**Example: Matrix Chain Multiplication**

```javascript
function matrixChainMultiplication(dims) {
  const n = dims.length - 1;
  const dp = Array(n).fill().map(() => Array(n).fill(0));
  
  for (let len = 2; len <= n; len++) {
    for (let i = 0; i <= n - len; i++) {
      const j = i + len - 1;
      dp[i][j] = Infinity;
      
      for (let k = i; k < j; k++) {
        const cost = dp[i][k] + dp[k + 1][j] + dims[i] * dims[k + 1] * dims[j + 1];
        dp[i][j] = Math.min(dp[i][j], cost);
      }
    }
  }
  
  return dp[0][n - 1];
}
```

### 4. Digit DP

**Concept:**
DP on digits of numbers for range queries.

**Example: Count Numbers with Digit Sum**

```javascript
function countNumbers(low, high, sum) {
  function count(num, sum) {
    const s = num.toString();
    const n = s.length;
    const dp = Array(n + 1).fill().map(() => Array(sum + 1).fill(0));
    
    dp[0][0] = 1;
    
    for (let i = 0; i < n; i++) {
      for (let j = 0; j <= sum; j++) {
        if (dp[i][j] === 0) continue;
        
        const maxDigit = i === n - 1 ? parseInt(s[i]) : 9;
        for (let d = 0; d <= maxDigit && j + d <= sum; d++) {
          dp[i + 1][j + d] += dp[i][j];
        }
      }
    }
    
    return dp[n][sum];
  }
  
  return count(high, sum) - count(low - 1, sum);
}
```

## Practice Thinking Guide

### How to Identify When to Use Dynamic Programming

**Key Signals in Problem Statements:**

1. **"Find minimum/maximum/optimal solution"**
   - Optimization problem
   - Example: "Minimum cost to reach destination"

2. **"Count the number of ways"**
   - Counting problem with overlapping subproblems
   - Example: "Number of ways to climb stairs"

3. **"Longest/shortest path/sequence"**
   - Path or sequence optimization
   - Example: "Longest increasing subsequence"

4. **"Can we partition/split"**
   - Partition problems
   - Example: "Partition equal subset sum"

5. **"Edit distance/difference"**
   - String comparison
   - Example: "Minimum edit distance"

6. **"Knapsack/subset"**
   - Selection under constraints
   - Example: "Maximum value with weight limit"

**Pattern Recognition:**

**Pattern 1: Linear DP**
```
Problem: Single sequence, linear recurrence
Solution: 1D DP array
```

**Pattern 2: Grid DP**
```
Problem: 2D grid, pathfinding
Solution: 2D DP array
```

**Pattern 3: Knapsack**
```
Problem: Select items under constraint
Solution: 1D/2D DP with capacity dimension
```

**Pattern 4: LCS/Edit Distance**
```
Problem: Compare two sequences
Solution: 2D DP with both sequences
```

**Pattern 5: Subsequence**
```
Problem: Find subsequence with property
Solution: 1D/2D DP with index tracking
```

**Decision Flowchart:**

```
Is there optimal substructure?
├─ Yes → Are subproblems overlapping?
│        ├─ Yes → Can we define recurrence?
│        │        ├─ Yes → Use DP
│        │        └─ No → Consider other approach
│        └─ No → Not DP (divide and conquer)
└─ No → Not DP (greedy or other)
```

**Example Problem Analysis:**

**Problem:** "Find minimum number of coins to make amount"

**Analysis:**
1. Need minimum → optimization problem
2. Subproblems: min coins for smaller amounts
3. Overlapping: same amount computed multiple times
4. Recurrence: dp[i] = min(dp[i-coin] + 1)
5. Solution: 1D DP (unbounded knapsack)

**Problem:** "Longest common subsequence of two strings"

**Analysis:**
1. Need longest → optimization problem
2. Subproblems: LCS of prefixes
3. Overlapping: same prefixes compared multiple times
4. Recurrence: match = dp[i-1][j-1] + 1, else max(dp[i-1][j], dp[i][j-1])
5. Solution: 2D DP

**Problem:** "Number of ways to climb n stairs"

**Analysis:**
1. Need count → counting problem
2. Subproblems: ways to reach smaller steps
3. Overlapping: same step computed multiple times
4. Recurrence: dp[i] = dp[i-1] + dp[i-2]
5. Solution: 1D DP

## Summary

Dynamic Programming is a powerful optimization technique that solves complex problems by breaking them into overlapping subproblems and storing results to avoid redundant computations. It's essential for optimization problems and forms the foundation for many advanced algorithms.

**Key Takeaways:**
- Requires overlapping subproblems and optimal substructure
- Two approaches: top-down (memoization) and bottom-up (tabulation)
- Time: O(states × transitions), Space: O(states) or optimized
- Define state, recurrence, and base cases clearly
- Always consider space optimization
- Choose approach based on problem constraints
- Verify with small examples before implementation

**Mastery Checklist:**
- ✅ Identify DP problems (overlapping subproblems)
- ✅ Define DP state correctly
- ✅ Derive recurrence relation
- ✅ Implement both top-down and bottom-up
- ✅ Handle base cases properly
- ✅ Optimize space when possible
- ✅ Recognize common DP patterns
- ✅ Debug DP solutions effectively
