# Graph Traversal

Graph Traversal means:

```text id="gt1"
Visiting all vertices/nodes in a graph
```

in a systematic way.

Traversal is the foundation for:

* Pathfinding
* Network analysis
* AI search
* Social networks
* Web crawling
* Recommendation systems

---

# Why Graph Traversal Matters

Graphs may contain:

* Cycles
* Multiple paths
* Disconnected components

Traversal algorithms help explore them efficiently.

---

# Two Main Traversal Algorithms

| Algorithm | Data Structure Used |
| --------- | ------------------- |
| BFS       | Queue               |
| DFS       | Stack / Recursion   |

---

# Example Graph

```text id="gt2"
        A
      /   \
     B     C
    / \     \
   D   E     F
```

---

# 1. Breadth First Search (BFS)

BFS explores:

```text id="gt3"
Level by level
```

---

# Traversal Order

Starting from A:

```text id="gt4"
A → B → C → D → E → F
```

---

# Key Idea

Visit all neighbors first before going deeper.

---

# Data Structure Used

```text id="gt5"
Queue
```

---

# BFS Visualization

```text id="gt6"
Queue:

[A]

↓

[B,C]

↓

[D,E,F]
```

---

# BFS Algorithm

1. Start node → enqueue
2. Mark visited
3. Remove from queue
4. Visit neighbors
5. Repeat

---

# BFS Code

```js id="gt7"
function bfs(graph, start) {
  const queue = [start];
  const visited = new Set();

  visited.add(start);

  while (queue.length) {
    const node = queue.shift();

    console.log(node);

    for (const neighbor of graph[node]) {

      if (!visited.has(neighbor)) {
        visited.add(neighbor);
        queue.push(neighbor);
      }
    }
  }
}
```

---

# Graph Example

```js id="gt8"
const graph = {
  A: ["B", "C"],
  B: ["D", "E"],
  C: ["F"],
  D: [],
  E: [],
  F: []
};
```

---

# BFS Complexity

| Complexity | Value    |
| ---------- | -------- |
| Time       | O(V + E) |
| Space      | O(V)     |

Where:

* V = Vertices
* E = Edges

---

# Why BFS is Powerful

BFS naturally finds:

```text id="gt9"
Shortest path in unweighted graphs
```

---

# Real-Time Applications of BFS

| System            | Usage              |
| ----------------- | ------------------ |
| Google Maps       | Shortest route     |
| Social networks   | Friend suggestions |
| Web crawlers      | Site exploration   |
| Multiplayer games | Pathfinding        |

---

# BFS Traversal Flow

---

# 2. Depth First Search (DFS)

DFS explores:

```text id="gt10"
As deep as possible first
```

before backtracking.

---

# Traversal Order

Possible DFS:

```text id="gt11"
A → B → D → E → C → F
```

---

# Key Idea

Go deep first,
then backtrack.

---

# Data Structure Used

| Method        | Structure      |
| ------------- | -------------- |
| Recursive DFS | Call Stack     |
| Iterative DFS | Explicit Stack |

---

# DFS Visualization

```text id="gt12"
A
↓
B
↓
D
↑
Backtrack
```

---

# Why DFS Matters

Useful for:

* Backtracking
* Cycle detection
* Topological sort
* Maze solving
* Dependency analysis

---

# 3. Recursive DFS

Most natural DFS implementation.

---

# Recursive Idea

Each node recursively explores neighbors.

---

# Recursive DFS Code

```js id="gt13"
function dfs(graph, node, visited = new Set()) {

  visited.add(node);

  console.log(node);

  for (const neighbor of graph[node]) {

    if (!visited.has(neighbor)) {
      dfs(graph, neighbor, visited);
    }
  }
}
```

---

# Traversal Example

Graph:

```text id="gt14"
A → B → D
  → C
```

Traversal:

```text id="gt15"
A B D C
```

---

# Recursive Call Stack

```text id="gt16"
dfs(A)
 dfs(B)
  dfs(D)
```

---

# Complexity

| Complexity | Value    |
| ---------- | -------- |
| Time       | O(V + E) |
| Space      | O(V)     |

---

# Advantages

* Clean code
* Natural tree/graph traversal
* Easier implementation

---

# Disadvantages

* Stack overflow risk
* Large graph issues

---

# Real-Time Applications

| System       | Usage               |
| ------------ | ------------------- |
| Maze solving | Deep exploration    |
| AI search    | State exploration   |
| File systems | Recursive traversal |
| Compilers    | Dependency analysis |

---

# 4. Iterative DFS

Uses explicit stack instead of recursion.

---

# Why Iterative DFS?

Avoids:

```text id="gt17"
Call stack overflow
```

---

# Data Structure

```text id="gt18"
Stack
```

---

# Iterative DFS Code

```js id="gt19"
function dfsIterative(graph, start) {

  const visited = new Set();
  const stack = [start];

  while (stack.length) {

    const node = stack.pop();

    if (!visited.has(node)) {

      visited.add(node);

      console.log(node);

      for (const neighbor of graph[node]) {
        stack.push(neighbor);
      }
    }
  }
}
```

---

# Visualization

```text id="gt20"
Stack:

[A]
↓

[C,B]
↓

[C,D,E]
```

---

# Complexity

| Complexity | Value    |
| ---------- | -------- |
| Time       | O(V + E) |
| Space      | O(V)     |

---

# Recursive DFS vs Iterative DFS

| Feature        | Recursive       | Iterative       |
| -------------- | --------------- | --------------- |
| Simplicity     | Easier          | Harder          |
| Stack Overflow | Possible        | Avoided         |
| Performance    | Slightly slower | Slightly faster |

---

# BFS vs DFS

Very important interview topic.

---

# Comparison

---

# Detailed Comparison

| Feature        | BFS        | DFS        |
| -------------- | ---------- | ---------- |
| Data Structure | Queue      | Stack      |
| Traversal      | Level-wise | Depth-wise |
| Shortest Path  | Yes        | No         |
| Memory Usage   | Higher     | Lower      |
| Backtracking   | Poor       | Excellent  |

---

# When to Use BFS

Use BFS when:

* Need shortest path
* Need level-order traversal
* Need nearest solution

---

# When to Use DFS

Use DFS when:

* Need exhaustive exploration
* Backtracking required
* Cycle detection needed

---

# 5. Connected Components

Very important graph problem.

---

# Definition

A Connected Component is:

```text id="gt21"
A group of connected vertices
```

---

# Example

```text id="gt22"
A --- B

C --- D

E
```

Connected components:

1. {A,B}
2. {C,D}
3. {E}

---

# Why Connected Components Matter

Used in:

* Social networks
* Network clustering
* Recommendation systems
* Image processing

---

# Algorithm Idea

Run:

* DFS
  or
* BFS

from every unvisited node.

Each traversal finds one component.

---

# Connected Components Code

```js id="gt23"
function connectedComponents(graph) {

  const visited = new Set();
  let count = 0;

  for (const node in graph) {

    if (!visited.has(node)) {

      dfs(graph, node, visited);

      count++;
    }
  }

  return count;
}
```

---

# Complexity

| Complexity | Value    |
| ---------- | -------- |
| Time       | O(V + E) |

---

# Real-Time Applications

| System           | Usage               |
| ---------------- | ------------------- |
| Facebook         | Friend communities  |
| Networking       | Isolated clusters   |
| AI systems       | Graph partitioning  |
| Image processing | Object segmentation |

---

# Traversal in Cyclic Graphs

Very important.

---

# Problem

Graphs may contain cycles.

```text id="gt24"
A → B → C
↑       ↓
← ← ← ←
```

Without visited set:

```text id="gt25"
Infinite loop
```

---

# Solution

Always maintain:

```text id="gt26"
Visited Set
```

---

# Directed vs Undirected Traversal

| Type       | Special Consideration   |
| ---------- | ----------------------- |
| Undirected | Avoid revisiting parent |
| Directed   | Respect edge direction  |

---

# Sparse vs Dense Graph Traversal

| Graph Type | Preferred Representation |
| ---------- | ------------------------ |
| Sparse     | Adjacency List           |
| Dense      | Adjacency Matrix         |

---

# Important Graph Traversal Interview Problems

| Problem           | Algorithm |
| ----------------- | --------- |
| Number of Islands | DFS/BFS   |
| Clone Graph       | DFS/BFS   |
| Rotten Oranges    | BFS       |
| Word Ladder       | BFS       |
| Detect Cycle      | DFS       |
| Course Schedule   | DFS       |

---

# Common Beginner Mistakes

| Mistake                      | Problem               |
| ---------------------------- | --------------------- |
| Forgetting visited set       | Infinite loops        |
| Wrong traversal order        | Incorrect answers     |
| Using recursion blindly      | Stack overflow        |
| Ignoring disconnected graphs | Missing nodes         |
| Confusing BFS/DFS use cases  | Inefficient solutions |

---

# Production Engineering Insights

Graph traversal powers:

* Google web crawling
* GPS navigation
* Recommendation engines
* Fraud detection
* AI search systems
* Kubernetes networking

Modern internet-scale systems rely heavily on BFS and DFS.

---

# DFS in AI Systems

DFS is heavily used in:

* Game engines
* Chess AI
* Backtracking problems
* Constraint solving

---

# BFS in Real-Time Systems

BFS powers:

* Routing protocols
* Multiplayer matchmaking
* Recommendation systems
* Social graph exploration

---

# Summary Table

| Topic                | Key Idea              |
| -------------------- | --------------------- |
| BFS                  | Level-order traversal |
| DFS                  | Deep traversal        |
| Recursive DFS        | Call stack traversal  |
| Iterative DFS        | Explicit stack        |
| Connected Components | Graph partitioning    |

---
