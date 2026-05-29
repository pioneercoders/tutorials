# Union Find (Disjoint Set Union)

Union Find (Disjoint Set Union) is a data structure that tracks elements partitioned into disjoint sets. It supports efficient union and find operations.

## Introduction

Union Find, also known as Disjoint Set Union (DSU), is a data structure that tracks a partition of elements into disjoint (non-overlapping) sets. It supports two primary operations: find (determine which set an element belongs to) and union (merge two sets). With optimizations like path compression and union by rank, these operations achieve near O(1) time complexity, making Union Find extremely efficient for dynamic connectivity problems. It's widely used in social networks, clustering algorithms, and graph algorithms like Kruskal's minimum spanning tree.

**Why Union Find Exists:**
- Need to efficiently manage dynamic connectivity
- Naive approaches require O(n) per operation
- Union Find provides near O(1) with optimizations
- Essential for connected components and clustering
- Foundation for many graph algorithms

**Where It Is Used:**
- Social network connectivity (friend groups)
- Image segmentation (pixel grouping)
- Clustering algorithms (grouping similar items)
- Kruskal's algorithm for minimum spanning tree
- Dynamic connectivity queries
- Percolation theory
- Network analysis
- Game development (connected regions)

## Core Concept Explanation

Union Find maintains a collection of disjoint sets where each set has a representative (root) element. The find operation returns the representative of the set containing a given element. The union operation merges two sets by attaching one root to another. Without optimizations, these operations can be O(n) in the worst case. However, with path compression (flattening the tree during find) and union by rank (attaching smaller tree to larger), the amortized time complexity becomes O(α(n)), where α is the inverse Ackermann function, which grows extremely slowly and is effectively constant for all practical purposes.

**Step-by-Step Breakdown:**
1. Initialize each element as its own parent (each element is its own set)
2. For find operation:
   - Follow parent pointers until reaching root
   - Apply path compression (update parent pointers to point directly to root)
   - Return root
3. For union operation:
   - Find roots of both elements
   - If roots are same, already in same set
   - If roots are different, attach one root to another using union by rank
   - Decrement component count

**Intuition Behind the Concept:**
Think of Union Find like managing friend groups in a social network. Each person starts in their own group. When two people become friends, their groups merge. To check if two people are in the same group, you follow the "friend chain" to find the group leader. Path compression is like everyone directly knowing the group leader instead of going through intermediaries. Union by rank is like always merging the smaller group into the larger group to keep the chain short.

**Visual Thinking:**
```
Initial State (5 elements):
parent = [0, 1, 2, 3, 4]
rank = [0, 0, 0, 0, 0]
Each element is its own set

After union(0, 1):
parent = [0, 0, 2, 3, 4]
rank = [1, 0, 0, 0, 0]
Sets: {0,1}, {2}, {3}, {4}

After union(2, 3):
parent = [0, 0, 2, 2, 4]
rank = [1, 0, 1, 0, 0]
Sets: {0,1}, {2,3}, {4}

After union(0, 2):
parent = [0, 0, 0, 2, 4]
rank = [2, 0, 1, 0, 0]
Sets: {0,1,2,3}, {4}

After find(3) with path compression:
parent = [0, 0, 0, 0, 4]
rank = [2, 0, 1, 0, 0]
Element 3 now points directly to root 0
```

## Internal Working / Logic

Union Find operates through a tree structure where each node points to its parent. The root of each tree is the representative of the set. The key operations are find and union, which traverse and modify this tree structure.

**Operation 1: Find**
- Start at given element
- Follow parent pointers until reaching root (element where parent[x] = x)
- Apply path compression: update all visited nodes to point directly to root
- Return root

**Operation 2: Union**
- Find roots of both elements
- If roots are same, elements already in same set, return false
- Apply union by rank: attach smaller tree to larger tree
- If ranks are equal, increment rank of new root
- Decrement component count, return true

**Operation 3: Path Compression**
- During find, update parent pointers
- Flattens the tree structure
- Future find operations become faster
- Achieved recursively or iteratively

**Operation 4: Union by Rank**
- Track rank (approximate tree height)
- Attach smaller tree to larger tree
- Keeps tree balanced
- Prevents degenerate cases

**Flow Explanation (Union with Path Compression):**
1. Find root of first element with path compression
2. Find root of second element with path compression
3. If roots are same, return false (already connected)
4. If rank of first root < rank of second root, swap
5. Attach second root to first root
6. If ranks were equal, increment rank of first root
7. Decrement component count, return true

**Decision Making Logic:**
The key decisions are:
- Use path compression for faster finds
- Use union by rank for balanced trees
- Track component count for connected components
- Handle 1-indexed vs 0-indexed inputs
- Use union by size as alternative to rank

## Algorithm / Approach

**Find Algorithm (with Path Compression)**

```
1. If element is not its own parent:
   a. Recursively find root
   b. Set parent to root (path compression)
2. Return parent (root)
```

**Union Algorithm (with Union by Rank)**

```
1. Find roots of both elements
2. If roots are same, return false
3. If rank of first root < rank of second root, swap
4. Set parent of second root to first root
5. If ranks were equal, increment rank of first root
6. Decrement component count, return true
```

**Connected Components Algorithm**

```
1. Initialize Union Find with n elements
2. For each edge (u, v):
   a. Union u and v
3. Return component count
```

**Cycle Detection Algorithm**

```
1. Initialize Union Find with n elements
2. For each edge (u, v):
   a. If union(u, v) returns false, cycle detected
   b. Return edge
3. No cycle found
```

## Implementations

### 1. Basic Union Find

```javascript
class UnionFind {
  constructor(n) {
    this.parent = Array.from({ length: n }, (_, i) => i);
    this.rank = new Array(n).fill(0);
    this.count = n;
  }
  
  find(x) {
    if (this.parent[x] !== x) {
      this.parent[x] = this.find(this.parent[x]); // Path compression
    }
    return this.parent[x];
  }
  
  union(x, y) {
    const px = this.find(x);
    const py = this.find(y);
    if (px === py) return false;
    
    // Union by rank
    if (this.rank[px] < this.rank[py]) {
      [px, py] = [py, px];
    }
    this.parent[py] = px;
    if (this.rank[px] === this.rank[py]) {
      this.rank[px]++;
    }
    
    this.count--;
    return true;
  }
  
  getCount() {
    return this.count;
  }
}
```

**Advantages:**
- Near O(1) operations with optimizations
- Simple and elegant
- Memory efficient
- Tracks component count

### 2. Number of Provinces

```javascript
function findCircleNum(isConnected) {
  const n = isConnected.length;
  const uf = new UnionFind(n);
  
  for (let i = 0; i < n; i++) {
    for (let j = i + 1; j < n; j++) {
      if (isConnected[i][j]) {
        uf.union(i, j);
      }
    }
  }
  
  return uf.getCount();
}
```

**Advantages:**
- Counts connected components
- Efficient for adjacency matrix
- O(n²) time for matrix processing

### 3. Redundant Connection

```javascript
function findRedundantConnection(edges) {
  const n = edges.length;
  const uf = new UnionFind(n + 1); // 1-indexed
  
  for (const [u, v] of edges) {
    if (!uf.union(u, v)) {
      return [u, v]; // Cycle detected
    }
  }
  
  return [];
}
```

**Advantages:**
- Detects cycles in undirected graph
- Returns the redundant edge
- O(n) time for n edges

### 4. Accounts Merge

```javascript
function accountsMerge(accounts) {
  const emailToId = new Map();
  const uf = new UnionFind(accounts.length);
  
  // Map emails to account IDs and union
  for (let i = 0; i < accounts.length; i++) {
    for (let j = 1; j < accounts[i].length; j++) {
      const email = accounts[i][j];
      if (emailToId.has(email)) {
        uf.union(i, emailToId.get(email));
      } else {
        emailToId.set(email, i);
      }
    }
  }
  
  // Group emails by root
  const idToEmails = new Map();
  for (const [email, id] of emailToId) {
    const root = uf.find(id);
    if (!idToEmails.has(root)) {
      idToEmails.set(root, new Set());
    }
    idToEmails.get(root).add(email);
  }
  
  // Build result
  const result = [];
  for (const [id, emails] of idToEmails) {
    const name = accounts[id][0];
    result.push([name, ...Array.from(emails).sort()]);
  }
  
  return result;
}
```

**Advantages:**
- Merges accounts with common emails
- Efficient for large datasets
- Handles multiple emails per account

### 5. Graph Valid Tree

```javascript
function validTree(n, edges) {
  if (edges.length !== n - 1) return false; // Tree has n-1 edges
  
  const uf = new UnionFind(n);
  
  for (const [u, v] of edges) {
    if (!uf.union(u, v)) {
      return false; // Cycle detected
    }
  }
  
  return uf.getCount() === 1; // Single connected component
}
```

**Advantages:**
- Validates if graph is a tree
- Checks for cycles and connectivity
- O(n) time complexity

## Dry Run

**Example: Union Operations**

**Input:**
```
Operations: union(0, 1), union(1, 2), union(3, 4), union(0, 3)
```

**Step-by-Step Execution:**

```
Initial State:
parent = [0, 1, 2, 3, 4]
rank = [0, 0, 0, 0, 0]
count = 5

Operation 1: union(0, 1)
find(0) = 0, find(1) = 1
rank[0] == rank[1], no swap
parent[1] = 0
rank[0] = 1
parent = [0, 0, 2, 3, 4]
rank = [1, 0, 0, 0, 0]
count = 4

Operation 2: union(1, 2)
find(1) = 0 (path compression: parent[1] = 0)
find(2) = 2
rank[0] > rank[2], no swap
parent[2] = 0
parent = [0, 0, 0, 3, 4]
rank = [1, 0, 0, 0, 0]
count = 3

Operation 3: union(3, 4)
find(3) = 3, find(4) = 4
rank[3] == rank[4], no swap
parent[4] = 3
rank[3] = 1
parent = [0, 0, 0, 3, 3]
rank = [1, 0, 0, 1, 0]
count = 2

Operation 4: union(0, 3)
find(0) = 0, find(3) = 3
rank[0] == rank[3], no swap
parent[3] = 0
rank[0] = 2
parent = [0, 0, 0, 0, 3]
rank = [2, 0, 0, 1, 0]
count = 1

Final: 1 connected component
```

**Variable Changes Table:**

| Operation | parent (after) | rank (after) | count (after) |
|-----------|----------------|--------------|---------------|
| Initial | [0, 1, 2, 3, 4] | [0, 0, 0, 0, 0] | 5 |
| union(0, 1) | [0, 0, 2, 3, 4] | [1, 0, 0, 0, 0] | 4 |
| union(1, 2) | [0, 0, 0, 3, 4] | [1, 0, 0, 0, 0] | 3 |
| union(3, 4) | [0, 0, 0, 3, 3] | [1, 0, 0, 1, 0] | 2 |
| union(0, 3) | [0, 0, 0, 0, 3] | [2, 0, 0, 1, 0] | 1 |

## Edge Cases

### 1. Single Element
```javascript
n = 1
UnionFind(1) → parent = [0], count = 1
Single element is its own component
```

### 2. Already Connected
```javascript
union(0, 1) → true
union(0, 1) → false (already connected)
Handle duplicate unions
```

### 3. Self-Loop
```javascript
union(0, 0) → false (same element)
Self-loops don't change structure
```

### 4. Large Dataset
```javascript
n = 1000000
Union Find handles large datasets efficiently
O(α(n)) per operation
```

### 5. 1-Indexed Input
```javascript
edges = [[1, 2], [2, 3]]
Initialize UnionFind(n + 1) for 1-indexed
Handle offset correctly
```

### 6. Disconnected Graph
```javascript
union(0, 1), union(2, 3)
count = 2 (two components)
Multiple connected components
```

**Why Edge Cases Matter:**
- Single element is base case
- Duplicate unions should return false
- Self-loops don't affect structure
- Large datasets test efficiency
- Indexing errors common
- Disconnected graphs need counting

## Variations / Extensions

### 1. Union by Size

```javascript
class UnionFind {
  constructor(n) {
    this.parent = Array.from({ length: n }, (_, i) => i);
    this.size = new Array(n).fill(1);
    this.count = n;
  }
  
  union(x, y) {
    const px = this.find(x);
    const py = this.find(y);
    if (px === py) return false;
    
    if (this.size[px] < this.size[py]) {
      [px, py] = [py, px];
    }
    this.parent[py] = px;
    this.size[px] += this.size[py];
    this.count--;
    return true;
  }
}
```

### 2. Iterative Path Compression

```javascript
find(x) {
  let root = x;
  while (this.parent[root] !== root) {
    root = this.parent[root];
  }
  
  // Path compression
  while (this.parent[x] !== x) {
    const next = this.parent[x];
    this.parent[x] = root;
    x = next;
  }
  
  return root;
}
```

### 3. Persistent Union Find

```javascript
class PersistentUnionFind {
  constructor(n) {
    this.parent = Array.from({ length: n }, (_, i) => i);
    this.rank = new Array(n).fill(0);
    this.history = [];
  }
  
  union(x, y) {
    this.history.push([...this.parent, ...this.rank]);
    // ... union logic
  }
  
  rollback() {
    const state = this.history.pop();
    this.parent = state.slice(0, this.parent.length);
    this.rank = state.slice(this.parent.length);
  }
}
```

### 4. Number of Islands II

```javascript
function numIslands2(m, n, positions) {
  const uf = new UnionFind(m * n);
  const grid = new Array(m).fill(null).map(() => new Array(n).fill(0));
  let count = 0;
  const result = [];
  const directions = [[0, 1], [1, 0], [0, -1], [-1, 0]];
  
  for (const [x, y] of positions) {
    if (grid[x][y] === 1) {
      result.push(count);
      continue;
    }
    
    grid[x][y] = 1;
    count++;
    const idx = x * n + y;
    
    for (const [dx, dy] of directions) {
      const nx = x + dx;
      const ny = y + dy;
      if (nx >= 0 && nx < m && ny >= 0 && ny < n && grid[nx][ny] === 1) {
        const nidx = nx * n + ny;
        if (uf.union(idx, nidx)) {
          count--;
        }
      }
    }
    
    result.push(count);
  }
  
  return result;
}
```

### 5. Longest Consecutive Sequence

```javascript
function longestConsecutive(nums) {
  const numSet = new Set(nums);
  const uf = new UnionFind(nums.length);
  const numToIdx = new Map();
  
  nums.forEach((num, i) => numToIdx.set(num, i));
  
  for (const num of nums) {
    if (numSet.has(num + 1)) {
      uf.union(numToIdx.get(num), numToIdx.get(num + 1));
    }
  }
  
  const rootCount = new Map();
  for (let i = 0; i < nums.length; i++) {
    const root = uf.find(i);
    rootCount.set(root, (rootCount.get(root) || 0) + 1);
  }
  
  return Math.max(...rootCount.values(), 0);
}
```

## Optimization Techniques

### 1. Path Compression

**Flatten Tree:**
```javascript
// Recursive path compression
find(x) {
  if (this.parent[x] !== x) {
    this.parent[x] = this.find(this.parent[x]);
  }
  return this.parent[x];
}
```

### 2. Union by Rank

**Balance Trees:**
```javascript
// Attach smaller to larger
if (this.rank[px] < this.rank[py]) {
  [px, py] = [py, px];
}
```

### 3. Iterative Find

**Avoid Recursion:**
```javascript
// Iterative path compression
// Avoids stack overflow
// More control
```

### 4. Trade-offs

**Union Find vs DFS/BFS:**

| Aspect | Union Find | DFS/BFS |
|--------|------------|---------|
| Dynamic Updates | Yes | No |
| Time per Query | `O(α(n))` | `O(1)` |
| Setup Time | `O(n)` | `O(1)` |
| Best For | Dynamic connectivity | Static connectivity |

**When to Use Union Find:**
- Dynamic connectivity (edges added over time)
- Need to merge sets
- Connected components with updates
- Kruskal's algorithm

## Complexity Analysis

### Time Complexity

**Find: O(α(n))**
- α is inverse Ackermann function
- Effectively constant for all practical n
- With path compression
- Example: find(5)

**Union: O(α(n))**
- Two find operations
- Constant time union
- With union by rank
- Example: union(3, 5)

**Connected Components: O(n² + nα(n))**
- O(n²) for adjacency matrix
- O(nα(n)) for unions
- Dominated by matrix processing
- Example: findCircleNum

### Space Complexity

**Space: O(n)**
- Parent array: O(n)
- Rank array: O(n)
- Total: O(n)
- Example: UnionFind(n)

**Explanation:**
Union Find achieves O(α(n)) time complexity for both find and union operations, where α is the inverse Ackermann function. This function grows extremely slowly - for all practical values of n (even up to 2^65536), α(n) is less than 5. This makes Union Find effectively constant time. Space complexity is O(n) for storing parent and rank arrays.

## Real-world Applications

### 1. Social Networks

**Friend Groups:**
- Find connected components
- Community detection
- Friend recommendations
- Example: Facebook friend groups

### 2. Image Segmentation

**Computer Vision:**
- Group similar pixels
- Region detection
- Object recognition
- Example: Medical imaging

### 3. Clustering Algorithms

**Machine Learning:**
- Group similar data points
- Hierarchical clustering
- Data analysis
- Example: Customer segmentation

### 4. Network Analysis

**Infrastructure:**
- Connected components
- Network reliability
- Fault tolerance
- Example: Power grid analysis

### 5. Game Development

**Connected Regions:**
- Territory control
- Pathfinding
- Map generation
- Example: Strategy games

### 6. Percolation Theory

**Physics:**
- Fluid flow in porous media
- Connectivity analysis
- Phase transitions
- Example: Material science

### 7. Database Systems

**Query Optimization:**
- Table relationships
- Join optimization
- Dependency tracking
- Example: SQL optimization

### 8. Version Control

**Merge Detection:**
- Code branches
- Conflict detection
- Merge history
- Example: Git operations

## Common Mistakes

### 1. Not Implementing Path Compression

**Mistake:**
```javascript
// No path compression
find(x) {
  while (this.parent[x] !== x) {
    x = this.parent[x];
  }
  return x;
}
```

**Correct:**
```javascript
// With path compression
find(x) {
  if (this.parent[x] !== x) {
    this.parent[x] = this.find(this.parent[x]);
  }
  return this.parent[x];
}
```

**Why It Matters:**
- Without path compression, O(n) worst case
- Path compression makes it O(α(n))
- Critical for performance

### 2. Not Using Union by Rank

**Mistake:**
```javascript
// Always attach first to second
this.parent[px] = py;
```

**Correct:**
```javascript
// Union by rank
if (this.rank[px] < this.rank[py]) {
  [px, py] = [py, px];
}
this.parent[py] = px;
```

**Why It Matters:**
- Without union by rank, trees become unbalanced
- Union by rank keeps trees balanced
- Ensures O(α(n)) complexity

### 3. Off-by-One Errors

**Mistake:**
```javascript
// 1-indexed input, but 0-indexed UF
const uf = new UnionFind(n); // Wrong for 1-indexed
```

**Correct:**
```javascript
// Adjust for 1-indexed
const uf = new UnionFind(n + 1);
```

**Why It Matters:**
- Indexing errors cause bugs
- Common in competitive programming
- Must match input format

### 4. Not Handling Self-Loops

**Mistake:**
```javascript
// Self-loop creates cycle incorrectly
union(0, 0) → true (wrong!)
```

**Correct:**
```javascript
// Check if same element
if (px === py) return false;
```

**Why It Matters:**
- Self-loops don't create cycles
- Must handle edge case
- Critical for correctness

### 5. Forgetting to Decrement Count

**Mistake:**
```javascript
// Not tracking component count
union(x, y) {
  // ... union logic
  // Forgot to decrement count
}
```

**Correct:**
```javascript
// Track component count
union(x, y) {
  // ... union logic
  this.count--;
}
```

**Why It Matters:**
- Component count is useful
- Many problems need it
- Easy to forget

### 6. Not Checking Union Return Value

**Mistake:**
```javascript
// Not checking if union succeeded
uf.union(u, v);
// Don't know if cycle detected
```

**Correct:**
```javascript
// Check return value
if (!uf.union(u, v)) {
  // Cycle detected
}
```

**Why It Matters:**
- Union returns false if already connected
- Important for cycle detection
- Critical for many problems

## Advanced Concepts

### 1. Persistent Union Find

**Concept:**
Version control for Union Find.

**Features:**
- Rollback to previous state
- Time travel queries
- Used in competitive programming

### 2. Dynamic Connectivity

**Concept:**
Handle edge additions and deletions.

**Features:**
- Online queries
- Edge deletions
- More complex algorithms

### 3. Offline Queries

**Concept:**
Process queries in reverse order.

**Features:**
- Handle deletions efficiently
- Process backwards
- Use with persistent UF

### 4. Union Find with Rollback

**Concept:**
Undo union operations.

**Features:**
- Backtracking
- Search with constraints
- Used in optimization

## Practice Thinking Guide

### How to Identify When to Use Union Find

**Key Signals in Problem Statements:**

1. **"Connected components"**
   - Union Find
   - Example: "Number of provinces"

2. **"Dynamic connectivity"**
   - Union Find
   - Example: "Edges added over time"

3. **"Cycle detection"**
   - Union Find
   - Example: "Redundant connection"

4. **"Merge sets"**
   - Union Find
   - Example: "Accounts merge"

5. **"Minimum spanning tree"**
   - Union Find (Kruskal's)
   - Example: "Kruskal's algorithm"

6. **"Group similar items"**
   - Union Find
   - Example: "Clustering"

**Pattern Recognition:**

**Pattern 1: Connected Components**
```
Problem: Count connected components
Solution: Union all edges, return count
```

**Pattern 2: Cycle Detection**
```
Problem: Detect cycle in undirected graph
Solution: Union edges, return false if already connected
```

**Pattern 3: Accounts Merge**
```
Problem: Merge accounts with common emails
Solution: Map emails to IDs, union, group by root
```

**Pattern 4: Graph Valid Tree**
```
Problem: Check if graph is valid tree
Solution: Check n-1 edges, no cycles, single component
```

**Pattern 5: Number of Islands II**
```
Problem: Dynamic island counting
Solution: Union adjacent lands, track count
```

**Decision Flowchart:**

```
Involves connectivity?
├─ Yes → Dynamic (edges added over time)?
│        ├─ Yes → Use Union Find
│        └─ No → Static? → DFS/BFS may suffice
├─ No → Involves merging sets?
│        ├─ Yes → Use Union Find
│        └─ No → Consider other
└─ No → Not Union Find problem
```

**Example Problem Analysis:**

**Problem:** "Number of provinces (connected components in graph)"

**Analysis:**
1. Need to count connected components
2. Adjacency matrix representation
3. Union all connected cities
4. Return component count
5. Solution: Union Find with count tracking

**Problem:** "Redundant connection (find edge that creates cycle)"

**Analysis:**
1. Need to detect cycle in undirected graph
2. Add edges one by one
3. If edge connects already connected nodes, it's redundant
4. Union Find perfect for this
5. Solution: Union edges, return first that fails

**Problem:** "Accounts merge (merge accounts with common emails)"

**Analysis:**
1. Need to merge accounts sharing emails
2. Map emails to account IDs
3. Union accounts with common emails
4. Group emails by root
5. Solution: Union Find with email mapping

## Summary

Union Find is a data structure that tracks elements partitioned into disjoint sets. It supports efficient find and union operations with near O(1) time complexity when optimized with path compression and union by rank. Union Find is essential for dynamic connectivity problems, connected components, cycle detection, and clustering algorithms. It's widely used in social networks, image segmentation, and graph algorithms like Kruskal's minimum spanning tree.

**Key Takeaways:**
- Track disjoint sets with parent pointers
- Find returns set representative
- Union merges two sets
- Path compression flattens tree
- Union by rank balances tree
- O(α(n)) time complexity (effectively constant)
- O(n) space complexity
- Essential for dynamic connectivity

**Mastery Checklist:**
- ✅ Understand disjoint sets concept
- ✅ Implement find with path compression
- ✅ Implement union by rank
- ✅ Track component count
- ✅ Handle 1-indexed inputs
- ✅ Detect cycles
- ✅ Count connected components
- ✅ Know when to use Union Find
