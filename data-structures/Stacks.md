# Stacks in Data Structures

Stacks are one of the most important linear data structures.

A stack follows the principle:

```text id="jlwm4v"
LIFO → Last In First Out
```

The last element inserted is the first one removed.

---

# Real-Life Analogy

Think of:

* Stack of plates
* Browser history
* Undo operations
* Call stack in programs

```text id="jlwmc2"
Top
 ↓
[30]
[20]
[10]
```

Remove happens from the top.

---

# Why Stacks Matter

Stacks are heavily used in:

* Compilers
* Browsers
* Expression evaluation
* Parsing
* Recursion
* Operating systems
* Memory management

---

# 1. Stack Basics

---

# Core Operations

| Operation    | Description        |
| ------------ | ------------------ |
| push()       | Insert element     |
| pop()        | Remove top element |
| peek()/top() | View top element   |
| isEmpty()    | Check empty        |
| size()       | Number of elements |

---

# Visualization

```text id="jlwm9g"
Push 10
[10]

Push 20
[20]
[10]

Pop
[10]
```

---

# Time Complexity

| Operation | Complexity |
| --------- | ---------- |
| Push      | O(1)       |
| Pop       | O(1)       |
| Peek      | O(1)       |

---

# JavaScript Stack Example

```js id="jlwm0n"
const stack = [];

stack.push(10);
stack.push(20);

console.log(stack.pop());
console.log(stack[stack.length - 1]);
```

---

# Real-Time Applications

| System             | Usage       |
| ------------------ | ----------- |
| Browser history    | Back button |
| VS Code            | Undo/Redo   |
| Function calls     | Call stack  |
| Expression parsing | Compilers   |

---

# 2. Stack using Arrays

Arrays are the most common stack implementation.

---

# Implementation

```js id="jlwmr8"
class Stack {
  constructor() {
    this.items = [];
  }

  push(element) {
    this.items.push(element);
  }

  pop() {
    if (this.isEmpty()) {
      return "Stack Underflow";
    }

    return this.items.pop();
  }

  peek() {
    return this.items[this.items.length - 1];
  }

  isEmpty() {
    return this.items.length === 0;
  }
}
```

---

# Visualization

```text id="jlwm6o"
Top
 ↓
[30]
[20]
[10]
```

---

# Advantages

* Easy implementation
* Cache friendly
* Fast indexing

---

# Disadvantages

* Fixed size issue in some languages
* Resizing overhead

---

# Real-Time Example

## Browser Navigation Stack

When visiting pages:

```text id="jlwmxv"
Google
YouTube
GitHub
```

Back button pops history stack.

---

# 3. Stack using Linked List

Useful when dynamic memory is needed.

---

# Why Linked List?

Avoids:

* Fixed size limitations
* Array resizing

---

# Node Structure

```js id="jlwm17"
class Node {
  constructor(data) {
    this.data = data;
    this.next = null;
  }
}
```

---

# Stack Implementation

```js id="jlwm61"
class Stack {
  constructor() {
    this.top = null;
  }

  push(data) {
    const newNode = new Node(data);

    newNode.next = this.top;
    this.top = newNode;
  }

  pop() {
    if (!this.top) {
      return null;
    }

    const removed = this.top;
    this.top = this.top.next;

    return removed.data;
  }
}
```

---

# Complexity

| Operation | Complexity |
| --------- | ---------- |
| Push      | O(1)       |
| Pop       | O(1)       |

---

# Array vs Linked List Stack

| Feature           | Array      | Linked List  |
| ----------------- | ---------- | ------------ |
| Memory            | Contiguous | Dynamic      |
| Resize            | Required   | Not required |
| Cache Performance | Better     | Worse        |
| Flexibility       | Lower      | Higher       |

---

# 4. Infix, Prefix, Postfix Expressions

Very important in:

* Compilers
* Calculators
* Expression parsers

---

# Infix Expression

Operator between operands.

```text id="jlwm2t"
A + B
```

Human readable.

---

# Prefix Expression

Operator before operands.

```text id="jlwmde"
+ A B
```

---

# Postfix Expression

Operator after operands.

```text id="jlwm74"
A B +
```

Also called:

```text id="jlwm0w"
Reverse Polish Notation
```

---

# Why Prefix/Postfix?

No ambiguity.
No brackets needed.

---

# Example

Infix:

```text id="jlwmle"
(A + B) * C
```

Postfix:

```text id="jlwm2m"
A B + C *
```

Prefix:

```text id="jlwm6n"
* + A B C
```

---

# Real-Time Applications

| System           | Usage                 |
| ---------------- | --------------------- |
| Compilers        | Expression parsing    |
| Calculators      | Expression evaluation |
| Virtual machines | Stack-based execution |

---

# Infix to Postfix Conversion

Uses:

* Stack
* Operator precedence

---

# Precedence Example

| Operator | Priority |
| -------- | -------- |
| * /      | High     |
| + -      | Low      |

---

# Simplified Algorithm

1. Scan expression
2. Operand → output
3. Operator → stack
4. Pop based on precedence

---

# 5. Expression Evaluation

Stack evaluates postfix/prefix efficiently.

---

# Postfix Evaluation Example

```text id="jlwmic"
2 3 + 4 *
```

Steps:

```text id="jlwmz9"
2 3 → push
+ → pop 2,3 → 5
4 → push
* → 5 * 4 = 20
```

---

# Postfix Evaluation Code

```js id="jlwmwr"
function evaluatePostfix(expression) {
  const stack = [];

  for (const token of expression.split(" ")) {
    if (!isNaN(token)) {
      stack.push(Number(token));
    } else {
      const b = stack.pop();
      const a = stack.pop();

      switch (token) {
        case "+":
          stack.push(a + b);
          break;

        case "-":
          stack.push(a - b);
          break;

        case "*":
          stack.push(a * b);
          break;

        case "/":
          stack.push(a / b);
          break;
      }
    }
  }

  return stack.pop();
}
```

---

# Complexity

| Operation  | Complexity |
| ---------- | ---------- |
| Evaluation | O(n)       |

---

# Real-Time Example

## Calculator Applications

Mobile calculators internally use stacks.

---

# 6. Monotonic Stack

Advanced and extremely important interview pattern.

---

# What is Monotonic Stack?

A stack that maintains:

* Increasing order
  or
* Decreasing order

---

# Types

| Type             | Order            |
| ---------------- | ---------------- |
| Increasing Stack | Smaller → Larger |
| Decreasing Stack | Larger → Smaller |

---

# Why Monotonic Stack?

Optimizes:

* Next greater/smaller problems
* Range problems
* Histogram problems

---

# Example

Find next greater element.

---

# Visualization

```text id="jlwm11"
Array:
[2,1,3]

Stack maintains decreasing order.
```

---

# Complexity

```text id="jlwmu2"
O(n)
```

Each element pushed/popped once.

---

# Real-Time Applications

| System              | Usage              |
| ------------------- | ------------------ |
| Stock span analysis | Price tracking     |
| Weather systems     | Temperature trends |
| Data streams        | Range optimization |

---

# 7. Min Stack

Special stack supporting:

```text id="jlwmn4"
getMin() → O(1)
```

---

# Problem

Normal stack:
Finding minimum requires:

```text id="jlwmz1"
O(n)
```

---

# Solution

Maintain extra stack.

---

# Implementation

```js id="jlwmhk"
class MinStack {
  constructor() {
    this.stack = [];
    this.minStack = [];
  }

  push(val) {
    this.stack.push(val);

    if (
      this.minStack.length === 0 ||
      val <= this.getMin()
    ) {
      this.minStack.push(val);
    }
  }

  pop() {
    const removed = this.stack.pop();

    if (removed === this.getMin()) {
      this.minStack.pop();
    }
  }

  getMin() {
    return this.minStack[this.minStack.length - 1];
  }
}
```

---

# Complexity

| Operation | Complexity |
| --------- | ---------- |
| Push      | O(1)       |
| Pop       | O(1)       |
| Get Min   | O(1)       |

---

# Real-Time Applications

| System             | Usage              |
| ------------------ | ------------------ |
| Financial systems  | Lowest stock price |
| Monitoring systems | Minimum metrics    |
| Gaming engines     | Min-state tracking |

---

# 8. Next Greater Element (NGE)

Classic monotonic stack problem.

---

# Problem

Find next greater element for every element.

---

# Example

```text id="jlwm37"
[2,1,3]

Output:
[3,3,-1]
```

---

# Brute Force

Nested loops:

```text id="jlwmff"
O(n²)
```

---

# Optimized Stack Solution

```js id="jlwmyl"
function nextGreater(arr) {
  const result = Array(arr.length).fill(-1);
  const stack = [];

  for (let i = 0; i < arr.length; i++) {
    while (
      stack.length &&
      arr[i] > arr[stack[stack.length - 1]]
    ) {
      const index = stack.pop();
      result[index] = arr[i];
    }

    stack.push(i);
  }

  return result;
}
```

---

# Complexity

```text id="jlwm6c"
O(n)
```

---

# Real-Time Applications

| System               | Usage                 |
| -------------------- | --------------------- |
| Stock market         | Next higher price     |
| Temperature analysis | Warmer day prediction |
| CPU monitoring       | Load spikes           |

---

# 9. Histogram Problems

Very famous stack interview topic.

---

# Largest Rectangle in Histogram

Given bar heights:
Find maximum rectangle area.

---

# Example

```text id="jlwm0f"
[2,1,5,6,2,3]
```

Maximum area:

```text id="jlwmvr"
10
```

---

# Why Stack?

Need:

* Previous smaller element
* Next smaller element

Efficiently.

---

# Brute Force

```text id="jlwmqe"
O(n²)
```

---

# Optimized Monotonic Stack

```text id="jlwmj0"
O(n)
```

---

# Key Idea

Maintain increasing stack.

When smaller element appears:

* Calculate areas.

---

# Real-Time Applications

| System           | Usage               |
| ---------------- | ------------------- |
| Image processing | Rectangle detection |
| Data analytics   | Range computations  |
| Graphics engines | Histogram analysis  |

---

# Advanced Stack Problems

| Problem             | Pattern         |
| ------------------- | --------------- |
| Valid Parentheses   | Basic stack     |
| Min Stack           | Auxiliary stack |
| Largest Rectangle   | Monotonic stack |
| Daily Temperatures  | Next greater    |
| Stock Span          | Monotonic stack |
| Decode String       | Nested stacks   |
| Evaluate Expression | Parsing         |

---

# Stack in System Design

Stacks are deeply used in:

* Runtime environments
* Virtual machines
* Recursive execution
* Memory allocation
* Undo systems
* Expression parsing

---

# Call Stack in JavaScript

When functions execute:

```js id="jlwm7u"
function a() {
  b();
}

function b() {
  c();
}

function c() {
  console.log("Hello");
}

a();
```

---

# Call Stack Visualization

```text id="jlwmfc"
c()
b()
a()
main()
```

Functions pop after execution.

---

# Stack Overflow

Occurs when recursion becomes too deep.

---

# Example

```js id="jlwm3l"
function recurse() {
  recurse();
}

recurse();
```

Causes:

```text id="jlwmbo"
Maximum call stack exceeded
```

---

# Common Beginner Mistakes

| Mistake                     | Problem              |
| --------------------------- | -------------------- |
| Popping empty stack         | Underflow            |
| Forgetting precedence       | Wrong expressions    |
| Using brute force           | Poor performance     |
| Ignoring monotonic patterns | Missed optimizations |
| Infinite recursion          | Stack overflow       |

---

# Production Engineering Insights

Stacks power:

* Browser rendering engines
* JavaScript runtimes
* Databases
* Compilers
* Kubernetes schedulers
* AI parsers

---

# Stack vs Queue

| Feature   | Stack | Queue      |
| --------- | ----- | ---------- |
| Order     | LIFO  | FIFO       |
| Insert    | Top   | Rear       |
| Remove    | Top   | Front      |
| Use Cases | Undo  | Scheduling |

---

# Summary Table

| Topic                 | Key Idea              |
| --------------------- | --------------------- |
| Stack Basics          | LIFO                  |
| Array Stack           | Simple implementation |
| Linked List Stack     | Dynamic memory        |
| Expression Evaluation | Parsing math          |
| Monotonic Stack       | Optimization pattern  |
| Min Stack             | O(1) minimum          |
| Next Greater Element  | Stack optimization    |
| Histogram Problems    | Range computation     |

---
