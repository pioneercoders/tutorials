# Advanced Graph Algorithms

Advanced Graph Algorithms are the backbone of:

* Google Maps
* GPS navigation
* AI pathfinding
* Network routing
* Distributed systems
* Social networks
* Compilers
* Recommendation engines

These algorithms solve:

* Dependency ordering
* Shortest path
* Network optimization
* Connectivity analysis
* Route planning
* Cycle detection

---

# Why Advanced Graph Algorithms Matter

Basic traversal:

* Only explores graph

Advanced algorithms:

* Optimize routes
* Find cheapest paths
* Detect dependencies
* Build efficient networks
* Analyze connectivity

---

# Major Advanced Graph Topics

| Algorithm        | Purpose                  |
| ---------------- | ------------------------ |
| Topological Sort | Dependency ordering      |
| Dijkstra         | Shortest path            |
| Bellman-Ford     | Negative weights         |
| Floyd-Warshall   | All-pairs shortest paths |
| MST              | Cheapest network         |
| Kruskal          | MST using sorting        |
| Prim’s           | MST using heap           |
| Union Find       | Dynamic connectivity     |
| SCC              | Strong graph groups      |
| Tarjan           | SCC optimization         |
| Kosaraju         | SCC detection            |
| A*               | Heuristic pathfinding    |

---

# 1. Topological Sort

Very important directed graph algorithm.

---

# What is Topological Sorting?

Linear ordering of vertices such that:

```text id="ag1"
For every directed edge U → V,
U comes before V
```

---

# Works Only On

```text id="ag2"
Directed Acyclic Graphs (DAG)
```

---

# Example

```text id="ag3"
Course Dependencies:

Math → Algorithms → AI
```

Valid order:

```text id="ag4"
Math, Algorithms, AI
```

---

# Real-World Applications

| System            | Usage                 |
| ----------------- | --------------------- |
| Build systems     | Dependency resolution |
| Course scheduling | Prerequisites         |
| CI/CD pipelines   | Task ordering         |
| Compilers         | Compilation ordering  |

---

# DFS-Based Topological Sort

Idea:

* DFS
* Push nodes after visiting children

---

# Topological Sort Code

```js id="ag5"
function topoSort(graph) {

  const visited = new Set();
  const stack = [];

  function dfs(node) {

    visited.add(node);

    for (const neighbor of graph[node]) {

      if (!visited.has(neighbor)) {
        dfs(neighbor);
      }
    }

    stack.push(node);
  }

  for (const node in graph) {

    if (!visited.has(node)) {
      dfs(node);
    }
  }

  return stack.reverse();
}
```

---

# Complexity

| Complexity | Value    |
| ---------- | -------- |
| Time       | O(V + E) |

---

# DAG Workflow Visualization

---

# 2. Dijkstra Algorithm

One of the most famous graph algorithms.

---

# Purpose

Find:

```text id="ag6"
Shortest path from source node
```

in weighted graphs.

---

# Important Limitation

Works only when:

```text id="ag7"
No negative weights
```

---

# Real-World Applications

| System      | Usage                 |
| ----------- | --------------------- |
| Google Maps | Shortest routes       |
| Networking  | Packet routing        |
| GPS systems | Navigation            |
| AI games    | Movement optimization |

---

# Core Idea

Always expand:

```text id="ag8"
Closest unvisited node
```

---

# Data Structures Used

| Structure      | Purpose              |
| -------------- | -------------------- |
| Priority Queue | Minimum distance     |
| Distance Array | Best known distances |

---

# Example Graph

```text id="ag9"
A --4--> B
A --1--> C
C --2--> B
```

Shortest:

```text id="ag10"
A → C → B
```

---

# Dijkstra Complexity

| Implementation      | Complexity     |
| ------------------- | -------------- |
| Array               | O(V²)          |
| Heap/Priority Queue | O((V+E) log V) |

---

# Simplified Code

```js id="ag11"
function dijkstra(graph, start) {

  const distances = {};

  for (const node in graph) {
    distances[node] = Infinity;
  }

  distances[start] = 0;
}
```

---

# 3. Bellman-Ford Algorithm

Handles:

```text id="ag12"
Negative edge weights
```

---

# Why Needed?

Dijkstra fails with negative weights.

---

# Example

```text id="ag13"
A → B = -5
```

---

# Bellman-Ford Idea

Relax all edges:

```text id="ag14"
V - 1 times
```

---

# Relaxation Formula

\text{dist}[v] = \min(\text{dist}[v],\ \text{dist}[u] + w)

---

# Key Feature

Detects:

```text id="ag15"
Negative cycles
```

---

# Real-Time Applications

| System               | Usage                  |
| -------------------- | ---------------------- |
| Currency trading     | Arbitrage detection    |
| Network optimization | Negative cost analysis |
| Finance systems      | Profit cycle detection |

---

# Complexity

| Complexity | Value |
| ---------- | ----- |
| Time       | O(VE) |

---

# Dijkstra vs Bellman-Ford

| Feature                  | Dijkstra | Bellman-Ford |
| ------------------------ | -------- | ------------ |
| Negative weights         | No       | Yes          |
| Speed                    | Faster   | Slower       |
| Negative cycle detection | No       | Yes          |

---

# 4. Floyd-Warshall Algorithm

Computes:

```text id="ag16"
Shortest paths between ALL pairs
```

---

# Why Important?

Instead of:

* Single source shortest path

Find:

* Every node → every node shortest path

---

# Dynamic Programming Based

---

# Formula

dist[i][j] = \min(dist[i][j],\ dist[i][k] + dist[k][j])

---

# Complexity

| Complexity | Value |
| ---------- | ----- |
| Time       | O(V³) |

---

# Real-Time Applications

| System          | Usage                  |
| --------------- | ---------------------- |
| Airline systems | All-route optimization |
| Networking      | Routing tables         |
| AI systems      | Global path analysis   |

---

# 5. Minimum Spanning Tree (MST)

Very important optimization problem.

---

# Goal

Connect all vertices with:

* Minimum total edge weight
* No cycles

---

# Example

```text id="ag17"
Electric cable layout
```

Need:

* Minimum wiring cost.

---

# MST Properties

For:

```text id="ag18"
V vertices
```

MST contains:

```text id="ag19"
V - 1 edges
```

---

# Real-Time Applications

| System           | Usage              |
| ---------------- | ------------------ |
| Network design   | Minimum cable      |
| Road planning    | Cheapest roads     |
| Electrical grids | Power optimization |

---

# MST Algorithms

| Algorithm | Strategy     |
| --------- | ------------ |
| Kruskal   | Edge-based   |
| Prim      | Vertex-based |

---

# 6. Kruskal Algorithm

Greedy MST algorithm.

---

# Core Idea

1. Sort edges
2. Pick smallest edge
3. Avoid cycles

---

# Uses

```text id="ag20"
Union Find (DSU)
```

---

# Workflow

```text id="ag21"
Sort edges → Add smallest safe edge
```

---

# Complexity

| Complexity | Value      |
| ---------- | ---------- |
| Time       | O(E log E) |

---

# Real-Time Applications

| System                 | Usage               |
| ---------------------- | ------------------- |
| Network infrastructure | Cable optimization  |
| Distributed systems    | Cluster connections |

---

# 7. Prim’s Algorithm

Another MST algorithm.

---

# Core Idea

Grow tree gradually.

Always select:

```text id="ag22"
Minimum edge from visited set
```

---

# Uses

```text id="ag23"
Priority Queue / Min Heap
```

---

# Complexity

| Implementation | Complexity |
| -------------- | ---------- |
| Heap           | O(E log V) |

---

# Prim vs Kruskal

---

# 8. Union Find (Disjoint Set Union - DSU)

Very important connectivity structure.

---

# Purpose

Efficiently track:

```text id="ag24"
Connected components
```

---

# Core Operations

| Operation  | Purpose          |
| ---------- | ---------------- |
| find(x)    | Find parent/root |
| union(x,y) | Merge sets       |

---

# Why Important?

Efficient cycle detection.

---

# Optimizations

| Optimization     | Purpose          |
| ---------------- | ---------------- |
| Path Compression | Faster find      |
| Union by Rank    | Balanced merging |

---

# Complexity

Almost constant time:

```text id="ag25"
O(α(n))
```

where:

```text id="ag26"
α = inverse Ackermann function
```

Practically constant.

---

# Real-Time Applications

| System             | Usage              |
| ------------------ | ------------------ |
| Network clustering | Connectivity       |
| Image segmentation | Component grouping |
| Kruskal MST        | Cycle prevention   |

---

# DSU Code

```js id="ag27"
class DSU {

  constructor(n) {
    this.parent = Array.from(
      { length: n },
      (_, i) => i
    );
  }

  find(x) {

    if (this.parent[x] !== x) {
      this.parent[x] =
        this.find(this.parent[x]);
    }

    return this.parent[x];
  }
}
```

---

# 9. Strongly Connected Components (SCC)

Applicable only in:

```text id="ag28"
Directed graphs
```

---

# Definition

A component where:

```text id="ag29"
Every node can reach every other node
```

---

# Example

```text id="ag30"
A → B → C
↑       ↓
← ← ← ←
```

All strongly connected.

---

# Real-Time Applications

| System                | Usage             |
| --------------------- | ----------------- |
| Social networks       | Communities       |
| Compiler optimization | Dependency groups |
| Web analysis          | Link structures   |

---

# 10. Tarjan Algorithm

Efficient SCC algorithm.

---

# Core Idea

Uses:

* DFS
* Low-link values

---

# Complexity

| Complexity | Value    |
| ---------- | -------- |
| Time       | O(V + E) |

---

# Key Insight

Detect SCCs during single DFS traversal.

---

# Real-Time Applications

| System           | Usage            |
| ---------------- | ---------------- |
| Network analysis | Strong clusters  |
| AI systems       | Dependency loops |

---

# 11. Kosaraju Algorithm

Another SCC algorithm.

---

# Steps

1. DFS ordering
2. Reverse graph
3. DFS again

---

# Complexity

| Complexity | Value    |
| ---------- | -------- |
| Time       | O(V + E) |

---

# Tarjan vs Kosaraju

| Feature    | Tarjan | Kosaraju |
| ---------- | ------ | -------- |
| DFS Passes | One    | Two      |
| Simplicity | Harder | Easier   |

---

# 12. A* Algorithm

Very important AI pathfinding algorithm.

---

# Purpose

Optimized shortest path search.

Used heavily in:

* Games
* Robotics
* Navigation systems

---

# Why Better Than Dijkstra?

Uses:

```text id="ag31"
Heuristic estimation
```

to guide search.

---

# Formula

f(n) = g(n) + h(n)

Where:

* g(n) = current path cost
* h(n) = estimated remaining cost

---

# Real-Time Applications

| System              | Usage         |
| ------------------- | ------------- |
| Google Maps         | Smart routing |
| Game AI             | NPC movement  |
| Robotics            | Navigation    |
| Autonomous vehicles | Path planning |

---

# Dijkstra vs A*

| Feature      | Dijkstra | A*       |
| ------------ | -------- | -------- |
| Heuristic    | No       | Yes      |
| Speed        | Slower   | Faster   |
| Search Scope | Broader  | Targeted |

---

# Advanced Graph Algorithm Complexity Overview

---

# Important Graph Interview Problems

| Problem              | Algorithm        |
| -------------------- | ---------------- |
| Course Schedule      | Topological Sort |
| Network Delay Time   | Dijkstra         |
| Cheapest Flights     | Bellman-Ford     |
| Connecting Cities    | MST              |
| Redundant Connection | DSU              |
| Alien Dictionary     | Topological Sort |
| Word Ladder          | BFS              |
| SCC Detection        | Tarjan/Kosaraju  |

---

# Common Beginner Mistakes

| Mistake                            | Problem              |
| ---------------------------------- | -------------------- |
| Using Dijkstra on negative weights | Incorrect paths      |
| Forgetting cycle checks            | Invalid MST          |
| Confusing MST vs shortest path     | Wrong solution       |
| Ignoring heuristics in A*          | Poor optimization    |
| Wrong SCC traversal                | Incorrect components |

---

# Production Engineering Insights

These algorithms power:

* Google Maps
* Kubernetes networking
* AI game engines
* Distributed databases
* Internet routing protocols
* Recommendation systems
* Autonomous vehicles

Modern infrastructure heavily depends on graph optimization algorithms.

---

# Summary Table

| Topic            | Key Idea                 |
| ---------------- | ------------------------ |
| Topological Sort | Dependency ordering      |
| Dijkstra         | Shortest path            |
| Bellman-Ford     | Negative weights         |
| Floyd-Warshall   | All-pairs shortest paths |
| MST              | Cheapest connection      |
| Kruskal          | Edge-based MST           |
| Prim             | Vertex-based MST         |
| DSU              | Connectivity tracking    |
| SCC              | Strong graph groups      |
| Tarjan           | Efficient SCC            |
| Kosaraju         | Two-pass SCC             |
| A*               | Heuristic pathfinding    |

---
