# Backtracking

Backtracking is a systematic way to iterate through all possible configurations of a problem. It builds candidates incrementally and abandons a candidate ("backtracks") as soon as it determines it cannot lead to a valid solution.

## Introduction

Backtracking is a systematic algorithmic technique that explores all possible configurations of a problem by building solutions incrementally and abandoning candidates ("backtracking") as soon as it determines they cannot lead to a valid solution. It's essentially a depth-first search with pruning, where we explore a decision tree and cut off branches that cannot possibly lead to a solution. This makes backtracking ideal for problems requiring exhaustive search with constraints, such as generating permutations, combinations, subsets, and solving constraint satisfaction problems like N-Queens and Sudoku.

**Why Backtracking Exists:**
- Some problems require exploring all possibilities
- Brute force is too slow without pruning
- Constraints can be checked incrementally
- Need to find all valid configurations
- Natural for decision tree problems

**Where It Is Used:**
- Generating permutations, combinations, subsets
- Solving N-Queens, Sudoku, crossword puzzles
- Constraint satisfaction problems
- Scheduling and resource allocation
- Path finding in mazes
- Test case generation
- Configuration generation

## Core Concept Explanation

Backtracking works by building a solution incrementally, making a series of decisions at each step. When a decision leads to an invalid state (violates constraints), we "backtrack" by undoing that decision and trying a different option. This continues until we either find a valid solution or exhaust all possibilities. The key is pruning - cutting off branches early when they cannot possibly lead to a solution, which dramatically reduces the search space.

**Step-by-Step Breakdown:**
1. Start with an empty or initial state
2. Make a decision (choose an option)
3. Check if the decision is valid (satisfies constraints)
4. If valid, recursively continue building the solution
5. If invalid or complete, backtrack (undo the decision)
6. Try the next option
7. Repeat until all possibilities are explored

**Intuition Behind the Concept:**
Think of exploring a maze. You start at the entrance and choose a path. If you hit a dead end, you backtrack to the last intersection and try a different path. You continue this until you find the exit or have explored all possible paths. Backtracking is the same idea applied to decision trees.

**Visual Thinking:**
```
Backtracking Decision Tree:

Problem: Generate subsets of [1, 2]

                    []
                   /  \
                 [1]  []
                /  \    \
            [1,2] [1]  [2]
               |    |    |
            [1,2] [1]  [2]

Backtracking Process:
1. Start with []
2. Choose to include 1 → [1]
3. Choose to include 2 → [1,2] (valid, add to result)
4. Backtrack: remove 2 → [1]
5. Choose to exclude 2 → [1] (valid, add to result)
6. Backtrack: remove 1 → []
7. Choose to exclude 1 → []
8. Choose to include 2 → [2] (valid, add to result)
9. Backtrack: remove 2 → []
10. Choose to exclude 2 → [] (valid, add to result)

Result: [[1,2], [1], [2], []]
```

## Internal Working / Logic

Backtracking operates through a recursive exploration of a decision tree, where each node represents a partial solution and each edge represents a decision. The algorithm maintains the current state and explores all valid options at each step, backtracking when a path cannot lead to a solution.

**Phase 1: Decision Making**
- At each step, choose from available options
- Check if the choice is valid (satisfies constraints)
- If valid, make the choice and proceed
- If invalid, skip to next option

**Phase 2: Recursive Exploration**
- Recursively continue building the solution
- Maintain the current state
- Check if we've reached a complete solution
- If complete, add to results

**Phase 3: Backtracking**
- After exploring a path, undo the last decision
- Restore the previous state
- Try the next option
- Continue until all options are exhausted

**Flow Explanation (Subsets):**
1. Start with empty subset
2. For each element, decide to include or exclude
3. Include: add to current subset, recurse
4. Backtrack: remove from current subset
5. Exclude: don't add, recurse
6. Continue until all elements processed
7. Add complete subset to results

**Decision Making Logic:**
The key decision is when to prune:
- Prune when constraints are violated
- Prune when remaining elements cannot complete solution
- Prune when solution is found (if only one needed)
- Don't prune if all possibilities needed

## Algorithm / Approach

**General Backtracking Algorithm**

```
1. Define function with current state
2. Check if current state is complete solution:
   a. If yes: add to results, return
3. For each available option:
   a. Check if option is valid
   b. If valid: make choice, update state
   c. Recursively call with new state
   d. Backtrack: undo choice, restore state
4. Return
```

**Subset Generation Algorithm**

```
1. Start with empty subset
2. For each element:
   a. Include element: add to subset
   b. Recurse with next element
   c. Backtrack: remove element
   d. Exclude element: don't add
   e. Recurse with next element
3. Add complete subset to results
```

**Permutation Generation Algorithm**

```
1. Start with original array
2. For each position:
   a. Try each unused element
   b. Swap element to current position
   c. Recurse with next position
   d. Backtrack: swap back
3. Add complete permutation to results
```

**N-Queens Algorithm**

```
1. Start with empty board
2. For each row:
   a. Try each column
   b. Check if queen placement is valid
   c. If valid: place queen, mark attacks
   d. Recurse with next row
   e. Backtrack: remove queen, unmark attacks
3. Add complete board to results
```

## Implementations

### 1. Generate All Subsets

```javascript
function generateSubsets(nums) {
  const result = [];
  
  function backtrack(index, current) {
    if (index === nums.length) {
      result.push([...current]);
      return;
    }
    
    // Include current element
    current.push(nums[index]);
    backtrack(index + 1, current);
    current.pop();
    
    // Exclude current element
    backtrack(index + 1, current);
  }
  
  backtrack(0, []);
  return result;
}
```

**Advantages:**
- Generates all 2^n subsets
- Simple decision tree
- Easy to understand

### 2. Generate All Permutations

```javascript
function generatePermutations(nums) {
  const result = [];
  
  function backtrack(start) {
    if (start === nums.length) {
      result.push([...nums]);
      return;
    }
    
    for (let i = start; i < nums.length; i++) {
      [nums[start], nums[i]] = [nums[i], nums[start]];
      backtrack(start + 1);
      [nums[start], nums[i]] = [nums[i], nums[start]];
    }
  }
  
  backtrack(0);
  return result;
}
```

**Advantages:**
- Generates all n! permutations
- In-place swapping
- No extra space for visited

### 3. Combination Sum

```javascript
function combinationSum(candidates, target) {
  const result = [];
  
  function backtrack(start, current, remaining) {
    if (remaining === 0) {
      result.push([...current]);
      return;
    }
    
    if (remaining < 0) return;
    
    for (let i = start; i < candidates.length; i++) {
      current.push(candidates[i]);
      backtrack(i, current, remaining - candidates[i]);
      current.pop();
    }
  }
  
  backtrack(0, [], target);
  return result;
}
```

**Advantages:**
- Allows reuse of elements
- Prunes when sum exceeds target
- Efficient with sorting

### 4. N-Queens

```javascript
function solveNQueens(n) {
  const result = [];
  
  function backtrack(row, cols, diag1, diag2, board) {
    if (row === n) {
      result.push([...board]);
      return;
    }
    
    for (let col = 0; col < n; col++) {
      const d1 = row - col;
      const d2 = row + col;
      
      if (cols.has(col) || diag1.has(d1) || diag2.has(d2)) continue;
      
      cols.add(col);
      diag1.add(d1);
      diag2.add(d2);
      board.push('.'.repeat(col) + 'Q' + '.'.repeat(n - col - 1));
      
      backtrack(row + 1, cols, diag1, diag2, board);
      
      board.pop();
      cols.delete(col);
      diag1.delete(d1);
      diag2.delete(d2);
    }
  }
  
  backtrack(0, new Set(), new Set(), new Set(), []);
  return result;
}
```

**Advantages:**
- Uses sets for O(1) conflict checking
- Efficient pruning
- Classic backtracking problem

### 5. Sudoku Solver

```javascript
function solveSudoku(board) {
  function isValid(row, col, num) {
    for (let i = 0; i < 9; i++) {
      if (board[row][i] === num) return false;
      if (board[i][col] === num) return false;
      const boxRow = 3 * Math.floor(row / 3) + Math.floor(i / 3);
      const boxCol = 3 * Math.floor(col / 3) + i % 3;
      if (board[boxRow][boxCol] === num) return false;
    }
    return true;
  }
  
  function solve(row, col) {
    if (row === 9) return true;
    if (col === 9) return solve(row + 1, 0);
    if (board[row][col] !== '.') return solve(row, col + 1);
    
    for (let num = 1; num <= 9; num++) {
      if (isValid(row, col, num.toString())) {
        board[row][col] = num.toString();
        if (solve(row, col + 1)) return true;
        board[row][col] = '.';
      }
    }
    
    return false;
  }
  
  return solve(0, 0);
}
```

### 6. Word Search

```javascript
function exist(board, word) {
  const rows = board.length;
  const cols = board[0].length;
  
  function backtrack(row, col, index) {
    if (index === word.length) return true;
    if (row < 0 || row >= rows || col < 0 || col >= cols) return false;
    if (board[row][col] !== word[index]) return false;
    
    const temp = board[row][col];
    board[row][col] = '#';
    
    const found = backtrack(row + 1, col, index + 1) ||
                  backtrack(row - 1, col, index + 1) ||
                  backtrack(row, col + 1, index + 1) ||
                  backtrack(row, col - 1, index + 1);
    
    board[row][col] = temp;
    return found;
  }
  
  for (let i = 0; i < rows; i++) {
    for (let j = 0; j < cols; j++) {
      if (backtrack(i, j, 0)) return true;
    }
  }
  
  return false;
}
```

## Dry Run

**Example: Generate Subsets of [1, 2]**

**Input:**
```
nums = [1, 2]
```

**Step-by-Step Execution:**

```
Initial State:
result = []
backtrack(0, [])

Iteration 1 (index = 0, current = []):
Include nums[0] = 1
current = [1]
backtrack(1, [1])

  Iteration 2 (index = 1, current = [1]):
  Include nums[1] = 2
  current = [1, 2]
  backtrack(2, [1, 2])
  
    Iteration 3 (index = 2, current = [1, 2]):
    index === nums.length
    result.push([1, 2])
    result = [[1, 2]]
    return
  
  Backtrack: current.pop() → [1]
  Exclude nums[1] = 2
  backtrack(2, [1])
  
    Iteration 4 (index = 2, current = [1]):
    index === nums.length
    result.push([1])
    result = [[1, 2], [1]]
    return

Backtrack: current.pop() → []
Exclude nums[0] = 1
backtrack(1, [])

  Iteration 5 (index = 1, current = []):
  Include nums[1] = 2
  current = [2]
  backtrack(2, [2])
  
    Iteration 6 (index = 2, current = [2]):
    index === nums.length
    result.push([2])
    result = [[1, 2], [1], [2]]
    return
  
  Backtrack: current.pop() → []
  Exclude nums[1] = 2
  backtrack(2, [])
  
    Iteration 7 (index = 2, current = []):
    index === nums.length
    result.push([])
    result = [[1, 2], [1], [2], []]
    return

Final: result = [[1, 2], [1], [2], []]
```

**Variable Changes Table:**

| Call | index | current | Action | result (after) |
|------|-------|---------|--------|----------------|
| 1 | 0 | [] | Include 1 | - |
| 2 | 1 | [1] | Include 2 | - |
| 3 | 2 | [1, 2] | Complete | [[1, 2]] |
| 4 | 2 | [1] | Complete | [[1, 2], [1]] |
| 5 | 1 | [] | Include 2 | - |
| 6 | 2 | [2] | Complete | [[1, 2], [1], [2]] |
| 7 | 2 | [] | Complete | [[1, 2], [1], [2], []] |

## Edge Cases

### 1. Empty Input
```javascript
nums = []
generateSubsets([]) → [[]]
Only empty subset exists
```

### 2. Single Element
```javascript
nums = [1]
generateSubsets([1]) → [[1], []]
Two subsets: include and exclude
```

### 3. Duplicates in Input
```javascript
nums = [1, 1]
generateSubsets([1, 1]) → [[1,1], [1], [1], []]
Duplicates cause duplicate subsets
Need to handle with sorting
```

### 4. No Valid Solution
```javascript
combinationSum([2, 4, 6], 7) → []
No combination sums to 7
Return empty result
```

### 5. Large Input
```javascript
nums = [1, 2, 3, 4, 5, 6, 7, 8]
generatePermutations(nums) → 40320 permutations
Exponential growth
```

### 6. Zero Target
```javascript
combinationSum([1, 2, 3], 0) → [[]]
Empty combination sums to 0
```

**Why Edge Cases Matter:**
- Empty input tests boundary
- Single element tests base case
- Duplicates need special handling
- No solution tests pruning
- Large input tests performance
- Zero target tests edge case

## Variations / Extensions

### 1. Subsets with Duplicates

```javascript
function subsetsWithDup(nums) {
  nums.sort((a, b) => a - b);
  const result = [];
  
  function backtrack(index, current) {
    result.push([...current]);
    
    for (let i = index; i < nums.length; i++) {
      if (i > index && nums[i] === nums[i - 1]) continue;
      current.push(nums[i]);
      backtrack(i + 1, current);
      current.pop();
    }
  }
  
  backtrack(0, []);
  return result;
}
```

### 2. Permutations with Duplicates

```javascript
function permuteUnique(nums) {
  nums.sort((a, b) => a - b);
  const result = [];
  const used = new Array(nums.length).fill(false);
  
  function backtrack(current) {
    if (current.length === nums.length) {
      result.push([...current]);
      return;
    }
    
    for (let i = 0; i < nums.length; i++) {
      if (used[i] || (i > 0 && nums[i] === nums[i - 1] && !used[i - 1])) continue;
      used[i] = true;
      current.push(nums[i]);
      backtrack(current);
      current.pop();
      used[i] = false;
    }
  }
  
  backtrack([]);
  return result;
}
```

### 3. Combination Sum II

```javascript
function combinationSum2(candidates, target) {
  candidates.sort((a, b) => a - b);
  const result = [];
  
  function backtrack(start, current, remaining) {
    if (remaining === 0) {
      result.push([...current]);
      return;
    }
    
    if (remaining < 0) return;
    
    for (let i = start; i < candidates.length; i++) {
      if (i > start && candidates[i] === candidates[i - 1]) continue;
      current.push(candidates[i]);
      backtrack(i + 1, current, remaining - candidates[i]);
      current.pop();
    }
  }
  
  backtrack(0, [], target);
  return result;
}
```

### 4. Palindrome Partitioning

```javascript
function partition(s) {
  const result = [];
  
  function isPalindrome(str, left, right) {
    while (left < right) {
      if (str[left] !== str[right]) return false;
      left++;
      right--;
    }
    return true;
  }
  
  function backtrack(start, current) {
    if (start === s.length) {
      result.push([...current]);
      return;
    }
    
    for (let end = start; end < s.length; end++) {
      if (isPalindrome(s, start, end)) {
        current.push(s.substring(start, end + 1));
        backtrack(end + 1, current);
        current.pop();
      }
    }
  }
  
  backtrack(0, []);
  return result;
}
```

### 5. Letter Combinations of Phone Number

```javascript
function letterCombinations(digits) {
  if (!digits.length) return [];
  
  const mapping = {
    '2': 'abc', '3': 'def', '4': 'ghi', '5': 'jkl',
    '6': 'mno', '7': 'pqrs', '8': 'tuv', '9': 'wxyz'
  };
  
  const result = [];
  
  function backtrack(index, current) {
    if (index === digits.length) {
      result.push(current.join(''));
      return;
    }
    
    for (const char of mapping[digits[index]]) {
      current.push(char);
      backtrack(index + 1, current);
      current.pop();
    }
  }
  
  backtrack(0, []);
  return result;
}
```

## Optimization Techniques

### 1. Pruning

**Early Termination:**
```javascript
// Stop when constraints violated
// Don't explore invalid paths
// Dramatically reduces search space
```

### 2. Sorting

**Pre-sort Input:**
```javascript
// Sort to handle duplicates
// Enables early pruning
// Improves efficiency
```

### 3. Memoization

**Cache Results:**
```javascript
// Cache subproblem results
// Avoid redundant computation
// Trade space for time
```

### 4. Trade-offs

**Backtracking vs Dynamic Programming:**

| Aspect | Backtracking | Dynamic Programming |
|--------|--------------|---------------------|
| Approach | Exhaustive search | Optimal substructure |
| Time | Exponential | Polynomial |
| Space | `O(n)` recursion | `O(n)` table |
| Best For | All solutions | Optimal solution |
| Pruning | Possible | Not needed |

**When to Use DP Instead:**
- Need optimal solution, not all solutions
- Overlapping subproblems exist
- Optimal substructure property
- Time is critical

## Complexity Analysis

### Time Complexity

**Subsets: O(2^n)**
- Each element has 2 choices
- 2^n total subsets
- Example: Generate all subsets

**Permutations: O(n!)**
- n! possible arrangements
- Each position has n choices
- Example: Generate all permutations

**Combination Sum: O(2^n)**
- Each element can be used multiple times
- Exponential in worst case
- Example: Combination sum

**N-Queens: O(n!)**
- n! possible arrangements
- Pruning reduces actual work
- Example: N-Queens problem

### Space Complexity

**Recursion Stack: O(n)**
- Maximum depth of recursion
- Store current state
- Example: All backtracking problems

**Result Storage: O(n * 2^n)**
- Store all solutions
- Exponential in worst case
- Example: Subsets, permutations

**Explanation:**
Backtracking has exponential time complexity because it explores all possibilities. Space is O(n) for recursion stack, but storing all results can be exponential. Pruning can significantly reduce actual work.

## Real-world Applications

### 1. Scheduling

**Task Scheduling:**
- Assign tasks to time slots
- Satisfy constraints
- Example: Course scheduling

### 2. Resource Allocation

**Resource Management:**
- Allocate resources to tasks
- Satisfy constraints
- Example: Cloud resource allocation

### 3. Configuration Generation

**System Configuration:**
- Generate valid configurations
- Satisfy constraints
- Example: Software configuration

### 4. Test Case Generation

**Software Testing:**
- Generate test cases
- Cover all possibilities
- Example: Combinatorial testing

### 5. Constraint Satisfaction

**CSP Problems:**
- Satisfy constraints
- Find valid assignments
- Example: Sudoku, crossword

### 6. Path Finding

**Maze Solving:**
- Find all paths
- Avoid obstacles
- Example: Maze solving algorithms

### 7. Game AI

**Game Solving:**
- Explore all moves
- Find winning strategy
- Example: Tic-tac-toe solver

### 8. Cryptography

**Code Breaking:**
- Try all combinations
- Find valid keys
- Example: Brute force decryption

## Common Mistakes

### 1. Not Backtracking

**Mistake:**
```javascript
// Forgot to undo choice
current.push(nums[i]);
backtrack(index + 1, current);
// Forgot to pop!
```

**Correct:**
```javascript
// Always backtrack
current.push(nums[i]);
backtrack(index + 1, current);
current.pop(); // Backtrack
```

**Why It Matters:**
- State gets corrupted
- Wrong results
- Must undo choices

### 2. Not Pruning

**Mistake:**
```javascript
// No pruning
for (let i = 0; i < nums.length; i++) {
  // Always explore
}
```

**Correct:**
```javascript
// Prune invalid paths
if (remaining < 0) return; // Prune
for (let i = start; i < nums.length; i++) {
  // Only explore valid
}
```

**Why It Matters:**
- Without pruning, exponential time
- Pruning dramatically reduces work
- Essential for performance

### 3. Not Handling Duplicates

**Mistake:**
```javascript
// Doesn't handle duplicates
// Generates duplicate results
```

**Correct:**
```javascript
// Sort and skip duplicates
nums.sort((a, b) => a - b);
if (i > start && nums[i] === nums[i - 1]) continue;
```

**Why It Matters:**
- Duplicates cause duplicate results
- Must skip duplicates
- Sorting enables this

### 4. Not Copying State

**Mistake:**
```javascript
// Reference copy
result.push(current); // Wrong!
```

**Correct:**
```javascript
// Deep copy
result.push([...current]); // Correct
```

**Why It Matters:**
- Reference copy shares state
- Results get corrupted
- Must deep copy

### 5. Stack Overflow

**Mistake:**
```javascript
// Deep recursion
// Stack overflow
```

**Correct:**
```javascript
// Use iterative approach
// Or increase stack limit
```

**Why It Matters:**
- Deep recursion causes overflow
- Must handle large inputs
- Consider iterative solution

### 6. Wrong Base Case

**Mistake:**
```javascript
// Wrong base case
if (index > nums.length) return; // Wrong
```

**Correct:**
```javascript
// Correct base case
if (index === nums.length) return; // Correct
```

**Why It Matters:**
- Wrong base case causes errors
- Must check exact condition
- Critical for correctness

## Advanced Concepts

### 1. Branch and Bound

**Concept:**
Use bounds to prune entire branches.

**Features:**
- Calculate upper/lower bounds
- Prune if bound exceeds best
- Used in optimization problems

### 2. Constraint Propagation

**Concept:**
Propagate constraints to reduce search space.

**Features:**
- Reduce domain of variables
- Detect conflicts early
- Used in CSP solvers

### 3. Heuristic Search

**Concept:**
Use heuristics to guide search.

**Features:**
- Prioritize promising paths
- Find solution faster
- Used in AI search

### 4. Parallel Backtracking

**Concept:**
Explore branches in parallel.

**Features:**
- Multi-threaded exploration
- Faster for large problems
- Complex synchronization

## Practice Thinking Guide

### How to Identify When to Use Backtracking

**Key Signals in Problem Statements:**

1. **"All possible/permutations/combinations"**
   - Need to generate all possibilities
   - Example: "Generate all subsets"

2. **"Find all solutions"**
   - Multiple valid solutions exist
   - Example: "Solve N-Queens"

3. **"Satisfy constraints"**
   - Constraint satisfaction problem
   - Example: "Sudoku solver"

4. **"Can be placed/arranged"**
   - Placement/arrangement problem
   - Example: "Word search"

5. **"Sum equals target"**
   - Combination sum problem
   - Example: "Combination sum"

6. **"Valid configuration"**
   - Find valid configurations
   - Example: "Palindrome partitioning"

**Pattern Recognition:**

**Pattern 1: Subsets**
```
Problem: Generate all subsets
Solution: Include/exclude each element
```

**Pattern 2: Permutations**
```
Problem: Generate all permutations
Solution: Swap elements to each position
```

**Pattern 3: Combination Sum**
```
Problem: Sum to target
Solution: Include/exclude with remaining sum
```

**Pattern 4: N-Queens**
```
Problem: Place queens without attacks
Solution: Try each column, check constraints
```

**Pattern 5: Word Search**
```
Problem: Find word in grid
Solution: Try each cell, explore neighbors
```

**Decision Flowchart:**

```
Need all possibilities?
├─ Yes → Can prune invalid paths?
│        ├─ Yes → Use backtracking
│        └─ No → Use brute force
├─ No → Need optimal solution?
│        ├─ Yes → Use DP
│        └─ No → Consider other
└─ No → Not backtracking problem
```

**Example Problem Analysis:**

**Problem:** "Generate all subsets of array"

**Analysis:**
1. Need to generate all subsets
2. Each element has 2 choices (include/exclude)
3. Backtracking naturally handles this
4. 2^n subsets
5. Solution: Include/exclude backtracking

**Problem:** "Solve N-Queens"

**Analysis:**
1. Need to place N queens
2. Each row needs one queen
3. Check column and diagonal constraints
4. Backtrack when conflict
5. Solution: Try each column, check constraints

**Problem:** "Combination sum to target"

**Analysis:**
1. Need combinations that sum to target
2. Can reuse elements
3. Prune when sum exceeds target
4. Backtracking with remaining sum
5. Solution: Include/exclude with remaining sum

## Summary

Backtracking is a powerful technique for exploring all possible configurations of a problem. It builds solutions incrementally and backtracks when a path cannot lead to a valid solution. Understanding the decision tree, pruning, and state management is crucial for effective backtracking.

**Key Takeaways:**
- Build solutions incrementally
- Backtrack when invalid
- Prune invalid paths early
- Always undo choices after recursion
- Handle duplicates with sorting
- Exponential time complexity
- O(n) space for recursion stack
- Use when all solutions needed

**Mastery Checklist:**
- ✅ Understand backtracking concept
- ✅ Generate subsets
- ✅ Generate permutations
- ✅ Solve combination sum
- ✅ Solve N-Queens
- ✅ Handle duplicates
- ✅ Implement pruning
- ✅ Choose backtracking vs DP

