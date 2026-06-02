# Advanced Graph Algorithms

Advanced graph algorithms solve complex problems on graphs including shortest paths, minimum spanning trees, and network flow. They build on basic BFS/DFS with optimization techniques.

## Introduction

Advanced graph algorithms extend basic graph traversal (BFS/DFS) to solve complex optimization problems on weighted graphs. These include finding shortest paths (Dijkstra, Bellman-Ford), computing minimum spanning trees (Kruskal's, Prim's), solving network flow problems (Ford-Fulkerson), and finding all-pairs shortest paths (Floyd-Warshall). These algorithms are fundamental to navigation systems, network routing, social network analysis, and resource allocation. Unlike basic traversal, these algorithms consider edge weights and optimize for specific objectives like minimizing distance, cost, or maximizing flow.

**Why Advanced Graph Algorithms Exist:**
- Basic BFS/DFS insufficient for weighted graphs
- Need optimal solutions for shortest paths
- Handle negative edge weights and cycles
- Compute minimum spanning trees for network design
- Solve network flow problems for resource allocation
- Optimize routes in navigation systems

**Where It Is Used:**
- GPS navigation (shortest path)
- Network routing (packet routing)
- Social network analysis (influence maximization)
- Delivery optimization (route planning)
- Airline scheduling (minimum spanning tree)
- Resource allocation (network flow)
- Game AI (pathfinding)
- Telecommunications (network design)

## Core Concept Explanation

Advanced graph algorithms solve optimization problems on weighted graphs. Dijkstra's algorithm finds the shortest path from a source to all other nodes in a graph with non-negative edge weights using a greedy approach with a priority queue. Bellman-Ford handles graphs with negative edge weights and can detect negative cycles. Floyd-Warshall computes all-pairs shortest paths using dynamic programming. These algorithms build on the concept of "relaxation" - iteratively improving path estimates by considering intermediate nodes.

**Step-by-Step Breakdown:**
1. Represent graph with weighted edges
2. Initialize distances (infinity for all, 0 for source)
3. Use priority queue (Dijkstra) or iterative relaxation (Bellman-Ford)
4. For each node, relax edges to neighbors
5. Update distances if shorter path found
6. Repeat until no more improvements possible
7. For all-pairs, use dynamic programming (Floyd-Warshall)

**Intuition Behind the Concept:**
Think of finding the shortest path like planning a road trip. You start at your location and consider all possible routes. Dijkstra's algorithm is like always taking the closest unvisited city next - it's greedy but optimal for non-negative weights. Bellman-Ford is like checking all roads multiple times to ensure you haven't missed a shortcut, which handles negative weights (like going back in time). Floyd-Warshall is like considering every possible intermediate city for every pair of cities.

**Visual Thinking:**
```
Weighted Graph:
    A --4--> B
    | \       |
    2   1     5
    v   v     v
    C --8--> D
    \       /
     3     5
      \   /
       v v
        E

Dijkstra from A:
Initial: dist[A]=0, others=∞
Visit A: dist[B]=4, dist[C]=2
Visit C: dist[E]=5 (2+3)
Visit B: dist[D]=6 (4+1) or 9 (4+5)
Visit E: dist[D]=8 (5+5) or 6 (current)
Final: A=0, B=4, C=2, D=6, E=5
```

## Internal Working / Logic

Advanced graph algorithms operate through iterative relaxation of edge weights. The key concept is "relaxation" - if we find a shorter path to a node through an intermediate node, we update the distance. Different algorithms use different strategies for selecting which edges to relax and in what order.

**Operation 1: Relaxation**
- For edge (u, v) with weight w
- If dist[u] + w < dist[v], update dist[v] = dist[u] + w
- This is the core operation in all shortest path algorithms
- Repeated until no more improvements possible

**Operation 2: Dijkstra's Greedy Selection**
- Use priority queue (min-heap)
- Always select node with minimum distance
- Once selected, distance is final (for non-negative weights)
- Efficient for sparse graphs

**Operation 3: Bellman-Ford Iterative Relaxation**
- Relax all edges V-1 times
- Each iteration finds shortest paths with at most i edges
- V-1 iterations ensure shortest paths found (no negative cycles)
- Additional iteration detects negative cycles

**Operation 4: Floyd-Warshall Dynamic Programming**
- For each intermediate node k
- For each pair (i, j)
- Check if path through k is shorter
- Update dist[i][j] = min(dist[i][j], dist[i][k] + dist[k][j])

**Flow Explanation (Dijkstra):**
1. Initialize distances: source = 0, others = infinity
2. Add source to priority queue with distance 0
3. While queue not empty:
   - Extract node with minimum distance
   - For each neighbor:
     - Calculate new distance through current node
     - If shorter, update and add to queue
4. Return distances (shortest paths from source)

**Decision Making Logic:**
The key decision is which algorithm to use:
- Dijkstra: Non-negative weights, single source
- Bellman-Ford: Negative weights, negative cycle detection
- Floyd-Warshall: All-pairs shortest paths
- A*: Heuristic-guided search for single target
- Consider graph density and constraints

## Algorithm / Approach

**Dijkstra's Algorithm**

```
1. Initialize distances: source = 0, others = infinity
2. Add source to priority queue
3. While queue not empty:
   a. Extract node with minimum distance
   b. For each neighbor:
      i. Calculate new distance
      ii. If shorter, update and add to queue
4. Return distances
```

**Bellman-Ford Algorithm**

```
1. Initialize distances: source = 0, others = infinity
2. Repeat V-1 times:
   a. For each edge (u, v, w):
      i. If dist[u] + w < dist[v], update dist[v]
3. Check for negative cycles:
   a. For each edge (u, v, w):
      i. If dist[u] + w < dist[v], negative cycle exists
4. Return distances or error
```

**Floyd-Warshall Algorithm**

```
1. Initialize distance matrix
2. For each intermediate node k:
   a. For each pair (i, j):
      i. dist[i][j] = min(dist[i][j], dist[i][k] + dist[k][j])
3. Return distance matrix
```

**A* Algorithm**

```
1. Initialize g-score (actual cost) and f-score (estimated total)
2. Add start to priority queue with f-score
3. While queue not empty:
   a. Extract node with minimum f-score
   b. If target, reconstruct path
   c. For each neighbor:
      i. Calculate tentative g-score
      ii. If better, update and add to queue
4. Return path or failure
```

## Implementations

### 1. Dijkstra's Algorithm

```javascript
function dijkstra(graph, start) {
  const distances = {};
  const pq = new MinPriorityQueue();
  
  for (const node in graph) {
    distances[node] = Infinity;
  }
  distances[start] = 0;
  pq.enqueue(start, 0);
  
  while (!pq.isEmpty()) {
    const { element: node, priority: dist } = pq.dequeue();
    
    if (dist > distances[node]) continue;
    
    for (const [neighbor, weight] of Object.entries(graph[node])) {
      const newDist = dist + weight;
      if (newDist < distances[neighbor]) {
        distances[neighbor] = newDist;
        pq.enqueue(neighbor, newDist);
      }
    }
  }
  
  return distances;
}
```

**Advantages:**
- Optimal for non-negative weights
- Efficient with priority queue
- Widely used in navigation systems

### 2. Bellman-Ford Algorithm

```javascript
function bellmanFord(graph, start) {
  const distances = {};
  const nodes = Object.keys(graph);
  
  for (const node of nodes) {
    distances[node] = Infinity;
  }
  distances[start] = 0;
  
  // Relax edges V-1 times
  for (let i = 0; i < nodes.length - 1; i++) {
    for (const u of nodes) {
      for (const [v, weight] of Object.entries(graph[u])) {
        if (distances[u] + weight < distances[v]) {
          distances[v] = distances[u] + weight;
        }
      }
    }
  }
  
  // Check for negative cycles
  for (const u of nodes) {
    for (const [v, weight] of Object.entries(graph[u])) {
      if (distances[u] + weight < distances[v]) {
        return null; // Negative cycle detected
      }
    }
  }
  
  return distances;
}
```

**Advantages:**
- Handles negative edge weights
- Detects negative cycles
- Simpler than Dijkstra

### 3. Floyd-Warshall Algorithm

```javascript
function floydWarshall(graph) {
  const nodes = Object.keys(graph);
  const n = nodes.length;
  const dist = Array(n).fill(null).map(() => Array(n).fill(Infinity));
  
  // Initialize distance matrix
  for (let i = 0; i < n; i++) {
    dist[i][i] = 0;
    for (const [neighbor, weight] of Object.entries(graph[nodes[i]])) {
      dist[i][nodes.indexOf(neighbor)] = weight;
    }
  }
  
  // Floyd-Warshall algorithm
  for (let k = 0; k < n; k++) {
    for (let i = 0; i < n; i++) {
      for (let j = 0; j < n; j++) {
        if (dist[i][k] + dist[k][j] < dist[i][j]) {
          dist[i][j] = dist[i][k] + dist[k][j];
        }
      }
    }
  }
  
  return dist;
}
```

**Advantages:**
- All-pairs shortest paths
- Simple to implement
- Handles negative weights

### 4. A* Algorithm

```javascript
function aStar(graph, start, goal, heuristic) {
  const gScore = {};
  const fScore = {};
  const pq = new MinPriorityQueue();
  
  for (const node in graph) {
    gScore[node] = Infinity;
    fScore[node] = Infinity;
  }
  
  gScore[start] = 0;
  fScore[start] = heuristic(start, goal);
  pq.enqueue(start, fScore[start]);
  
  while (!pq.isEmpty()) {
    const { element: current } = pq.dequeue();
    
    if (current === goal) {
      return gScore[goal];
    }
    
    for (const [neighbor, weight] of Object.entries(graph[current])) {
      const tentativeG = gScore[current] + weight;
      
      if (tentativeG < gScore[neighbor]) {
        gScore[neighbor] = tentativeG;
        fScore[neighbor] = tentativeG + heuristic(neighbor, goal);
        pq.enqueue(neighbor, fScore[neighbor]);
      }
    }
  }
  
  return Infinity; // No path found
}
```

**Advantages:**
- Heuristic-guided search
- Faster than Dijkstra for single target
- Used in game AI and navigation

### 5. Network Delay Time

```javascript
function networkDelayTime(times, n, k) {
  const graph = {};
  
  for (let i = 1; i <= n; i++) {
    graph[i] = {};
  }
  
  for (const [u, v, w] of times) {
    graph[u][v] = w;
  }
  
  const distances = dijkstra(graph, k);
  let maxDist = 0;
  
  for (let i = 1; i <= n; i++) {
    if (distances[i] === Infinity) return -1;
    maxDist = Math.max(maxDist, distances[i]);
  }
  
  return maxDist;
}
```

**Advantages:**
- Finds time for signal to reach all nodes
- Uses Dijkstra's algorithm
- Practical network application

## Dry Run

**Example: Dijkstra's Algorithm**

**Input:**
```
graph = {
  'A': {'B': 4, 'C': 2},
  'B': {'C': 1, 'D': 5},
  'C': {'D': 8, 'B': 3},
  'D': {}
}
start = 'A'
```

**Step-by-Step Execution:**

```
Initial State:
distances = {A: 0, B: ∞, C: ∞, D: ∞}
pq = [(0, 'A')]

Iteration 1:
Extract 'A' with dist = 0
Neighbors: B (weight 4), C (weight 2)
dist[B] = min(∞, 0 + 4) = 4
dist[C] = min(∞, 0 + 2) = 2
pq = [(2, 'C'), (4, 'B')]
distances = {A: 0, B: 4, C: 2, D: ∞}

Iteration 2:
Extract 'C' with dist = 2
Neighbors: D (weight 8), B (weight 3)
dist[D] = min(∞, 2 + 8) = 10
dist[B] = min(4, 2 + 3) = 4 (no change)
pq = [(4, 'B'), (10, 'D')]
distances = {A: 0, B: 4, C: 2, D: 10}

Iteration 3:
Extract 'B' with dist = 4
Neighbors: C (weight 1), D (weight 5)
dist[C] = min(2, 4 + 1) = 2 (no change)
dist[D] = min(10, 4 + 5) = 9
pq = [(9, 'D')]
distances = {A: 0, B: 4, C: 2, D: 9}

Iteration 4:
Extract 'D' with dist = 9
Neighbors: none
pq = []
distances = {A: 0, B: 4, C: 2, D: 9}

Final: distances = {A: 0, B: 4, C: 2, D: 9}
```

**Variable Changes Table:**

| Iteration | Extracted | dist[A] | dist[B] | dist[C] | dist[D] | pq (after) |
|-----------|-----------|---------|---------|---------|---------|------------|
| Initial | - | 0 | ∞ | ∞ | ∞ | [(0, A)] |
| 1 | A | 0 | 4 | 2 | ∞ | [(2, C), (4, B)] |
| 2 | C | 0 | 4 | 2 | 10 | [(4, B), (10, D)] |
| 3 | B | 0 | 4 | 2 | 9 | [(9, D)] |
| 4 | D | 0 | 4 | 2 | 9 | [] |

## Edge Cases

### 1. Disconnected Graph
```javascript
graph = {A: {B: 1}, B: {}, C: {D: 2}, D: {}}
dijkstra(graph, 'A') → {A: 0, B: 1, C: ∞, D: ∞}
Some nodes unreachable
```

### 2. Negative Edge Weights
```javascript
graph = {A: {B: -1}, B: {C: 2}, C: {}}
dijkstra(graph, 'A') → May not work correctly
Use Bellman-Ford instead
```

### 3. Negative Cycle
```javascript
graph = {A: {B: 1}, B: {C: -2}, C: {A: 1}}
Bellman-Ford detects negative cycle
Returns null or error
```

### 4. Single Node
```javascript
graph = {A: {}}
dijkstra(graph, 'A') → {A: 0}
Base case
```

### 5. Self-Loop
```javascript
graph = {A: {A: 5, B: 1}, B: {}}
dijkstra(graph, 'A') → {A: 0, B: 1}
Self-loop ignored
```

### 6. Zero Weight Edges
```javascript
graph = {A: {B: 0}, B: {C: 1}, C: {}}
dijkstra(graph, 'A') → {A: 0, B: 0, C: 1}
Zero weights handled correctly
```

**Why Edge Cases Matter:**
- Disconnected graphs need infinity handling
- Negative weights require Bellman-Ford
- Negative cycles cause infinite loops
- Single node is base case
- Self-loops should be ignored
- Zero weights are valid

## Variations / Extensions

### 1. Cheapest Flights Within K Stops

```javascript
function findCheapestPrice(n, flights, src, dst, k) {
  const prices = new Array(n).fill(Infinity);
  prices[src] = 0;
  
  for (let i = 0; i <= k; i++) {
    const temp = [...prices];
    for (const [u, v, w] of flights) {
      if (prices[u] !== Infinity) {
        temp[v] = Math.min(temp[v], prices[u] + w);
      }
    }
    prices = temp;
  }
  
  return prices[dst] === Infinity ? -1 : prices[dst];
}
```

### 2. Path with Minimum Effort

```javascript
function minimumEffortPath(heights) {
  const m = heights.length;
  const n = heights[0].length;
  const directions = [[0, 1], [1, 0], [0, -1], [-1, 0]];
  
  const pq = new MinPriorityQueue();
  const efforts = new Array(m).fill(null).map(() => new Array(n).fill(Infinity));
  
  efforts[0][0] = 0;
  pq.enqueue([0, 0], 0);
  
  while (!pq.isEmpty()) {
    const { element: [x, y], priority: effort } = pq.dequeue();
    
    if (x === m - 1 && y === n - 1) return effort;
    
    for (const [dx, dy] of directions) {
      const nx = x + dx;
      const ny = y + dy;
      
      if (nx >= 0 && nx < m && ny >= 0 && ny < n) {
        const newEffort = Math.max(effort, Math.abs(heights[x][y] - heights[nx][ny]));
        if (newEffort < efforts[nx][ny]) {
          efforts[nx][ny] = newEffort;
          pq.enqueue([nx, ny], newEffort);
        }
      }
    }
  }
  
  return 0;
}
```

### 3. Reconstruct Itinerary

```javascript
function findItinerary(tickets) {
  const graph = {};
  
  for (const [from, to] of tickets) {
    if (!graph[from]) graph[from] = [];
    graph[from].push(to);
  }
  
  for (const from in graph) {
    graph[from].sort();
  }
  
  const result = [];
  
  function dfs(node) {
    while (graph[node] && graph[node].length > 0) {
      const next = graph[node].shift();
      dfs(next);
    }
    result.push(node);
  }
  
  dfs('JFK');
  return result.reverse();
}
```

### 4. Kruskal's Algorithm (MST)

```javascript
function kruskal(n, edges) {
  edges.sort((a, b) => a[2] - b[2]);
  const uf = new UnionFind(n);
  let mstWeight = 0;
  
  for (const [u, v, w] of edges) {
    if (uf.union(u, v)) {
      mstWeight += w;
    }
  }
  
  return mstWeight;
}
```

### 5. Prim's Algorithm (MST)

```javascript
function prim(n, graph) {
  const visited = new Set();
  const pq = new MinPriorityQueue();
  let mstWeight = 0;
  
  pq.enqueue([0, 0], 0); // [node, weight]
  
  while (visited.size < n) {
    const { element: [node, weight] } = pq.dequeue();
    
    if (visited.has(node)) continue;
    
    visited.add(node);
    mstWeight += weight;
    
    for (const [neighbor, w] of Object.entries(graph[node])) {
      if (!visited.has(neighbor)) {
        pq.enqueue([neighbor, w], w);
      }
    }
  }
  
  return mstWeight;
}
```

## Optimization Techniques

### 1. Priority Queue Optimization

**Efficient Extraction:**
```javascript
// Use binary heap or Fibonacci heap
// O(log V) extraction
// O(log V) insertion
```

### 2. Early Termination

**Stop When Target Found:**
```javascript
// For single-target problems
// Stop when target is extracted
// Saves unnecessary computation
```

### 3. Bidirectional Search

**Search from Both Ends:**
```javascript
// Start from source and target
// Meet in the middle
// Reduces search space
```

### 4. Trade-offs

**Algorithm Comparison:**

| Algorithm | Time | Space | Weights | Use Case |
|-----------|------|-------|---------|----------|
| Dijkstra | `O((V+E)log V)` | `O(V)` | Non-negative | Single source |
| Bellman-Ford | `O(VE)` | `O(V)` | Any | Negative weights |
| Floyd-Warshall | `O(V³)` | `O(V²)` | Any | All-pairs |
| A* | `O(E)` | `O(V)` | Non-negative | Single target |

**When to Use Each:**
- Dijkstra: Non-negative weights, single source
- Bellman-Ford: Negative weights, cycle detection
- Floyd-Warshall: All-pairs, dense graphs
- A*: Heuristic available, single target

## Complexity Analysis

### Time Complexity

**Dijkstra: O((V + E) log V)**
- V = vertices, E = edges
- Priority queue operations
- Each vertex processed once
- Each edge relaxed once

**Bellman-Ford: O(VE)**
- V = vertices, E = edges
- V-1 iterations over all edges
- Additional iteration for cycle detection

**Floyd-Warshall: O(V³)**
- V = vertices
- Three nested loops
- All-pairs shortest paths

**A*: O(E)**
- E = edges
- Depends on heuristic quality
- Best case: O(E), worst case: O(V²)

### Space Complexity

**Dijkstra: O(V)**
- Distance array: O(V)
- Priority queue: O(V)
- Total: O(V)

**Bellman-Ford: O(V)**
- Distance array: O(V)
- No additional space
- Total: O(V)

**Floyd-Warshall: O(V²)**
- Distance matrix: O(V²)
- No additional space
- Total: O(V²)

**Explanation:**
Dijkstra uses a priority queue for efficient greedy selection, giving O((V + E) log V) time. Bellman-Ford iterates V-1 times over all edges, giving O(VE) time but handles negative weights. Floyd-Warshall uses dynamic programming with three nested loops, giving O(V³) time for all-pairs shortest paths. Space complexity varies from O(V) for single-source algorithms to O(V²) for all-pairs algorithms.

## Real-world Applications

### 1. GPS Navigation

**Route Planning:**
- Find shortest path between locations
- Consider traffic and road conditions
- Real-time updates
- Example: Google Maps

### 2. Network Routing

**Packet Routing:**
- Find optimal paths for data packets
- Load balancing
- Network optimization
- Example: Internet routing

### 3. Social Network Analysis

**Influence Maximization:**
- Find shortest paths between users
- Degree of separation
- Community detection
- Example: LinkedIn connections

### 4. Delivery Optimization

**Route Planning:**
- Optimize delivery routes
- Minimize travel time/cost
- Multiple stops
- Example: Amazon delivery

### 5. Airline Scheduling

**Network Design:**
- Minimum spanning tree for routes
- Hub and spoke model
- Cost optimization
- Example: Airline networks

### 6. Game AI

**Pathfinding:**
- NPC movement
- Navigation meshes
- Real-time pathfinding
- Example: Strategy games

### 7. Telecommunications

**Network Design:**
- Optimize cable layouts
- Minimize infrastructure cost
- Reliability analysis
- Example: Fiber optic networks

### 8. Resource Allocation

**Flow Optimization:**
- Maximize resource flow
- Bottleneck detection
- Capacity planning
- Example: Supply chain

## Common Mistakes

### 1. Using Dijkstra with Negative Weights

**Mistake:**
```javascript
// Dijkstra doesn't handle negative weights
dijkstra(graph, 'A') // Wrong for negative weights
```

**Correct:**
```javascript
// Use Bellman-Ford for negative weights
bellmanFord(graph, 'A')
```

**Why It Matters:**
- Dijkstra fails with negative weights
- Greedy choice not optimal
- Must use Bellman-Ford

### 2. Not Checking for Negative Cycles

**Mistake:**
```javascript
// Not checking for negative cycles
// May return incorrect results
```

**Correct:**
```javascript
// Always check for negative cycles
// Return error if detected
```

**Why It Matters:**
- Negative cycles cause infinite loops
- No shortest path exists
- Must detect and handle

### 3. Incorrect Priority Queue Usage

**Mistake:**
```javascript
// Not using min-heap correctly
// May extract wrong node
```

**Correct:**
```javascript
// Use proper priority queue
// Extract minimum distance node
```

**Why It Matters:**
- Wrong extraction breaks algorithm
- Dijkstra requires min-heap
- Critical for correctness

### 4. Not Handling Disconnected Graphs

**Mistake:**
```javascript
// Assuming all nodes reachable
// May return infinity for some
```

**Correct:**
```javascript
// Check for infinity
// Handle unreachable nodes
```

**Why It Matters:**
- Some nodes may be unreachable
- Need to handle gracefully
- Return appropriate value

### 5. Forgetting to Initialize Distances

**Mistake:**
```javascript
// Not initializing distances
// May have undefined values
```

**Correct:**
```javascript
// Initialize all to infinity
// Set source to 0
```

**Why It Matters:**
- Uninitialized values cause errors
- Infinity is correct initial value
- Source must be 0

### 6. Wrong Algorithm Choice

**Mistake:**
```javascript
// Using Dijkstra for all-pairs
// Inefficient for dense graphs
```

**Correct:**
```javascript
// Use Floyd-Warshall for all-pairs
// More efficient for dense graphs
```

**Why It Matters:**
- Wrong algorithm is inefficient
- Choose based on problem requirements
- Consider graph density

## Advanced Concepts

### 1. A* Search

**Concept:**
Heuristic-guided shortest path search.

**Features:**
- Uses heuristic function
- Faster than Dijkstra for single target
- Optimal with admissible heuristic

### 2. Minimum Spanning Tree

**Concept:**
Minimum weight spanning tree of graph.

**Features:**
- Kruskal's algorithm (Union Find)
- Prim's algorithm (Priority Queue)
- Network design applications

### 3. Network Flow

**Concept:**
Maximum flow through network.

**Features:**
- Ford-Fulkerson algorithm
- Edmonds-Karp (BFS)
- Resource allocation

### 4. Johnson's Algorithm

**Concept:**
All-pairs shortest paths for sparse graphs.

**Features:**
- Uses Bellman-Ford and Dijkstra
- Faster than Floyd-Warshall for sparse graphs
- Handles negative weights

## Practice Thinking Guide

### How to Identify When to Use Advanced Graph Algorithms

**Key Signals in Problem Statements:**

1. **"Shortest path"**
   - Dijkstra (non-negative)
   - Bellman-Ford (negative)
   - Example: "Find shortest route"

2. **"All-pairs shortest paths"**
   - Floyd-Warshall
   - Example: "Distances between all cities"

3. **"Negative weights"**
   - Bellman-Ford
   - Example: "Profit/loss edges"

4. **"Minimum spanning tree"**
   - Kruskal's/Prim's
   - Example: "Connect with minimum cost"

5. **"K stops" or "K edges"**
   - Modified Bellman-Ford
   - Example: "At most K stops"

6. **"Heuristic" or "estimated"**
   - A* search
   - Example: "Grid with obstacles"

**Pattern Recognition:**

**Pattern 1: Single Source Shortest Path**
```
Problem: Shortest path from source to all nodes
Solution: Dijkstra (non-negative) or Bellman-Ford (negative)
```

**Pattern 2: All-Pairs Shortest Path**
```
Problem: Shortest paths between all pairs
Solution: Floyd-Warshall or Johnson's algorithm
```

**Pattern 3: Constrained Path**
```
Problem: Shortest path with K stops
Solution: Modified Bellman-Ford with K iterations
```

**Pattern 4: Minimum Spanning Tree**
```
Problem: Connect all nodes with minimum cost
Solution: Kruskal's (Union Find) or Prim's (Priority Queue)
```

**Pattern 5: Heuristic Search**
```
Problem: Find path to target efficiently
Solution: A* with heuristic function
```

**Decision Flowchart:**

```
Weighted graph problem?
├─ Yes → Single source?
│        ├─ Yes → Non-negative weights? → Dijkstra
│        │        └─ Negative weights? → Bellman-Ford
│        └─ No → All-pairs? → Floyd-Warshall
├─ No → MST problem?
│        ├─ Yes → Kruskal's/Prim's
│        └─ No → Consider other
└─ No → Not advanced graph problem
```

**Example Problem Analysis:**

**Problem:** "Network delay time - time for signal to reach all nodes"

**Analysis:**
1. Need shortest path from source to all nodes
2. Non-negative edge weights (time)
3. Single source, multiple targets
4. Dijkstra's algorithm perfect
5. Solution: Dijkstra from source

**Problem:** "Cheapest flights within K stops"

**Analysis:**
1. Need shortest path with constraint
2. Maximum K stops allowed
3. Modified Bellman-Ford
4. Limit iterations to K+1
5. Solution: Bellman-Ford with K+1 iterations

**Problem:** "Find minimum cost to connect all cities"

**Analysis:**
1. Need to connect all nodes
2. Minimum total cost
3. Minimum spanning tree problem
4. Kruskal's or Prim's algorithm
5. Solution: Kruskal's with Union Find

## Summary

Advanced graph algorithms solve complex optimization problems on weighted graphs. Dijkstra's algorithm finds shortest paths with non-negative weights using a greedy approach with a priority queue. Bellman-Ford handles negative edge weights and detects negative cycles through iterative relaxation. Floyd-Warshall computes all-pairs shortest paths using dynamic programming. These algorithms are essential for navigation systems, network routing, social network analysis, and resource allocation.

**Key Takeaways:**
- Dijkstra for non-negative weights, single source
- Bellman-Ford for negative weights, cycle detection
- Floyd-Warshall for all-pairs shortest paths
- A* for heuristic-guided search
- Relaxation is core operation
- Choose algorithm based on constraints
- Consider graph density and weights
- Essential for optimization problems

**Mastery Checklist:**
- ✅ Understand relaxation concept
- ✅ Implement Dijkstra's algorithm
- ✅ Implement Bellman-Ford algorithm
- ✅ Implement Floyd-Warshall algorithm
- ✅ Handle negative weights and cycles
- ✅ Choose appropriate algorithm
- ✅ Understand time/space complexity
- ✅ Know real-world applications
