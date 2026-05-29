# Database Scaling

Database scaling increases database capacity to handle growing data volumes and traffic. Two main approaches: vertical scaling (scale up - add resources to single server) and horizontal scaling (scale out - add more servers).

## Introduction

Database scaling increases database capacity to handle growing data volumes and traffic. Two main approaches are vertical scaling (scale up - adding more resources like CPU, RAM, and storage to a single server) and horizontal scaling (scale out - adding more servers to distribute the load). Vertical scaling is simpler but has hardware limits and can be expensive. Horizontal scaling is more complex but offers unlimited scalability. Horizontal scaling techniques include read replicas (copying data for read operations), sharding (splitting data across servers), and partitioning (dividing tables into smaller pieces). Read replicas improve read performance by distributing read queries across multiple copies of the data. Sharding distributes both read and write load by splitting data based on a shard key. Consistent hashing is used to minimize data movement when adding or removing shards. Database scaling is essential for high-traffic applications, large datasets, and systems requiring high availability.

**Why Database Scaling Matters:**
- Handles growing data volumes
- Supports increasing traffic
- Improves application performance
- Ensures high availability
- Enables global distribution
- Critical for production systems

**Where It Is Used:**
- High-traffic web applications
- Large e-commerce platforms
- Social media platforms
- Analytics and big data
- Global applications
- Any system with growing data

## Core Concept Explanation

Database scaling addresses the challenge of handling increasing data volumes and traffic loads. Vertical scaling (scale up) involves upgrading a single server with more CPU, RAM, and storage. This is simple to implement but has hardware limits and can be expensive. Horizontal scaling (scale out) involves adding more servers to distribute the load. This is more complex but offers unlimited scalability. Read replicas create copies of the primary database for read operations, distributing read load while writes go to the primary. Sharding splits data across multiple servers based on a shard key (like user ID or region), distributing both read and write load. Partitioning divides a single table into smaller pieces stored separately. Consistent hashing is used in sharding to minimize data movement when adding or removing shards. The choice between vertical and horizontal scaling depends on the use case, budget, and complexity tolerance.

**Step-by-Step Breakdown:**
1. Identify scaling bottleneck (CPU, RAM, storage, I/O)
2. Choose scaling approach (vertical vs horizontal)
3. For vertical: Upgrade server resources
4. For horizontal: Implement read replicas or sharding
5. Configure data replication
6. Update application to route queries
7. Monitor performance and capacity
8. Add more capacity as needed
9. Handle failover and high availability

**Intuition Behind the Concept:**
Think of database scaling like managing a growing restaurant. Vertical scaling is like making the kitchen bigger (more staff, more equipment) - it helps but has space limits. Horizontal scaling is like opening multiple restaurant locations - it's more complex to manage but can handle unlimited customers. Read replicas are like having multiple waiters serving from the same kitchen. Sharding is like having multiple kitchens, each serving different types of food or different neighborhoods.

**Visual Thinking:**
```
Vertical Scaling:
Single Server → Upgrade → Larger Server
CPU: 4 cores → 8 cores
RAM: 16GB → 64GB
Storage: 1TB → 10TB

Horizontal Scaling (Read Replicas):
Primary (writes) → Replica 1 (reads)
                 → Replica 2 (reads)
                 → Replica 3 (reads)

Horizontal Scaling (Sharding):
Shard 0: Users 0-999
Shard 1: Users 1000-1999
Shard 2: Users 2000-2999
Shard 3: Users 3000-3999
```

## Internal Working / Logic

Database scaling operates through different mechanisms depending on the approach. Vertical scaling involves upgrading hardware resources on a single server. The database continues running on the same server but with more resources available. This is typically done by migrating to a larger server instance in cloud environments or adding hardware in on-premises environments. Horizontal scaling with read replicas involves setting up replication from a primary database to one or more replica databases. The primary handles all write operations, while replicas handle read operations. The application must be configured to route read queries to replicas and write queries to the primary. Replication can be synchronous (primary waits for replicas to confirm) or asynchronous (primary doesn't wait). Sharding involves splitting data across multiple database instances based on a shard key. The application uses a sharding function (like hash or range) to determine which shard to query for a given data item. Consistent hashing is used to minimize data movement when adding or removing shards.

**Operation 1: Vertical Scaling**
- Identify resource bottleneck
- Select larger server instance
- Migrate database to new server
- Update DNS or connection string
- Monitor performance
- Scale further if needed

**Operation 2: Read Replica Setup**
- Create replica database instance
- Configure replication from primary
- Wait for initial data sync
- Configure application to route reads
- Monitor replication lag
- Add more replicas as needed

**Operation 3: Sharding Setup**
- Choose shard key (user ID, region, etc.)
- Create shard database instances
- Implement sharding function
- Migrate data to shards
- Update application to use sharding
- Monitor shard distribution

**Operation 4: Query Routing**
- Application receives query
- Determine if read or write
- For read: route to replica or shard
- For write: route to primary or shard
- Execute query on target database
- Return results to application

**Flow Explanation (Read Replica Routing):**
1. Application sends read query
2. Router determines it's a read query
3. Router selects replica (round-robin, least connections)
4. Query executed on replica
5. Results returned to application
6. Application sends write query
7. Router determines it's a write query
8. Query executed on primary
9. Changes replicated to replicas
10. Results returned to application

**Decision Making Logic:**
The key decisions are:
- Vertical vs horizontal scaling (budget, complexity, limits)
- Read replicas vs sharding (read-heavy vs write-heavy)
- Synchronous vs asynchronous replication (consistency vs performance)
- Shard key selection (data distribution, query patterns)
- Number of replicas or shards (capacity, cost)
- Consistent hashing vs simple hashing (data movement)

## Algorithm / Approach

**Vertical Scaling Algorithm**

```
1. Monitor database performance metrics
2. Identify resource bottleneck (CPU, RAM, I/O)
3. Select larger server instance
4. Schedule maintenance window
5. Migrate database to new server
6. Update connection configuration
7. Verify performance improvement
8. Monitor for new bottlenecks
```

**Read Replica Routing Algorithm**

```
1. Application sends query
2. Determine if read or write
3. If write, route to primary
4. If read, select replica
5. Execute query on selected database
6. Return results
7. Monitor replica health
8. Remove unhealthy replicas
```

**Sharding Algorithm**

```
1. Application sends query with shard key
2. Compute shard index using hash function
3. Select shard based on index
4. Execute query on selected shard
5. Return results
6. For cross-shard queries, query all shards
7. Aggregate results
8. Return combined results
```

**Consistent Hashing Algorithm**

```
1. Map shards to hash ring
2. For each data item, compute hash
3. Find nearest shard on ring
4. Route to that shard
5. When adding shard, remap minimal data
6. When removing shard, remap minimal data
7. Maintain balanced distribution
```

## Implementations

### 1. Read Replica Router

```javascript
class ReadReplicaRouter {
  constructor(primary, replicas) {
    this.primary = primary;
    this.replicas = replicas;
    this.currentReplica = 0;
    this.healthyReplicas = new Set(replicas);
  }
  
  executeRead(query) {
    if (this.healthyReplicas.size === 0) {
      // Fallback to primary if no healthy replicas
      return this.primary.execute(query);
    }
    
    const healthyReplicasArray = Array.from(this.healthyReplicas);
    const replica = healthyReplicasArray[this.currentReplica];
    this.currentReplica = (this.currentReplica + 1) % healthyReplicasArray.length;
    
    try {
      return replica.execute(query);
    } catch (error) {
      // Mark replica as unhealthy
      this.healthyReplicas.delete(replica);
      // Retry with next replica
      return this.executeRead(query);
    }
  }
  
  executeWrite(query) {
    return this.primary.execute(query);
  }
  
  markUnhealthy(replica) {
    this.healthyReplicas.delete(replica);
  }
  
  markHealthy(replica) {
    if (this.replicas.includes(replica)) {
      this.healthyReplicas.add(replica);
    }
  }
}

// Usage
const primary = new Database('primary-db');
const replicas = [
  new Database('replica-1'),
  new Database('replica-2'),
  new Database('replica-3')
];
const router = new ReadReplicaRouter(primary, replicas);

// Read query goes to replica
router.executeRead('SELECT * FROM users');

// Write query goes to primary
router.executeWrite('INSERT INTO users ...');
```

**Advantages:**
- Distributes read load
- Simple to implement
- Improves read performance
- High availability for reads

### 2. Sharded Database

```javascript
class ShardedDatabase {
  constructor(shards) {
    this.shards = shards;
  }
  
  _hash(key) {
    let hash = 0;
    for (let i = 0; i < key.length; i++) {
      hash = ((hash << 5) - hash) + key.charCodeAt(i);
      hash |= 0;
    }
    return Math.abs(hash);
  }
  
  getShard(key) {
    const hash = this._hash(key);
    return hash % this.shards.length;
  }
  
  async get(key) {
    const shardIndex = this.getShard(key);
    return await this.shards[shardIndex].get(key);
  }
  
  async set(key, value) {
    const shardIndex = this.getShard(key);
    return await this.shards[shardIndex].set(key, value);
  }
  
  async delete(key) {
    const shardIndex = this.getShard(key);
    return await this.shards[shardIndex].delete(key);
  }
  
  async query(shardKey, query) {
    const shardIndex = this.getShard(shardKey);
    return await this.shards[shardIndex].query(query);
  }
  
  async queryAll(query) {
    // Query all shards and aggregate results
    const results = await Promise.all(
      this.shards.map(shard => shard.query(query))
    );
    return results.flat();
  }
}

// Usage
const shards = [
  new Database('shard-0'),
  new Database('shard-1'),
  new Database('shard-2'),
  new Database('shard-3')
];
const shardedDB = new ShardedDatabase(shards);

// Data automatically routed to correct shard
await shardedDB.set('user:123', { name: 'John' });
const user = await shardedDB.get('user:123');
```

**Advantages:**
- Distributes both read and write load
- Unlimited scalability
- Better performance for large datasets
- Geographic distribution possible

### 3. Consistent Hashing

```javascript
class ConsistentHash {
  constructor(virtualNodes = 100) {
    this.ring = new Map();
    this.virtualNodes = virtualNodes;
  }
  
  _hash(key) {
    let hash = 0;
    for (let i = 0; i < key.length; i++) {
      hash = ((hash << 5) - hash) + key.charCodeAt(i);
      hash |= 0;
    }
    return Math.abs(hash);
  }
  
  addShard(shard) {
    for (let i = 0; i < this.virtualNodes; i++) {
      const virtualNode = `${shard}:${i}`;
      const hash = this._hash(virtualNode);
      this.ring.set(hash, shard);
    }
  }
  
  removeShard(shard) {
    for (let i = 0; i < this.virtualNodes; i++) {
      const virtualNode = `${shard}:${i}`;
      const hash = this._hash(virtualNode);
      this.ring.delete(hash);
    }
  }
  
  getShard(key) {
    if (this.ring.size === 0) {
      throw new Error('No shards available');
    }
    
    const hash = this._hash(key);
    const sortedHashes = Array.from(this.ring.keys()).sort((a, b) => a - b);
    
    // Find first hash >= key hash
    for (const ringHash of sortedHashes) {
      if (ringHash >= hash) {
        return this.ring.get(ringHash);
      }
    }
    
    // Wrap around to first shard
    return this.ring.get(sortedHashes[0]);
  }
}

// Usage
const consistentHash = new ConsistentHash(100);
consistentHash.addShard('shard-1');
consistentHash.addShard('shard-2');
consistentHash.addShard('shard-3');

// Get shard for a key
const shard = consistentHash.getShard('user:123');
console.log(shard); // shard-1 or shard-2 or shard-3

// Add new shard - minimal data movement
consistentHash.addShard('shard-4');
```

**Advantages:**
- Minimal data movement
- Balanced distribution
- Easy to add/remove shards
- Good for dynamic scaling

### 4. Connection Pooling

```javascript
class ConnectionPool {
  constructor(config, maxConnections = 10) {
    this.config = config;
    this.maxConnections = maxConnections;
    this.pool = [];
    this.activeConnections = 0;
  }
  
  async getConnection() {
    if (this.pool.length > 0) {
      return this.pool.pop();
    }
    
    if (this.activeConnections < this.maxConnections) {
      this.activeConnections++;
      return await this.createConnection();
    }
    
    // Wait for available connection
    return await this.waitForConnection();
  }
  
  async createConnection() {
    // Create database connection
    return new Promise((resolve) => {
      setTimeout(() => {
        resolve({ connection: 'db-connection', inUse: true });
      }, 100);
    });
  }
  
  releaseConnection(connection) {
    connection.inUse = false;
    this.pool.push(connection);
  }
  
  async query(sql, params) {
    const connection = await this.getConnection();
    try {
      // Execute query
      const result = await this.executeQuery(connection, sql, params);
      return result;
    } finally {
      this.releaseConnection(connection);
    }
  }
  
  async executeQuery(connection, sql, params) {
    // Simulate query execution
    return { rows: [], affectedRows: 0 };
  }
  
  async waitForConnection() {
    return new Promise((resolve) => {
      const checkInterval = setInterval(() => {
        if (this.pool.length > 0) {
          clearInterval(checkInterval);
          resolve(this.pool.pop());
        }
      }, 100);
    });
  }
}

// Usage
const pool = new ConnectionPool({ host: 'localhost' }, 10);
const result = await pool.query('SELECT * FROM users');
```

**Advantages:**
- Reduces connection overhead
- Better performance
- Limits resource usage
- Handles concurrency

### 5. Database Scaling Manager

```javascript
class DatabaseScalingManager {
  constructor() {
    this.metrics = {
      cpu: 0,
      memory: 0,
      connections: 0,
      queries: 0
    };
    this.thresholds = {
      cpu: 80,
      memory: 80,
      connections: 1000
    };
  }
  
  updateMetrics(metrics) {
    this.metrics = { ...this.metrics, ...metrics };
  }
  
  shouldScale() {
    return (
      this.metrics.cpu > this.thresholds.cpu ||
      this.metrics.memory > this.thresholds.memory ||
      this.metrics.connections > this.thresholds.connections
    );
  }
  
  async scaleVertical() {
    console.log('Scaling vertically...');
    // Add more resources to server
    // Migrate to larger instance
  }
  
  async addReadReplica() {
    console.log('Adding read replica...');
    // Create new replica
    // Configure replication
    // Update routing
  }
  
  async addShard() {
    console.log('Adding shard...');
    // Create new shard
    // Rebalance data
    // Update sharding config
  }
  
  async autoScale() {
    if (this.shouldScale()) {
      // Decide scaling strategy based on metrics
      if (this.metrics.queries > 10000) {
        await this.addReadReplica();
      } else if (this.metrics.connections > 2000) {
        await this.addShard();
      } else {
        await this.scaleVertical();
      }
    }
  }
}

// Usage
const scalingManager = new DatabaseScalingManager();
scalingManager.updateMetrics({ cpu: 85, memory: 70, connections: 1200, queries: 5000 });
await scalingManager.autoScale();
```

**Advantages:**
- Automatic scaling
- Metric-based decisions
- Flexible scaling strategies
- Proactive capacity management

## Dry Run

**Example: Read Replica Routing**

**Initial State:**
```
Primary: Handles writes
Replicas: 3 replicas (replica-1, replica-2, replica-3)
Current replica index: 0
All replicas healthy
```

**Step-by-Step Execution:**

```
Request 1 (Read):
1. Application sends SELECT query
2. Router determines it's a read query
3. Router selects replica-1 (index 0)
4. Query executed on replica-1
5. Results returned to application
6. Index incremented to 1

Request 2 (Read):
1. Application sends SELECT query
2. Router determines it's a read query
3. Router selects replica-2 (index 1)
4. Query executed on replica-2
5. Results returned to application
6. Index incremented to 2

Request 3 (Write):
1. Application sends INSERT query
2. Router determines it's a write query
3. Query executed on primary
4. Changes replicated to replicas
5. Results returned to application

Request 4 (Read):
1. Application sends SELECT query
2. Router determines it's a read query
3. Router selects replica-3 (index 2)
4. Query executed on replica-3
5. Results returned to application
6. Index wrapped to 0
```

**Request/Response Table:**

| Request | Type | Target | Status |
|---------|------|--------|--------|
| 1 | Read | replica-1 | Success |
| 2 | Read | replica-2 | Success |
| 3 | Write | primary | Success |
| 4 | Read | replica-3 | Success |
| 5 | Read | replica-1 | Success |

## Edge Cases

### 1. Replication Lag
```javascript
// Replica behind primary
- Stale data read
// Solution: Monitor lag, route recent reads to primary
```

### 2. Shard Rebalancing
```javascript
// Data unevenly distributed
- Some shards overloaded
// Solution: Rebalance data, add more shards
```

### 3. Cross-Shard Queries
```javascript
// Query needs data from multiple shards
- Complex aggregation
// Solution: Query all shards, aggregate results
```

### 4. Data Consistency
```javascript
// Data inconsistent across shards
- Incorrect results
// Solution: Distributed transactions, eventual consistency
```

### 5. Shard Key Selection
```javascript
// Poor shard key choice
- Uneven distribution
// Solution: Choose high-cardinality, evenly distributed key
```

### 6. Failover Handling
```javascript
// Primary or replica fails
- Downtime
// Solution: Automatic failover, health checks
```

**Why Edge Cases Matter:**
- Replication lag causes stale data
- Uneven distribution degrades performance
- Cross-shard queries are complex
- Consistency issues cause errors
- Poor shard key wastes capacity
- Failover affects availability

## Variations / Extensions

### 1. Geo-Distributed Replication

```javascript
// Replicas in different regions
- Low latency for local users
// Example: Global applications
```

### 2. Multi-Master Replication

```javascript
// Multiple primaries for writes
- Higher write throughput
// Example: Write-heavy workloads
```

### 3. Auto-Sharding

```javascript
// Automatic shard management
- Dynamic scaling
// Example: Cloud databases
```

### 4. Hybrid Scaling

```javascript
// Combine vertical and horizontal
- Optimal resource usage
// Example: Complex workloads
```

### 5. Database as a Service

```javascript
// Managed database scaling
- Automatic scaling
// Example: AWS RDS, Google Cloud SQL
```

## Optimization Techniques

### 1. Connection Pooling

**Reuse Connections:**
```javascript
// Pool database connections
- Reduce overhead
// Better performance
```

### 2. Query Optimization

**Optimize Queries:**
```javascript
// Use indexes, optimize queries
- Reduce load
// Better performance
```

### 3. Caching

**Cache Results:**
```javascript
// Cache frequently accessed data
- Reduce database load
// Faster responses
```

### 4. Read-Write Splitting

**Route Queries:**
```javascript
// Route reads to replicas, writes to primary
- Distribute load
// Better performance
```

### 5. Trade-offs

**Scaling Approach Comparison:**

| Approach | Complexity | Scalability | Cost | Use Case |
|----------|------------|-------------|------|----------|
| Vertical | Low | Limited | High | Small to medium |
| Read Replicas | Medium | High | Medium | Read-heavy |
| Sharding | High | Unlimited | Low | Write-heavy |
| Hybrid | Very High | Unlimited | Medium | Complex |

**When to Use Each:**
- Vertical: Small to medium, simple
- Read Replicas: Read-heavy workloads
- Sharding: Write-heavy, large datasets
- Hybrid: Complex, mixed workloads

## Complexity Analysis

### Time Complexity

**Vertical Scaling: O(1)**
- Single server
- No routing overhead
- Simple

**Read Replicas: O(1)**
- Single replica selection
- Constant time routing
- Simple

**Sharding: O(1)**
- Hash computation
- Constant time routing
- Simple

**Cross-Shard Query: O(n)**
- n = number of shards
- Query all shards
- Aggregate results

### Space Complexity

**Vertical Scaling: O(n)**
- n = data size
- Single server storage
- Linear with data

**Read Replicas: O(n * m)**
- n = data size
- m = number of replicas
- Linear with replicas

**Sharding: O(n)**
- n = data size
- Distributed across shards
- Linear with data

**Explanation:**
Vertical scaling is O(1) time complexity - single server, no routing. Read replicas are O(1) - single replica selection. Sharding is O(1) - hash computation. Cross-shard queries are O(n) where n is the number of shards. Space complexity for vertical scaling is O(n) where n is data size. Read replicas are O(n * m) where m is the number of replicas. Sharding is O(n) distributed across shards. The trade-off is between complexity and scalability.

## Real-world Applications

### 1. E-commerce

**User Data Sharding:**
- Shard by user ID
- Distribute user load
- Example: Amazon, Shopify

### 2. Social Media

**Post Sharding:**
- Shard by user or region
- Handle high write load
- Example: Facebook, Twitter

### 3. Analytics

**Time-Series Partitioning:**
- Partition by time
- Efficient time-range queries
- Example: Google Analytics

### 4. Gaming

**Player Data Sharding:**
- Shard by player ID
- Distribute game load
- Example: Multiplayer games

### 5. IoT

**Device Data Sharding:**
- Shard by device ID
- Handle high device count
- Example: Smart home platforms

### 6. Financial

**Transaction Sharding:**
- Shard by account or time
- Handle high transaction volume
- Example: Banking systems

### 7. Content Delivery

**Content Sharding:**
- Shard by content type or region
- Distribute content load
- Example: Netflix, YouTube

### 8. SaaS

**Tenant Sharding:**
- Shard by tenant ID
- Multi-tenant isolation
- Example: Salesforce

## Common Mistakes

### 1. Wrong Scaling Approach

**Mistake:**
```javascript
// Use vertical scaling when horizontal needed
- Hit hardware limits
// Poor scalability
```

**Correct:**
```javascript
// Choose appropriate scaling approach
- Vertical for small, horizontal for large
// Better scalability
```

**Why It Matters:**
- Wrong approach = poor scalability
- Vertical has hardware limits
- Match approach to needs

### 2. Poor Shard Key

**Mistake:**
```javascript
// Use low-cardinality shard key
- Uneven distribution
// Poor performance
```

**Correct:**
```javascript
// Use high-cardinality, evenly distributed key
- Balanced distribution
// Better performance
```

**Why It Matters:**
- Poor shard key = uneven distribution
- Some shards overloaded
- Good key essential

### 3. Ignoring Replication Lag

**Mistake:**
```javascript
// Don't monitor replication lag
- Stale data read
// Incorrect results
```

**Correct:**
```javascript
// Monitor replication lag
- Route recent reads to primary
// Better consistency
```

**Why It Matters:**
- Replication lag = stale data
- Incorrect results for users
- Monitoring essential

### 4. No Connection Pooling

**Mistake:**
```javascript
// Create new connection per query
- High overhead
// Poor performance
```

**Correct:**
```javascript
// Use connection pooling
- Reuse connections
// Better performance
```

**Why It Matters:**
- No pooling = high overhead
- Poor performance
- Pooling essential

### 5. Not Planning for Failover

**Mistake:**
```javascript
// No failover mechanism
- Downtime on failure
// Poor availability
```

**Correct:**
```javascript
// Implement automatic failover
- High availability
// Better reliability
```

**Why It Matters:**
- No failover = downtime
- Poor availability
- Failover essential

### 6. Over-Sharding

**Mistake:**
```javascript
// Too many shards
- Complex management
// Poor performance
```

**Correct:**
```javascript
// Use appropriate number of shards
- Balance complexity and performance
// Better management
```

**Why It Matters:**
- Too many shards = complex
- Management overhead
- Balance is key

## Advanced Concepts

### 1. Geo-Distributed Replication

**Concept:**
Replicas in different regions.

**Features:**
- Low latency for local users
- Disaster recovery
- Compliance requirements

### 2. Multi-Master Replication

**Concept:**
Multiple write primaries.

**Features:**
- Higher write throughput
- Conflict resolution
- Complex consistency

### 3. Auto-Sharding

**Concept:**
Automatic shard management.

**Features:**
- Dynamic scaling
- Automatic rebalancing
- Reduced operational overhead

### 4. Distributed Transactions

**Concept:**
Transactions across shards.

**Features:**
- Two-phase commit
- Saga pattern
- Eventual consistency

## Practice Thinking Guide

### How to Design Database Scaling Strategy

**Key Questions to Ask:**

1. **Vertical or horizontal?**
   - Vertical for small, simple
   - Horizontal for large, complex
   - Example: "Vertical for startup, horizontal for scale"

2. **Read replicas or sharding?**
   - Read replicas for read-heavy
   - Sharding for write-heavy
   - Example: "Read replicas for analytics, sharding for user data"

3. **What shard key?**
   - High cardinality
   - Even distribution
   - Example: "User ID, region, time"

4. **How many replicas/shards?**
   - Based on capacity needs
   - Cost considerations
   - Example: "3 replicas for 3x read capacity"

5. **How to handle failover?**
   - Automatic failover
   - Health checks
   - Example: "Automatic failover with health checks"

**Pattern Recognition:**

**Pattern 1: Read-Heavy Workload**
```
Requirements: High read, low write
Solution: Read replicas
Implementation: Primary + multiple replicas
```

**Pattern 2: Write-Heavy Workload**
```
Requirements: High write, high data volume
Solution: Sharding
Implementation: Hash-based sharding on user ID
```

**Pattern 3: Global Application**
```
Requirements: Global users, low latency
Solution: Geo-distributed replicas
Implementation: Replicas in multiple regions
```

**Pattern 4: Time-Series Data**
```
Requirements: Time-based queries
Solution: Time-based partitioning
Implementation: Partition by date/time
```

**Pattern 5: Multi-Tenant SaaS**
```
Requirements: Tenant isolation
Solution: Tenant-based sharding
Implementation: Shard by tenant ID
```

**Decision Flowchart:**

```
Database Scaling Decision:
├─ Read-heavy or write-heavy?
│        ├─ Read-heavy → Read replicas
│        └─ Write-heavy → Sharding
├─ Global or local?
│        ├─ Global → Geo-distributed
│        └─ Local → Single region
├─ Data size?
│        ├─ Small → Vertical scaling
│        └─ Large → Horizontal scaling
└─ Consistency requirements?
         ├─ Strong → Synchronous replication
         └─ Eventual → Asynchronous replication
```

**Example Analysis:**

**Scenario:** "Design scaling for e-commerce platform"

**Analysis:**
1. Workload: Read-heavy (product browsing), some writes (orders)
2. Solution: Read replicas for products, sharding for orders
3. Shard key: User ID for orders
4. Replicas: 3-5 replicas for product data
5. Failover: Automatic failover for high availability
6. Implementation: Hybrid approach

**Scenario:** "Design scaling for social media platform"

**Analysis:**
1. Workload: Write-heavy (posts, likes), read-heavy (feed)
2. Solution: Sharding for user data, read replicas for content
3. Shard key: User ID for user data
4. Replicas: Multiple replicas for content
5. Failover: Multi-region for global users
6. Implementation: Geo-distributed sharding

## Summary

Database scaling increases database capacity to handle growing data volumes and traffic. Two main approaches are vertical scaling (scale up - adding more resources to a single server) and horizontal scaling (scale out - adding more servers). Vertical scaling is simpler but has hardware limits and can be expensive. Horizontal scaling is more complex but offers unlimited scalability. Horizontal scaling techniques include read replicas (copying data for read operations), sharding (splitting data across servers), and partitioning (dividing tables into smaller pieces). Read replicas improve read performance by distributing read queries across multiple copies of the data. Sharding distributes both read and write load by splitting data based on a shard key. Consistent hashing is used to minimize data movement when adding or removing shards. The choice between vertical and horizontal scaling depends on the use case, budget, and complexity tolerance.

**Key Takeaways:**
- Vertical scaling has hardware limits
- Horizontal scaling is unlimited but complex
- Read replicas for read-heavy workloads
- Sharding for write-heavy workloads
- Consistent hashing minimizes data movement
- Monitor replication lag
- Choose appropriate shard key
- Implement failover for high availability

**Mastery Checklist:**
- ✅ Understand vertical vs horizontal scaling
- ✅ Implement read replicas
- ✅ Implement sharding
- ✅ Use consistent hashing
- ✅ Handle replication lag
- ✅ Choose appropriate shard key
- ✅ Implement connection pooling
- ✅ Design for high availability

