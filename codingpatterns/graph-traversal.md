# Graph Traversal

Graph traversal is the process of visiting all vertices and edges of a graph systematically. The two main approaches are Breadth-First Search (BFS) and Depth-First Search (DFS), each with different characteristics.

## Introduction

Graph traversal is the process of visiting all vertices and edges of a graph in a systematic way. The two fundamental traversal algorithms are Breadth-First Search (BFS) and Depth-First Search (DFS). BFS explores neighbors level by level using a queue, while DFS explores as deep as possible along each branch before backtracking using a stack or recursion. Both algorithms are essential for solving graph problems like shortest path, cycle detection, connected components, and topological sorting.

**Why Graph Traversal Exists:**
- Systematic exploration of graph structures
- Foundation for all graph algorithms
- Essential for pathfinding and connectivity
- Used in social networks, web crawling, and more
- Basis for advanced algorithms (Dijkstra, A*, etc.)

**Where It Is Used:**
- Social network analysis (friend recommendations)
- Web crawling and search engines
- Network routing and topology
- Dependency management (package managers)
- Game AI and pathfinding
- Recommendation systems
- Social media features
- Database query optimization

## Core Concept Explanation

Graph traversal works by systematically visiting each vertex and edge of a graph. The key challenge is avoiding cycles (revisiting nodes) and ensuring all nodes are visited. This is achieved using a visited set to track visited nodes. BFS uses a queue to explore nodes level by level, guaranteeing the shortest path in unweighted graphs. DFS uses a stack (or recursion) to explore as deep as possible before backtracking, which is useful for exploration and pathfinding.

**Step-by-Step Breakdown:**
1. Start from a given vertex
2. Mark the starting vertex as visited
3. Add it to the data structure (queue for BFS, stack for DFS)
4. While the data structure is not empty:
   - Remove a vertex from the data structure
   - Process the vertex
   - For each unvisited neighbor:
     - Mark as visited
     - Add to data structure
5. Repeat until all reachable vertices are visited

**Intuition Behind the Concept:**
Think of graph traversal like exploring a maze. BFS is like exploring the maze level by level - you check all paths at your current depth before going deeper. This guarantees you find the shortest path. DFS is like following a path as far as you can until you hit a dead end, then backtracking and trying another path. This is useful for exploring all possible paths.

**Visual Thinking:**
```
Graph Structure:
    A
   / \
  B   C
 / \   \
D   E   F

BFS Traversal (Level by Level):
Level 0: A
Level 1: B, C
Level 2: D, E, F
Order: A → B → C → D → E → F

DFS Traversal (Deep First):
Path: A → B → D (backtrack) → E (backtrack) → C → F
Order: A → B → D → E → C → F
```

## Internal Working / Logic

Graph traversal operates through a systematic process of visiting nodes using either a queue (BFS) or stack (DFS). The visited set is critical to avoid infinite loops in cyclic graphs.

**Operation 1: BFS (Breadth-First Search)**
- Uses a queue (FIFO)
- Explores level by level
- Guarantees shortest path in unweighted graphs
- Uses more memory (stores entire level)

**Operation 2: DFS (Depth-First Search)**
- Uses a stack (LIFO) or recursion
- Explores deep first
- Uses less memory (stores only current path)
- Can cause stack overflow with deep recursion

**Operation 3: Visited Set**
- Tracks visited nodes
- Prevents infinite loops
- Essential for cyclic graphs
- O(1) lookup time

**Flow Explanation (BFS):**
1. Initialize queue with start node
2. Mark start node as visited
3. While queue is not empty:
   - Dequeue front node
   - Process node
   - For each unvisited neighbor:
     - Mark as visited
     - Enqueue neighbor

**Decision Making Logic:**
The key decision is BFS vs DFS:
- Use BFS for shortest path in unweighted graphs
- Use BFS for level-order traversal
- Use DFS for exploration and pathfinding
- Use DFS for topological sorting
- Use DFS for cycle detection
- Consider memory constraints

## Algorithm / Approach

**BFS Algorithm**

```
1. Initialize queue with start node
2. Mark start node as visited
3. While queue is not empty:
   a. Dequeue front node
   b. Process node
   c. For each unvisited neighbor:
      i. Mark as visited
      ii. Enqueue neighbor
```

**DFS Algorithm (Iterative)**

```
1. Initialize stack with start node
2. Mark start node as visited
3. While stack is not empty:
   a. Pop top node
   b. Process node
   c. For each unvisited neighbor:
      i. Mark as visited
      ii. Push neighbor
```

**DFS Algorithm (Recursive)**

```
1. Mark current node as visited
2. Process current node
3. For each unvisited neighbor:
   a. Recursively call DFS
```

**Shortest Path Algorithm (BFS)**

```
1. Initialize queue with [start, distance]
2. Mark start as visited
3. While queue is not empty:
   a. Dequeue [node, distance]
   b. If node is target, return distance
   c. For each unvisited neighbor:
      i. Mark as visited
      ii. Enqueue [neighbor, distance + 1]
```

## Implementations

### 1. BFS (Breadth-First Search)

```javascript
function bfs(graph, start) {
  const visited = new Set();
  const queue = [start];
  visited.add(start);
  const result = [];
  
  while (queue.length > 0) {
    const vertex = queue.shift();
    result.push(vertex);
    
    for (const neighbor of graph[vertex]) {
      if (!visited.has(neighbor)) {
        visited.add(neighbor);
        queue.push(neighbor);
      }
    }
  }
  
  return result;
}
```

**Advantages:**
- Guarantees shortest path in unweighted graphs
- Level-order traversal
- Easy to implement iteratively

### 2. DFS (Recursive)

```javascript
function dfs(graph, start, visited = new Set()) {
  visited.add(start);
  const result = [start];
  
  for (const neighbor of graph[start]) {
    if (!visited.has(neighbor)) {
      result.push(...dfs(graph, neighbor, visited));
    }
  }
  
  return result;
}
```

**Advantages:**
- Simple and elegant
- Natural for recursive problems
- Less memory than BFS

### 3. DFS (Iterative)

```javascript
function dfsIterative(graph, start) {
  const visited = new Set();
  const stack = [start];
  const result = [];
  
  while (stack.length > 0) {
    const vertex = stack.pop();
    
    if (!visited.has(vertex)) {
      visited.add(vertex);
      result.push(vertex);
      
      for (const neighbor of graph[vertex]) {
        if (!visited.has(neighbor)) {
          stack.push(neighbor);
        }
      }
    }
  }
  
  return result;
}
```

**Advantages:**
- Avoids stack overflow
- More control over traversal
- Same memory benefits as recursive DFS

### 4. Shortest Path (BFS)

```javascript
function shortestPath(graph, start, end) {
  const visited = new Set();
  const queue = [[start, 0]];
  visited.add(start);
  
  while (queue.length > 0) {
    const [vertex, distance] = queue.shift();
    
    if (vertex === end) return distance;
    
    for (const neighbor of graph[vertex]) {
      if (!visited.has(neighbor)) {
        visited.add(neighbor);
        queue.push([neighbor, distance + 1]);
      }
    }
  }
  
  return -1;
}
```

**Advantages:**
- Guarantees shortest path
- O(V + E) time
- Works for unweighted graphs

### 5. Cycle Detection (DFS)

```javascript
function hasCycle(graph) {
  const visited = new Set();
  
  function dfs(node, parent) {
    visited.add(node);
    
    for (const neighbor of graph[node]) {
      if (!visited.has(neighbor)) {
        if (dfs(neighbor, node)) return true;
      } else if (neighbor !== parent) {
        return true;
      }
    }
    
    return false;
  }
  
  for (const node in graph) {
    if (!visited.has(node)) {
      if (dfs(node, null)) return true;
    }
  }
  
  return false;
}
```

**Advantages:**
- Detects cycles efficiently
- Works for undirected graphs
- O(V + E) time

### 6. Number of Islands (DFS)

```javascript
function numIslands(grid) {
  if (!grid.length) return 0;
  
  let count = 0;
  const rows = grid.length;
  const cols = grid[0].length;
  
  function dfs(r, c) {
    if (r < 0 || c < 0 || r >= rows || c >= cols || grid[r][c] === '0') {
      return;
    }
    
    grid[r][c] = '0';
    dfs(r + 1, c);
    dfs(r - 1, c);
    dfs(r, c + 1);
    dfs(r, c - 1);
  }
  
  for (let i = 0; i < rows; i++) {
    for (let j = 0; j < cols; j++) {
      if (grid[i][j] === '1') {
        count++;
        dfs(i, j);
      }
    }
  }
  
  return count;
}
```

**Advantages:**
- Counts connected components
- Works on 2D grids
- Flood fill algorithm

## Dry Run

**Example: BFS Traversal**

**Input:**
```
graph = {
  A: ['B', 'C'],
  B: ['A', 'D', 'E'],
  C: ['A', 'F'],
  D: ['B'],
  E: ['B'],
  F: ['C']
}
start = 'A'
```

**Step-by-Step Execution:**

```
Initial State:
visited = {}
queue = ['A']
result = []

Iteration 1:
vertex = 'A'
result = ['A']
neighbors = ['B', 'C']
  'B' not visited → visited.add('B'), queue.push('B')
  'C' not visited → visited.add('C'), queue.push('C')
visited = {A, B, C}
queue = ['B', 'C']

Iteration 2:
vertex = 'B'
result = ['A', 'B']
neighbors = ['A', 'D', 'E']
  'A' visited → skip
  'D' not visited → visited.add('D'), queue.push('D')
  'E' not visited → visited.add('E'), queue.push('E')
visited = {A, B, C, D, E}
queue = ['C', 'D', 'E']

Iteration 3:
vertex = 'C'
result = ['A', 'B', 'C']
neighbors = ['A', 'F']
  'A' visited → skip
  'F' not visited → visited.add('F'), queue.push('F')
visited = {A, B, C, D, E, F}
queue = ['D', 'E', 'F']

Iteration 4:
vertex = 'D'
result = ['A', 'B', 'C', 'D']
neighbors = ['B']
  'B' visited → skip
visited = {A, B, C, D, E, F}
queue = ['E', 'F']

Iteration 5:
vertex = 'E'
result = ['A', 'B', 'C', 'D', 'E']
neighbors = ['B']
  'B' visited → skip
visited = {A, B, C, D, E, F}
queue = ['F']

Iteration 6:
vertex = 'F'
result = ['A', 'B', 'C', 'D', 'E', 'F']
neighbors = ['C']
  'C' visited → skip
visited = {A, B, C, D, E, F}
queue = []

Final: result = ['A', 'B', 'C', 'D', 'E', 'F']
```

**Variable Changes Table:**

| Iteration | vertex | result (after) | visited (after) | queue (after) |
|-----------|--------|----------------|-----------------|---------------|
| 1 | `A` | `[A]` | `{A, B, C}` | `[B, C]` |
| 2 | `B` | `[A, B]` | `{A, B, C, D, E}` | `[C, D, E]` |
| 3 | `C` | `[A, B, C]` | `{A, B, C, D, E, F}` | `[D, E, F]` |
| 4 | `D` | `[A, B, C, D]` | `{A, B, C, D, E, F}` | `[E, F]` |
| 5 | `E` | `[A, B, C, D, E]` | `{A, B, C, D, E, F}` | `[F]` |
| 6 | `F` | `[A, B, C, D, E, F]` | `{A, B, C, D, E, F}` | `[]` |

## Edge Cases

### 1. Empty Graph
```javascript
graph = {}
bfs(graph, 'A') → Error or handle gracefully
Check if graph is empty
```

### 2. Disconnected Graph
```javascript
graph = {A: [B], B: [A], C: [D], D: [C]}
bfs(graph, 'A') → [A, B]
Need to iterate all nodes for full traversal
```

### 3. Self-Loop
```javascript
graph = {A: [A]}
bfs(graph, 'A') → [A]
Visited set prevents infinite loop
```

### 4. Single Node
```javascript
graph = {A: []}
bfs(graph, 'A') → [A]
Only one node, no neighbors
```

### 5. Directed Graph
```javascript
graph = {A: [B], B: []}
bfs(graph, 'A') → [A, B]
bfs(graph, 'B') → [B]
Direction matters
```

### 6. Parallel Edges
```javascript
graph = {A: [B, B], B: [A]}
bfs(graph, 'A') → [A, B]
Visited set handles duplicates
```

**Why Edge Cases Matter:**
- Empty graph needs special handling
- Disconnected graphs need iteration
- Self-loops can cause infinite loops
- Single node is base case
- Direction affects traversal
- Parallel edges handled by visited set

## Variations / Extensions

### 1. Topological Sort (DFS)

```javascript
function topologicalSort(graph) {
  const visited = new Set();
  const result = [];
  
  function dfs(node) {
    visited.add(node);
    
    for (const neighbor of graph[node]) {
      if (!visited.has(neighbor)) {
        dfs(neighbor);
      }
    }
    
    result.push(node);
  }
  
  for (const node in graph) {
    if (!visited.has(node)) {
      dfs(node);
    }
  }
  
  return result.reverse();
}
```

### 2. Connected Components (DFS)

```javascript
function connectedComponents(graph) {
  const visited = new Set();
  const components = [];
  
  function dfs(node, component) {
    visited.add(node);
    component.push(node);
    
    for (const neighbor of graph[node]) {
      if (!visited.has(neighbor)) {
        dfs(neighbor, component);
      }
    }
  }
  
  for (const node in graph) {
    if (!visited.has(node)) {
      const component = [];
      dfs(node, component);
      components.push(component);
    }
  }
  
  return components;
}
```

### 3. Bipartite Graph Check (BFS)

```javascript
function isBipartite(graph) {
  const colors = {};
  
  for (const node in graph) {
    if (!(node in colors)) {
      colors[node] = 0;
      const queue = [node];
      
      while (queue.length > 0) {
        const current = queue.shift();
        
        for (const neighbor of graph[current]) {
          if (!(neighbor in colors)) {
            colors[neighbor] = 1 - colors[current];
            queue.push(neighbor);
          } else if (colors[neighbor] === colors[current]) {
            return false;
          }
        }
      }
    }
  }
  
  return true;
}
```

### 4. Path Reconstruction (BFS)

```javascript
function shortestPathWithNodes(graph, start, end) {
  const visited = new Set();
  const queue = [start];
  const parent = {};
  visited.add(start);
  
  while (queue.length > 0) {
    const vertex = queue.shift();
    
    if (vertex === end) {
      const path = [];
      let current = end;
      while (current !== start) {
        path.unshift(current);
        current = parent[current];
      }
      path.unshift(start);
      return path;
    }
    
    for (const neighbor of graph[vertex]) {
      if (!visited.has(neighbor)) {
        visited.add(neighbor);
        parent[neighbor] = vertex;
        queue.push(neighbor);
      }
    }
  }
  
  return null;
}
```

### 5. Level Order Traversal (BFS)

```javascript
function levelOrder(graph, start) {
  const visited = new Set();
  const queue = [start];
  visited.add(start);
  const result = [];
  
  while (queue.length > 0) {
    const levelSize = queue.length;
    const level = [];
    
    for (let i = 0; i < levelSize; i++) {
      const vertex = queue.shift();
      level.push(vertex);
      
      for (const neighbor of graph[vertex]) {
        if (!visited.has(neighbor)) {
          visited.add(neighbor);
          queue.push(neighbor);
        }
      }
    }
    
    result.push(level);
  }
  
  return result;
}
```

## Optimization Techniques

### 1. Bidirectional BFS

**Search from Both Ends:**
```javascript
// Start BFS from both start and end
// Meet in the middle
// Reduces search space by half
```

### 2. Early Termination

**Stop When Found:**
```javascript
// Terminate as soon as target found
// Don't explore entire graph
// Saves time for specific queries
```

### 3. Adjacency List vs Matrix

**Data Structure Choice:**
```javascript
// Adjacency list: O(V + E) space
// Adjacency matrix: O(V²) space
// List is better for sparse graphs
```

### 4. Trade-offs

**BFS vs DFS:**

| Aspect | BFS | DFS |
|--------|-----|-----|
| Data Structure | Queue | Stack/Recursion |
| Shortest Path | Yes (unweighted) | No |
| Memory | `O(V)` (level) | `O(V)` (path) |
| Use Case | Shortest path | Exploration |
| Best For | Level order | Pathfinding |

**When to Use BFS:**
- Shortest path in unweighted graph
- Level-order traversal
- Social network degrees of separation

**When to Use DFS:**
- Exploration and pathfinding
- Topological sorting
- Cycle detection
- Maze solving

## Complexity Analysis

### Time Complexity

**BFS: O(V + E)**
- V = number of vertices
- E = number of edges
- Visit each vertex once
- Check each edge once

**DFS: O(V + E)**
- V = number of vertices
- E = number of edges
- Visit each vertex once
- Check each edge once

**Shortest Path: O(V + E)**
- Same as BFS
- Additional O(1) for distance tracking
- Guarantees shortest path

### Space Complexity

**BFS: O(V)**
- Store visited set: O(V)
- Store queue: O(V) in worst case
- Total: O(V)

**DFS (Recursive): O(V)**
- Store visited set: O(V)
- Call stack: O(V) in worst case
- Total: O(V)

**DFS (Iterative): O(V)**
- Store visited set: O(V)
- Store stack: O(V) in worst case
- Total: O(V)

**Explanation:**
Both BFS and DFS have O(V + E) time complexity because they visit each vertex once and check each edge once. Space complexity is O(V) for storing the visited set and the data structure (queue or stack). BFS may use more memory in practice because it stores an entire level, while DFS stores only the current path.

## Real-world Applications

### 1. Social Networks

**Friend Recommendations:**
- Find friends of friends
- Degrees of separation
- Suggest connections
- Example: LinkedIn connections

### 2. Web Crawling

**Search Engines:**
- Crawl web pages
- Build search index
- Discover new pages
- Example: Google crawler

### 3. Network Routing

**Path Finding:**
- Find shortest path
- Network topology
- Route packets
- Example: Internet routing

### 4. Recommendation Systems

**Product Recommendations:**
- Similar users
- Collaborative filtering
- Suggest products
- Example: Amazon recommendations

### 5. Game AI

**Pathfinding:**
- NPC movement
- Maze solving
- Strategy games
- Example: Game pathfinding

### 6. Dependency Management

**Package Managers:**
- Resolve dependencies
- Topological sort
- Install order
- Example: npm, pip

### 7. Social Media Features

**Content Discovery:**
- Trending topics
- Feed ranking
- Content suggestions
- Example: Twitter timeline

### 8. Database Query Optimization

**Query Planning:**
- Join order optimization
- Index selection
- Query execution
- Example: SQL optimizer

## Common Mistakes

### 1. Not Using Visited Set

**Mistake:**
```javascript
// Not tracking visited nodes
function bfs(graph, start) {
  const queue = [start];
  // No visited set!
  // Infinite loop in cyclic graphs
}
```

**Correct:**
```javascript
// Always use visited set
function bfs(graph, start) {
  const visited = new Set();
  const queue = [start];
  visited.add(start);
}
```

**Why It Matters:**
- Without visited set, infinite loops
- Cyclic graphs cause problems
- Essential for correctness

### 2. Not Handling Disconnected Graphs

**Mistake:**
```javascript
// Only starting from one node
bfs(graph, 'A')
// Misses disconnected components
```

**Correct:**
```javascript
// Iterate all nodes
for (const node in graph) {
  if (!visited.has(node)) {
    bfs(graph, node);
  }
}
```

**Why It Matters:**
- Disconnected graphs exist
- Need to visit all components
- Complete traversal required

### 3. Stack Overflow in Recursive DFS

**Mistake:**
```javascript
// Deep recursion causes stack overflow
function dfs(graph, node) {
  // Very deep graph
  dfs(graph, neighbor);
}
```

**Correct:**
```javascript
// Use iterative DFS
function dfsIterative(graph, start) {
  const stack = [start];
  // No recursion
}
```

**Why It Matters:**
- Deep graphs cause stack overflow
- Iterative version avoids this
- More robust solution

### 4. Wrong Data Structure

**Mistake:**
```javascript
// Using stack for BFS
const stack = [start]; // Wrong!
// Not level-order
```

**Correct:**
```javascript
// Use queue for BFS
const queue = [start]; // Correct!
// Level-order traversal
```

**Why It Matters:**
- BFS requires queue (FIFO)
- DFS requires stack (LIFO)
- Wrong structure gives wrong order

### 5. Not Reconstructing Path

**Mistake:**
```javascript
// Only finding distance
function shortestPath(graph, start, end) {
  // Returns distance only
  // Doesn't return path
}
```

**Correct:**
```javascript
// Track parent for path reconstruction
function shortestPathWithNodes(graph, start, end) {
  const parent = {};
  // Reconstruct path
}
```

**Why It Matters:**
- Often need actual path
- Distance alone insufficient
- Parent tracking needed

### 6. Not Checking Bounds (Grid)

**Mistake:**
```javascript
// Not checking grid bounds
dfs(r + 1, c) // May go out of bounds
```

**Correct:**
```javascript
// Check bounds before recursion
if (r >= 0 && r < rows && c >= 0 && c < cols) {
  dfs(r + 1, c);
}
```

**Why It Matters:**
- Out of bounds causes errors
- Grid traversal needs bounds check
- Essential for correctness

## Advanced Concepts

### 1. Bidirectional BFS

**Concept:**
Search from both start and end simultaneously.

**Features:**
- Reduces search space
- Faster for large graphs
- Meet in the middle

### 2. A* Search

**Concept:**
Heuristic-guided search for shortest path.

**Features:**
- Uses heuristic function
- Faster than BFS
- Optimal with admissible heuristic

### 3. Dijkstra's Algorithm

**Concept:**
Shortest path in weighted graphs.

**Features:**
- Uses priority queue
- Handles edge weights
- Generalization of BFS

### 4. Topological Sort

**Concept:**
Linear ordering of directed acyclic graph.

**Features:**
- Uses DFS
- Dependency resolution
- Build systems

## Practice Thinking Guide

### How to Identify When to Use Graph Traversal

**Key Signals in Problem Statements:**

1. **"Shortest path"**
   - Unweighted graph → BFS
   - Weighted graph → Dijkstra
   - Example: "Minimum steps"

2. **"Connected components"**
   - Count components
   - Example: "Number of islands"

3. **"Cycle detection"**
   - Check for cycles
   - Example: "Detect cycle in graph"

4. **"Level order"**
   - BFS traversal
   - Example: "Level by level"

5. **"Path finding"**
   - DFS or BFS
   - Example: "Find path between nodes"

6. **"Maze" or "grid"**
   - 2D traversal
   - Example: "Solve maze"

**Pattern Recognition:**

**Pattern 1: Shortest Path**
```
Problem: Find shortest path in unweighted graph
Solution: BFS with distance tracking
```

**Pattern 2: Connected Components**
```
Problem: Count connected components
Solution: DFS/BFS from each unvisited node
```

**Pattern 3: Cycle Detection**
```
Problem: Detect cycle in graph
Solution: DFS with parent tracking
```

**Pattern 4: Topological Sort**
```
Problem: Order tasks with dependencies
Solution: DFS with post-order processing
```

**Pattern 5: Number of Islands**
```
Problem: Count islands in grid
Solution: DFS flood fill
```

**Decision Flowchart:**

```
Involves graph/network?
├─ Yes → Need shortest path?
│        ├─ Yes → Unweighted? → BFS
│        │        └─ Weighted → Dijkstra
│        └─ No → Need level order? → BFS
│                 └─ Need exploration? → DFS
├─ No → Not graph traversal problem
└─ No → Consider other
```

**Example Problem Analysis:**

**Problem:** "Find shortest path in unweighted graph"

**Analysis:**
1. Need shortest path
2. Graph is unweighted
3. BFS guarantees shortest path
4. Track distance during BFS
5. Solution: BFS with distance tracking

**Problem:** "Count number of islands in 2D grid"

**Analysis:**
1. Need to count connected components
2. Grid is 2D array
3. Each '1' is land, '0' is water
4. DFS flood fill to mark visited
5. Solution: DFS from each unvisited '1'

**Problem:** "Detect cycle in undirected graph"

**Analysis:**
1. Need to detect cycles
2. Undirected graph
3. DFS with parent tracking
4. If visited neighbor not parent, cycle exists
5. Solution: DFS with parent parameter

## Summary

Graph traversal is the process of systematically visiting all vertices and edges of a graph. BFS explores level by level using a queue and guarantees the shortest path in unweighted graphs. DFS explores deep first using a stack or recursion and is useful for exploration and pathfinding. Both algorithms are fundamental to solving graph problems and form the basis for more advanced algorithms.

**Key Takeaways:**
- Always use visited set to avoid infinite loops
- BFS for shortest path in unweighted graphs
- DFS for exploration and pathfinding
- Handle disconnected graphs by iterating all nodes
- BFS uses queue, DFS uses stack/recursion
- Time complexity: O(V + E)
- Space complexity: O(V)
- Foundation for advanced graph algorithms

**Mastery Checklist:**
- ✅ Understand BFS and DFS differences
- ✅ Implement BFS with queue
- ✅ Implement DFS (recursive and iterative)
- ✅ Always use visited set
- ✅ Handle disconnected graphs
- ✅ Find shortest path with BFS
- ✅ Detect cycles with DFS
- ✅ Choose BFS vs DFS appropriately

