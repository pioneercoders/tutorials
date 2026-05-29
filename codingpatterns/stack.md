# Stack

Stack is a linear data structure that follows Last-In-First-Out (LIFO) principle. Elements are added and removed from the same end (top).

## Introduction

Stack is a linear data structure that follows the Last-In-First-Out (LIFO) principle, meaning the last element added is the first one to be removed. Think of it like a stack of plates: you can only add a plate to the top and remove the top plate. This makes stacks ideal for tracking state in reverse order, implementing undo/redo functionality, parsing expressions, and backtracking algorithms.

**Why Stack Exists:**
- LIFO behavior is needed for many problems
- Natural for tracking state history
- Essential for expression parsing and evaluation
- Used to simulate recursion iteratively
- Foundation for many algorithms (DFS, backtracking)

**Where It Is Used:**
- Function call stack in programming languages
- Undo/redo functionality in applications
- Expression parsing and evaluation
- Backtracking algorithms
- Browser history navigation
- Parentheses matching
- Monotonic stack for range queries
- Implementing recursion iteratively

## Core Concept Explanation

Stack operates on the LIFO principle: the last element pushed onto the stack is the first one popped off. This is implemented using two primary operations: push (add to top) and pop (remove from top). Additional operations include peek (view top without removing), isEmpty (check if empty), and size (number of elements).

**Step-by-Step Breakdown:**
1. Initialize empty stack
2. Push elements onto stack (they accumulate)
3. Pop elements from stack (removed in reverse order)
4. Peek to view top element without removing
5. Check if empty before popping
6. All operations are O(1) time complexity

**Intuition Behind the Concept:**
Think of a stack of plates in a cafeteria. You can only add a plate to the top of the stack, and you can only remove the top plate. If you push plates A, B, C in that order, you must pop them in reverse order: C, B, A. This is exactly how a stack data structure works.

**Visual Thinking:**
```
Stack Operations:

Initial: []
Push(5):    [5]
Push(3):    [5, 3]
Push(7):    [5, 3, 7]
Peek():      7 (top element)
Pop():      7 → [5, 3]
Pop():      3 → [5]
Push(2):    [5, 2]
Pop():      2 → [5]
Pop():      5 → []
isEmpty():  true

Visual Representation:
┌───┐
│ 7 │ ← Top
├───┤
│ 3 │
├───┤
│ 5 │
└───┘
```

## Internal Working / Logic

Stack operates through a simple mechanism where elements are added and removed from the same end (top). The underlying implementation can use an array or a linked list, but the operations remain the same.

**Operation 1: Push**
- Add element to the end of the array
- Increment size
- Time: O(1) amortized (array may need resizing)

**Operation 2: Pop**
- Remove element from the end of the array
- Decrement size
- Return removed element
- Time: O(1)

**Operation 3: Peek**
- Return element at the end of the array
- Don't remove it
- Time: O(1)

**Operation 4: isEmpty**
- Check if size is 0
- Return boolean
- Time: O(1)

**Flow Explanation (Push):**
1. Check if stack needs resizing (array implementation)
2. Add element to end of array
3. Increment size
4. Return

**Flow Explanation (Pop):**
1. Check if stack is empty
2. If empty, return null or throw error
3. Remove element from end of array
4. Decrement size
5. Return removed element

**Decision Making Logic:**
The key decision is the underlying implementation:
- Array: Simple, O(1) amortized push, may need resizing
- Linked list: Consistent O(1) push, more memory overhead
- Choice depends on expected usage patterns

## Algorithm / Approach

**Push Algorithm**

```
1. Check if stack needs resizing (array implementation)
2. Add element to top of stack
3. Increment size
4. Return
```

**Pop Algorithm**

```
1. Check if stack is empty
2. If empty: return null or throw error
3. Remove element from top of stack
4. Decrement size
5. Return removed element
```

**Peek Algorithm**

```
1. Check if stack is empty
2. If empty: return null or throw error
3. Return element at top of stack
4. Don't remove it
```

**isEmpty Algorithm**

```
1. Check if size is 0
2. Return true if empty, false otherwise
```

## Implementations

### 1. Basic Stack Implementation

```javascript
class Stack {
  constructor() {
    this.items = [];
  }
  
  push(item) {
    this.items.push(item);
  }
  
  pop() {
    if (!this.isEmpty()) {
      return this.items.pop();
    }
    return null;
  }
  
  peek() {
    if (!this.isEmpty()) {
      return this.items[this.items.length - 1];
    }
    return null;
  }
  
  isEmpty() {
    return this.items.length === 0;
  }
  
  size() {
    return this.items.length;
  }
  
  clear() {
    this.items = [];
  }
}
```

**Advantages:**
- O(1) time for all operations
- Simple to implement
- Uses array for storage

### 2. Valid Parentheses

```javascript
function isValidParentheses(s) {
  const stack = [];
  const mapping = { ')': '(', '}': '{', ']': '[' };
  
  for (const char of s) {
    if (char in mapping) {
      // Closing bracket
      if (stack.length > 0 && stack[stack.length - 1] === mapping[char]) {
        stack.pop();
      } else {
        return false;
      }
    } else {
      // Opening bracket
      stack.push(char);
    }
  }
  
  return stack.length === 0;
}
```

**Advantages:**
- O(n) time, O(n) space
- Handles nested parentheses
- Classic stack application

### 3. Min Stack

```javascript
class MinStack {
  constructor() {
    this.stack = [];
    this.minStack = [];
  }
  
  push(val) {
    this.stack.push(val);
    if (this.minStack.length === 0 || val <= this.minStack[this.minStack.length - 1]) {
      this.minStack.push(val);
    }
  }
  
  pop() {
    if (this.stack.length > 0) {
      if (this.stack[this.stack.length - 1] === this.minStack[this.minStack.length - 1]) {
        this.minStack.pop();
      }
      this.stack.pop();
    }
  }
  
  top() {
    return this.stack[this.stack.length - 1];
  }
  
  getMin() {
    return this.minStack[this.minStack.length - 1];
  }
}
```

**Advantages:**
- O(1) time for all operations
- Tracks minimum efficiently
- Uses auxiliary stack

### 4. Evaluate Reverse Polish Notation

```javascript
function evalRPN(tokens) {
  const stack = [];
  
  for (const token of tokens) {
    if (token === '+' || token === '-' || token === '*' || token === '/') {
      const b = stack.pop();
      const a = stack.pop();
      
      if (token === '+') stack.push(a + b);
      else if (token === '-') stack.push(a - b);
      else if (token === '*') stack.push(a * b);
      else if (token === '/') stack.push(Math.trunc(a / b));
    } else {
      stack.push(parseInt(token));
    }
  }
  
  return stack.pop();
}
```

**Advantages:**
- O(n) time, O(n) space
- Evaluates postfix expressions
- No need for parentheses

### 5. Next Greater Element

```javascript
function nextGreaterElement(nums) {
  const result = new Array(nums.length).fill(-1);
  const stack = [];
  
  for (let i = nums.length - 1; i >= 0; i--) {
    while (stack.length > 0 && stack[stack.length - 1] <= nums[i]) {
      stack.pop();
    }
    
    if (stack.length > 0) {
      result[i] = stack[stack.length - 1];
    }
    
    stack.push(nums[i]);
  }
  
  return result;
}
```

**Advantages:**
- O(n) time, O(n) space
- Monotonic stack pattern
- Efficient for range queries

### 6. Simplify Path

```javascript
function simplifyPath(path) {
  const stack = [];
  const components = path.split('/');
  
  for (const component of components) {
    if (component === '' || component === '.') {
      continue;
    } else if (component === '..') {
      if (stack.length > 0) {
        stack.pop();
      }
    } else {
      stack.push(component);
    }
  }
  
  return '/' + stack.join('/');
}
```

## Dry Run

**Example: Valid Parentheses**

**Input:**
```
s = "()[]{}"
```

**Step-by-Step Execution:**

```
Initial State:
stack = []

Iteration 1 (char = '('):
'(' is opening bracket
stack.push('(')
stack = ['(']

Iteration 2 (char = ')'):
')' is closing bracket
mapping[')'] = '('
stack[-1] = '('
Match! stack.pop()
stack = []

Iteration 3 (char = '['):
'[' is opening bracket
stack.push('[')
stack = ['[']

Iteration 4 (char = ']'):
']' is closing bracket
mapping[']'] = '['
stack[-1] = '['
Match! stack.pop()
stack = []

Iteration 5 (char = '{'):
'{' is opening bracket
stack.push('{')
stack = ['{']

Iteration 6 (char = '}'):
'}' is closing bracket
mapping['}'] = '{'
stack[-1] = '{'
Match! stack.pop()
stack = []

Final: stack.length === 0 → true
```

**Variable Changes Table:**

| Iteration | char | Action | stack (after) |
|-----------|------|--------|--------------|
| 1 | `(` | Push | `['(']` |
| 2 | `)` | Pop | `[]` |
| 3 | `[` | Push | `['[']` |
| 4 | `]` | Pop | `[]` |
| 5 | `{` | Push | `['{']` |
| 6 | `}` | Pop | `[]` |

## Edge Cases

### 1. Empty Stack Operations
```javascript
stack = []
stack.pop() → null
stack.peek() → null
stack.isEmpty() → true
```

### 2. Mismatched Parentheses
```javascript
s = "(]"
stack = ['(']
']' doesn't match '('
Return false
```

### 3. Stack Overflow
```javascript
Too many pushes
Array may need resizing
Linked list handles better
```

### 4. Single Element
```javascript
stack = [5]
stack.pop() → 5
stack = []
stack.isEmpty() → true
```

### 5. Invalid Input
```javascript
evalRPN(["+", "5"])
Not enough operands
Error or handle gracefully
```

### 6. All Same Elements
```javascript
nums = [2, 2, 2, 2]
nextGreaterElement → [-1, -1, -1, -1]
No greater element exists
```

**Why Edge Cases Matter:**
- Empty operations prevent errors
- Mismatched parentheses test correctness
- Stack overflow tests resilience
- Single element tests boundaries
- Invalid input needs validation

## Variations / Extensions

### 1. Linked List Stack

```javascript
class Node {
  constructor(value) {
    this.value = value;
    this.next = null;
  }
}

class LinkedListStack {
  constructor() {
    this.top = null;
    this.size = 0;
  }
  
  push(value) {
    const newNode = new Node(value);
    newNode.next = this.top;
    this.top = newNode;
    this.size++;
  }
  
  pop() {
    if (!this.top) return null;
    const value = this.top.value;
    this.top = this.top.next;
    this.size--;
    return value;
  }
  
  peek() {
    return this.top ? this.top.value : null;
  }
}
```

### 2. Fixed Size Stack

```javascript
class FixedSizeStack {
  constructor(capacity) {
    this.capacity = capacity;
    this.stack = new Array(capacity);
    this.top = -1;
  }
  
  push(item) {
    if (this.top === this.capacity - 1) {
      throw new Error('Stack overflow');
    }
    this.stack[++this.top] = item;
  }
  
  pop() {
    if (this.top === -1) {
      throw new Error('Stack underflow');
    }
    return this.stack[this.top--];
  }
}
```

### 3. Two Stacks in One Array

```javascript
class TwoStacks {
  constructor(size) {
    this.array = new Array(size);
    this.top1 = -1;
    this.top2 = size;
  }
  
  push1(item) {
    if (this.top1 < this.top2 - 1) {
      this.array[++this.top1] = item;
    }
  }
  
  push2(item) {
    if (this.top1 < this.top2 - 1) {
      this.array[--this.top2] = item;
    }
  }
}
```

### 4. Stack with Max

```javascript
class MaxStack {
  constructor() {
    this.stack = [];
    this.maxStack = [];
  }
  
  push(val) {
    this.stack.push(val);
    if (this.maxStack.length === 0 || val >= this.maxStack[this.maxStack.length - 1]) {
      this.maxStack.push(val);
    }
  }
  
  pop() {
    if (this.stack[this.stack.length - 1] === this.maxStack[this.maxStack.length - 1]) {
      this.maxStack.pop();
    }
    return this.stack.pop();
  }
  
  getMax() {
    return this.maxStack[this.maxStack.length - 1];
  }
}
```

### 5. Undo/Redo Stack

```javascript
class UndoRedo {
  constructor() {
    this.undoStack = [];
    this.redoStack = [];
  }
  
  do(action) {
    this.undoStack.push(action);
    this.redoStack = []; // Clear redo on new action
  }
  
  undo() {
    if (this.undoStack.length > 0) {
      const action = this.undoStack.pop();
      this.redoStack.push(action);
      return action;
    }
  }
  
  redo() {
    if (this.redoStack.length > 0) {
      const action = this.redoStack.pop();
      this.undoStack.push(action);
      return action;
    }
  }
}
```

## Optimization Techniques

### 1. Array Resizing

**Dynamic Resizing:**
```javascript
// Double capacity when full
// Amortized O(1) push
// Similar to dynamic array
```

### 2. Memory Pool

**Object Pooling:**
```javascript
// Reuse stack nodes
// Reduce garbage collection
// Improve performance
```

### 3. Trade-offs

**Array vs Linked List:**

| Aspect | Array | Linked List |
|--------|-------|-------------|
| Push | `O(1)` amortized | `O(1)` |
| Pop | `O(1)` | `O(1)` |
| Peek | `O(1)` | `O(1)` |
| Memory | Contiguous | Scattered |
| Resizing | May need | No need |
| Cache | Better | Worse |

**When to Use Linked List:**
- Frequent push/pop operations
- Need consistent O(1) performance
- Memory fragmentation is acceptable

## Complexity Analysis

### Time Complexity

**Push: O(1) amortized**
- Add to end of array
- May need to resize (rare)
- Amortized constant time

**Pop: O(1)**
- Remove from end of array
- No traversal needed
- Constant time

**Peek: O(1)**
- Access last element
- No removal
- Constant time

**isEmpty: O(1)**
- Check size
- Constant time

### Space Complexity

**Storage: O(n)**
- Store n elements
- Array or linked list
- Linear space

**Auxiliary Operations:**
- Min stack: O(n) additional
- Max stack: O(n) additional
- Depends on variant

**Explanation:**
Stack operations are O(1) time because they only access the top element. Space is O(n) to store all elements. Some variants like min/max stack use additional O(n) space for auxiliary stacks.

## Real-world Applications

### 1. Function Call Stack

**Call Stack Management:**
- Track function calls
- Manage local variables
- Return addresses
- Example: Programming language runtime

### 2. Undo/Redo

**State Management:**
- Track history of actions
- Undo last action
- Redo undone actions
- Example: Text editors, IDEs

### 3. Expression Parsing

**Compiler Design:**
- Parse arithmetic expressions
- Convert infix to postfix
- Evaluate expressions
- Example: Compilers, calculators

### 4. Backtracking

**Algorithm Design:**
- Track current state
- Backtrack on failure
- Explore alternatives
- Example: N-Queens, Sudoku

### 5. Browser History

**Navigation:**
- Track visited pages
- Back button functionality
- Forward button
- Example: Web browsers

### 6. Parentheses Matching

**Syntax Validation:**
- Check balanced parentheses
- Validate code syntax
- Example: Code editors, linters

### 7. Monotonic Stack

**Range Queries:**
- Find next greater/smaller
- Calculate ranges
- Example: Stock prices, weather data

### 8. Text Editor

**Undo Functionality:**
- Track character insertions
- Undo last edit
- Redo undone edit
- Example: Word processors

## Common Mistakes

### 1. Not Checking Empty Before Pop

**Mistake:**
```javascript
// Not checking if empty
stack.pop(); // May return undefined
```

**Correct:**
```javascript
// Check before popping
if (!stack.isEmpty()) {
  stack.pop();
}
```

**Why It Matters:**
- Popping empty stack causes errors
- Must check before operations
- Prevents undefined behavior

### 2. Wrong Bracket Mapping

**Mistake:**
```javascript
// Wrong mapping
const mapping = { ')': '[', '}': '{', ']': '(' }; // Wrong!
```

**Correct:**
```javascript
// Correct mapping
const mapping = { ')': '(', '}': '{', ']': '[' };
```

**Why It Matters:**
- Wrong mapping causes validation failure
- Must match correct pairs
- Critical for correctness

### 3. Not Handling Edge Cases

**Mistake:**
```javascript
// Not handling empty string
isValidParentheses("") // Should return true
```

**Correct:**
```javascript
// Handle empty string
if (s.length === 0) return true;
```

**Why It Matters:**
- Edge cases must be handled
- Empty string is valid
- Prevents incorrect results

### 4. Not Clearing Redo Stack

**Mistake:**
```javascript
// Not clearing redo on new action
do(action) {
  this.undoStack.push(action);
  // Forgot to clear redo!
}
```

**Correct:**
```javascript
// Clear redo on new action
do(action) {
  this.undoStack.push(action);
  this.redoStack = [];
}
```

**Why It Matters:**
- Redo stack must be cleared
- Otherwise invalid history
- Correct undo/redo behavior

### 5. Using Stack When Queue Needed

**Mistake:**
```javascript
// Using stack for FIFO
stack.push(1);
stack.push(2);
stack.pop(); // Returns 2, not 1!
```

**Correct:**
```javascript
// Use queue for FIFO
queue.enqueue(1);
queue.enqueue(2);
queue.dequeue(); // Returns 1
```

**Why It Matters:**
- Stack is LIFO, queue is FIFO
- Wrong choice gives wrong order
- Must choose correct structure

### 6. Not Handling Stack Overflow

**Mistake:**
```javascript
// Not checking capacity
push(item) {
  this.stack.push(item); // May overflow
}
```

**Correct:**
```javascript
// Check capacity
push(item) {
  if (this.size >= this.capacity) {
    throw new Error('Stack overflow');
  }
  this.stack.push(item);
}
```

**Why It Matters:**
- Stack overflow causes errors
- Must check capacity
- Prevents crashes

## Advanced Concepts

### 1. Monotonic Stack

**Concept:**
Maintain stack in monotonic order (increasing or decreasing).

**Features:**
- Efficient for range queries
- O(n) time for many problems
- Used in next greater/smaller element

### 2. Stack Sorting

**Concept:**
Sort stack using only stack operations.

**Features:**
- Uses temporary stack
- O(n²) time complexity
- Demonstrates stack manipulation

### 3. Expression Evaluation

**Concept:**
Convert and evaluate infix, postfix, prefix expressions.

**Features:**
- Shunting-yard algorithm
- Operator precedence
- Parentheses handling

### 4. Stack Machine

**Concept:**
Computer architecture using stack for operations.

**Features:**
- Push/pop operands
- Stack-based execution
- Used in JVM, .NET

## Practice Thinking Guide

### How to Identify When to Use Stack

**Key Signals in Problem Statements:**

1. **"Last-in-first-out"**
   - Need LIFO behavior
   - Example: "Undo operations"

2. **"Nested structure"**
   - Nested parentheses, brackets
   - Example: "Valid parentheses"

3. **"Reverse order"**
   - Process in reverse
   - Example: "Reverse string"

4. **"Next greater/smaller"**
   - Find next element
   - Example: "Next greater element"

5. **"Expression evaluation"**
   - Evaluate mathematical expressions
   - Example: "RPN evaluation"

6. **"Backtracking"**
   - Track state history
   - Example: "DFS, N-Queens"

**Pattern Recognition:**

**Pattern 1: Parentheses Matching**
```
Problem: Check balanced parentheses
Solution: Stack with opening brackets
```

**Pattern 2: Expression Evaluation**
```
Problem: Evaluate expression
Solution: Stack for operands/operators
```

**Pattern 3: Next Greater Element**
```
Problem: Find next greater element
Solution: Monotonic stack
```

**Pattern 4: Undo/Redo**
```
Problem: Track history
Solution: Two stacks (undo, redo)
```

**Pattern 5: Backtracking**
```
Problem: Explore possibilities
Solution: Stack for state
```

**Decision Flowchart:**

```
Need LIFO behavior?
├─ Yes → Need to track history?
│        ├─ Yes → Use stack
│        └─ No → Consider other
├─ No → Need to match pairs?
│        ├─ Yes → Use stack
│        └─ No → Consider other
└─ No → Not stack problem
```

**Example Problem Analysis:**

**Problem:** "Check if parentheses are valid"

**Analysis:**
1. Need to match opening/closing brackets
2. LIFO behavior needed
3. Push opening brackets
4. Pop and match closing brackets
5. Solution: Stack with bracket mapping

**Problem:** "Evaluate reverse Polish notation"

**Analysis:**
1. Need to evaluate postfix expression
2. Push operands, pop for operators
3. Stack naturally handles order
4. O(n) time, O(n) space
5. Solution: Stack for operands

**Problem:** "Find next greater element"

**Analysis:**
1. Need to find next greater element
2. Monotonic stack pattern
3. Process from right to left
4. O(n) time, O(n) space
5. Solution: Monotonic decreasing stack

## Summary

Stack is a fundamental data structure that follows the LIFO principle. It's essential for tracking state in reverse order, implementing undo/redo functionality, parsing expressions, and backtracking algorithms. Understanding stack operations and patterns is crucial for solving many algorithmic problems.

**Key Takeaways:**
- LIFO principle (last-in-first-out)
- O(1) time for all operations
- O(n) space for storage
- Essential for parentheses matching
- Used in expression evaluation
- Monotonic stack for range queries
- Simulates recursion iteratively
- Check empty before popping

**Mastery Checklist:**
- ✅ Understand LIFO principle
- ✅ Implement basic stack operations
- ✅ Solve parentheses matching
- ✅ Implement min/max stack
- ✅ Evaluate RPN expressions
- ✅ Use monotonic stack
- ✅ Implement undo/redo
- ✅ Choose array vs linked list

