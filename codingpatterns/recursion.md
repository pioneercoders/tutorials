# Recursion

Recursion is a technique where a function calls itself to solve smaller instances of the same problem. It follows the divide and conquer principle - break down complex problems into simpler, self-similar subproblems.

## Introduction

Recursion is a powerful problem-solving technique where a function calls itself to solve smaller instances of the same problem. It's based on the principle of divide and conquer: break down a complex problem into simpler, self-similar subproblems, solve the base case (simplest instance), and combine solutions to solve the original problem. Recursion is particularly useful for problems with recursive structures like trees, graphs, and nested data.

**Why Recursion Exists:**
- Some problems are naturally recursive (trees, graphs, nested structures)
- Recursive solutions are often more elegant and readable
- Divide and conquer algorithms rely on recursion
- Backtracking and exploration algorithms use recursion
- Mathematical definitions are often recursive

**Where It Is Used:**
- Tree and graph traversals
- Divide and conquer algorithms (merge sort, quicksort)
- Backtracking problems (N-Queens, Sudoku)
- Dynamic programming (with memoization)
- Parsing nested structures (JSON, XML, HTML)
- File system traversal
- Mathematical computations (factorial, Fibonacci)

## Core Concept Explanation

Recursion works by breaking a problem into smaller subproblems of the same type, solving the base case directly, and using the solutions to subproblems to build the solution to the original problem. The key components are the base case (stopping condition) and the recursive case (function calls itself with smaller input).

**Step-by-Step Breakdown:**
1. Identify if the problem can be broken into smaller subproblems
2. Define the base case (simplest instance that can be solved directly)
3. Define the recursive case (how to solve using smaller subproblems)
4. Ensure each recursive call moves toward the base case
5. Combine results from subproblems to solve the original problem

**Intuition Behind the Concept:**
Think of Russian nesting dolls. To open the largest doll, you open the next smaller one, then the next, until you reach the smallest doll (base case). Then you work backwards, putting the dolls back together to solve the original problem.

**Visual Thinking:**
```
Factorial(5):
factorial(5) = 5 * factorial(4)
factorial(4) = 4 * factorial(3)
factorial(3) = 3 * factorial(2)
factorial(2) = 2 * factorial(1)
factorial(1) = 1 (base case)

Unwinding:
factorial(1) = 1
factorial(2) = 2 * 1 = 2
factorial(3) = 3 * 2 = 6
factorial(4) = 4 * 6 = 24
factorial(5) = 5 * 24 = 120

Call Stack:
┌─────────────┐
│ factorial(5)│ → Waiting for factorial(4)
├─────────────┤
│ factorial(4)│ → Waiting for factorial(3)
├─────────────┤
│ factorial(3)│ → Waiting for factorial(2)
├─────────────┤
│ factorial(2)│ → Waiting for factorial(1)
├─────────────┤
│ factorial(1)│ → Returns 1 (base case)
└─────────────┘
```

## Internal Working / Logic

Recursion operates through the call stack, which keeps track of function calls and their local variables. Each recursive call adds a new frame to the stack, and when the base case is reached, the stack unwinds as results are returned.

**Phase 1: Recursive Calls (Stack Growth)**
- Function calls itself with smaller input
- Each call adds a frame to the call stack
- Local variables are stored in each frame
- Continues until base case is reached

**Phase 2: Base Case (Stack Peak)**
- Simplest instance is solved directly
- No more recursive calls
- Returns result to previous call

**Phase 3: Unwinding (Stack Shrinkage)**
- Results are returned up the call stack
- Each frame uses returned values
- Stack frames are popped as functions return
- Final result is returned to original caller

**Flow Explanation (Factorial):**
1. Call factorial(5)
2. 5 > 1, so call factorial(4)
3. 4 > 1, so call factorial(3)
4. 3 > 1, so call factorial(2)
5. 2 > 1, so call factorial(1)
6. 1 `<=` 1, return 1 (base case)
7. factorial(2) returns 2 * 1 = 2
8. factorial(3) returns 3 * 2 = 6
9. factorial(4) returns 4 * 6 = 24
10. factorial(5) returns 5 * 24 = 120

**Decision Making Logic:**
The key decision is whether to use recursion:
- Use when problem has recursive structure
- Use when divide and conquer is natural
- Use when exploring all possibilities (backtracking)
- Don't use for simple loops (iteration is better)
- Don't use if stack overflow is likely (use iteration or tail recursion)

## Algorithm / Approach

**General Recursive Algorithm**

```
1. Define function with parameters
2. Check base case:
   a. If base case: return base value
3. Recursive case:
   a. Break problem into smaller subproblems
   b. Call function recursively with smaller input
   c. Combine results from subproblems
4. Return result
```

**Linear Recursion Algorithm**

```
1. Single recursive call per function call
2. Process in order: pre-order, in-order, post-order
3. Each call makes progress toward base case
4. Return result
```

**Divide and Conquer Algorithm**

```
1. Divide problem into subproblems
2. Conquer subproblems recursively
3. Combine subproblem solutions
4. Return combined result
```

**Backtracking Algorithm**

```
1. Make a choice
2. Recursively explore
3. Backtrack (undo choice)
4. Try next choice
5. Return when all choices explored
```

## Implementations

### 1. Factorial (Linear Recursion)

```javascript
function factorial(n) {
  if (n <= 1) return 1; // Base case
  return n * factorial(n - 1); // Recursive case
}
```

**Advantages:**
- Simple and elegant
- Matches mathematical definition
- Easy to understand

**Disadvantages:**
- Stack overflow for large n
- O(n) space for call stack
- Can be converted to iteration

### 2. Fibonacci (Tree Recursion with Memoization)

```javascript
function fibonacci(n, memo = {}) {
  if (n in memo) return memo[n]; // Check memo
  if (n <= 1) return n; // Base case
  
  memo[n] = fibonacci(n - 1, memo) + fibonacci(n - 2, memo);
  return memo[n];
}
```

**Advantages:**
- Memoization reduces time from O(2^n) to O(n)
- Handles overlapping subproblems
- Still elegant recursive solution

### 3. Binary Search (Divide and Conquer)

```javascript
function binarySearch(arr, target, left = 0, right = arr.length - 1) {
  if (left > right) return -1; // Base case: not found
  
  const mid = Math.floor((left + right) / 2);
  
  if (arr[mid] === target) return mid; // Base case: found
  if (arr[mid] < target) {
    return binarySearch(arr, target, mid + 1, right); // Search right half
  }
  return binarySearch(arr, target, left, mid - 1); // Search left half
}
```

**Advantages:**
- O(log n) time complexity
- Divide and conquer approach
- Clean recursive implementation

### 4. Tree Traversal (Inorder)

```javascript
function inorderTraversal(root) {
  const result = [];
  
  function traverse(node) {
    if (!node) return; // Base case: empty node
    
    traverse(node.left); // Recurse left
    result.push(node.val); // Process current
    traverse(node.right); // Recurse right
  }
  
  traverse(root);
  return result;
}
```

**Advantages:**
- Natural for tree structures
- In-order, pre-order, post-order variants
- Clean and readable

### 5. Generate Subsets (Backtracking)

```javascript
function subsets(nums) {
  const result = [];
  
  function backtrack(index, current) {
    if (index === nums.length) {
      result.push([...current]); // Base case: complete subset
      return;
    }
    
    // Include current element
    current.push(nums[index]);
    backtrack(index + 1, current);
    current.pop(); // Backtrack
    
    // Exclude current element
    backtrack(index + 1, current);
  }
  
  backtrack(0, []);
  return result;
}
```

**Advantages:**
- Explores all possibilities
- Backtracking pattern
- Generates all subsets

### 6. Tower of Hanoi

```javascript
function towerOfHanoi(n, source, destination, auxiliary) {
  if (n === 1) {
    console.log(`Move disk 1 from ${source} to ${destination}`);
    return;
  }
  
  towerOfHanoi(n - 1, source, auxiliary, destination);
  console.log(`Move disk ${n} from ${source} to ${destination}`);
  towerOfHanoi(n - 1, auxiliary, destination, source);
}
```

**Advantages:**
- Classic recursive problem
- Demonstrates divide and conquer
- 2^n - 1 moves for n disks

## Dry Run

**Example: Factorial(3)**

**Input:**
```
n = 3
```

**Step-by-Step Execution:**

```
Call Stack Growth:
┌─────────────┐
│ factorial(3)│ → Calls factorial(2)
├─────────────┤
│ factorial(2)│ → Calls factorial(1)
├─────────────┤
│ factorial(1)│ → Returns 1 (base case)
└─────────────┘

Call Stack Unwinding:
factorial(1) returns 1
factorial(2) returns 2 * 1 = 2
factorial(3) returns 3 * 2 = 6

Final Result: 6
```

**Variable Changes Table:**

| Call | n | Action | Returns |
|------|---|--------|---------|
| factorial(3) | 3 | Calls factorial(2) | 6 |
| factorial(2) | 2 | Calls factorial(1) | 2 |
| factorial(1) | 1 | Base case | 1 |

## Edge Cases

### 1. Missing Base Case
```javascript
function factorial(n) {
  return n * factorial(n - 1); // No base case!
}
// Infinite recursion → Stack overflow
```

### 2. Negative Input
```javascript
factorial(-1)
// Never reaches base case (n <= 1)
// Infinite recursion → Stack overflow
```

### 3. Stack Overflow
```javascript
factorial(10000)
// Too many recursive calls
// Stack overflow
```

### 4. Empty Input
```javascript
subsets([])
// Should return [[]] (empty subset)
// Handle base case correctly
```

### 5. Single Element
```javascript
subsets([1])
// Should return [[], [1]]
// Base case: index === nums.length
```

### 6. Circular Reference
```javascript
// Graph with cycle
// DFS without visited set
// Infinite recursion
```

**Why Edge Cases Matter:**
- Base case prevents infinite recursion
- Negative inputs need validation
- Stack overflow limits recursion depth
- Empty/single element tests boundaries
- Cycles need visited tracking

## Variations / Extensions

### 1. Tail Recursion

```javascript
function factorialTail(n, accumulator = 1) {
  if (n <= 1) return accumulator;
  return factorialTail(n - 1, n * accumulator);
}
```

### 2. Mutual Recursion

```javascript
function isEven(n) {
  if (n === 0) return true;
  return isOdd(n - 1);
}

function isOdd(n) {
  if (n === 0) return false;
  return isEven(n - 1);
}
```

### 3. Indirect Recursion

```javascript
function A(n) {
  if (n <= 0) return;
  console.log('A:', n);
  B(n - 1);
}

function B(n) {
  if (n <= 0) return;
  console.log('B:', n);
  A(n - 1);
}
```

### 4. Nested Recursion

```javascript
function ackermann(m, n) {
  if (m === 0) return n + 1;
  if (n === 0) return ackermann(m - 1, 1);
  return ackermann(m - 1, ackermann(m, n - 1));
}
```

### 5. Memoization Wrapper

```javascript
function memoize(fn) {
  const cache = new Map();
  
  return function(...args) {
    const key = JSON.stringify(args);
    if (cache.has(key)) return cache.get(key);
    
    const result = fn.apply(this, args);
    cache.set(key, result);
    return result;
  };
}

const memoFib = memoize(fibonacci);
```

## Optimization Techniques

### 1. Memoization

**Cache Results:**
```javascript
// Store computed results
// Avoid redundant computations
// Reduces time from exponential to polynomial
```

### 2. Tail Call Optimization

**Convert to Tail Recursion:**
```javascript
// Pass accumulator as parameter
// Last operation is recursive call
// Some compilers optimize to iteration
```

### 3. Iterative Conversion

**Replace with Loop:**
```javascript
// Use explicit stack or loop
// Avoid call stack overhead
// No stack overflow risk
```

### 4. Trade-offs

**Recursion vs Iteration:**

| Aspect | Recursion | Iteration |
|--------|-----------|-----------|
| Readability | High | Medium |
| Stack Space | `O(n)` | `O(1)` |
| Overhead | Function calls | Loop overhead |
| Stack Overflow | Risk | No risk |
| Best For | Recursive structures | Simple loops |

**When to Use Iteration Instead:**
- Performance is critical
- Stack overflow is likely
- Simple loops suffice
- Language doesn't optimize tail calls

## Complexity Analysis

### Time Complexity

**Linear Recursion: O(n)**
- Single recursive call per level
- Each level processes once
- Example: Factorial, linear search

**Tree Recursion: O(2^n) without memoization**
- Two recursive calls per level
- Exponential growth
- Example: Naive Fibonacci

**With Memoization: O(n)**
- Cache results
- Each subproblem solved once
- Example: Fibonacci with memoization

**Divide and Conquer: O(n log n)**
- Divide: O(1), Conquer: 2 * O(n/2), Combine: O(n)
- Example: Merge sort

### Space Complexity

**Call Stack: O(n)**
- Each recursive call adds frame
- Maximum depth = n
- Example: Linear recursion

**With Memoization: O(n)**
- Call stack + cache
- O(n) for both
- Example: Fibonacci with memoization

**Tail Recursion: O(1)**
- Optimized to iteration
- No stack growth
- Example: Tail-recursive factorial

**Explanation:**
Recursion time depends on number of recursive calls and work per call. Space is dominated by call stack depth. Memoization trades space for time. Tail recursion can be optimized to O(1) space.

## Real-world Applications

### 1. File System Traversal

**Directory Walking:**
- Recursively traverse directories
- Find files matching pattern
- Example: File search tools

### 2. Parsing Nested Structures

**JSON/XML Parsing:**
- Parse nested objects/arrays
- Build tree structure
- Example: API response parsing

### 3. Comment Threads

**Nested Comments:**
- Render comment hierarchies
- Recursively display replies
- Example: Reddit, social media

### 4. Category Hierarchies

**Taxonomy Navigation:**
- Navigate category trees
- Display subcategories
- Example: E-commerce categories

### 5. Game AI

**Minimax Algorithm:**
- Recursively evaluate game states
- Optimal move selection
- Example: Chess, tic-tac-toe

### 6. Compilers

**AST Traversal:**
- Parse and analyze code
- Recursively process nodes
- Example: Code analysis tools

### 7. Network Protocols

**Packet Routing:**
- Recursively find paths
- Traverse network graphs
- Example: Routing algorithms

### 8. Graphics

**Fractal Generation:**
- Recursively draw patterns
- Self-similar structures
- Example: Fractal trees, Mandelbrot

## Common Mistakes

### 1. Missing Base Case

**Mistake:**
```javascript
function factorial(n) {
  return n * factorial(n - 1); // No base case!
}
```

**Correct:**
```javascript
function factorial(n) {
  if (n <= 1) return 1; // Base case
  return n * factorial(n - 1);
}
```

**Why It Matters:**
- Without base case, infinite recursion
- Stack overflow guaranteed
- Must have stopping condition

### 2. Not Making Progress

**Mistake:**
```javascript
function factorial(n) {
  if (n <= 1) return 1;
  return n * factorial(n); // Same input!
}
```

**Correct:**
```javascript
function factorial(n) {
  if (n <= 1) return 1;
  return n * factorial(n - 1); // Smaller input
}
```

**Why It Matters:**
- Must move toward base case
- Same input causes infinite recursion
- Progress is essential

### 3. Stack Overflow

**Mistake:**
```javascript
function factorial(n) {
  if (n <= 1) return 1;
  return n * factorial(n - 1);
}
factorial(10000); // Stack overflow!
```

**Correct:**
```javascript
// Use iteration or tail recursion
function factorialIterative(n) {
  let result = 1;
  for (let i = 2; i <= n; i++) {
    result *= i;
  }
  return result;
}
```

**Why It Matters:**
- Deep recursion causes stack overflow
- Must limit recursion depth
- Use iteration for large inputs

### 4. Redundant Computations

**Mistake:**
```javascript
function fibonacci(n) {
  if (n <= 1) return n;
  return fibonacci(n - 1) + fibonacci(n - 2); // Exponential!
}
```

**Correct:**
```javascript
function fibonacci(n, memo = {}) {
  if (n in memo) return memo[n];
  if (n <= 1) return n;
  memo[n] = fibonacci(n - 1, memo) + fibonacci(n - 2, memo);
  return memo[n];
}
```

**Why It Matters:**
- Without memoization, exponential time
- Same subproblems computed repeatedly
- Memoization is essential for tree recursion

### 5. Not Backtracking

**Mistake:**
```javascript
function subsets(nums) {
  const result = [];
  
  function backtrack(index, current) {
    if (index === nums.length) {
      result.push([...current]);
      return;
    }
    
    current.push(nums[index]);
    backtrack(index + 1, current);
    // Forgot to pop!
    backtrack(index + 1, current);
  }
  
  backtrack(0, []);
  return result;
}
```

**Correct:**
```javascript
function subsets(nums) {
  const result = [];
  
  function backtrack(index, current) {
    if (index === nums.length) {
      result.push([...current]);
      return;
    }
    
    current.push(nums[index]);
    backtrack(index + 1, current);
    current.pop(); // Backtrack
    backtrack(index + 1, current);
  }
  
  backtrack(0, []);
  return result;
}
```

**Why It Matters:**
- Must undo choices after exploring
- Otherwise state is corrupted
- Backtracking is essential

### 6. Modifying Input

**Mistake:**
```javascript
function reverseArray(arr, start = 0, end = arr.length - 1) {
  if (start >= end) return;
  
  [arr[start], arr[end]] = [arr[end], arr[start]];
  reverseArray(arr, start + 1, end - 1); // Modifies original
}
```

**Correct:**
```javascript
function reverseArray(arr) {
  const result = [...arr];
  
  function helper(start, end) {
    if (start >= end) return;
    [result[start], result[end]] = [result[end], result[start]];
    helper(start + 1, end - 1);
  }
  
  helper(0, result.length - 1);
  return result;
}
```

**Why It Matters:**
- Modifying input causes side effects
- Should work on copy
- Pure functions are better

## Advanced Concepts

### 1. Continuation-Passing Style

**Concept:**
Pass the next step as a parameter instead of returning.

**Features:**
- Explicit control flow
- No return statements
- Used in functional programming

### 2. Trampolining

**Concept:**
Convert recursion to iteration using thunks.

**Features:**
- Avoids stack overflow
- Lazy evaluation
- Used in functional languages

### 3. Recursion Schemes

**Concept:**
General patterns for recursive algorithms (catamorphism, anamorphism).

**Features:**
- Mathematical foundation
- Category theory
- Used in functional programming

### 4. Y Combinator

**Concept:**
Enable recursion without named functions.

**Features:**
- Lambda calculus
- Theoretical interest
- Demonstrates recursion theory

## Practice Thinking Guide

### How to Identify When to Use Recursion

**Key Signals in Problem Statements:**

1. **"Tree/graph traversal"**
   - Natural recursive structure
   - Example: "Inorder traversal"

2. **"Divide and conquer"**
   - Break into subproblems
   - Example: "Merge sort"

3. **"All combinations/subsets"**
   - Explore all possibilities
   - Example: "Generate subsets"

4. **"Nested structure"**
   - Recursive data structure
   - Example: "Parse nested JSON"

5. **"Mathematical definition"**
   - Defined recursively
   - Example: "Factorial, Fibonacci"

6. **"N-Queens/Sudoku"**
   - Backtracking needed
   - Example: "Solve N-Queens"

**Pattern Recognition:**

**Pattern 1: Linear Recursion**
```
Problem: Single recursive call
Solution: Linear recursion
```

**Pattern 2: Divide and Conquer**
```
Problem: Split into subproblems
Solution: Divide and conquer
```

**Pattern 3: Tree Recursion**
```
Problem: Multiple recursive branches
Solution: Tree recursion with memoization
```

**Pattern 4: Backtracking**
```
Problem: Explore all possibilities
Solution: Backtracking
```

**Pattern 5: Tree Traversal**
```
Problem: Process tree structure
Solution: Recursive traversal
```

**Decision Flowchart:**

```
Problem has recursive structure?
├─ Yes → Need to explore all possibilities?
│        ├─ Yes → Use backtracking
│        └─ No → Use divide and conquer
├─ No → Data structure is tree/graph?
│        ├─ Yes → Use recursive traversal
│        └─ No → Consider iteration
└─ No → Not recursion problem
```

**Example Problem Analysis:**

**Problem:** "Calculate factorial of n"

**Analysis:**
1. Mathematical definition is recursive
2. n! = n * (n-1)!
3. Base case: 0! = 1, 1! = 1
4. Simple linear recursion
5. Solution: Linear recursion

**Problem:** "Generate all subsets of array"

**Analysis:**
1. Need to explore all possibilities
2. For each element: include or exclude
3. Backtracking pattern
4. 2^n subsets
5. Solution: Backtracking

**Problem:** "Traverse binary tree in-order"

**Analysis:**
1. Tree structure is naturally recursive
2. Process left, current, right
3. In-order traversal pattern
4. Solution: Recursive traversal

## Summary

Recursion is a powerful technique for solving problems with recursive structures. It's elegant and readable for divide and conquer, tree traversals, and backtracking problems. Understanding base cases, recursive cases, and optimization techniques like memoization is crucial for effective use.

**Key Takeaways:**
- Always define base case to stop recursion
- Ensure each call makes progress toward base case
- Use memoization for overlapping subproblems
- Watch for stack overflow in deep recursion
- Consider iteration for performance-critical code
- Tail recursion can be optimized by some compilers
- Backtracking requires undoing choices

**Mastery Checklist:**
- ✅ Understand base case and recursive case
- ✅ Implement linear recursion
- ✅ Implement divide and conquer
- ✅ Implement tree traversal
- ✅ Implement backtracking
- ✅ Use memoization for optimization
- ✅ Convert recursion to iteration
- ✅ Handle stack overflow

