# Trees Fundamentals

Trees are one of the most important non-linear data structures.

Almost every large-scale software system internally uses trees.

Trees power:

* Databases
* File systems
* Search engines
* Compilers
* AI systems
* Networking
* Operating systems

---

# Why Trees Exist

Arrays and Linked Lists are linear.

But many real-world relationships are hierarchical.

Example:

```text id="t1"
Company
 ├── HR
 ├── Engineering
 │    ├── Frontend
 │    └── Backend
 └── Sales
```

This hierarchical structure is naturally represented using Trees.

---

# Real-World Examples

| System              | Tree Usage       |
| ------------------- | ---------------- |
| File systems        | Folder hierarchy |
| DOM in browsers     | HTML structure   |
| Databases           | B-Trees          |
| AI decision systems | Decision Trees   |
| DNS                 | Domain hierarchy |

---

# 1. What is a Tree?

A Tree is a hierarchical data structure consisting of:

* Nodes
* Edges

---

# Basic Structure

```text id="t2"
        A
      /   \
     B     C
    / \
   D   E
```

---

# Components

| Component | Meaning               |
| --------- | --------------------- |
| Node      | Data element          |
| Edge      | Connection            |
| Root      | Top node              |
| Leaf      | Node with no children |

---

# Properties

A tree:

* Has one root
* Has no cycles
* Is connected

---

# Why Trees Matter

Trees provide:

* Efficient searching
* Hierarchical representation
* Faster operations
* Scalable organization

---

# 2. Tree Terminologies

Very important for interviews.

---

# Root Node

Topmost node.

```text id="t3"
        A
```

A is root.

---

# Parent Node

A node having children.

```text id="t4"
A is parent of B and C
```

---

# Child Node

Nodes connected downward.

```text id="t5"
B and C are children of A
```

---

# Leaf Node

Node with no children.

```text id="t6"
D, E, C
```

---

# Siblings

Nodes sharing same parent.

```text id="t7"
B and C
```

---

# Ancestor

Nodes above current node.

For E:

```text id="t8"
A, B
```

---

# Descendant

Nodes below current node.

For A:

```text id="t9"
B, C, D, E
```

---

# Degree

Number of children.

```text id="t10"
Degree(B) = 2
```

---

# Subtree

Tree inside tree.

```text id="t11"
Subtree of B:
   B
  / \
 D   E
```

---

# Path

Sequence of connected nodes.

```text id="t12"
A → B → E
```

---

# Levels

Distance from root.

```text id="t13"
Level 0 → A
Level 1 → B,C
Level 2 → D,E
```

---

# Important Interview Note

Trees with:

```text id="t14"
n nodes
```

always have:

```text id="t15"
n - 1 edges
```

---

# 3. Binary Trees

One of the most important tree structures.

---

# Definition

A Binary Tree is a tree where each node has at most:

```text id="t16"
2 children
```

---

# Structure

```text id="t17"
        1
       / \
      2   3
     / \
    4   5
```

---

# Node Structure

```js id="t18"
class TreeNode {
  constructor(data) {
    this.data = data;
    this.left = null;
    this.right = null;
  }
}
```

---

# Why Binary Trees Matter

Foundation for:

* BST
* Heap
* Segment Trees
* AVL Trees
* Red-Black Trees

---

# Real-Time Applications

| System      | Usage            |
| ----------- | ---------------- |
| Compilers   | Expression trees |
| Databases   | B/B+ Trees       |
| AI          | Decision trees   |
| Compression | Huffman trees    |

---

# Types of Binary Trees

---

# 4. Full Binary Tree

Every node has:

* Either 0 children
* Or 2 children

---

# Example

```text id="t19"
        1
       / \
      2   3
         / \
        4   5
```

---

# Invalid Example

```text id="t20"
Node with only one child
```

Not full.

---

# Applications

* Expression trees
* Parsing systems

---

# 5. Perfect Binary Tree

All internal nodes have 2 children,
AND
all leaves are at same level.

---

# Example

```text id="t21"
        1
      /   \
     2     3
    / \   / \
   4  5  6  7
```

---

# Properties

For height h:

\text{Total Nodes} = 2^{h+1} - 1

---

# Why Important

Very balanced.

Efficient for:

* Searching
* Traversal

---

# 6. Complete Binary Tree

All levels filled except possibly last level.

Last level filled from left to right.

---

# Example

```text id="t22"
        1
      /   \
     2     3
    / \   /
   4  5  6
```

---

# Why Complete Trees Matter

Used heavily in:

```text id="t23"
Heap Data Structure
```

because array representation becomes efficient.

---

# 7. Tree Traversals

Traversal means visiting all nodes.

One of the most important topics in Trees.

---

# Major Traversals

| Traversal   | Order           |
| ----------- | --------------- |
| Preorder    | Root Left Right |
| Inorder     | Left Root Right |
| Postorder   | Left Right Root |
| Level Order | BFS traversal   |

---

# Example Tree

```text id="t24"
        A
      /   \
     B     C
    / \
   D   E
```

---

# 8. Preorder Traversal

Visit:

```text id="t25"
Root → Left → Right
```

---

# Traversal Order

```text id="t26"
A B D E C
```

---

# Recursive Code

```js id="t27"
function preorder(node) {
  if (!node) return;

  console.log(node.data);

  preorder(node.left);
  preorder(node.right);
}
```

---

# Real-Time Applications

| System             | Usage                  |
| ------------------ | ---------------------- |
| File copying       | Parent before children |
| Serialization      | Tree storage           |
| Expression parsing | Prefix notation        |

---

# 9. Inorder Traversal

Visit:

```text id="t28"
Left → Root → Right
```

---

# Traversal Order

```text id="t29"
D B E A C
```

---

# Code

```js id="t30"
function inorder(node) {
  if (!node) return;

  inorder(node.left);

  console.log(node.data);

  inorder(node.right);
}
```

---

# Very Important Property

For:

```text id="t31"
Binary Search Tree
```

Inorder traversal gives:

```text id="t32"
Sorted Order
```

---

# Real-Time Applications

| System      | Usage             |
| ----------- | ----------------- |
| BST sorting | Ordered traversal |
| Databases   | Sorted retrieval  |

---

# 10. Postorder Traversal

Visit:

```text id="t33"
Left → Right → Root
```

---

# Traversal Order

```text id="t34"
D E B C A
```

---

# Code

```js id="t35"
function postorder(node) {
  if (!node) return;

  postorder(node.left);
  postorder(node.right);

  console.log(node.data);
}
```

---

# Real-Time Applications

| System                | Usage                 |
| --------------------- | --------------------- |
| File deletion         | Delete children first |
| Memory cleanup        | Bottom-up freeing     |
| Expression evaluation | Postfix evaluation    |

---

# 11. Level Order Traversal

Uses:

```text id="t36"
Queue + BFS
```

---

# Traversal Order

```text id="t37"
A B C D E
```

---

# Code

```js id="t38"
function levelOrder(root) {
  if (!root) return;

  const queue = [root];

  while (queue.length) {
    const node = queue.shift();

    console.log(node.data);

    if (node.left) queue.push(node.left);
    if (node.right) queue.push(node.right);
  }
}
```

---

# Complexity

| Traversal      | Complexity |
| -------------- | ---------- |
| DFS Traversals | O(n)       |
| BFS Traversal  | O(n)       |

---

# 12. Height & Depth

Very important concepts.

---

# Height of Tree

Longest path from root to leaf.

---

# Example

```text id="t39"
        A
       /
      B
     /
    C
```

Height:

```text id="t40"
2
```

---

# Recursive Formula

\text{Height(node)} = 1 + \max(\text{leftHeight}, \text{rightHeight})

---

# Height Code

```js id="t41"
function height(node) {
  if (!node) return -1;

  return 1 + Math.max(
    height(node.left),
    height(node.right)
  );
}
```

---

# Depth of Node

Distance from root to node.

---

# Example

```text id="t42"
Depth(C) = 2
```

---

# Real-Time Applications

| System          | Usage          |
| --------------- | -------------- |
| Network routing | Path depth     |
| DOM trees       | Nested levels  |
| AI search       | Decision depth |

---

# 13. Recursive Traversal

Most tree algorithms use recursion naturally.

---

# Why Recursion Works Well

Trees are recursive structures.

Each subtree is itself a tree.

---

# General Recursive Pattern

```js id="t43"
function dfs(node) {
  if (!node) return;

  dfs(node.left);
  dfs(node.right);
}
```

---

# Advantages

* Cleaner code
* Natural tree processing
* Easier implementation

---

# Disadvantages

* Stack overflow risk
* Extra recursion memory

---

# 14. Iterative Traversal

Uses explicit stack instead of recursion.

Important for:

* Large trees
* System-level programming

---

# Iterative Preorder

```js id="t44"
function preorder(root) {
  if (!root) return;

  const stack = [root];

  while (stack.length) {
    const node = stack.pop();

    console.log(node.data);

    if (node.right) stack.push(node.right);
    if (node.left) stack.push(node.left);
  }
}
```

---

# Why Iterative Matters

Avoids:

```text id="t45"
Call Stack Overflow
```

---

# Iterative Inorder

More complex because:

* Need left traversal simulation

---

# Core Idea

```text id="t46"
Use explicit stack manually
```

---

# Recursive vs Iterative

| Feature     | Recursive       | Iterative       |
| ----------- | --------------- | --------------- |
| Simplicity  | Easier          | Harder          |
| Memory      | Call stack      | Explicit stack  |
| Performance | Slightly slower | Slightly faster |
| Large trees | Risky           | Safer           |

---

# Important Tree Interview Problems

| Problem                | Pattern          |
| ---------------------- | ---------------- |
| Maximum Depth          | DFS              |
| Level Order Traversal  | BFS              |
| Symmetric Tree         | Recursion        |
| Diameter of Tree       | DFS              |
| Balanced Tree          | Height recursion |
| Lowest Common Ancestor | Tree traversal   |
| Serialize Tree         | DFS/BFS          |

---

# Common Beginner Mistakes

| Mistake                | Problem            |
| ---------------------- | ------------------ |
| Forgetting base case   | Infinite recursion |
| Confusing height/depth | Wrong calculations |
| Wrong traversal order  | Incorrect output   |
| Ignoring null nodes    | Runtime errors     |
| Stack overflow         | Deep recursion     |

---

# Production Engineering Insights

Trees power:

* Google indexing
* Linux file systems
* Database indexing
* AI decision systems
* HTML DOM rendering
* Compiler syntax trees

Modern computing infrastructure relies heavily on trees.

---

# Tree vs Linked List

| Feature    | Tree           | Linked List |
| ---------- | -------------- | ----------- |
| Structure  | Hierarchical   | Linear      |
| Traversal  | Multiple paths | Sequential  |
| Searching  | Faster         | Slower      |
| Complexity | More complex   | Simpler     |

---

# Summary Table

| Topic               | Key Idea               |
| ------------------- | ---------------------- |
| Tree Basics         | Hierarchical structure |
| Binary Tree         | Max 2 children         |
| Full Tree           | 0 or 2 children        |
| Perfect Tree        | Completely balanced    |
| Complete Tree       | Heap-friendly          |
| Traversals          | Visit nodes            |
| Height              | Longest root-leaf path |
| Depth               | Distance from root     |
| Recursive Traversal | Natural DFS            |
| Iterative Traversal | Stack-based DFS        |

---
