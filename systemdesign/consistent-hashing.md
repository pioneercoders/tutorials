# Consistent Hashing

Consistent hashing is a technique that distributes data across servers in a way that minimizes data movement when servers are added or removed, unlike traditional modulo-based hashing.

## Introduction

Consistent hashing is a technique that distributes data across servers in a way that minimizes data movement when servers are added or removed, unlike traditional modulo-based hashing. In traditional hashing, using `hash(key) % n` where n is the number of servers, adding or removing a server causes almost all keys to be remapped, resulting in massive data movement. Consistent hashing solves this by mapping both servers and data keys to a hash ring, where each server is responsible for a contiguous segment of the ring. When a server is added or removed, only the keys in its adjacent segments need to be remapped, minimizing data movement to O(k/n) where k is the number of keys and n is the number of servers. This technique is essential for distributed caches, load balancers, database sharding, and any system that requires dynamic scaling without massive data redistribution. Popular implementations include Memcached, DynamoDB, Cassandra, and many distributed systems.

**Why Consistent Hashing Matters:**
- Minimizes data movement during scaling
- Enables dynamic server addition/removal
- Reduces cache invalidation overhead
- Improves system availability
- Essential for distributed systems
- Critical for horizontal scaling

**Where It Is Used:**
- Distributed caches (Memcached, Redis)
- Load balancers (Nginx, HAProxy)
- Database sharding (Cassandra, DynamoDB)
- Content delivery networks (CDN)
- Distributed file systems
- Peer-to-peer networks

## Core Concept Explanation

Consistent hashing works by mapping both servers and data keys to points on a circular hash space (the ring). The hash space is typically a large range, such as 0 to `2^32-1`. Each server is assigned one or more points on the ring by hashing the server identifier (or server:replica for virtual nodes). Each data key is also hashed to a point on the ring. The key is assigned to the first server encountered when moving clockwise around the ring from the key's position. When a server is added, it takes over a segment of the ring, and only the keys in that segment need to be remapped. When a server is removed, its segment is taken over by the next server clockwise, and only those keys need to be remapped. This ensures minimal data movement during scaling events. Virtual nodes (multiple hash points per physical server) improve load distribution and reduce hot spots.

**Step-by-Step Breakdown:**
1. Define hash space (e.g., 0 to `2^32-1`)
2. Hash each server to one or more points on the ring
3. Hash each data key to a point on the ring
4. Assign key to first server clockwise from key's position
5. When adding server, only remap keys in its segment
6. When removing server, remap keys to next server clockwise
7. Use virtual nodes for better distribution
8. Monitor ring balance and hot spots

**Intuition Behind the Concept:**
Think of consistent hashing like a circular pizza with servers as slices. Each slice (server) is responsible for a portion of the pizza (data). When you add a new slice, you only need to cut a small portion from an existing slice - you don't need to redistribute the entire pizza. When you remove a slice, the adjacent slice simply expands to cover that portion. This is much more efficient than traditional hashing, which is like rearranging all the toppings every time you add or remove a slice.

**Visual Thinking:**
```
Hash Ring (0 to `2^32-1`):
      0
    /   \
  /       \
 |  Server A |
 |           |
  \       /
    \   /
      `2^32-1`

Keys mapped to ring:
Key1 → Position 100 → Server A
Key2 → Position 500 → Server B
Key3 → Position 900 → Server C

Adding Server D:
Server D → Position 300
Only keys between 200-300 remapped from A to D

Removing Server B:
Keys between 400-600 remapped from B to C
```

## Internal Working / Logic

Consistent hashing operates by maintaining a sorted list of hash values representing server positions on the ring. When a key needs to be assigned, the key is hashed and the algorithm finds the first server position that is greater than or equal to the key's hash value (wrapping around if necessary). This is typically done using binary search for O(log n) lookup time. Each server can have multiple virtual nodes (replicas) to improve load distribution - these are created by hashing the server ID with different suffixes (e.g., "server1:0", "server1:1", "server1:2"). When a server is added, only the keys between the new server's position and the next server's position need to be remapped. When a server is removed, its keys are remapped to the next server clockwise. The ring can also support replication by assigning each key to N consecutive servers for redundancy.

**Operation 1: Add Server**
- Hash server ID to get position on ring
- For virtual nodes, hash server:replica for each replica
- Insert server positions into sorted ring
- Find segment that new server will handle
- Remap keys in that segment from previous server
- Update ring structure

**Operation 2: Remove Server**
- Find server positions on ring
- Remove server positions from ring
- Find keys assigned to removed server
- Remap keys to next server clockwise
- Update ring structure

**Operation 3: Get Server for Key**
- Hash the key to get position on ring
- Binary search for first server position >= key position
- If no position found, wrap to first server (ring is circular)
- Return the server at that position
- For replication, return N consecutive servers

**Operation 4: Virtual Node Management**
- Create multiple hash points per physical server
- Distribute virtual nodes evenly around ring
- Improves load distribution
- Reduces hot spots
- Each virtual node treated as independent server

**Flow Explanation (Get Server for Key):**
1. Client requests to store/retrieve key
2. Hash the key to get position on ring
3. Binary search ring for first server position >= key position
4. If found, return that server
5. If not found (key position > all server positions), wrap to first server
6. Return server to client
7. Client stores/retrieves data from that server

**Decision Making Logic:**
The key decisions are:
- How many virtual nodes per server (trade-off between distribution and overhead)
- Hash function choice (uniformity, speed)
- Replication factor (redundancy vs cost)
- How to handle server failures (failover strategy)
- How to rebalance ring (automatic vs manual)
- How to monitor ring health (hot spot detection)

## Algorithm / Approach

**Consistent Hashing Algorithm**

```
1. Define hash space (0 to `2^32-1`)
2. Hash each server to position on ring
3. For virtual nodes, hash server:replica for each replica
4. Sort server positions
5. For each key:
   a. Hash key to position on ring
   b. Find first server position >= key position
   c. If none, wrap to first server
   d. Assign key to that server
```

**Add Server Algorithm**

```
1. Hash server to position(s) on ring
2. Insert position(s) into sorted ring
3. Find keys in new server's segment
4. Remap those keys to new server
5. Update ring structure
```

**Remove Server Algorithm**

```
1. Find server position(s) on ring
2. Remove position(s) from ring
3. Find keys assigned to removed server
4. Remap keys to next server clockwise
5. Update ring structure
```

**Virtual Node Algorithm**

```
1. For each physical server:
   a. Create N virtual nodes
   b. Hash server:i for i in 0..N-1
   c. Insert all virtual node positions into ring
2. Treat each virtual node as independent server
3. Map keys to virtual nodes
4. Virtual nodes map to same physical server
```

## Implementations

### 1. Basic Consistent Hashing

```javascript
class ConsistentHash {
  constructor(replicas = 3) {
    this.replicas = replicas;
    this.ring = new Map();
    this.sortedKeys = [];
  }
  
  _hash(key) {
    let hash = 0;
    for (let i = 0; i < key.length; i++) {
      hash = ((hash << 5) - hash) + key.charCodeAt(i);
      hash |= 0;
    }
    return Math.abs(hash);
  }
  
  addServer(server) {
    for (let i = 0; i < this.replicas; i++) {
      const key = this._hash(`${server}:${i}`);
      this.ring.set(key, server);
      this._insertSorted(key);
    }
  }
  
  removeServer(server) {
    for (let i = 0; i < this.replicas; i++) {
      const key = this._hash(`${server}:${i}`);
      this.ring.delete(key);
      this._removeSorted(key);
    }
  }
  
  getServer(key) {
    if (this.sortedKeys.length === 0) return null;
    const hashValue = this._hash(key);
    const index = this._findIndex(hashValue);
    return this.ring.get(this.sortedKeys[index]);
  }
  
  _insertSorted(key) {
    let left = 0, right = this.sortedKeys.length;
    while (left < right) {
      const mid = Math.floor((left + right) / 2);
      if (this.sortedKeys[mid] < key) left = mid + 1;
      else right = mid;
    }
    this.sortedKeys.splice(left, 0, key);
  }
  
  _findIndex(hashValue) {
    let left = 0, right = this.sortedKeys.length;
    while (left < right) {
      const mid = Math.floor((left + right) / 2);
      if (this.sortedKeys[mid] <= hashValue) left = mid + 1;
      else right = mid;
    }
    return left % this.sortedKeys.length;
  }
  
  _removeSorted(key) {
    const index = this.sortedKeys.indexOf(key);
    if (index > -1) {
      this.sortedKeys.splice(index, 1);
    }
  }
}

// Usage
const ch = new ConsistentHash(3);
ch.addServer('server1');
ch.addServer('server2');
ch.addServer('server3');

console.log(ch.getServer('user123')); // server1
console.log(ch.getServer('product456')); // server2
```

**Advantages:**
- Minimal data movement on scaling
- O(log n) lookup time
- Simple implementation
- Works with any hash function

### 2. Consistent Hashing with Replication

```javascript
class ConsistentHashWithReplication {
  constructor(replicas = 3, replicationFactor = 2) {
    this.replicas = replicas;
    this.replicationFactor = replicationFactor;
    this.ring = new Map();
    this.sortedKeys = [];
  }
  
  _hash(key) {
    let hash = 0;
    for (let i = 0; i < key.length; i++) {
      hash = ((hash << 5) - hash) + key.charCodeAt(i);
      hash |= 0;
    }
    return Math.abs(hash);
  }
  
  addServer(server) {
    for (let i = 0; i < this.replicas; i++) {
      const key = this._hash(`${server}:${i}`);
      this.ring.set(key, server);
      this._insertSorted(key);
    }
  }
  
  getServers(key) {
    if (this.sortedKeys.length === 0) return [];
    const hashValue = this._hash(key);
    const index = this._findIndex(hashValue);
    const servers = [];
    
    for (let i = 0; i < this.replicationFactor; i++) {
      const idx = (index + i) % this.sortedKeys.length;
      const server = this.ring.get(this.sortedKeys[idx]);
      if (!servers.includes(server)) {
        servers.push(server);
      }
    }
    
    return servers;
  }
  
  _insertSorted(key) {
    let left = 0, right = this.sortedKeys.length;
    while (left < right) {
      const mid = Math.floor((left + right) / 2);
      if (this.sortedKeys[mid] < key) left = mid + 1;
      else right = mid;
    }
    this.sortedKeys.splice(left, 0, key);
  }
  
  _findIndex(hashValue) {
    let left = 0, right = this.sortedKeys.length;
    while (left < right) {
      const mid = Math.floor((left + right) / 2);
      if (this.sortedKeys[mid] <= hashValue) left = mid + 1;
      else right = mid;
    }
    return left % this.sortedKeys.length;
  }
}

// Usage
const ch = new ConsistentHashWithReplication(3, 2);
ch.addServer('server1');
ch.addServer('server2');
ch.addServer('server3');

console.log(ch.getServers('user123')); // ['server1', 'server2']
```

**Advantages:**
- Data redundancy
- High availability
- Fault tolerance
- Automatic failover

### 3. Weighted Consistent Hashing

```javascript
class WeightedConsistentHash {
  constructor() {
    this.ring = new Map();
    this.sortedKeys = [];
  }
  
  _hash(key) {
    let hash = 0;
    for (let i = 0; i < key.length; i++) {
      hash = ((hash << 5) - hash) + key.charCodeAt(i);
      hash |= 0;
    }
    return Math.abs(hash);
  }
  
  addServer(server, weight) {
    // Create virtual nodes based on weight
    const virtualNodes = weight * 10; // Scale factor
    for (let i = 0; i < virtualNodes; i++) {
      const key = this._hash(`${server}:${i}`);
      this.ring.set(key, server);
      this._insertSorted(key);
    }
  }
  
  removeServer(server) {
    // Remove all virtual nodes for this server
    const keysToRemove = [];
    for (const [key, srv] of this.ring) {
      if (srv === server) {
        keysToRemove.push(key);
      }
    }
    
    for (const key of keysToRemove) {
      this.ring.delete(key);
      this._removeSorted(key);
    }
  }
  
  getServer(key) {
    if (this.sortedKeys.length === 0) return null;
    const hashValue = this._hash(key);
    const index = this._findIndex(hashValue);
    return this.ring.get(this.sortedKeys[index]);
  }
  
  _insertSorted(key) {
    let left = 0, right = this.sortedKeys.length;
    while (left < right) {
      const mid = Math.floor((left + right) / 2);
      if (this.sortedKeys[mid] < key) left = mid + 1;
      else right = mid;
    }
    this.sortedKeys.splice(left, 0, key);
  }
  
  _findIndex(hashValue) {
    let left = 0, right = this.sortedKeys.length;
    while (left < right) {
      const mid = Math.floor((left + right) / 2);
      if (this.sortedKeys[mid] <= hashValue) left = mid + 1;
      else right = mid;
    }
    return left % this.sortedKeys.length;
  }
  
  _removeSorted(key) {
    const index = this.sortedKeys.indexOf(key);
    if (index > -1) {
      this.sortedKeys.splice(index, 1);
    }
  }
}

// Usage
const wch = new WeightedConsistentHash();
wch.addServer('server1', 3); // Weight 3
wch.addServer('server2', 1); // Weight 1
wch.addServer('server3', 2); // Weight 2

console.log(wch.getServer('user123')); // More likely to be server1
```

**Advantages:**
- Handles heterogeneous servers
- Proportional load distribution
- Better resource utilization
- Flexible scaling

### 4. Consistent Hashing with MD5

```javascript
const crypto = require('crypto');

class MD5ConsistentHash {
  constructor(replicas = 3) {
    this.replicas = replicas;
    this.ring = new Map();
    this.sortedKeys = [];
  }
  
  _hash(key) {
    const md5 = crypto.createHash('md5');
    md5.update(key);
    const hash = md5.digest('hex');
    // Convert to integer
    return parseInt(hash.substring(0, 8), 16);
  }
  
  addServer(server) {
    for (let i = 0; i < this.replicas; i++) {
      const key = this._hash(`${server}:${i}`);
      this.ring.set(key, server);
      this._insertSorted(key);
    }
  }
  
  removeServer(server) {
    for (let i = 0; i < this.replicas; i++) {
      const key = this._hash(`${server}:${i}`);
      this.ring.delete(key);
      this._removeSorted(key);
    }
  }
  
  getServer(key) {
    if (this.sortedKeys.length === 0) return null;
    const hashValue = this._hash(key);
    const index = this._findIndex(hashValue);
    return this.ring.get(this.sortedKeys[index]);
  }
  
  _insertSorted(key) {
    let left = 0, right = this.sortedKeys.length;
    while (left < right) {
      const mid = Math.floor((left + right) / 2);
      if (this.sortedKeys[mid] < key) left = mid + 1;
      else right = mid;
    }
    this.sortedKeys.splice(left, 0, key);
  }
  
  _findIndex(hashValue) {
    let left = 0, right = this.sortedKeys.length;
    while (left < right) {
      const mid = Math.floor((left + right) / 2);
      if (this.sortedKeys[mid] <= hashValue) left = mid + 1;
      else right = mid;
    }
    return left % this.sortedKeys.length;
  }
  
  _removeSorted(key) {
    const index = this.sortedKeys.indexOf(key);
    if (index > -1) {
      this.sortedKeys.splice(index, 1);
    }
  }
}

// Usage
const md5ch = new MD5ConsistentHash(3);
md5ch.addServer('server1');
md5ch.addServer('server2');
md5ch.addServer('server3');

console.log(md5ch.getServer('user123')); // server1
```

**Advantages:**
- Better hash distribution
- Cryptographically secure
- Reduces collisions
- Industry standard

### 5. Consistent Hashing with Jump Consistent Hash

```javascript
class JumpConsistentHash {
  constructor() {
    this.servers = [];
  }
  
  addServer(server) {
    this.servers.push(server);
  }
  
  removeServer(server) {
    const index = this.servers.indexOf(server);
    if (index > -1) {
      this.servers.splice(index, 1);
    }
  }
  
  getServer(key) {
    if (this.servers.length === 0) return null;
    
    let hash = this._hash(key);
    const n = this.servers.length;
    let b = -1;
    let j = 0;
    
    while (j < n) {
      b = j;
      hash = hash * 2862933555777941757 + 1;
      j = Math.floor((b + 1) * ((1 << 31) / ((hash >>> 33) + 1)));
    }
    
    return this.servers[b];
  }
  
  _hash(key) {
    let hash = 0;
    for (let i = 0; i < key.length; i++) {
      hash = ((hash << 5) - hash) + key.charCodeAt(i);
      hash |= 0;
    }
    return Math.abs(hash);
  }
}

// Usage
const jch = new JumpConsistentHash();
jch.addServer('server1');
jch.addServer('server2');
jch.addServer('server3');

console.log(jch.getServer('user123')); // server1
```

**Advantages:**
- No memory overhead
- O(1) lookup time
- No need to maintain ring
- Better distribution

## Dry Run

**Example: Adding a Server**

**Initial State:**
```
Ring with 3 servers:
Server A at position 100
Server B at position 500
Server C at position 900

Keys:
Key1 (position 200) → Server B
Key2 (position 600) → Server C
Key3 (position 50) → Server A (wrap around)
```

**Add Server D at position 300:**

**Step-by-Step Execution:**

```
1. Hash Server D to position 300
2. Insert Server D into ring
3. Find segment: Server B (500) to Server D (300)
4. Remap keys between 200-300 from B to D
5. Key1 (position 200) now → Server D
6. Key2 (position 600) still → Server C
7. Key3 (position 50) still → Server A
8. Only 1 key remapped (1/3 = 33%)
```

**Request/Response Table:**

| Step | Component | Action | Status |
|------|-----------|--------|--------|
| 1 | System | Hash Server D | Position 300 |
| 2 | Ring | Insert Server D | - |
| 3 | System | Find segment | 200-300 |
| 4 | System | Remap Key1 | B → D |
| 5 | Key1 | New assignment | Server D |
| 6 | Key2 | No change | Server C |
| 7 | Key3 | No change | Server A |
| 8 | System | Complete | 33% remapped |

## Edge Cases

### 1. Server Failure
```javascript
// Server goes down unexpectedly
// Keys need remapping
// Failover to next server
```

### 2. Uneven Distribution
```javascript
// Some servers get more keys
// Hot spots develop
// Solution: More virtual nodes
```

### 3. Ring Imbalance
```javascript
// Servers not evenly distributed
// Some segments larger
// Solution: Add virtual nodes
```

### 4. Hash Collisions
```javascript
// Two keys hash to same position
// Need collision resolution
// Solution: Better hash function
```

### 5. Small Number of Servers
```javascript
// Few servers = uneven distribution
// High variance in load
// Solution: More virtual nodes
```

### 6. Rapid Scaling
```javascript
// Frequent add/remove operations
// Continuous remapping
// Solution: Batch operations
```

**Why Edge Cases Matter:**
- Server failures are common
- Uneven distribution causes hot spots
- Ring imbalance affects performance
- Hash collisions cause incorrect routing
- Small server count worsens distribution
- Rapid scaling causes instability

## Variations / Extensions

### 1. Rendezvous Hashing

```javascript
// Hash (server, key) pairs
// Choose server with highest hash
- No ring needed
```

### 2. Maglev Hashing

```javascript
// Google's consistent hashing
- Better distribution
- Faster lookup
```

### 3. HRW (Highest Random Weight)

```javascript
// Hash with weights
- Weighted distribution
- No ring needed
```

### 4. Consistent Hashing with Bounded Loads

```javascript
// Limit per-server load
- Prevent hot spots
- Better balance
```

### 5. Consistent Hashing with Partitioning

```javascript
// Partition ring into segments
- Each server owns segment
- Easier management
```

## Optimization Techniques

### 1. Virtual Node Tuning

**Optimize Virtual Node Count:**
```javascript
// More virtual nodes = better distribution
// Higher memory overhead
// Find optimal balance
```

### 2. Hash Function Selection

**Choose Appropriate Hash:**
```javascript
// MD5, SHA-1, MurmurHash
- Better distribution
- Faster computation
```

### 3. Binary Search Optimization

**Use Efficient Search:**
```javascript
// Binary search for O(log n)
- Faster lookup
- Better performance
```

### 4. Caching

**Cache Server Assignments:**
```javascript
// Cache frequently accessed keys
- Reduce computation
- Faster response
```

### 5. Trade-offs

**Hashing Algorithms Comparison:**

| Algorithm | Distribution | Memory | Lookup Time | Use Case |
|-----------|--------------|--------|-------------|----------|
| Consistent Hashing | Good | `O(n)` | `O(log n)` | General purpose |
| Jump Consistent Hash | Excellent | `O(1)` | `O(1)` | Large scale |
| Rendezvous Hashing | Excellent | `O(n)` | `O(n)` | Small scale |
| Maglev Hashing | Excellent | `O(n)` | `O(1)` | High performance |

**When to Use Each:**
- Consistent Hashing: General purpose, moderate scale
- Jump Consistent Hash: Large scale, memory constrained
- Rendezvous Hashing: Small scale, simple
- Maglev Hashing: High performance, load balancing

## Complexity Analysis

### Time Complexity

**Add Server: O(n)**
- n = number of virtual nodes
- Hash each virtual node
- Insert into sorted array

**Remove Server: O(n)**
- n = number of virtual nodes
- Find and remove each virtual node

**Get Server: O(log n)**
- Binary search on sorted array
- n = number of virtual nodes

**Jump Consistent Hash: O(1)**
- Constant time lookup
- No ring maintenance

### Space Complexity

**Ring Storage: O(n)**
- n = number of virtual nodes
- Each node stores server reference
- Sorted array of hash values

**Explanation:**
Consistent hashing has O(n) space complexity where n is the number of virtual nodes. Time complexity for add/remove is O(n) due to hashing and inserting/removing virtual nodes. Lookup is O(log n) with binary search. Jump consistent hash achieves O(1) lookup and O(1) space by avoiding the ring entirely. The trade-off is between distribution quality and performance.

## Real-world Applications

### 1. Distributed Caches

**Memcached:**
- Client-side consistent hashing
- Server addition/removal
- Example: Session storage

### 2. Databases

**Cassandra:**
- Token-based partitioning
- Virtual nodes (vnodes)
- Example: Distributed database

### 3. Load Balancers

**Nginx:**
- Consistent hashing module
- Session persistence
- Example: Web server load balancing

### 4. Content Delivery

**CDN:**
- Edge server selection
- Content distribution
- Example: Video streaming

### 5. Distributed File Systems

**Dynamo:**
- Partitioning
- Replication
- Example: Amazon Dynamo

### 6. Peer-to-Peer Networks

**DHT:**
- Node lookup
- Data routing
- Example: BitTorrent

### 7. Message Queues

**Kafka:**
- Partition selection
- Consumer assignment
- Example: Event streaming

### 8. Microservices

**Service Discovery:**
- Instance selection
- Request routing
- Example: gRPC load balancing

## Common Mistakes

### 1. Too Few Virtual Nodes

**Mistake:**
```javascript
// Only 1 virtual node per server
// Uneven distribution
// Hot spots
```

**Correct:**
```javascript
// Use 100-1000 virtual nodes per server
// Better distribution
// Reduce hot spots
```

**Why It Matters:**
- Few virtual nodes = poor distribution
- Hot spots overload servers
- Better distribution = better performance

### 2. Poor Hash Function

**Mistake:**
```javascript
// Simple hash function
// Poor distribution
// Many collisions
```

**Correct:**
```javascript
// Use cryptographic hash (MD5, SHA-1)
// Better distribution
// Fewer collisions
```

**Why It Matters:**
- Poor hash = poor distribution
- Collisions cause incorrect routing
- Better hash = better performance

### 3. No Replication

**Mistake:**
```javascript
// Single server per key
// No redundancy
- Data loss on failure
```

**Correct:**
```javascript
// Replicate to N servers
- High availability
// Fault tolerance
```

**Why It Matters:**
- No replication = single point of failure
- Data loss unacceptable
- Replication ensures availability

### 4. Ignoring Server Weights

**Mistake:**
```javascript
// All servers treated equally
// Heterogeneous servers
// Uneven load
```

**Correct:**
```javascript
// Use weighted consistent hashing
// Proportional load distribution
- Better resource utilization
```

**Why It Matters:**
- Heterogeneous servers need different weights
- Equal weights = uneven load
- Weighted hashing = better balance

### 5. No Monitoring

**Mistake:**
```javascript
// No ring monitoring
// Don't detect hot spots
// Can't optimize
```

**Correct:**
```javascript
// Monitor ring balance
// Track key distribution
// Set up alerts
```

**Why It Matters:**
- Hot spots degrade performance
- Monitoring enables optimization
- Alerts catch issues early

### 6. Using Modulo Hashing

**Mistake:**
```javascript
// Use hash(key) % n
// Massive remapping on scale
// Poor performance
```

**Correct:**
```javascript
// Use consistent hashing
// Minimal remapping
- Better scaling
```

**Why It Matters:**
- Modulo hashing causes massive remapping
- Consistent hashing minimizes movement
- Better scaling performance

## Advanced Concepts

### 1. Maglev Hashing

**Concept:**
Google's consistent hashing algorithm.

**Features:**
- Better distribution
- O(1) lookup
- Fast assignment

### 2. Rendezvous Hashing

**Concept:**
Hash server-key pairs, choose highest.

**Features:**
- No ring needed
- Excellent distribution
- Simple implementation

### 3. Bounded Loads

**Concept:**
Limit per-server load.

**Features:**
- Prevent hot spots
- Better balance
- Load-aware routing

### 4. Consistent Hashing with Partitioning

**Concept:**
Partition ring into segments.

**Features:**
- Easier management
- Better control
- Simplified operations

## Practice Thinking Guide

### How to Design Consistent Hashing

**Key Questions to Ask:**

1. **How many virtual nodes per server?**
   - More nodes = better distribution
   - Higher memory overhead
   - Example: "100-1000 virtual nodes"

2. **Which hash function?**
   - MD5, SHA-1, MurmurHash
   - Balance speed and distribution
   - Example: "MD5 for good distribution"

3. **What replication factor?**
   - Higher = more redundancy
   - Higher cost
   - Example: "3 replicas for high availability"

4. **How to handle failures?**
   - Automatic failover
   - Manual intervention
   - Example: "Automatic failover to next server"

5. **How to monitor?**
   - Track distribution
   - Detect hot spots
   - Example: "Monitor key distribution per server"

**Pattern Recognition:**

**Pattern 1: Distributed Cache**
```
Requirements: Dynamic scaling, minimal remapping
Solution: Consistent hashing with virtual nodes
Implementation: Client-side hashing
```

**Pattern 2: Database Sharding**
```
Requirements: Even distribution, replication
Solution: Consistent hashing with replication
Implementation: Server-side hashing
```

**Pattern 3: Load Balancing**
```
Requirements: Session persistence, high availability
Solution: Consistent hashing with weighted nodes
Implementation: Load balancer module
```

**Pattern 4: Content Delivery**
```
Requirements: Geographic distribution, low latency
Solution: Consistent hashing with location awareness
Implementation: CDN edge selection
```

**Pattern 5: Peer-to-Peer**
```
Requirements: Dynamic nodes, fault tolerance
Solution: Consistent hashing with DHT
Implementation: Distributed hash table
```

**Decision Flowchart:**

```
Consistent Hashing Decision:
├─ Need dynamic scaling?
│        ├─ Yes → Use consistent hashing
│        └─ No → May use modulo hashing
├─ Need even distribution?
│        ├─ Yes → Use many virtual nodes
│        └─ No → Fewer virtual nodes OK
├─ Need high availability?
│        ├─ Yes → Use replication
│        └─ No → Single server OK
└─ Heterogeneous servers?
         ├─ Yes → Use weighted hashing
         └─ No → Standard hashing OK
```

**Example Analysis:**

**Scenario:** "Design distributed cache for session storage"

**Analysis:**
1. Requirements: Dynamic scaling, minimal remapping
2. Solution: Consistent hashing with virtual nodes
3. Virtual nodes: 100 per server
4. Hash function: MD5
5. Replication: 2 replicas
6. Implementation: Client-side hashing

**Scenario:** "Design load balancer for web servers"

**Analysis:**
1. Requirements: Session persistence, high availability
2. Solution: Consistent hashing with weighted nodes
3. Virtual nodes: Based on server capacity
4. Hash function: Fast hash (MurmurHash)
5. Replication: Not needed (load balancer)
6. Implementation: Load balancer module

## Summary

Consistent hashing is a technique that distributes data across servers in a way that minimizes data movement when servers are added or removed, unlike traditional modulo-based hashing. It works by mapping both servers and data keys to points on a circular hash space (the ring). Each server is responsible for a contiguous segment of the ring. When a server is added or removed, only the keys in its adjacent segments need to be remapped, minimizing data movement to O(k/n) where k is the number of keys and n is the number of servers. Virtual nodes (multiple hash points per physical server) improve load distribution and reduce hot spots. Consistent hashing is essential for distributed caches, load balancers, database sharding, and any system that requires dynamic scaling without massive data redistribution.

**Key Takeaways:**
- Minimizes data movement during scaling
- Ring-based distribution
- Virtual nodes improve distribution
- O(log n) lookup time
- Essential for distributed systems
- Used in caches, databases, load balancers
- Replication provides high availability
- Weighted hashing handles heterogeneous servers

**Mastery Checklist:**
- ✅ Understand consistent hashing concept
- ✅ Implement basic consistent hashing
- ✅ Use virtual nodes for distribution
- ✅ Implement replication
- ✅ Use weighted hashing
- ✅ Choose appropriate hash function
- ✅ Monitor ring balance
- ✅ Handle server failures gracefully

