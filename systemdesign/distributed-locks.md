# Distributed Locks

Distributed locks provide mutual exclusion across multiple nodes in a distributed system, ensuring only one node can access a shared resource at a time.

## Introduction

Distributed locks provide mutual exclusion across multiple nodes in a distributed system, ensuring only one node can access a shared resource at a time. In a distributed system where multiple processes or nodes need to access shared resources (like databases, files, or external APIs), distributed locks prevent race conditions and ensure data consistency. Unlike local locks (mutexes) that work within a single process, distributed locks work across multiple machines connected over a network. Common implementations include Redis-based locks (using SET with NX and EX options), ZooKeeper-based locks (using ephemeral znodes), and database-based locks (using SELECT FOR UPDATE). Distributed locks must handle challenges like network failures, node crashes, clock drift, and split-brain scenarios. Key features include lock acquisition with expiry (TTL) to prevent deadlocks, fencing tokens to prevent split-brain, and lock renewal for long-running operations. Distributed locks are essential for resource reservation, job scheduling, inventory management, and rate limiting in distributed systems.

**Why Distributed Locks Matter:**
- Prevents race conditions across nodes
- Ensures data consistency
- Coordinates resource access
- Prevents duplicate processing
- Essential for distributed systems
- Critical for high availability

**Where It Is Used:**
- Resource reservation (tickets, inventory)
- Job scheduling (cron jobs, task queues)
- Leader election (coordinator selection)
- Rate limiting (API throttling)
- Cache invalidation (coordinated cache updates)
- Distributed transactions

## Core Concept Explanation

Distributed locks provide mutual exclusion across multiple nodes in a distributed system. When a node needs to access a shared resource, it first acquires a lock from a distributed lock service (like Redis, ZooKeeper, or a database). If the lock is available, the node acquires it and proceeds to access the resource. Other nodes attempting to acquire the same lock will wait or fail. After the node finishes using the resource, it releases the lock, allowing other nodes to acquire it. To prevent deadlocks (where a node crashes while holding the lock), locks are acquired with a TTL (time-to-live) - if the lock isn't released within the TTL, it automatically expires. Fencing tokens are used to prevent split-brain scenarios where a node thinks it still holds the lock after a network partition. Lock renewal allows long-running operations to extend the lock duration before it expires. The Redlock algorithm uses multiple Redis instances to improve reliability and safety.

**Step-by-Step Breakdown:**
1. Node requests lock from lock service
2. Lock service checks if lock is available
3. If available, grant lock with unique identifier and TTL
4. Node holds lock identifier
5. Node accesses shared resource
6. Node releases lock when done
7. Lock service verifies identifier
8. If valid, release lock
9. If lock expires, automatic release

**Intuition Behind the Concept:**
Think of distributed locks like a bathroom key in a shared house. Only one person can have the key at a time. If someone takes the key, others must wait. If someone forgets to return the key (crashes), the key automatically returns after a timeout (TTL). To prevent someone from using an old key after a timeout, each key has a unique identifier (fencing token) that's checked before allowing access.

**Visual Thinking:**
```
Lock Acquisition Flow:
Node 1 → Lock Service → Lock Available?
         ↓                    ↓
    Request Lock           Grant Lock
         ↓                    ↓
    Get Identifier      Set with TTL
         ↓                    ↓
    Access Resource    Other Nodes Wait

Lock Release Flow:
Node 1 → Lock Service → Verify Identifier
         ↓                    ↓
    Release Lock       Check Identifier
         ↓                    ↓
    Identifier OK?    Release Lock
         ↓                    ↓
    Lock Released     Other Nodes Can Acquire
```

## Internal Working / Logic

Distributed locks operate through a lock service that manages lock state across multiple nodes. When a node requests a lock, the lock service checks if the lock is available. If available, it grants the lock with a unique identifier (like a UUID) and sets a TTL. The node must provide this identifier when releasing the lock to ensure it's the rightful owner. This prevents a node from accidentally releasing a lock it doesn't own. The TTL ensures that if a node crashes while holding the lock, the lock automatically expires after the TTL, preventing deadlocks. For long-running operations, the node can renew (extend) the lock before it expires. Fencing tokens are used to prevent split-brain scenarios where a node thinks it still holds the lock after a network partition - each operation is tagged with a monotonically increasing token, and the resource rejects operations with old tokens. The Redlock algorithm improves safety by requiring the lock to be acquired from a majority of independent Redis instances.

**Operation 1: Lock Acquisition**
- Node generates unique identifier
- Node requests lock from lock service
- Lock service checks if lock is available
- If available, set lock with identifier and TTL
- Return success to node
- If not available, return failure or wait
- Node may retry with backoff

**Operation 2: Lock Release**
- Node sends release request with identifier
- Lock service verifies identifier matches
- If matches, delete lock
- Return success
- If doesn't match, return failure
- Lock remains held by rightful owner

**Operation 3: Lock Renewal**
- Node sends renewal request with identifier
- Lock service verifies identifier matches
- If matches, extend TTL
- Return success
- If doesn't match, return failure
- Lock may have expired or owned by another

**Operation 4: Lock Expiry**
- TTL expires
- Lock service automatically removes lock
- Lock becomes available
- Other nodes can acquire
- Prevents deadlock from crashes

**Flow Explanation (Redis Lock):**
1. Node generates unique identifier (UUID)
2. Node executes SET lock_name identifier NX EX ttl
3. Redis checks if lock_name exists
4. If not exists, set with identifier and TTL
5. Return OK (success) to node
6. Node accesses shared resource
7. Node executes Lua script to release
8. Redis checks if value matches identifier
9. If matches, delete key
10. Return success to node

**Decision Making Logic:**
The key decisions are:
- Which lock service to use (Redis, ZooKeeper, database)
- What TTL to set (based on operation duration)
- Whether to use fencing tokens (split-brain prevention)
- Whether to use Redlock (multi-instance safety)
- How to handle lock acquisition failures (retry, wait)
- How to handle lock renewal (automatic, manual)

## Algorithm / Approach

**Simple Lock Acquisition Algorithm**

```
1. Generate unique identifier
2. Try to set lock with identifier and TTL
3. If successful, lock acquired
4. If failed, wait and retry
5. After retry attempts, give up
6. Return success or failure
```

**Lock Release Algorithm**

```
1. Send release request with identifier
2. Verify identifier matches lock owner
3. If matches, delete lock
4. Return success
5. If doesn't match, return failure
6. Lock remains held
```

**Lock Renewal Algorithm**

```
1. Send renewal request with identifier
2. Verify identifier matches lock owner
3. If matches, extend TTL
4. Return success
5. If doesn't match, return failure
6. Lock may have expired
```

**Redlock Algorithm**

```
1. Get current timestamp
2. Try to acquire lock on N/2 + 1 Redis instances
3. Use same identifier and TTL on all instances
4. If acquired from majority, lock acquired
5. Record acquisition time
6. If not acquired from majority, release all
7. Calculate lock validity time
8. Ensure lock validity time > 0
9. Return success or failure
```

## Implementations

### 1. Redis Distributed Lock

```javascript
const crypto = require('crypto');

class RedisLock {
  constructor(redisClient, lockName, expiry = 10) {
    this.redis = redisClient;
    this.lockName = lockName;
    this.expiry = expiry;
    this.identifier = crypto.randomUUID();
  }
  
  async acquire() {
    // Try to acquire lock with expiry
    // NX: Only set if key doesn't exist
    // EX: Set expiry in seconds
    const acquired = await this.redis.set(
      this.lockName,
      this.identifier,
      'NX',
      'EX',
      this.expiry
    );
    return acquired === 'OK';
  }
  
  async release() {
    // Only release if we own the lock
    // Lua script ensures atomicity
    const luaScript = `
      if redis.call("get", KEYS[1]) == ARGV[1] then
        return redis.call("del", KEYS[1])
      else
        return 0
      end
    `;
    return await this.redis.eval(luaScript, 1, this.lockName, this.identifier);
  }
  
  async extend(additionalTime) {
    // Extend lock expiry
    const luaScript = `
      if redis.call("get", KEYS[1]) == ARGV[1] then
        return redis.call("expire", KEYS[1], ARGV[2])
      else
        return 0
      end
    `;
    return await this.redis.eval(luaScript, 1, this.lockName, this.identifier, additionalTime);
  }
  
  async acquireWithRetry(maxRetries = 3, retryDelay = 100) {
    for (let i = 0; i < maxRetries; i++) {
      const acquired = await this.acquire();
      if (acquired) {
        return true;
      }
      await new Promise(resolve => setTimeout(resolve, retryDelay));
    }
    return false;
  }
}

// Usage
const redis = require('redis').createClient();
const lock = new RedisLock(redis, 'resource:123', 10);

// Acquire lock
const acquired = await lock.acquireWithRetry();
if (acquired) {
  try {
    // Access shared resource
    console.log('Lock acquired, accessing resource');
    // Do work...
  } finally {
    // Release lock
    await lock.release();
    console.log('Lock released');
  }
}
```

**Advantages:**
- Simple implementation
- Fast performance
- Automatic expiry
- Widely used

### 2. Redlock Implementation

```javascript
class Redlock {
  constructor(redisClients, lockName, expiry = 10) {
    this.redisClients = redisClients;
    this.lockName = lockName;
    this.expiry = expiry;
    this.identifier = crypto.randomUUID();
    this.quorum = Math.floor(redisClients.length / 2) + 1;
  }
  
  async acquire() {
    const startTime = Date.now();
    const acquiredCount = 0;
    
    // Try to acquire lock on all Redis instances
    const promises = this.redisClients.map(async (redis) => {
      try {
        const result = await redis.set(
          this.lockName,
          this.identifier,
          'NX',
          'PX',
          this.expiry * 1000 // milliseconds
        );
        return result === 'OK';
      } catch (error) {
        return false;
      }
    });
    
    const results = await Promise.all(promises);
    const successfulAcquisitions = results.filter(r => r).length;
    
    // Check if we acquired majority
    if (successfulAcquisitions >= this.quorum) {
      const elapsedTime = Date.now() - startTime;
      const validityTime = this.expiry * 1000 - elapsedTime;
      
      if (validityTime > 0) {
        return { success: true, validityTime };
      }
    }
    
    // Release all locks if not acquired majority
    await this.release();
    return { success: false };
  }
  
  async release() {
    const luaScript = `
      if redis.call("get", KEYS[1]) == ARGV[1] then
        return redis.call("del", KEYS[1])
      else
        return 0
      end
    `;
    
    const promises = this.redisClients.map(async (redis) => {
      try {
        await redis.eval(luaScript, 1, this.lockName, this.identifier);
      } catch (error) {
        // Ignore errors during release
      }
    });
    
    await Promise.all(promises);
  }
}

// Usage
const redisClients = [
  require('redis').createClient({ host: 'redis1' }),
  require('redis').createClient({ host: 'redis2' }),
  require('redis').createClient({ host: 'redis3' })
];
const redlock = new Redlock(redisClients, 'resource:123', 10);

const result = await redlock.acquire();
if (result.success) {
  try {
    console.log('Lock acquired');
    // Do work...
  } finally {
    await redlock.release();
  }
}
```

**Advantages:**
- Multi-instance safety
- Fault tolerance
- Better reliability
- Prevents single point of failure

### 3. ZooKeeper Distributed Lock

```javascript
class ZooKeeperLock {
  constructor(zkClient, lockPath) {
    this.zk = zkClient;
    this.lockPath = lockPath;
    this.currentNode = null;
  }
  
  async acquire() {
    // Create ephemeral sequential node
    const nodeName = `${this.lockPath}/lock-`;
    this.currentNode = await this.zk.create(nodeName, '', {
      ephemeral: true,
      sequence: true
    });
    
    // Get all children
    const children = await this.zk.getChildren(this.lockPath);
    children.sort();
    
    // Check if we are the smallest node
    if (this.currentNode === children[0]) {
      return true; // Lock acquired
    }
    
    // Wait for previous node to be deleted
    const previousNode = children[children.indexOf(this.currentNode) - 1];
    await this.waitForNodeDeletion(previousNode);
    
    // Check again if we are the smallest
    const newChildren = await this.zk.getChildren(this.lockPath);
    newChildren.sort();
    return this.currentNode === newChildren[0];
  }
  
  async waitForNodeDeletion(nodePath) {
    return new Promise((resolve, reject) => {
      const watcher = () => {
        this.zk.exists(nodePath, watcher, (error, stat) => {
          if (error || !stat) {
            resolve();
          }
        });
      };
      watcher();
    });
  }
  
  async release() {
    if (this.currentNode) {
      await this.zk.delete(this.currentNode);
      this.currentNode = null;
    }
  }
}

// Usage
const ZooKeeper = require('node-zookeeper-client');
const zk = ZooKeeper.createClient('localhost:2181');
const lock = new ZooKeeperLock(zk, '/locks/resource-123');

await lock.acquire();
try {
  console.log('Lock acquired');
  // Do work...
} finally {
  await lock.release();
}
```

**Advantages:**
- Strong consistency
- Automatic cleanup on disconnect
- Ordered node creation
- Good for leader election

### 4. Database Distributed Lock

```javascript
class DatabaseLock {
  constructor(pool, lockName, expiry = 10) {
    this.pool = pool;
    this.lockName = lockName;
    this.expiry = expiry;
    this.identifier = crypto.randomUUID();
  }
  
  async acquire() {
    const query = `
      INSERT INTO distributed_locks (lock_name, identifier, expires_at)
      VALUES ($1, $2, NOW() + INTERVAL '${this.expiry} seconds')
      ON CONFLICT (lock_name) DO NOTHING
      RETURNING identifier
    `;
    
    const result = await this.pool.query(query, [this.lockName, this.identifier]);
    return result.rows.length > 0 && result.rows[0].identifier === this.identifier;
  }
  
  async release() {
    const query = `
      DELETE FROM distributed_locks
      WHERE lock_name = $1 AND identifier = $2
    `;
    
    const result = await this.pool.query(query, [this.lockName, this.identifier]);
    return result.rowCount > 0;
  }
  
  async extend(additionalTime) {
    const query = `
      UPDATE distributed_locks
      SET expires_at = NOW() + INTERVAL '${additionalTime} seconds'
      WHERE lock_name = $1 AND identifier = $2
      RETURNING identifier
    `;
    
    const result = await this.pool.query(query, [this.lockName, this.identifier]);
    return result.rows.length > 0;
  }
  
  async cleanupExpired() {
    const query = `
      DELETE FROM distributed_locks
      WHERE expires_at < NOW()
    `;
    
    await this.pool.query(query);
  }
}

// Usage
const { Pool } = require('pg');
const pool = new Pool({ connectionString: 'postgres://localhost/db' });
const lock = new DatabaseLock(pool, 'resource:123', 10);

const acquired = await lock.acquire();
if (acquired) {
  try {
    console.log('Lock acquired');
    // Do work...
  } finally {
    await lock.release();
  }
}
```

**Advantages:**
- Uses existing database
- Persistent storage
- Transaction support
- No additional infrastructure

### 5. Fencing Token Implementation

```javascript
class FencingTokenLock {
  constructor(redisClient, lockName, expiry = 10) {
    this.redis = redisClient;
    this.lockName = lockName;
    this.expiry = expiry;
    this.identifier = crypto.randomUUID();
    this.token = 0;
  }
  
  async acquire() {
    // Increment fencing token
    this.token = await this.redis.incr(`${this.lockName}:token`);
    
    // Acquire lock with token
    const acquired = await this.redis.set(
      this.lockName,
      JSON.stringify({ identifier: this.identifier, token: this.token }),
      'NX',
      'EX',
      this.expiry
    );
    
    return acquired === 'OK';
  }
  
  async release() {
    const luaScript = `
      local data = redis.call("get", KEYS[1])
      if data then
        local parsed = cjson.decode(data)
        if parsed.identifier == ARGV[1] then
          return redis.call("del", KEYS[1])
        end
      end
      return 0
    `;
    
    return await this.redis.eval(luaScript, 1, this.lockName, this.identifier);
  }
  
  getToken() {
    return this.token;
  }
  
  async validateToken(token) {
    const data = await this.redis.get(this.lockName);
    if (data) {
      const parsed = JSON.parse(data);
      return parsed.token >= token;
    }
    return false;
  }
}

// Usage
const lock = new FencingTokenLock(redis, 'resource:123', 10);

await lock.acquire();
const token = lock.getToken();

// Use token when accessing resource
await resource.doSomething({ fencingToken: token });
```

**Advantages:**
- Prevents split-brain
- Monotonically increasing tokens
- Resource can reject old operations
- Better safety guarantees

## Dry Run

**Example: Redis Lock Acquisition**

**Initial State:**
```
Lock: Not acquired
Redis: No lock key
Node 1: Requests lock
Node 2: Requests lock
```

**Step-by-Step Execution:**

```
Step 1: Node 1 generates identifier (uuid-1)
Step 2: Node 1 executes SET lock:123 uuid-1 NX EX 10
Step 3: Redis checks if lock:123 exists
Step 4: lock:123 doesn't exist
Step 5: Redis sets lock:123 = uuid-1 with TTL 10s
Step 6: Redis returns OK to Node 1
Step 7: Node 1 has lock, accesses resource

Step 8: Node 2 generates identifier (uuid-2)
Step 9: Node 2 executes SET lock:123 uuid-2 NX EX 10
Step 10: Redis checks if lock:123 exists
Step 11: lock:123 exists (held by uuid-1)
Step 12: Redis returns nil to Node 2
Step 13: Node 2 lock acquisition fails
Step 14: Node 2 waits and retries

Step 15: Node 1 finishes, executes release Lua script
Step 16: Redis checks if lock:123 value == uuid-1
Step 17: Values match
Step 18: Redis deletes lock:123
Step 19: Redis returns 1 to Node 1
Step 20: Lock released

Step 21: Node 2 retries lock acquisition
Step 22: Node 2 executes SET lock:123 uuid-2 NX EX 10
Step 23: Redis checks if lock:123 exists
Step 24: lock:123 doesn't exist
Step 25: Redis sets lock:123 = uuid-2 with TTL 10s
Step 26: Redis returns OK to Node 2
Step 27: Node 2 has lock, accesses resource
```

**Request/Response Table:**

| Step | Node | Action | Redis Response | Status |
|------|------|--------|---------------|--------|
| 1 | Node 1 | Generate uuid-1 | - | - |
| 2 | Node 1 | SET lock:123 uuid-1 NX EX 10 | OK | Lock acquired |
| 3 | Node 2 | Generate uuid-2 | - | - |
| 4 | Node 2 | SET lock:123 uuid-2 NX EX 10 | nil | Failed |
| 5 | Node 1 | Release with uuid-1 | 1 | Released |
| 6 | Node 2 | SET lock:123 uuid-2 NX EX 10 | OK | Lock acquired |

## Edge Cases

### 1. Node Crash with Lock
```javascript
// Node crashes while holding lock
- Lock not released
// Solution: TTL ensures automatic expiry
```

### 2. Network Partition
```javascript
// Node isolated from lock service
- Cannot release lock
// Solution: TTL ensures automatic expiry
```

### 3. Clock Drift
```javascript
// Clocks out of sync
- TTL不准确
// Solution: Use lock service time, not local time
```

### 4. Split-Brain Scenario
```javascript
// Node thinks it still has lock after expiry
- Multiple nodes access resource
// Solution: Fencing tokens
```

### 5. Lock Service Failure
```javascript
// Lock service unavailable
- Cannot acquire locks
// Solution: Redlock with multiple instances
```

### 6. Long-Running Operation
```javascript
// Operation longer than TTL
- Lock expires during operation
// Solution: Lock renewal
```

**Why Edge Cases Matter:**
- Node crash causes deadlock without TTL
- Network partition prevents lock release
- Clock drift affects TTL accuracy
- Split-brain causes data corruption
- Lock service failure prevents coordination
- Long operations need lock renewal

## Variations / Extensions

### 1. Read-Write Locks

```javascript
// Multiple readers, single writer
- Better concurrency
// Example: Cache updates
```

### 2. Fair Locks

```javascript
// FIFO order for lock acquisition
- Prevents starvation
// Example: Job queues
```

### 3. Reentrant Locks

```javascript
// Same node can reacquire
- Recursive locking
// Example: Nested operations
```

### 4. Shared Locks

```javascript
// Multiple nodes can hold lock
- For read operations
// Example: Distributed reads
```

### 5. Lease-based Locks

```javascript
// Time-based ownership
- Automatic expiry
// Example: Resource leases
```

## Optimization Techniques

### 1. Lock Renewal

**Extend Lock Duration:**
```javascript
// Renew lock before expiry
- For long operations
// Prevents lock expiry
```

### 2. Backoff Retry

**Exponential Backoff:**
```javascript
// Retry with increasing delay
- Reduce contention
// Better performance
```

### 3. Lock Pooling

**Pool of Locks:**
```javascript
// Multiple locks for resources
- Reduce contention
// Better throughput
```

### 4. Asynchronous Release

**Non-blocking Release:**
```javascript
// Release asynchronously
- Faster operation
// Better performance
```

### 5. Trade-offs

**Lock Service Comparison:**

| Service | Performance | Reliability | Complexity | Use Case |
|---------|-------------|-------------|------------|----------|
| Redis | High | Medium | Low | General purpose |
| ZooKeeper | Medium | High | High | Strong consistency |
| Database | Low | High | Medium | Existing infrastructure |
| Redlock | Medium | High | High | High reliability |

**When to Use Each:**
- Redis: General purpose, high performance
- ZooKeeper: Strong consistency required
- Database: Existing infrastructure, no new deps
- Redlock: High reliability, fault tolerance

## Complexity Analysis

### Time Complexity

**Lock Acquisition: O(1)**
- Single SET operation
- Constant time
- Fast

**Lock Release: O(1)**
- Single Lua script execution
- Constant time
- Fast

**Redlock Acquisition: O(n)**
- n = number of Redis instances
- Parallel operations
- Majority required

### Space Complexity

**Lock Storage: O(1)**
- Single key per lock
- Constant space
- Minimal

**Explanation:**
Redis lock acquisition is O(1) - single SET operation. Lock release is O(1) - single Lua script execution. Redlock acquisition is O(n) where n is the number of Redis instances, but operations are parallel. Space complexity is O(1) - single key per lock with minimal storage. The trade-off is between performance (Redis) and reliability (Redlock, ZooKeeper).

## Real-world Applications

### 1. Resource Reservation

**Ticket Booking:**
- Prevent overselling
- Ensure one ticket per person
- Example: Concert tickets

### 2. Job Scheduling

**Cron Jobs:**
- Prevent duplicate execution
- Single instance runs
- Example: Scheduled tasks

### 3. Inventory Management

**Stock Control:**
- Prevent overselling
- Accurate inventory
- Example: E-commerce

### 4. Leader Election

**Coordinator Selection:**
- Single leader
- Failover support
- Example: Cluster coordination

### 5. Rate Limiting

**API Throttling:**
- Limit request rate
- Prevent abuse
- Example: API protection

### 6. Cache Invalidation

**Coordinated Updates:**
- Single updater
- Prevent cache stampede
- Example: Distributed cache

### 7. Distributed Transactions

**Two-Phase Commit:**
- Coordinate participants
- Ensure consistency
- Example: Cross-service transactions

### 8. File Operations

**File Access:**
- Prevent concurrent writes
- Ensure data integrity
- Example: Shared file systems

## Common Mistakes

### 1. No TTL

**Mistake:**
```javascript
// Lock without expiry
- Node crashes, deadlock
// Poor availability
```

**Correct:**
```javascript
// Set TTL on lock
- Automatic expiry
// Better availability
```

**Why It Matters:**
- No TTL = deadlock on crash
- Poor availability
- TTL essential

### 2. No Identifier Verification

**Mistake:**
```javascript
// Release without verifying owner
- Release wrong lock
// Data corruption
```

**Correct:**
```javascript
// Verify identifier before release
- Safe release
// Better safety
```

**Why It Matters:**
- No verification = release wrong lock
- Data corruption
- Verification essential

### 3. No Fencing Tokens

**Mistake:**
```javascript
// No fencing tokens
- Split-brain possible
// Data corruption
```

**Correct:**
```javascript
// Use fencing tokens
- Prevent split-brain
// Better safety
```

**Why It Matters:**
- No fencing = split-brain
- Data corruption
- Fencing essential

### 4. No Lock Renewal

**Mistake:**
```javascript
// Long operation, no renewal
- Lock expires during operation
// Race condition
```

**Correct:**
```javascript
// Renew lock for long operations
- Prevent expiry
// Better safety
```

**Why It Matters:**
- No renewal = lock expires
- Race condition
- Renewal essential

### 5. Single Point of Failure

**Mistake:**
```javascript
// Single Redis instance
- Lock service failure
// No coordination
```

**Correct:**
```javascript
// Use Redlock or ZooKeeper
- Multiple instances
// Better reliability
```

**Why It Matters:**
- Single instance = SPOF
- Lock service failure
- Redundancy essential

### 6. Ignoring Clock Drift

**Mistake:**
```javascript
// Use local time for TTL
- Clock drift affects accuracy
// Lock expiry issues
```

**Correct:**
```javascript
// Use lock service time
- Accurate TTL
// Better reliability
```

**Why It Matters:**
- Clock drift = inaccurate TTL
- Lock expiry issues
- Service time essential

## Advanced Concepts

### 1. Read-Write Locks

**Concept:**
Multiple readers, single writer.

**Features:**
- Better read concurrency
- Write exclusivity
- Fairness guarantees

### 2. Fair Locks

**Concept:**
FIFO lock acquisition.

**Features:**
- Prevents starvation
- Ordered acquisition
- Better fairness

### 3. Reentrant Locks

**Concept:**
Same node can reacquire.

**Features:**
- Recursive locking
- Count-based
- Nested operations

### 4. Leases

**Concept:**
Time-based ownership.

**Features:**
- Automatic expiry
- Renewable
- Resource leases

## Practice Thinking Guide

### How to Design Distributed Lock Strategy

**Key Questions to Ask:**

1. **Which lock service?**
   - Redis for performance
   - ZooKeeper for consistency
   - Database for simplicity
   - Example: "Redis for general purpose"

2. **What TTL to set?**
   - Based on operation duration
   - Add safety margin
   - Example: "10s for 5s operation"

3. **Need fencing tokens?**
   - Critical resources
   - Split-brain prevention
   - Example: "Yes for financial transactions"

4. **Need Redlock?**
   - High reliability required
   - Fault tolerance
   - Example: "Yes for critical systems"

5. **How to handle failures?**
   - Retry with backoff
   - Fallback mechanisms
   - Example: "Exponential backoff retry"

**Pattern Recognition:**

**Pattern 1: Resource Reservation**
```
Requirements: Prevent overselling
Solution: Distributed lock with TTL
Implementation: Redis lock with fencing token
```

**Pattern 2: Job Scheduling**
```
Requirements: Single instance execution
Solution: Distributed lock for job
Implementation: ZooKeeper ephemeral node
```

**Pattern 3: Leader Election**
```
Requirements: Single leader
Solution: Distributed lock for leadership
Implementation: Redlock with fencing token
```

**Pattern 4: Inventory Management**
```
Requirements: Accurate inventory
Solution: Lock during update
Implementation: Database lock with transaction
```

**Pattern 5: Cache Invalidation**
```
Requirements: Coordinated cache update
Solution: Lock during cache update
Implementation: Redis lock with short TTL
```

**Decision Flowchart:**

```
Distributed Lock Decision:
├─ Performance or consistency?
│        ├─ Performance → Redis
│        └─ Consistency → ZooKeeper
├─ High reliability?
│        ├─ Yes → Redlock
│        └─ No → Single instance
├─ Critical resource?
│        ├─ Yes → Fencing token
│        └─ No → Simple lock
└─ Long operation?
         ├─ Yes → Lock renewal
         └─ No → Simple TTL
```

**Example Analysis:**

**Scenario:** "Design lock for ticket booking"

**Analysis:**
1. Requirements: Prevent overselling, high reliability
2. Service: Redis with Redlock
3. TTL: 30 seconds (operation time + margin)
4. Fencing token: Yes (critical resource)
5. Renewal: No (short operation)
6. Implementation: Redlock with fencing token

**Scenario:** "Design lock for scheduled job"

**Analysis:**
1. Requirements: Single instance, fault tolerance
2. Service: ZooKeeper (automatic cleanup)
3. TTL: Ephemeral node (auto-cleanup)
4. Fencing token: No (not critical)
5. Renewal: No (short operation)
6. Implementation: ZooKeeper ephemeral node

## Summary

Distributed locks provide mutual exclusion across multiple nodes in a distributed system, ensuring only one node can access a shared resource at a time. Unlike local locks, distributed locks work across multiple machines connected over a network. Common implementations include Redis-based locks (using SET with NX and EX options), ZooKeeper-based locks (using ephemeral znodes), and database-based locks (using SELECT FOR UPDATE). Distributed locks must handle challenges like network failures, node crashes, clock drift, and split-brain scenarios. Key features include lock acquisition with expiry (TTL) to prevent deadlocks, fencing tokens to prevent split-brain, and lock renewal for long-running operations. The Redlock algorithm uses multiple Redis instances to improve reliability and safety. Distributed locks are essential for resource reservation, job scheduling, inventory management, and rate limiting in distributed systems.

**Key Takeaways:**
- Prevents race conditions across nodes
- Ensures data consistency
- Set lock with TTL to prevent deadlock
- Use fencing tokens to prevent split-brain
- Lock renewal for long operations
- Redlock for high reliability
- Choose appropriate lock service
- Handle failures gracefully

**Mastery Checklist:**
- ✅ Understand distributed lock concepts
- ✅ Implement Redis distributed lock
- ✅ Implement Redlock algorithm
- ✅ Use fencing tokens
- ✅ Handle lock renewal
- ✅ Choose appropriate TTL
- ✅ Handle failures gracefully
- ✅ Design for high availability

