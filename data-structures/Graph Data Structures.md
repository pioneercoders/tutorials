# Graph Data Structures

Graphs are one of the most powerful and important data structures in Computer Science.

Graphs model:

* Relationships
* Connections
* Networks
* Paths
* Dependencies

Modern systems heavily rely on graphs:

* Google Maps
* Social networks
* Internet routing
* Recommendation systems
* AI knowledge graphs
* Blockchain
* Operating systems

---

# Why Graphs Matter

Many real-world systems are NOT linear or hierarchical.

Example:

* Social network users connect arbitrarily.
* Roads connect cities in multiple ways.

Trees cannot model these efficiently.

Graphs solve this.

---

# Real-World Examples

| System          | Graph Representation     |
| --------------- | ------------------------ |
| Facebook        | Users + friendships      |
| Google Maps     | Cities + roads           |
| LinkedIn        | Professional connections |
| Internet        | Routers + connections    |
| Airline systems | Airports + flights       |

---

# 1. What is a Graph?

A Graph consists of:

* Vertices (Nodes)
* Edges (Connections)

---

# Basic Structure

```text id="g1"
    A ----- B
    |       |
    |       |
    C ----- D
```

---

# Components

| Component     | Meaning           |
| ------------- | ----------------- |
| Vertex (Node) | Entity            |
| Edge          | Connection        |
| Weight        | Cost/distance     |
| Path          | Sequence of edges |

---

# Mathematical Representation

G = (V, E)

Where:

* V = Vertices
* E = Edges

---

# Example

```text id="g2"
Vertices:
A, B, C

Edges:
(A,B), (B,C)
```

---

# Graph Terminologies

| Term               | Meaning                   |
| ------------------ | ------------------------- |
| Degree             | Number of connected edges |
| Path               | Sequence of nodes         |
| Cycle              | Path returning to start   |
| Connected Graph    | All nodes reachable       |
| Disconnected Graph | Some unreachable nodes    |

---

# Why Graphs Are Powerful

Graphs can represent:

* Networks
* Dependencies
* Routes
* Relationships
* Flows

far better than arrays or trees.

---

# 2. Graph Representation

Very important interview and system-design topic.

Two major ways:

1. Adjacency Matrix
2. Adjacency List

---

# Why Representation Matters

Different representations affect:

* Memory usage
* Traversal speed
* Algorithm efficiency

---

# Example Graph

```text id="g3"
    A --- B
    |   /
    | /
    C
```

---

# 3. Adjacency Matrix

2D matrix representation.

---

# Idea

If edge exists:

```text id="g4"
matrix[i][j] = 1
```

Else:

```text id="g5"
0
```

---

# Matrix Representation

For graph:

```text id="g6"
A-B
A-C
B-C
```

Matrix:

```text id="g7"
    A B C
A [ 0 1 1 ]
B [ 1 0 1 ]
C [ 1 1 0 ]
```

---

# JavaScript Example

```js id="g8"
const graph = [
  [0, 1, 1],
  [1, 0, 1],
  [1, 1, 0]
];
```

---

# Complexity

| Operation  | Complexity |
| ---------- | ---------- |
| Add Edge   | O(1)       |
| Check Edge | O(1)       |
| Space      | O(V²)      |

---

# Advantages

* Fast edge lookup
* Simple implementation

---

# Disadvantages

* Huge memory usage
* Poor for sparse graphs

---

# Real-Time Applications

Used in:

* Dense networks
* Mathematical graph problems
* GPU graph processing

---

# 4. Adjacency List

Most commonly used graph representation.

---

# Idea

Store neighbors for each node.

---

# Representation

```text id="g9"
A → B → C
B → A → C
C → A → B
```

---

# JavaScript Example

```js id="g10"
const graph = {
  A: ["B", "C"],
  B: ["A", "C"],
  C: ["A", "B"]
};
```

---

# Complexity

| Operation  | Complexity |
| ---------- | ---------- |
| Add Edge   | O(1)       |
| Check Edge | O(V)       |
| Space      | O(V + E)   |

---

# Advantages

* Memory efficient
* Great for sparse graphs
* Most practical representation

---

# Disadvantages

* Edge lookup slower

---

# Real-Time Applications

| System                 | Usage            |
| ---------------------- | ---------------- |
| Social networks        | Friend lists     |
| Google Maps            | Road networks    |
| Recommendation engines | User-item graphs |

---

# Adjacency Matrix vs Adjacency List

---

# Comparison Table

| Feature       | Matrix | List      |
| ------------- | ------ | --------- |
| Space         | O(V²)  | O(V+E)    |
| Edge Lookup   | Fast   | Slower    |
| Sparse Graphs | Bad    | Excellent |
| Dense Graphs  | Good   | Good      |

---

# 5. Directed vs Undirected Graphs

Very important concept.

---

# Undirected Graph

Edges work both ways.

---

# Example

```text id="g11"
A ----- B
```

Means:

* A connected to B
* B connected to A

---

# Real-Time Examples

| System              | Usage             |
| ------------------- | ----------------- |
| Facebook friendship | Mutual connection |
| Road networks       | Two-way roads     |

---

# Adjacency List

```js id="g12"
A: [B]
B: [A]
```

---

# Directed Graph (Digraph)

Edges have direction.

---

# Example

```text id="g13"
A → B
```

Means:

* A points to B
* B may NOT point to A

---

# Real-Time Examples

| System            | Usage          |
| ----------------- | -------------- |
| Twitter followers | One-way        |
| Web links         | Directed pages |
| Task dependencies | Directed flow  |

---

# Directed Graph Representation

```js id="g14"
A: [B]
B: []
```

---

# Key Difference

| Type       | Direction     |
| ---------- | ------------- |
| Undirected | Bidirectional |
| Directed   | One-way       |

---

# Degree Terminologies

For directed graphs:

| Type       | Meaning        |
| ---------- | -------------- |
| In-degree  | Incoming edges |
| Out-degree | Outgoing edges |

---

# Example

```text id="g15"
A → B → C
```

For B:

* In-degree = 1
* Out-degree = 1

---

# 6. Weighted Graphs

Edges store weights/costs.

---

# Example

```text id="g16"
A --5-- B
 \      /
  2    1
   \  /
     C
```

Weights:

* Distance
* Cost
* Time
* Capacity

---

# Why Weighted Graphs Matter

Real systems need:

* Shortest path
* Cheapest route
* Fastest delivery

---

# JavaScript Representation

```js id="g17"
const graph = {
  A: [
    { node: "B", weight: 5 },
    { node: "C", weight: 2 }
  ],

  B: [
    { node: "C", weight: 1 }
  ],

  C: []
};
```

---

# Real-Time Applications

| System         | Weight Meaning |
| -------------- | -------------- |
| Google Maps    | Distance       |
| Airlines       | Ticket cost    |
| Networks       | Latency        |
| AI pathfinding | Movement cost  |

---

# Weighted vs Unweighted Graphs

| Feature    | Weighted | Unweighted   |
| ---------- | -------- | ------------ |
| Edge Cost  | Yes      | No           |
| Complexity | Higher   | Simpler      |
| Use Cases  | Routing  | Connectivity |

---

# Sparse vs Dense Graphs

Very important optimization concept.

---

# Sparse Graph

Few edges.

Example:

```text id="g18"
Social networks
```

Usually use:

```text id="g19"
Adjacency List
```

---

# Dense Graph

Many edges.

Example:

```text id="g20"
Fully connected systems
```

Usually use:

```text id="g21"
Adjacency Matrix
```

---

# Graph Complexity

For graph:

```text id="g22"
V = vertices
E = edges
```

Most graph algorithms use:

```text id="g23"
O(V + E)
```

---

# Graph Traversal Preview

Two major traversal algorithms:

| Algorithm | Structure Used  |
| --------- | --------------- |
| DFS       | Stack/Recursion |
| BFS       | Queue           |

These are foundational for:

* Pathfinding
* AI
* Networking
* Social graphs

---

# Important Graph Interview Problems

| Problem            | Pattern          |
| ------------------ | ---------------- |
| Number of Islands  | DFS/BFS          |
| Clone Graph        | Graph traversal  |
| Detect Cycle       | DFS              |
| Course Schedule    | Topological sort |
| Shortest Path      | BFS/Dijkstra     |
| Network Delay Time | Weighted graph   |

---

# Common Beginner Mistakes

| Mistake                     | Problem           |
| --------------------------- | ----------------- |
| Confusing tree/graph        | Wrong traversal   |
| Forgetting visited set      | Infinite loops    |
| Wrong representation choice | Memory waste      |
| Ignoring direction          | Incorrect results |
| Using matrix unnecessarily  | Poor scalability  |

---

# Production Engineering Insights

Graphs power:

* Google Maps routing
* Social recommendation engines
* Internet infrastructure
* AI knowledge graphs
* Blockchain networks
* Distributed systems

Modern internet-scale systems rely heavily on graph algorithms.

---

# Graph vs Tree

| Feature     | Tree         | Graph      |
| ----------- | ------------ | ---------- |
| Cycles      | No           | Possible   |
| Root        | Required     | Optional   |
| Connections | Hierarchical | Arbitrary  |
| Edges       | n-1          | Any number |

---

# Summary Table

| Topic            | Key Idea          |
| ---------------- | ----------------- |
| Graph Basics     | Nodes + edges     |
| Adjacency Matrix | 2D representation |
| Adjacency List   | Neighbor lists    |
| Directed Graph   | One-way edges     |
| Undirected Graph | Two-way edges     |
| Weighted Graph   | Cost-based edges  |

---
