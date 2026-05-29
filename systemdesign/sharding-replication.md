# Sharding vs Replication

Sharding splits data across multiple databases (horizontal partitioning). Replication copies data across multiple databases for redundancy and read scaling.

## Introduction

Sharding splits data across multiple databases (horizontal partitioning) to scale write operations. Replication copies data across multiple databases for redundancy and read scaling. Sharding partitions data based on a shard key (e.g., user ID, geographic region) and distributes it across multiple database instances called shards. Each shard contains a subset of the data, allowing write operations to be distributed across multiple servers. Replication creates copies of data across multiple database instances called replicas. Replication provides high availability (if one replica fails, others can serve requests), read scaling (read requests can be distributed across replicas), and redundancy (data is copied for backup). Common sharding strategies include hash-based sharding (hash of shard key determines shard), range-based sharding (range of shard key determines shard), and consistent hashing (minimize data movement when adding/removing shards). Common replication strategies include master-slave (one master for writes, multiple slaves for reads), multi-master (multiple masters for writes), and leaderless (all nodes can read and write). Sharding and replication can be combined for both read and write scaling. Sharding is essential for large datasets that don't fit on a single server, high write throughput, and geographic distribution. Replication is essential for high availability, read scaling, and disaster recovery.

**Why Sharding and Replication Matter:**
- Sharding scales write operations horizontally
- Replication provides high availability and read scaling
- Combined: both read and write scaling
- Essential for large-scale applications
- Enables geographic distribution
- Provides disaster recovery

**Where It Is Used:**
- Large-scale databases (Facebook, Twitter)
- E-commerce platforms (Amazon, Shopify)
- Social media applications (Instagram, TikTok)
- Gaming platforms (Steam, Epic Games)
- IoT platforms (smart home, industrial IoT)
- Financial services (PayPal, Stripe)

## Core Concept Explanation

Sharding partitions data across multiple database instances called shards based on a shard key. Each shard contains a subset of the data, allowing write operations to be distributed across multiple servers. Sharding scales write operations horizontally - as data grows, you can add more shards. Common sharding strategies include hash-based sharding (hash of shard key determines shard using modulo), range-based sharding (range of shard key determines shard), and consistent hashing (hash ring to minimize data movement when adding/removing shards). Replication creates copies of data across multiple database instances called replicas. Replication provides high availability (if one replica fails, others can serve requests), read scaling (read requests can be distributed across replicas), and redundancy (data is copied for backup). Common replication strategies include master-slave (one master for writes, multiple slaves for reads), multi-master (multiple masters for writes with conflict resolution), and leaderless (all nodes can read and write with quorum). Sharding and replication can be combined - each shard can have its own replicas for both read and write scaling. The choice between sharding and replication depends on the scaling requirement (write vs read), data size, and availability requirements.

**Step-by-Step Breakdown:**
1. Determine scaling requirement (write vs read)
2. For write scaling: implement sharding
3. Choose shard key (user ID, region, etc.)
4. Choose sharding strategy (hash, range, consistent hashing)
5. Partition data across shards
6. For read scaling: implement replication
7. Choose replication strategy (master-slave, multi-master, leaderless)
8. Replicate data across replicas
9. Combine sharding and replication for both
10. Monitor and rebalance as needed

**Intuition Behind the Concept:**
Think of sharding like splitting a large library into multiple smaller libraries based on book categories. Each library (shard) contains books from a specific category. When you need to add a book, you go to the appropriate library. This distributes the load across multiple libraries. Think of replication like having multiple copies of the same library in different locations. If one library is closed or busy, you can go to another copy. This provides availability and redundancy. Combined, you have multiple libraries with categories (sharding) and multiple copies of each library (replication) for both distribution and availability.

**Visual Thinking:**
```
Sharding:
User 1, 2, 3 → Shard A
User 4, 5, 6 → Shard B
User 7, 8, 9 → Shard C

Replication:
Master → Replica 1
       → Replica 2
       → Replica 3

Combined:
Shard A → Master A → Replica A1, Replica A2
Shard B → Master B → Replica B1, Replica B2
Shard C → Master C → Replica C1, Replica C2
```

## Internal Working / Logic

Sharding operates through partitioning data based on a shard key. When a write operation arrives, the system determines the shard key (e.g., user ID), computes the shard using a sharding strategy (hash, range, consistent hashing), and routes the write to the appropriate shard. Each shard is a separate database instance containing a subset of the data. Hash-based sharding computes a hash of the shard key and uses modulo to determine the shard. Range-based sharding uses ranges of the shard key to determine the shard (e.g., user ID 1-1000 in shard 1, 1001-2000 in shard 2). Consistent hashing uses a hash ring to minimize data movement when adding/removing shards - each shard is assigned a position on the ring, and data is assigned to the nearest shard. Replication operates through copying data from a primary node to replica nodes. In master-slave replication, writes go to the master, and the master replicates changes to slaves. Reads can be served from slaves for read scaling. In multi-master replication, multiple masters can accept writes, and changes are replicated between masters with conflict resolution. In leaderless replication, all nodes can read and write, and quorum is used for consistency (e.g., write to 3 nodes, read from 2 nodes). Sharding and replication can be combined - each shard can have its own master and replicas for both read and write scaling.

**Operation 1: Hash-Based Sharding**
- Write operation arrives
- Extract shard key (e.g., user ID)
- Compute hash of shard key
- Compute shard index using modulo
- Route write to shard
- Shard processes write
- Return result

**Operation 2: Consistent Hashing**
- Write operation arrives
- Extract shard key
- Compute hash of shard key
- Map hash to hash ring
- Find nearest shard on ring
- Route write to shard
- Shard processes write
- Return result

**Operation 3: Master-Slave Replication**
- Write operation arrives
- Route to master
- Master processes write
- Master replicates to slaves
- Slaves apply changes
- Master returns result
- Reads can be served from slaves

**Operation 4: Combined Sharding and Replication**
- Write operation arrives
- Extract shard key
- Determine shard
- Route to shard's master
- Master processes write
- Master replicates to shard's replicas
- Master returns result
- Reads served from shard's replicas

**Flow Explanation (User Data with Sharding and Replication):**
1. User creates account with user ID 12345
2. System extracts shard key: user ID 12345
3. System computes hash: hash(12345) = 67890
4. System determines shard: 67890 % 3 = 0 (Shard A)
5. System routes write to Shard A's master
6. Shard A's master processes write
7. Shard A's master replicates to Shard A's replicas
8. Shard A's master returns result
9. User reads data
10. System routes read to Shard A's replica
11. Shard A's replica returns data

**Decision Making Logic:**
The key decisions are:
- Sharding strategy (hash, range, consistent hashing)
- Shard key selection (user ID, region, etc.)
- Replication strategy (master-slave, multi-master, leaderless)
- Number of shards and replicas
- Consistency level (strong vs eventual)
- Rebalancing strategy

## Algorithm / Approach

**Hash-Based Sharding Algorithm**

```
1. Extract shard key
2. Compute hash of shard key
3. Compute shard index: hash % numShards
4. Route to shard
5. Shard processes operation
6. Return result
```

**Consistent Hashing Algorithm**

```
1. Extract shard key
2. Compute hash of shard key
3. Map hash to hash ring
4. Find nearest shard clockwise
5. Route to shard
6. Shard processes operation
7. Return result
```

**Master-Slave Replication Algorithm**

```
1. Write operation arrives
2. Route to master
3. Master processes write
4. Master replicates to slaves
5. Slaves apply changes
6. Master returns result
7. Reads served from slaves
```

**Leaderless Replication Algorithm**

```
1. Write operation arrives
2. Write to N nodes
3. Wait for W acknowledgments (quorum)
4. Return result
5. Read operation arrives
6. Read from R nodes (quorum)
7. Return most recent version
```

## Implementations

### 1. Hash-Based Sharding

```javascript
class HashBasedShardManager {
  constructor(numShards) {
    this.numShards = numShards;
    this.shards = Array.from({ length: numShards }, (_, i) => ({
      id: i,
      name: `shard_${i}`,
      data: new Map()
    }));
  }
  
  getShard(key) {
    const hash = this._hash(key);
    const shardIndex = hash % this.numShards;
    return this.shards[shardIndex];
  }
  
  set(key, value) {
    const shard = this.getShard(key);
    shard.data.set(key, value);
    return shard;
  }
  
  get(key) {
    const shard = this.getShard(key);
    return shard.data.get(key);
  }
  
  _hash(key) {
    let hash = 0;
    const str = String(key);
    for (let i = 0; i < str.length; i++) {
      hash = ((hash << 5) - hash) + str.charCodeAt(i);
      hash |= 0;
    }
    return Math.abs(hash);
  }
}

// Usage
const shardManager = new HashBasedShardManager(3);

// Set data
shardManager.set('user_1', { name: 'John' });
shardManager.set('user_2', { name: 'Jane' });
shardManager.set('user_3', { name: 'Bob' });

// Get data
const user1 = shardManager.get('user_1');
console.log('User 1:', user1);
```

**Advantages:**
- Simple to implement
- Even distribution
- Easy to understand
- Good for most use cases

### 2. Consistent Hashing

```javascript
class ConsistentHashShardManager {
  constructor(virtualNodes = 100) {
    this.virtualNodes = virtualNodes;
    this.ring = new Map();
    this.sortedKeys = [];
    this.shards = new Map();
  }
  
  addShard(shardId) {
    for (let i = 0; i < this.virtualNodes; i++) {
      const key = `${shardId}_${i}`;
      const hash = this._hash(key);
      this.ring.set(hash, shardId);
      this.sortedKeys.push(hash);
    }
    this.sortedKeys.sort((a, b) => a - b);
    this.shards.set(shardId, new Map());
  }
  
  removeShard(shardId) {
    for (let i = 0; i < this.virtualNodes; i++) {
      const key = `${shardId}_${i}`;
      const hash = this._hash(key);
      this.ring.delete(hash);
      this.sortedKeys = this.sortedKeys.filter(k => k !== hash);
    }
    this.shards.delete(shardId);
  }
  
  getShard(key) {
    if (this.sortedKeys.length === 0) {
      throw new Error('No shards available');
    }
    
    const hash = this._hash(key);
    
    // Find first key >= hash
    let index = this.sortedKeys.findIndex(k => k >= hash);
    
    // If not found, wrap around to first shard
    if (index === -1) {
      index = 0;
    }
    
    const shardId = this.ring.get(this.sortedKeys[index]);
    return shardId;
  }
  
  set(key, value) {
    const shardId = this.getShard(key);
    const shard = this.shards.get(shardId);
    shard.set(key, value);
    return shardId;
  }
  
  get(key) {
    const shardId = this.getShard(key);
    const shard = this.shards.get(shardId);
    return shard.get(key);
  }
  
  _hash(key) {
    let hash = 0;
    const str = String(key);
    for (let i = 0; i < str.length; i++) {
      hash = ((hash << 5) - hash) + str.charCodeAt(i);
      hash |= 0;
    }
    return Math.abs(hash);
  }
}

// Usage
const shardManager = new ConsistentHashShardManager(100);

// Add shards
shardManager.addShard('shard_A');
shardManager.addShard('shard_B');
shardManager.addShard('shard_C');

// Set data
shardManager.set('user_1', { name: 'John' });
shardManager.set('user_2', { name: 'Jane' });

// Get data
const user1 = shardManager.get('user_1');
console.log('User 1:', user1);
```

**Advantages:**
- Minimizes data movement
- Handles shard addition/removal
- Better distribution
- Good for dynamic scaling

### 3. Master-Slave Replication

```javascript
class MasterSlaveReplication {
  constructor() {
    this.master = new Map();
    this.slaves = [new Map(), new Map()];
  }
  
  write(key, value) {
    // Write to master
    this.master.set(key, value);
    
    // Replicate to slaves
    for (const slave of this.slaves) {
      slave.set(key, value);
    }
    
    return true;
  }
  
  read(key) {
    // Read from first slave
    return this.slaves[0].get(key);
  }
  
  readFromMaster(key) {
    // Read from master (for consistency)
    return this.master.get(key);
  }
}

// Usage
const replication = new MasterSlaveReplication();

// Write data
replication.write('user_1', { name: 'John' });
replication.write('user_2', { name: 'Jane' });

// Read from slave
const user1 = replication.read('user_1');
console.log('User 1 (from slave):', user1);

// Read from master (for consistency)
const user1Master = replication.readFromMaster('user_1');
console.log('User 1 (from master):', user1Master);
```

**Advantages:**
- Simple to implement
- Read scaling
- High availability
- Strong consistency

### 4. Combined Sharding and Replication

```javascript
class ShardedReplicatedDatabase {
  constructor(numShards, replicasPerShard) {
    this.numShards = numShards;
    this.replicasPerShard = replicasPerShard;
    this.shards = [];
    
    for (let i = 0; i < numShards; i++) {
      const master = new Map();
      const replicas = [];
      
      for (let j = 0; j < replicasPerShard; j++) {
        replicas.push(new Map());
      }
      
      this.shards.push({
        id: i,
        master,
        replicas
      });
    }
  }
  
  getShard(key) {
    const hash = this._hash(key);
    const shardIndex = hash % this.numShards;
    return this.shards[shardIndex];
  }
  
  write(key, value) {
    const shard = this.getShard(key);
    
    // Write to master
    shard.master.set(key, value);
    
    // Replicate to replicas
    for (const replica of shard.replicas) {
      replica.set(key, value);
    }
    
    return shard.id;
  }
  
  read(key) {
    const shard = this.getShard(key);
    
    // Read from first replica
    return shard.replicas[0].get(key);
  }
  
  readFromMaster(key) {
    const shard = this.getShard(key);
    return shard.master.get(key);
  }
  
  _hash(key) {
    let hash = 0;
    const str = String(key);
    for (let i = 0; i < str.length; i++) {
      hash = ((hash << 5) - hash) + str.charCodeAt(i);
      hash |= 0;
    }
    return Math.abs(hash);
  }
}

// Usage
const db = new ShardedReplicatedDatabase(3, 2);

// Write data
db.write('user_1', { name: 'John' });
db.write('user_2', { name: 'Jane' });
db.write('user_3', { name: 'Bob' });

// Read from replica
const user1 = db.read('user_1');
console.log('User 1 (from replica):', user1);

// Read from master (for consistency)
const user1Master = db.readFromMaster('user_1');
console.log('User 1 (from master):', user1Master);
```

**Advantages:**
- Both read and write scaling
- High availability
- Redundancy
- Geographic distribution

### 5. Range-Based Sharding

```javascript
class RangeBasedShardManager {
  constructor() {
    this.shards = [];
    this.ranges = [];
  }
  
  addShard(shardId, minKey, maxKey) {
    this.shards.push({
      id: shardId,
      minKey,
      maxKey,
      data: new Map()
    });
    
    this.ranges.push({ minKey, maxKey, shardId });
    this.ranges.sort((a, b) => a.minKey - b.minKey);
  }
  
  getShard(key) {
    const numKey = Number(key);
    
    for (const range of this.ranges) {
      if (numKey >= range.minKey && numKey <= range.maxKey) {
        return this.shards.find(s => s.id === range.shardId);
      }
    }
    
    throw new Error('Key out of range');
  }
  
  set(key, value) {
    const shard = this.getShard(key);
    shard.data.set(key, value);
    return shard.id;
  }
  
  get(key) {
    const shard = this.getShard(key);
    return shard.data.get(key);
  }
}

// Usage
const shardManager = new RangeBasedShardManager();

// Add shards with ranges
shardManager.addShard('shard_A', 1, 1000);
shardManager.addShard('shard_B', 1001, 2000);
shardManager.addShard('shard_C', 2001, 3000);

// Set data
shardManager.set('500', { name: 'John' });
shardManager.set('1500', { name: 'Jane' });
shardManager.set('2500', { name: 'Bob' });

// Get data
const user1 = shardManager.get('500');
console.log('User 1:', user1);
```

**Advantages:**
- Range queries efficient
- Predictable distribution
- Easy to understand
- Good for sequential data

## Dry Run

**Example: Hash-Based Sharding with Replication**

**Initial State:**
```
Shards: 3 (Shard A, Shard B, Shard C)
Replicas per shard: 2
Data to write: user_1, user_2, user_3
```

**Step-by-Step Execution:**

```
Step 1: Write user_1
Step 2: Extract shard key: user_1
Step 3: Compute hash: hash('user_1') = 12345
Step 4: Determine shard: 12345 % 3 = 0 (Shard A)
Step 5: Write to Shard A's master
Step 6: Shard A's master stores user_1
Step 7: Shard A's master replicates to replicas
Step 8: Write user_2
Step 9: Extract shard key: user_2
Step 10: Compute hash: hash('user_2') = 67890
Step 11: Determine shard: 67890 % 3 = 1 (Shard B)
Step 12: Write to Shard B's master
Step 13: Shard B's master stores user_2
Step 14: Shard B's master replicates to replicas
Step 15: Read user_1
Step 16: Determine shard: Shard A
Step 17: Read from Shard A's replica
Step 18: Shard A's replica returns user_1
```

**Request/Response Table:**

| Step | Operation | Key | Hash | Shard | Action |
|------|------------|-----|------|-------|--------|
| 1 | Write | user_1 | 12345 | Shard A | Write to master |
| 2 | Replicate | user_1 | - | Shard A | Replicate to replicas |
| 3 | Write | user_2 | 67890 | Shard B | Write to master |
| 4 | Replicate | user_2 | - | Shard B | Replicate to replicas |
| 5 | Read | user_1 | 12345 | Shard A | Read from replica |

## Edge Cases

### 1. Hot Shards
```javascript
// Uneven data distribution
- Some shards overloaded
// Solution: Rebalancing, consistent hashing
```

### 2. Cross-Shard Queries
```javascript
// Query spans multiple shards
- Complex to execute
// Solution: Scatter-gather, denormalization
```

### 3. Replication Lag
```javascript
// Replicas behind master
- Stale reads
// Solution: Read from master, monitor lag
```

### 4. Shard Rebalancing
```javascript
// Adding/removing shards
- Data movement
// Solution: Consistent hashing, gradual rebalancing
```

### 5. Shard Failure
```javascript
// Shard unavailable
- Data unavailable
// Solution: Replication, failover
```

### 6. Network Partition
```javascript
// Shards cannot communicate
- Split-brain
// Solution: Quorum, conflict resolution
```

**Why Edge Cases Matter:**
- Hot shards cause uneven load
- Cross-shard queries cause complexity
- Replication lag causes stale reads
- Rebalancing causes data movement
- Shard failure causes unavailability
- Network partition causes split-brain

## Variations / Extensions

### 1. Geo-Sharding

```javascript
// Geographic distribution
- Data locality
// Example: Regional databases
```

### 2. Multi-Master Replication

```javascript
// Multiple write nodes
- Write scaling
// Example: Multi-region writes
```

### 3. Read Replicas

```javascript
// Dedicated read nodes
- Read scaling
// Example: Analytics replicas
```

### 4. Automatic Rebalancing

```javascript
// Automatic shard rebalancing
- Even distribution
// Example: Auto-scaling
```

### 5. Hybrid Sharding

```javascript
// Multiple sharding strategies
- Flexibility
// Example: Hash + range
```

## Optimization Techniques

### 1. Consistent Hashing

**Minimize Data Movement:**
```javascript
// Consistent hashing
- Less data movement
// Better scalability
```

### 2. Read Replicas

**Scale Reads:**
```javascript
// Dedicated read replicas
- Read scaling
// Better performance
```

### 3. Denormalization

**Avoid Cross-Shard Queries:**
```javascript
// Denormalize data
- Single-shard queries
// Better performance
```

### 4. Caching

**Cache Frequently Accessed Data:**
```javascript
// Cache layer
- Reduce database load
// Better performance
```

### 5. Trade-offs

**Strategy Comparison:**

| Strategy | Write Scaling | Read Scaling | Complexity | Use Case |
|----------|---------------|--------------|------------|----------|
| Sharding | High | Low | High | Write-heavy |
| Replication | Low | High | Low | Read-heavy |
| Combined | High | High | Very High | Balanced |

**When to Use Each:**
- Sharding: Write-heavy, large dataset
- Replication: Read-heavy, high availability
- Combined: Balanced, large-scale

## Complexity Analysis

### Time Complexity

**Hash-Based Sharding: O(1)**
- Constant time
- Hash computation
- Very fast

**Consistent Hashing: O(log n)**
- n = number of virtual nodes
- Binary search
- Fast

**Range-Based Sharding: O(n)**
- n = number of ranges
- Linear search
- Slower

### Space Complexity

**Sharding: O(n)**
- n = total data
- Linear with data
- Distributed across shards

**Replication: O(n * r)**
- n = total data, r = replicas
- Linear with data and replicas
- More storage

**Explanation:**
Hash-based sharding is O(1) time - constant time for hash computation. Consistent hashing is O(log n) where n is the number of virtual nodes - binary search on sorted keys. Range-based sharding is O(n) where n is the number of ranges - linear search. Space complexity for sharding is O(n) where n is the total data - linear with data, distributed across shards. Replication is O(n * r) where n is the total data and r is the number of replicas - linear with data and replicas. The trade-off is between complexity (hash-based) and query efficiency (range-based).

## Real-world Applications

### 1. User Data Sharding

**Social Media:**
- User data by user ID
- Example: Facebook, Twitter

### 2. Read Replicas for Analytics

**E-commerce:**
- Analytics on read replicas
- Example: Amazon, Shopify

### 3. Geo-Distributed Databases

**Global Applications:**
- Data by geographic region
- Example: Netflix, Spotify

### 4. Multi-Region Deployments

**Financial Services:**
- Data by region for compliance
- Example: PayPal, Stripe

### 5. Gaming Platforms

**Online Games:**
- Player data by region
- Example: Steam, Epic Games

### 6. IoT Platforms

**Smart Home:**
- Device data by region
- Example: AWS IoT, Google IoT

### 7. Messaging Platforms

**Chat Applications:**
- Messages by conversation ID
- Example: WhatsApp, Telegram

### 8. Content Delivery

**Streaming Services:**
- Content by region
- Example: YouTube, Netflix

## Common Mistakes

### 1. Wrong Shard Key

**Mistake:**
```javascript
// Poor shard key selection
- Uneven distribution
// Hot shards
```

**Correct:**
```javascript
// Choose appropriate shard key
- Even distribution
// Better performance
```

**Why It Matters:**
- Wrong key = uneven distribution
- Hot shards
- Appropriate key essential

### 2. No Replication

**Mistake:**
```javascript
// No replication
- Single point of failure
// Poor availability
```

**Correct:**
```javascript
// Implement replication
- High availability
// Better reliability
```

**Why It Matters:**
- No replication = single point of failure
- Poor availability
- Replication essential

### 3. Ignoring Replication Lag

**Mistake:**
```javascript
// Ignore replication lag
- Stale reads
// Poor consistency
```

**Correct:**
```javascript
// Monitor replication lag
- Read from master if needed
// Better consistency
```

**Why It Matters:**
- Ignore lag = stale reads
- Poor consistency
- Monitor lag essential

### 4. Cross-Shard Queries

**Mistake:**
```javascript
// Cross-shard queries
- Poor performance
// High complexity
```

**Correct:**
```javascript
// Avoid cross-shard queries
- Denormalize data
// Better performance
```

**Why It Matters:**
- Cross-shard = poor performance
- High complexity
- Avoid essential

### 5. No Rebalancing Strategy

**Mistake:**
```javascript
// No rebalancing
- Uneven distribution over time
// Poor performance
```

**Correct:**
```javascript
// Implement rebalancing
- Consistent hashing
// Better performance
```

**Why It Matters:**
- No rebalancing = uneven distribution
- Poor performance
- Rebalancing essential

### 6. No Monitoring

**Mistake:**
```javascript
// No monitoring
- Issues go unnoticed
// Poor visibility
```

**Correct:**
```javascript
// Monitor shards and replicas
- Detect issues early
// Better visibility
```

**Why It Matters:**
- No monitoring = issues unnoticed
- Poor visibility
- Monitoring essential

## Advanced Concepts

### 1. Consistent Hashing

**Concept:**
Hash ring to minimize data movement.

**Features:**
- Minimal data movement
- Dynamic scaling
- Better distribution

### 2. Multi-Master Replication

**Concept:**
Multiple write nodes with conflict resolution.

**Features:**
- Write scaling
- Conflict resolution
- Eventual consistency

### 3. Geo-Sharding

**Concept:**
Geographic distribution of data.

**Features:**
- Data locality
- Low latency
- Compliance

### 4. Automatic Rebalancing

**Concept:**
Automatic shard rebalancing.

**Features:**
- Even distribution
- Auto-scaling
- Better performance

## Practice Thinking Guide

### How to Design Sharding and Replication Strategy

**Key Questions to Ask:**

1. **Scaling requirement?**
   - Write: Sharding
   - Read: Replication
   - Both: Combined
   - Example: "Combined for balanced load"

2. **Data size?**
   - Small: Single database
   - Large: Sharding
   - Very Large: Sharding + Replication
   - Example: "Sharding for large dataset"

3. **Availability requirement?**
   - Low: Single database
   - High: Replication
   - Very High: Multi-region replication
   - Example: "Replication for high availability"

4. **Query pattern?**
   - Single-key: Hash-based sharding
   - Range queries: Range-based sharding
   - Complex: Denormalization
   - Example: "Range-based for range queries"

5. **Consistency requirement?**
   - Strong: Master-slave
   - Eventual: Multi-master
   - Flexible: Leaderless
   - Example: "Master-slave for strong consistency"

**Pattern Recognition:**

**Pattern 1: Write-Heavy Application**
```
Requirements: High write throughput
Solution: Hash-based sharding
Implementation: User ID as shard key
```

**Pattern 2: Read-Heavy Application**
```
Requirements: High read throughput
Solution: Master-slave replication
Implementation: Multiple read replicas
```

**Pattern 3: Global Application**
```
Requirements: Low latency, high availability
Solution: Geo-sharding + replication
Implementation: Region-based sharding, regional replicas
```

**Pattern 4: Analytics Application**
```
Requirements: Analytics on large dataset
Solution: Read replicas + sharding
Implementation: Dedicated analytics replicas
```

**Pattern 5: High Availability Application**
```
Requirements: High availability, disaster recovery
Solution: Multi-region replication
Implementation: Cross-region replication
```

**Decision Flowchart:**

```
Sharding/Replication Decision:
├─ Scaling requirement?
│        ├─ Write → Sharding
│        ├─ Read → Replication
│        └─ Both → Combined
├─ Data size?
│        ├─ Small → Single database
│        ├─ Large → Sharding
│        └─ Very Large → Sharding + Replication
├─ Availability?
│        ├─ Low → Single database
│        ├─ High → Replication
│        └─ Very High → Multi-region
└─ Query pattern?
         ├─ Single-key → Hash-based
         ├─ Range → Range-based
         └─ Complex → Denormalization
```

**Example Analysis:**

**Scenario:** "Design database for social media platform"

**Analysis:**
1. Requirements: High write and read throughput
2. Strategy: Combined sharding and replication
3. Sharding: Hash-based with user ID
4. Replication: Master-slave with read replicas
5. Implementation: 10 shards, 3 replicas per shard

**Scenario:** "Design database for e-commerce platform"

**Analysis:**
1. Requirements: High read throughput, analytics
2. Strategy: Replication with read replicas
3. Sharding: Not needed initially
4. Replication: Master-slave with analytics replicas
5. Implementation: 1 master, 5 read replicas

## Summary

Sharding splits data across multiple databases (horizontal partitioning) to scale write operations. Replication copies data across multiple databases for redundancy and read scaling. Sharding partitions data based on a shard key (e.g., user ID, geographic region) and distributes it across multiple database instances called shards. Each shard contains a subset of the data, allowing write operations to be distributed across multiple servers. Replication creates copies of data across multiple database instances called replicas. Replication provides high availability (if one replica fails, others can serve requests), read scaling (read requests can be distributed across replicas), and redundancy (data is copied for backup). Common sharding strategies include hash-based sharding (hash of shard key determines shard), range-based sharding (range of shard key determines shard), and consistent hashing (minimize data movement when adding/removing shards). Common replication strategies include master-slave (one master for writes, multiple slaves for reads), multi-master (multiple masters for writes), and leaderless (all nodes can read and write). Sharding and replication can be combined for both read and write scaling. The choice between sharding and replication depends on the scaling requirement (write vs read), data size, and availability requirements.

**Key Takeaways:**
- Sharding scales write operations horizontally
- Replication provides high availability and read scaling
- Combined: both read and write scaling
- Hash-based sharding for even distribution
- Consistent hashing for minimal data movement
- Master-slave for strong consistency
- Multi-master for write scaling
- Essential for large-scale applications

**Mastery Checklist:**
- ✅ Understand sharding and replication concepts
- ✅ Implement hash-based sharding
- ✅ Implement consistent hashing
- ✅ Implement range-based sharding
- ✅ Implement master-slave replication
- ✅ Implement combined sharding and replication
- ✅ Choose appropriate shard key
- ✅ Design sharding and replication strategy

