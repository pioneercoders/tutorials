# Leader Election

Leader election is a distributed algorithm that selects a special node (leader) from a group of nodes to coordinate operations, ensuring only one leader exists at any time.

## Introduction

Leader election is a distributed algorithm that selects a special node (leader) from a group of nodes to coordinate operations, ensuring only one leader exists at any time. In distributed systems, having a single leader simplifies coordination by centralizing decision-making. The leader is responsible for coordinating operations, managing state, and ensuring consistency. If the leader fails, a new election is held to select a new leader. Common leader election algorithms include the Bully algorithm (highest ID node becomes leader), Raft (term-based voting with majority), and ZooKeeper-based election (using ephemeral nodes). Leader election must handle challenges like split-brain scenarios (multiple leaders due to network partitions), network partitions, leader failure during election, and concurrent elections. Leader election is essential for distributed databases, message queues, coordination services, and cluster management. Key features include fault tolerance (automatic leader recovery), safety (only one leader at a time), and liveness (election always completes).

**Why Leader Election Matters:**
- Enables distributed coordination
- Ensures single point of coordination
- Provides fault tolerance
- Essential for consensus
- Critical for distributed databases
- Foundation for cluster management

**Where It Is Used:**
- Distributed databases (Cassandra, MongoDB)
- Message queues (Kafka, RabbitMQ)
- Coordination services (ZooKeeper, etcd)
- Cluster management (Kubernetes, Docker Swarm)
- Consensus systems (Raft, Paxos)
- Load balancers (HAProxy, Nginx)

## Core Concept Explanation

Leader election selects a single node from a group to act as the coordinator. The leader is responsible for coordinating operations, managing state, and ensuring consistency across the cluster. When a leader fails or becomes unavailable, a new election is held to select a replacement. The Bully algorithm works by having the node with the highest ID become the leader. When a node detects leader failure, it sends election messages to all nodes with higher IDs. If no higher ID node responds, it becomes the leader. Raft uses term-based voting where nodes vote for candidates in election rounds. A candidate needs majority votes to become leader. ZooKeeper-based election uses ephemeral nodes - the node that successfully creates an ephemeral node becomes the leader. If the leader fails, the ephemeral node is deleted, triggering a new election. Leader lease uses time-based leadership where the leader must renew its lease periodically. If the lease expires, a new election is held. The choice of algorithm depends on the use case, cluster size, and requirements.

**Step-by-Step Breakdown:**
1. Cluster starts with no leader
2. Nodes detect no leader
3. One node initiates election
4. Election algorithm runs (Bully, Raft, ZooKeeper)
5. Nodes vote or compete
6. Winner becomes leader
6. Leader coordinates operations
7. If leader fails, new election
8. New leader selected
9. Operations continue with new leader

**Intuition Behind the Concept:**
Think of leader election like electing a team captain. The captain coordinates the team, makes decisions, and ensures everyone works together. If the captain leaves, the team elects a new captain. Different election methods exist: the strongest player becomes captain (Bully), team members vote for captain (Raft), or whoever grabs the captain's badge first (ZooKeeper). The key is having only one captain at a time to avoid confusion.

**Visual Thinking:**
```
Leader Election Flow:
Cluster → No Leader → Election Started → Nodes Vote/Candidate → Winner → Leader Coordinates

Leader Failure:
Leader Fails → Election Triggered → New Election → New Leader → Operations Resume

Split-Brain Prevention:
Network Partition → Quorum Required → Only Partition with Majority Can Elect Leader
```

## Internal Working / Logic

Leader election operates through different algorithms depending on the requirements. The Bully algorithm is simple: the node with the highest ID becomes the leader. When a node detects leader failure, it sends election messages to all nodes with higher IDs. If no higher ID node responds within a timeout, it becomes the leader. If a higher ID node responds, it takes over the election. Raft uses a more sophisticated approach with terms and voting. Nodes start as followers. If a follower doesn't receive heartbeat from the leader within an election timeout, it becomes a candidate and starts an election. The candidate increments its term, votes for itself, and requests votes from other nodes. If it receives majority votes, it becomes the leader. ZooKeeper-based election uses ephemeral nodes. Nodes try to create an ephemeral node in a shared directory. The node that successfully creates the node becomes the leader. If the leader fails, the ephemeral node is automatically deleted by ZooKeeper, and other nodes compete to create it again. Leader lease uses time-based leadership where the leader must periodically renew its lease.

**Operation 1: Bully Election**
- Node detects leader failure
- Node sends election message to higher ID nodes
- Higher ID nodes respond with OK
- If no response within timeout, become leader
- Announce leadership to all nodes
- Lower ID nodes acknowledge

**Operation 2: Raft Election**
- Follower doesn't receive heartbeat
- Follower becomes candidate
- Candidate increments term
- Candidate votes for self
- Candidate requests votes from other nodes
- Nodes vote based on term and log
- If majority votes received, become leader
- Send heartbeats to maintain leadership

**Operation 3: ZooKeeper Election**
- Nodes try to create ephemeral node
- First successful creator becomes leader
- Leader periodically updates node
- If leader fails, node deleted
- Other nodes detect deletion
- New election starts
- New leader emerges

**Operation 4: Leader Lease**
- Leader acquires lease with TTL
- Leader periodically renews lease
- If lease expires, leadership lost
- Other nodes can acquire lease
- New leader emerges
- Old leader steps down

**Flow Explanation (Raft Election):**
1. Node 1 detects no heartbeat from leader
2. Node 1 becomes candidate, increments term to 5
3. Node 1 votes for self (votesReceived = 1)
4. Node 1 sends RequestVote RPC to Node 2, Node 3
5. Node 2 receives RequestVote, votes for Node 1
6. Node 3 receives RequestVote, votes for Node 1
7. Node 1 receives votes (votesReceived = 3)
8. Node 1 has majority (3 > 1.5)
9. Node 1 becomes leader
10. Node 1 sends heartbeats to Node 2, Node 3

**Decision Making Logic:**
The key decisions are:
- Which algorithm to use (Bully, Raft, ZooKeeper)
- Election timeout duration
- Quorum size (majority or supermajority)
- Lease duration (if using lease)
- Heartbeat interval
- Failure detection strategy

## Algorithm / Approach

**Bully Algorithm**

```
1. Node detects leader failure
2. Send election message to all higher ID nodes
3. Wait for responses
4. If all higher ID nodes respond:
   a. Highest ID node becomes leader
   b. Leader announces to all
5. If no response from higher ID nodes:
   a. Become leader
   b. Announce to all
6. If lower ID node initiates election:
   a. Send OK, take over election
```

**Raft Election Algorithm**

```
1. Follower doesn't receive heartbeat within timeout
2. Become candidate
3. Increment term
4. Vote for self
5. Send RequestVote RPC to all other nodes
6. Wait for votes
7. If majority votes received:
   a. Become leader
   b. Send heartbeats
8. If higher term received:
   a. Revert to follower
   b. Vote for higher term candidate
```

**ZooKeeper Election Algorithm**

```
1. Try to create ephemeral node
2. If creation successful:
   a. Become leader
   b. Periodically update node
3. If creation fails (node exists):
   a. Watch node for deletion
   b. Wait for leader failure
4. If node deleted:
   a. Retry creation
   b. Compete for leadership
```

**Leader Lease Algorithm**

```
1. Acquire lease with TTL
2. If successful, become leader
3. Periodically renew lease
4. If lease expires:
   a. Lose leadership
   b. Other nodes can acquire
5. If renewal fails:
   a. Step down
   b. Trigger new election
```

## Implementations

### 1. Bully Algorithm

```javascript
class BullyElection {
  constructor(nodeId, allNodes) {
    this.nodeId = nodeId;
    this.allNodes = allNodes;
    this.leader = null;
    this.timeout = 5000; // 5 seconds
  }
  
  async startElection() {
    const higherNodes = this.allNodes.filter(n => n > this.nodeId);
    
    if (higherNodes.length === 0) {
      this.leader = this.nodeId;
      console.log(`Node ${this.nodeId} is the leader (highest ID)`);
      this.announceLeadership();
      return;
    }
    
    console.log(`Node ${this.nodeId} starting election`);
    const responses = await this.sendElectionMessages(higherNodes);
    
    if (responses.length === 0) {
      this.leader = this.nodeId;
      console.log(`Node ${this.nodeId} became leader (no responses)`);
      this.announceLeadership();
    } else {
      const highestResponder = Math.max(...responses);
      console.log(`Node ${highestResponder} will become leader`);
    }
  }
  
  async sendElectionMessages(nodes) {
    const responses = [];
    const promises = nodes.map(node => 
      this.sendMessage(node, 'ELECTION')
        .then(() => node)
        .catch(() => null)
    );
    
    const results = await Promise.all(promises);
    return results.filter(r => r !== null);
  }
  
  async sendMessage(node, message) {
    // Simulate network message
    return new Promise((resolve, reject) => {
      setTimeout(() => {
        if (Math.random() > 0.3) { // 70% success rate
          resolve();
        } else {
          reject(new Error('Message failed'));
        }
      }, 100);
    });
  }
  
  async receiveElection(senderId) {
    if (senderId > this.nodeId) {
      console.log(`Node ${this.nodeId} received election from ${senderId}, sending OK`);
      await this.sendMessage(senderId, 'OK');
      // Wait for leader announcement
    } else {
      console.log(`Node ${this.nodeId} received election from ${senderId}, taking over`);
      this.startElection();
    }
  }
  
  announceLeadership() {
    console.log(`Node ${this.nodeId} announcing leadership`);
    // Send coordinator message to all nodes
  }
}

// Usage
const nodes = [1, 2, 3, 4, 5];
const bully1 = new BullyElection(1, nodes);
const bully2 = new BullyElection(2, nodes);
const bully5 = new BullyElection(5, nodes);

bully1.startElection(); // Node 5 will become leader
```

**Advantages:**
- Simple to implement
- No additional infrastructure
- Fast election
- Works well for small clusters

### 2. Raft-like Leader Election

```javascript
class RaftNode {
  constructor(nodeId, allNodes) {
    this.nodeId = nodeId;
    this.allNodes = allNodes;
    this.state = 'follower'; // follower, candidate, leader
    this.term = 0;
    this.votesReceived = 0;
    this.votedFor = null;
    this.leaderId = null;
    this.electionTimeout = this.randomTimeout();
    this.heartbeatInterval = 1000;
    this.timer = null;
  }
  
  randomTimeout() {
    return Math.random() * 5000 + 5000; // 5-10 seconds
  }
  
  start() {
    this.resetElectionTimer();
  }
  
  resetElectionTimer() {
    if (this.timer) clearTimeout(this.timer);
    this.timer = setTimeout(() => this.startElection(), this.electionTimeout);
  }
  
  startElection() {
    if (this.state === 'leader') return;
    
    console.log(`Node ${this.nodeId} starting election for term ${this.term + 1}`);
    this.state = 'candidate';
    this.term += 1;
    this.votesReceived = 1; // Vote for self
    this.votedFor = this.nodeId;
    
    // Request votes from other nodes
    for (const node of this.allNodes) {
      if (node !== this.nodeId) {
        this.requestVote(node);
      }
    }
    
    this.resetElectionTimer();
  }
  
  requestVote(targetNode) {
    console.log(`Node ${this.nodeId} requesting vote from ${targetNode}`);
    // In real implementation, send RPC to targetNode
    // Simulate response
    setTimeout(() => {
      this.receiveVote(targetNode, true); // Assume vote granted
    }, 100);
  }
  
  receiveVote(nodeId, voteGranted) {
    if (!voteGranted) return;
    
    this.votesReceived += 1;
    console.log(`Node ${this.nodeId} received vote from ${nodeId}, total: ${this.votesReceived}`);
    
    const majority = Math.floor(this.allNodes.length / 2) + 1;
    if (this.votesReceived >= majority && this.state === 'candidate') {
      this.becomeLeader();
    }
  }
  
  becomeLeader() {
    this.state = 'leader';
    this.leaderId = this.nodeId;
    console.log(`Node ${this.nodeId} became leader for term ${this.term}`);
    
    // Start sending heartbeats
    this.heartbeatTimer = setInterval(() => {
      this.sendHeartbeats();
    }, this.heartbeatInterval);
  }
  
  sendHeartbeats() {
    console.log(`Node ${this.nodeId} sending heartbeats for term ${this.term}`);
    // In real implementation, send AppendEntries RPC to all nodes
  }
  
  receiveHeartbeat(term, leaderId) {
    if (term > this.term) {
      this.term = term;
      this.state = 'follower';
      this.votedFor = null;
    }
    
    this.leaderId = leaderId;
    this.resetElectionTimer();
    console.log(`Node ${this.nodeId} received heartbeat from ${leaderId}, term ${term}`);
  }
  
  stepDown() {
    this.state = 'follower';
    if (this.heartbeatTimer) {
      clearInterval(this.heartbeatTimer);
    }
    console.log(`Node ${this.nodeId} stepping down`);
  }
}

// Usage
const nodes = [1, 2, 3, 4, 5];
const raftNodes = nodes.map(id => new RaftNode(id, nodes));

raftNodes.forEach(node => node.start());
```

**Advantages:**
- Strong consistency
- Majority-based
- Fault tolerant
- Widely used

### 3. ZooKeeper Leader Election

```javascript
class ZooKeeperLeaderElection {
  constructor(nodeId, zkClient, electionPath = '/election') {
    this.nodeId = nodeId;
    this.zk = zkClient;
    this.electionPath = electionPath;
    this.leaderNode = null;
    this.isLeader = false;
  }
  
  async participate() {
    try {
      // Try to create ephemeral sequential node
      const nodeName = `${this.electionPath}/node_`;
      this.leaderNode = await this.zk.create(nodeName, this.nodeId.toString(), {
        ephemeral: true,
        sequence: true
      });
      
      console.log(`Node ${this.nodeId} created election node: ${this.leaderNode}`);
      
      // Check if we are the leader (lowest sequence number)
      const children = await this.zk.getChildren(this.electionPath);
      children.sort();
      
      if (this.leaderNode === `${this.electionPath}/${children[0]}`) {
        this.becomeLeader();
      } else {
        this.watchPreviousNode(children);
      }
    } catch (error) {
      console.error('Election failed:', error);
      // Retry after delay
      setTimeout(() => this.participate(), 1000);
    }
  }
  
  async watchPreviousNode(children) {
    const myIndex = children.findIndex(c => this.leaderNode.includes(c));
    const previousNode = `${this.electionPath}/${children[myIndex - 1]}`;
    
    console.log(`Node ${this.nodeId} watching ${previousNode}`);
    
    // Watch previous node for deletion
    this.zk.exists(previousNode, (event) => {
      if (event.type === 'NODE_DELETED') {
        console.log(`Previous node deleted, re-checking leadership`);
        this.participate();
      }
    });
  }
  
  becomeLeader() {
    this.isLeader = true;
    console.log(`Node ${this.nodeId} is the leader`);
    // Start leading
  }
  
  async resign() {
    if (this.leaderNode) {
      await this.zk.delete(this.leaderNode);
      this.leaderNode = null;
      this.isLeader = false;
      console.log(`Node ${this.nodeId} resigned leadership`);
    }
  }
}

// Usage
const ZooKeeper = require('node-zookeeper-client');
const zk = ZooKeeper.createClient('localhost:2181');
const election = new ZooKeeperLeaderElection('node-1', zk);

election.participate();
```

**Advantages:**
- Automatic failover
- Strong consistency
- Handles network partitions
- Production-ready

### 4. Leader Lease

```javascript
class LeaderLease {
  constructor(nodeId, leaseService, leaseTTL = 10) {
    this.nodeId = nodeId;
    this.leaseService = leaseService;
    this.leaseTTL = leaseTTL;
    this.isLeader = false;
    this.leaseId = null;
    this.renewalTimer = null;
  }
  
  async acquireLease() {
    try {
      this.leaseId = await this.leaseService.acquire(this.nodeId, this.leaseTTL);
      this.isLeader = true;
      console.log(`Node ${this.nodeId} acquired lease: ${this.leaseId}`);
      
      // Start renewal timer
      this.startRenewal();
      return true;
    } catch (error) {
      console.log(`Node ${this.nodeId} failed to acquire lease: ${error.message}`);
      this.isLeader = false;
      // Retry after delay
      setTimeout(() => this.acquireLease(), 1000);
      return false;
    }
  }
  
  startRenewal() {
    const renewalInterval = this.leaseTTL * 1000 / 2; // Renew at half TTL
    
    this.renewalTimer = setInterval(async () => {
      try {
        await this.leaseService.renew(this.leaseId, this.leaseTTL);
        console.log(`Node ${this.nodeId} renewed lease`);
      } catch (error) {
        console.error(`Renewal failed: ${error.message}`);
        this.isLeader = false;
        clearInterval(this.renewalTimer);
        this.acquireLease();
      }
    }, renewalInterval);
  }
  
  async resign() {
    if (this.renewalTimer) {
      clearInterval(this.renewalTimer);
    }
    
    if (this.leaseId) {
      await this.leaseService.release(this.leaseId);
      this.leaseId = null;
      this.isLeader = false;
      console.log(`Node ${this.nodeId} resigned leadership`);
    }
  }
}

// Usage
class LeaseService {
  constructor() {
    this.leases = new Map();
  }
  
  async acquire(nodeId, ttl) {
    if (this.leases.size > 0) {
      throw new Error('Lease already held');
    }
    
    const leaseId = `lease-${Date.now()}`;
    this.leases.set(leaseId, { nodeId, expiry: Date.now() + ttl * 1000 });
    return leaseId;
  }
  
  async renew(leaseId, ttl) {
    const lease = this.leases.get(leaseId);
    if (!lease) {
      throw new Error('Lease not found');
    }
    
    lease.expiry = Date.now() + ttl * 1000;
  }
  
  async release(leaseId) {
    this.leases.delete(leaseId);
  }
}

const leaseService = new LeaseService();
const leaderLease = new LeaderLease('node-1', leaseService, 10);

leaderLease.acquireLease();
```

**Advantages:**
- Time-based leadership
- Prevents split-brain
- Automatic failover
- Simple to implement

### 5. Distributed Lock Leader Election

```javascript
class DistributedLockLeaderElection {
  constructor(nodeId, lockService, lockName = 'leader-lock') {
    this.nodeId = nodeId;
    this.lockService = lockService;
    this.lockName = lockName;
    this.isLeader = false;
    this.lockToken = null;
  }
  
  async elect() {
    try {
      this.lockToken = await this.lockService.acquire(this.lockName, this.nodeId, 10);
      this.isLeader = true;
      console.log(`Node ${this.nodeId} became leader`);
      
      // Start heartbeat
      this.startHeartbeat();
      return true;
    } catch (error) {
      console.log(`Node ${this.nodeId} failed to become leader`);
      this.isLeader = false;
      // Retry after delay
      setTimeout(() => this.elect(), 1000);
      return false;
    }
  }
  
  startHeartbeat() {
    this.heartbeatTimer = setInterval(async () => {
      try {
        await this.lockService.extend(this.lockName, this.lockToken, 10);
        console.log(`Node ${this.nodeId} heartbeat sent`);
      } catch (error) {
        console.error(`Heartbeat failed: ${error.message}`);
        this.isLeader = false;
        clearInterval(this.heartbeatTimer);
        this.elect();
      }
    }, 5000);
  }
  
  async resign() {
    if (this.heartbeatTimer) {
      clearInterval(this.heartbeatTimer);
    }
    
    if (this.lockToken) {
      await this.lockService.release(this.lockName, this.lockToken);
      this.lockToken = null;
      this.isLeader = false;
      console.log(`Node ${this.nodeId} resigned leadership`);
    }
  }
}

// Usage
class LockService {
  constructor() {
    this.locks = new Map();
  }
  
  async acquire(lockName, identifier, ttl) {
    if (this.locks.has(lockName)) {
      throw new Error('Lock already held');
    }
    
    const token = `token-${Date.now()}`;
    this.locks.set(lockName, { identifier, token, expiry: Date.now() + ttl * 1000 });
    return token;
  }
  
  async extend(lockName, token, ttl) {
    const lock = this.locks.get(lockName);
    if (!lock || lock.token !== token) {
      throw new Error('Lock not found or token mismatch');
    }
    
    lock.expiry = Date.now() + ttl * 1000;
  }
  
  async release(lockName, token) {
    const lock = this.locks.get(lockName);
    if (lock && lock.token === token) {
      this.locks.delete(lockName);
    }
  }
}

const lockService = new LockService();
const election = new DistributedLockLeaderElection('node-1', lockService);

election.elect();
```

**Advantages:**
- Uses distributed locks
- Prevents split-brain
- Automatic failover
- Widely available

## Dry Run

**Example: Raft Leader Election**

**Initial State:**
```
Nodes: [1, 2, 3, 4, 5]
State: All followers
Term: 0
Leader: None
```

**Step-by-Step Execution:**

```
Step 1: Node 1 election timeout expires
Step 2: Node 1 becomes candidate, term = 1
Step 3: Node 1 votes for self (votesReceived = 1)
Step 4: Node 1 sends RequestVote to Node 2, 3, 4, 5
Step 5: Node 2 receives RequestVote, votes for Node 1
Step 6: Node 3 receives RequestVote, votes for Node 1
Step 7: Node 4 receives RequestVote, votes for Node 1
Step 8: Node 5 receives RequestVote, votes for Node 1
Step 9: Node 1 receives votes (votesReceived = 5)
Step 10: Node 1 has majority (5 > 2.5)
Step 11: Node 1 becomes leader
Step 12: Node 1 sends heartbeats to all nodes
Step 13: All nodes receive heartbeat, acknowledge Node 1 as leader
```

**Request/Response Table:**

| Step | Node | Action | Response | State |
|------|------|--------|----------|-------|
| 1 | Node 1 | Timeout | - | Candidate |
| 2 | Node 1 | RequestVote to 2,3,4,5 | - | Candidate |
| 3 | Node 2 | Vote for 1 | Granted | Follower |
| 4 | Node 3 | Vote for 1 | Granted | Follower |
| 5 | Node 4 | Vote for 1 | Granted | Follower |
| 6 | Node 5 | Vote for 1 | Granted | Follower |
| 7 | Node 1 | Majority votes | - | Leader |

## Edge Cases

### 1. Split-Brain Scenario
```javascript
// Network partition, multiple leaders
- Inconsistent state
// Solution: Quorum, majority required
```

### 2. Network Partition
```javascript
// Nodes isolated
- Election cannot complete
// Solution: Quorum, wait for partition healing
```

### 3. Leader Failure During Election
```javascript
// Leader crashes while electing
- Election incomplete
// Solution: Timeout, retry election
```

### 4. Concurrent Elections
```javascript
// Multiple nodes start election
- Vote splitting
// Solution: Term-based voting, higher term wins
```

### 5. Clock Drift
```javascript
// Clocks out of sync
- Lease expiration issues
// Solution: Use lease service time
```

### 6. Slow Network
```javascript
// Network delays
- Heartbeat timeout
// Solution: Adjust timeout values
```

**Why Edge Cases Matter:**
- Split-brain causes inconsistency
- Network partition prevents election
- Leader failure causes re-election
- Concurrent elections cause vote splitting
- Clock drift affects lease
- Slow network causes false failures

## Variations / Extensions

### 1. Fast Leader Election

```javascript
// Quick recovery
- Optimized for speed
// Example: High-availability systems
```

### 2. Multi-Leader

```javascript
// Multiple leaders for different partitions
- Better scalability
// Example: Sharded systems
```

### 3. Hierarchical Leader Election

```javascript
// Leaders of leaders
- Better for large clusters
// Example: Large distributed systems
```

### 4. Weighted Election

```javascript
// Nodes have different weights
- Prioritize certain nodes
// Example: Heterogeneous clusters
```

### 5. Lease-Based Election

```javascript
// Time-based leadership
- Prevents split-brain
// Example: Cloud environments
```

## Optimization Techniques

### 1. Optimize Timeouts

**Adjust Election Timeout:**
```javascript
// Balance speed and stability
- Too fast: unnecessary elections
// Too slow: slow recovery
```

### 2. Pre-Vote

**Pre-Vote Before Election:**
```javascript
// Check if can win before election
- Reduce unnecessary elections
// Better stability
```

### 3. Priority-Based Election

**Prioritize Certain Nodes:**
```javascript
// Prefer certain nodes as leader
- Better resource utilization
// Example: Nodes with more resources
```

### 4. Batch Heartbeats

**Send Heartbeats in Batch:**
```javascript
// Reduce network overhead
- Better performance
// Lower latency
```

### 5. Trade-offs

**Algorithm Comparison:**

| Algorithm | Complexity | Speed | Fault Tolerance | Use Case |
|----------|------------|-------|-----------------|----------|
| Bully | Low | Fast | Low | Small clusters |
| Raft | High | Medium | High | General purpose |
| ZooKeeper | Medium | Medium | High | Production |
| Lease | Low | Fast | Medium | Cloud environments |

**When to Use Each:**
- Bully: Small clusters, simple
- Raft: General purpose, strong consistency
- ZooKeeper: Production, high availability
- Lease: Cloud, split-brain prevention

## Complexity Analysis

### Time Complexity

**Bully Algorithm: O(n)**
- n = number of nodes
- Send messages to higher nodes
- Linear with cluster size

**Raft Election: O(n)**
- n = number of nodes
- Request votes from all nodes
- Linear with cluster size

**ZooKeeper: O(1)**
- Single create operation
- Constant time
- Very fast

### Space Complexity

**Bully: O(1)**
- No additional storage
- Constant space
- Minimal

**Raft: O(n)**
- n = number of nodes
- Store votes
- Linear with cluster size

**ZooKeeper: O(1)**
- Single ephemeral node
- Constant space
- Minimal

**Explanation:**
Bully algorithm is O(n) time complexity where n is the number of nodes - sends messages to higher ID nodes. Raft is O(n) where n is the number of nodes - requests votes from all nodes. ZooKeeper is O(1) - single create operation. Space complexity for Bully is O(1) - no additional storage. Raft is O(n) where n is the number of nodes - stores votes. ZooKeeper is O(1) - single ephemeral node. The trade-off is between complexity (Bully) and fault tolerance (Raft, ZooKeeper).

## Real-world Applications

### 1. Distributed Databases

**Cassandra, MongoDB:**
- Coordinate writes
- Example: Master-slave replication

### 2. Message Queues

**Kafka, RabbitMQ:**
- Coordinate consumers
- Example: Partition leaders

### 3. Coordination Services

**ZooKeeper, etcd:**
- Service discovery
- Example: Configuration management

### 4. Cluster Management

**Kubernetes, Docker Swarm:**
- Manage cluster state
- Example: Pod scheduling

### 5. Consensus Systems

**Raft, Paxos:**
- Achieve consensus
- Example: Distributed log

### 6. Load Balancers

**HAProxy, Nginx:**
- Active-passive setup
- Example: High availability

### 7. Distributed Caches

**Redis Cluster:**
- Coordinate cache nodes
- Example: Master-slave setup

### 8. Microservices

**Service Mesh:**
- Coordinate services
- Example: Istio, Consul

## Common Mistakes

### 1. No Quorum

**Mistake:**
```javascript
// Election without quorum
- Split-brain possible
// Inconsistent state
```

**Correct:**
```javascript
// Require majority quorum
- Prevent split-brain
// Better consistency
```

**Why It Matters:**
- No quorum = split-brain
- Inconsistent state
- Quorum essential

### 2. Wrong Timeout Values

**Mistake:**
```javascript
// Timeout too short or long
- Unnecessary elections or slow recovery
// Poor performance
```

**Correct:**
```javascript
// Set appropriate timeouts
- Balance speed and stability
// Better performance
```

**Why It Matters:**
- Wrong timeout = poor performance
- Unnecessary elections
- Appropriate timeout essential

### 3. No Heartbeat

**Mistake:**
```javascript
// No heartbeat mechanism
- Cannot detect leader failure
// Poor availability
```

**Correct:**
```javascript
// Implement heartbeat
- Detect failure quickly
// Better availability
```

**Why It Matters:**
- No heartbeat = slow failure detection
- Poor availability
- Heartbeat essential

### 4. No Lease

**Mistake:**
```javascript
// No lease mechanism
- Split-brain possible
// Inconsistent state
```

**Correct:**
```javascript
// Implement lease
- Prevent split-brain
// Better consistency
```

**Why It Matters:**
- No lease = split-brain risk
- Inconsistent state
- Lease essential

### 5. No Fencing Token

**Mistake:**
```javascript
// No fencing token
- Old leader may still act
// Inconsistent state
```

**Correct:**
```javascript
// Use fencing token
- Prevent old leader actions
// Better consistency
```

**Why It Matters:**
- No fencing = old leader actions
- Inconsistent state
- Fencing essential

### 6. Ignoring Network Partitions

**Mistake:**
```javascript
// No handling for partitions
- Split-brain
// Inconsistent state
```

**Correct:**
```javascript
// Handle partitions with quorum
- Prevent split-brain
// Better consistency
```

**Why It Matters:**
- No partition handling = split-brain
- Inconsistent state
- Quorum essential

## Advanced Concepts

### 1. Raft Consensus

**Concept:**
Distributed consensus algorithm.

**Features:**
- Strong consistency
- Leader election
- Log replication

### 2. Paxos

**Concept:**
Family of consensus algorithms.

**Features:**
- Proven correctness
- Complex implementation
- High fault tolerance

### 3. Multi-Leader

**Concept:**
Multiple leaders for different partitions.

**Features:**
- Better scalability
- Conflict resolution
- Higher availability

### 4. Hierarchical Election

**Concept:**
Leaders of leaders.

**Features:**
- Scalable for large clusters
- Reduced coordination overhead
- Better performance

## Practice Thinking Guide

### How to Design Leader Election Strategy

**Key Questions to Ask:**

1. **Cluster size?**
   - Small: Bully algorithm
   - Large: Raft or ZooKeeper
   - Example: "Raft for 10+ nodes"

2. **Consistency requirements?**
   - Strong: Raft, ZooKeeper
   - Eventual: Bully, Lease
   - Example: "Raft for strong consistency"

3. **Split-brain prevention?**
   - Yes: Quorum, Lease
   - No: Simple election
   - Example: "Quorum for split-brain prevention"

4. **Speed vs stability?**
   - Speed: Bully, Lease
   - Stability: Raft, ZooKeeper
   - Example: "Raft for stability"

5. **Infrastructure available?**
   - ZooKeeper: Use ZooKeeper election
   - None: Implement Raft or Bully
   - Example: "ZooKeeper if available"

**Pattern Recognition:**

**Pattern 1: Small Cluster**
```
Requirements: Small cluster, simple coordination
Solution: Bully algorithm
Implementation: Highest ID becomes leader
```

**Pattern 2: Production System**
```
Requirements: High availability, strong consistency
Solution: Raft or ZooKeeper
Implementation: Majority-based election
```

**Pattern 3: Cloud Environment**
```
Requirements: Split-brain prevention, dynamic nodes
Solution: Leader lease
Implementation: Time-based leadership
```

**Pattern 4: Large Cluster**
```
Requirements: Scalability, reduced coordination
Solution: Hierarchical election
Implementation: Leaders of leaders
```

**Pattern 5: Database Cluster**
```
Requirements: Strong consistency, fault tolerance
Solution: Raft consensus
Implementation: Raft leader election
```

**Decision Flowchart:**

```
Leader Election Decision:
├─ Cluster size?
│        ├─ Small → Bully algorithm
│        └─ Large → Raft or ZooKeeper
├─ Consistency requirements?
│        ├─ Strong → Raft, ZooKeeper
│        └─ Eventual → Bully, Lease
├─ Split-brain prevention?
│        ├─ Yes → Quorum, Lease
│        └─ No → Simple election
└─ Infrastructure available?
         ├─ ZooKeeper → ZooKeeper election
         └─ None → Implement Raft or Bully
```

**Example Analysis:**

**Scenario:** "Design leader election for database cluster"

**Analysis:**
1. Requirements: Strong consistency, fault tolerance
2. Algorithm: Raft
3. Quorum: Majority (n/2 + 1)
4. Timeout: 5-10 seconds election timeout
5. Heartbeat: 1 second interval
6. Implementation: Raft leader election

**Scenario:** "Design leader election for microservices"

**Analysis:**
1. Requirements: Dynamic nodes, split-brain prevention
2. Algorithm: Leader lease
3. TTL: 10 seconds
4. Renewal: Every 5 seconds
5. Lock service: Distributed lock
6. Implementation: Lease-based election

## Summary

Leader election is a distributed algorithm that selects a special node (leader) from a group of nodes to coordinate operations, ensuring only one leader exists at any time. Common algorithms include the Bully algorithm (highest ID node becomes leader), Raft (term-based voting with majority), and ZooKeeper-based election (using ephemeral nodes). Leader election must handle challenges like split-brain scenarios, network partitions, leader failure during election, and concurrent elections. Key features include fault tolerance (automatic leader recovery), safety (only one leader at a time), and liveness (election always completes). Leader election is essential for distributed databases, message queues, coordination services, and cluster management. The choice of algorithm depends on the use case, cluster size, and requirements. Raft provides strong consistency with majority-based voting, ZooKeeper provides production-ready election with automatic failover, and Bully provides simple election for small clusters.

**Key Takeaways:**
- Enables distributed coordination
- Ensures single leader for coordination
- Multiple algorithms: Bully, Raft, ZooKeeper
- Quorum prevents split-brain
- Heartbeat detects failures
- Lease prevents split-brain
- Essential for distributed systems
- Choose algorithm based on requirements

**Mastery Checklist:**
- ✅ Understand leader election concepts
- ✅ Implement Bully algorithm
- ✅ Implement Raft election
- ✅ Implement ZooKeeper election
- ✅ Implement leader lease
- ✅ Handle split-brain scenarios
- ✅ Configure quorum
- ✅ Design election strategy

