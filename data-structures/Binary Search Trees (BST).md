# Binary Search Trees (BST)

Binary Search Trees are one of the most important tree-based data structures.

BSTs combine:

* Fast searching
* Ordered storage
* Hierarchical structure

They are heavily used in:

* Databases
* Search engines
* File systems
* Compilers
* In-memory indexes
* Scheduling systems

---

# Why BST Exists

Normal Binary Trees do NOT guarantee fast searching.

Example:

```text id="bst1"
        10
       /  \
      50   2
```

No ordering.

Searching becomes:

```text id="bst2"
O(n)
```

BST introduces ordering rules.

---

# 1. BST Properties

A Binary Search Tree follows:

```text id="bst3"
Left subtree < Root < Right subtree
```

for every node.

---

# Example

```text id="bst4"
         50
        /  \
      30    70
     / \   / \
   20 40 60 80
```

---

# Important BST Rule

For every node:

* Left values are smaller
* Right values are greater

---

# Why This Matters

Searching becomes efficient.

Similar to:

```text id="bst5"
Binary Search on arrays
```

---

# BST Node Structure

```js id="bst6"
class TreeNode {
  constructor(data) {
    this.data = data;
    this.left = null;
    this.right = null;
  }
}
```

---

# Time Complexity

| Operation | Average  | Worst |
| --------- | -------- | ----- |
| Search    | O(log n) | O(n)  |
| Insert    | O(log n) | O(n)  |
| Delete    | O(log n) | O(n)  |

Worst case occurs in skewed trees.

---

# Real-Time Applications

| System             | Usage            |
| ------------------ | ---------------- |
| Databases          | Ordered indexing |
| Search engines     | Sorted retrieval |
| Scheduling systems | Event ordering   |
| Compilers          | Symbol tables    |

---

# 2. Searching in BST

Very efficient because of ordering.

---

# Search Logic

At every node:

* If target smaller → go left
* If target larger → go right

---

# Example

Search:

```text id="bst7"
60
```

Traversal:

```text id="bst8"
50 → 70 → 60
```

---

# Search Code

```js id="bst9"
function search(root, target) {
  if (!root) return false;

  if (root.data === target) {
    return true;
  }

  if (target < root.data) {
    return search(root.left, target);
  }

  return search(root.right, target);
}
```

---

# Complexity

Balanced BST:

```text id="bst10"
O(log n)
```

---

# Real-Time Example

## Database Indexing

Instead of scanning every row:

* Tree traversal narrows search quickly.

---

# 3. Insertion in BST

Insert while maintaining BST property.

---

# Example

Insert:

```text id="bst11"
65
```

---

# Tree

Before:

```text id="bst12"
        50
       /  \
     30    70
          /
         60
```

After:

```text id="bst13"
        50
       /  \
     30    70
          /
         60
           \
            65
```

---

# Insert Algorithm

1. Compare with root
2. Move left/right
3. Insert at null position

---

# Insert Code

```js id="bst14"
function insert(root, value) {
  if (!root) {
    return new TreeNode(value);
  }

  if (value < root.data) {
    root.left = insert(root.left, value);
  } else {
    root.right = insert(root.right, value);
  }

  return root;
}
```

---

# Complexity

Balanced BST:

```text id="bst15"
O(log n)
```

---

# 4. Deletion in BST

One of the most important interview topics.

---

# Cases in Deletion

---

# Case 1: Leaf Node

Simply remove.

---

# Example

```text id="bst16"
Delete 20
```

```text id="bst17"
20 has no children
```

---

# Case 2: One Child

Replace node with child.

---

# Example

```text id="bst18"
30
 \
  40
```

Delete 30:

```text id="bst19"
40 replaces 30
```

---

# Case 3: Two Children

Most important case.

Replace with:

* Inorder Successor
  or
* Inorder Predecessor

---

# Inorder Successor

Smallest node in right subtree.

---

# Example

```text id="bst20"
        50
       /  \
     30    70
          / \
         60 80
```

Delete 70:

* Successor = 80

---

# Delete Code

```js id="bst21"
function deleteNode(root, key) {
  if (!root) return null;

  if (key < root.data) {
    root.left = deleteNode(root.left, key);

  } else if (key > root.data) {
    root.right = deleteNode(root.right, key);

  } else {

    if (!root.left) return root.right;
    if (!root.right) return root.left;

    let successor = root.right;

    while (successor.left) {
      successor = successor.left;
    }

    root.data = successor.data;

    root.right = deleteNode(
      root.right,
      successor.data
    );
  }

  return root;
}
```

---

# Complexity

| Operation | Complexity       |
| --------- | ---------------- |
| Delete    | O(log n) average |

---

# Real-Time Applications

Deletion logic is heavily used in:

* Databases
* Memory management
* Scheduling systems

---

# 5. Balanced BST Concepts

Extremely important for interviews and system design.

---

# Problem with Normal BST

BST can become skewed.

---

# Example

Insert:

```text id="bst22"
10,20,30,40
```

Tree becomes:

```text id="bst23"
10
 \
  20
    \
     30
       \
        40
```

---

# Complexity Degrades

Searching becomes:

```text id="bst24"
O(n)
```

Like Linked List.

---

# Balanced BST Solution

Maintain balanced height.

---

# Balanced Tree Example

```text id="bst25"
        20
       /  \
     10    30
```

---

# Complexity

Balanced BST guarantees:

```text id="bst26"
O(log n)
```

operations.

---

# Popular Balanced BSTs

| Tree           | Feature              |
| -------------- | -------------------- |
| AVL Tree       | Strict balancing     |
| Red-Black Tree | Relaxed balancing    |
| B-Tree         | Disk optimized       |
| Treap          | Randomized balancing |

---

# Real-Time Applications

| System       | Usage           |
| ------------ | --------------- |
| Linux Kernel | Red-Black Trees |
| Databases    | B/B+ Trees      |
| Java TreeMap | Red-Black Tree  |

---

# 6. Floor & Ceil in BST

Very common interview problem.

---

# Floor

Largest value ≤ target.

---

# Ceil

Smallest value ≥ target.

---

# Example

Tree:

```text id="bst27"
        20
       /  \
     10    30
```

Target:

```text id="bst28"
25
```

Floor:

```text id="bst29"
20
```

Ceil:

```text id="bst30"
30
```

---

# Floor Algorithm

```js id="bst31"
function floor(root, key) {
  let ans = null;

  while (root) {
    if (root.data === key) {
      return root.data;
    }

    if (root.data > key) {
      root = root.left;
    } else {
      ans = root.data;
      root = root.right;
    }
  }

  return ans;
}
```

---

# Complexity

Balanced BST:

```text id="bst32"
O(log n)
```

---

# Real-Time Applications

| System          | Usage             |
| --------------- | ----------------- |
| Scheduling      | Closest time slot |
| Trading systems | Nearest price     |
| Search systems  | Closest match     |

---

# 7. Lowest Common Ancestor (LCA)

One of the most important tree interview problems.

---

# Definition

Lowest node having both nodes as descendants.

---

# Example

```text id="bst33"
         20
        /  \
      10    30
     / \
    5  15
```

LCA of:

```text id="bst34"
5 and 15
```

is:

```text id="bst35"
10
```

---

# BST Optimization

Use BST ordering property.

---

# Algorithm

* If both smaller → go left
* If both larger → go right
* Otherwise current node is LCA

---

# Code

```js id="bst36"
function lca(root, p, q) {
  while (root) {

    if (p < root.data && q < root.data) {
      root = root.left;

    } else if (
      p > root.data &&
      q > root.data
    ) {
      root = root.right;

    } else {
      return root;
    }
  }
}
```

---

# Complexity

Balanced BST:

```text id="bst37"
O(log n)
```

---

# Real-Time Applications

| System       | Usage                |
| ------------ | -------------------- |
| File systems | Common directory     |
| Networking   | Routing ancestors    |
| DOM trees    | Common parent lookup |

---

# 8. BST Validation

Very famous interview problem.

---

# Problem

Check whether tree satisfies BST property.

---

# Wrong Approach

Checking only direct children is insufficient.

---

# Example

```text id="bst38"
        10
       /  \
      5   15
         /
        6
```

Invalid BST because:

```text id="bst39"
6 < 10
```

---

# Correct Approach

Maintain valid range.

---

# Validation Code

```js id="bst40"
function isValidBST(
  root,
  min = -Infinity,
  max = Infinity
) {
  if (!root) return true;

  if (
    root.data <= min ||
    root.data >= max
  ) {
    return false;
  }

  return (
    isValidBST(root.left, min, root.data) &&
    isValidBST(root.right, root.data, max)
  );
}
```

---

# Complexity

| Complexity | Value |
| ---------- | ----- |
| Time       | O(n)  |
| Space      | O(h)  |

---

# Real-Time Applications

Validation logic used in:

* Database indexing
* Compiler syntax trees
* Memory allocators

---

# Important BST Interview Problems

| Problem                     | Pattern               |
| --------------------------- | --------------------- |
| Search BST                  | Binary search         |
| Validate BST                | Range recursion       |
| Kth Smallest                | Inorder traversal     |
| LCA                         | BST optimization      |
| Delete Node                 | Successor replacement |
| BST Iterator                | Controlled inorder    |
| Convert Sorted Array to BST | Divide & conquer      |

---

# Common Beginner Mistakes

| Mistake                         | Problem           |
| ------------------------------- | ----------------- |
| Forgetting BST ordering         | Invalid tree      |
| Wrong deletion logic            | Broken tree       |
| Ignoring skewed trees           | O(n) slowdown     |
| Incorrect validation            | False positives   |
| Confusing successor/predecessor | Wrong replacement |

---

# Production Engineering Insights

BST concepts power:

* Database indexing
* Filesystem metadata
* Scheduling systems
* Search engines
* AI decision systems

Balanced BSTs are foundational in high-performance systems.

---

# BST vs Binary Tree

| Feature  | Binary Tree   | BST            |
| -------- | ------------- | -------------- |
| Ordering | None          | Ordered        |
| Search   | O(n)          | O(log n) avg   |
| Usage    | General trees | Fast searching |

---

# BST vs HashMap

| Feature       | BST       | HashMap   |
| ------------- | --------- | --------- |
| Ordering      | Sorted    | Unordered |
| Search        | O(log n)  | O(1) avg  |
| Range Queries | Efficient | Poor      |

---

# Summary Table

| Topic          | Key Idea            |
| -------------- | ------------------- |
| BST Properties | Left < Root < Right |
| Search         | Binary traversal    |
| Insert         | Ordered insertion   |
| Delete         | 3 deletion cases    |
| Balanced BST   | Maintain height     |
| Floor & Ceil   | Closest values      |
| LCA            | Common ancestor     |
| BST Validation | Range checking      |

---
