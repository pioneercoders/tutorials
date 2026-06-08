# Distributed Data Structures

Distributed Data Structures are data structures designed to work across:

* Multiple machines
* Multiple servers
* Multiple data centers

instead of a single computer.

They are the foundation of:

* Cloud computing
* Distributed databases
* Blockchain
* Large-scale caching
* Real-time collaboration
* Internet-scale systems

---

# Why Distributed Data Structures Exist

Single-machine systems eventually hit limits:

| Limitation  | Problem                 |
| ----------- | ----------------------- |
| CPU         | Processing bottleneck   |
| RAM         | Memory limit            |
| Storage     | Disk capacity           |
| Network     | Traffic overload        |
| Reliability | Single point of failure |

Distributed systems solve this by:

```text id="dd1"
Spreading data across many machines
```

---

# Real-World Analogy

Imagine:

* One supermarket handling an entire city.

Eventually:

* Too crowded
* Too slow
* Too risky

Solution:

```text id="dd2"
Multiple distributed branches
```

Distributed data structures work similarly.

---

# What Makes Distributed Systems Hard

Unlike normal data structures:

* Machines may fail
* Networks may disconnect
* Clocks differ
* Data replication becomes difficult

---

# Core Distributed Challenges

| Challenge       | Meaning                 |
| --------------- | ----------------------- |
| Partitioning    | Split data across nodes |
| Replication     | Duplicate data safely   |
| Consistency     | Same data everywhere    |
| Availability    | System keeps running    |
| Fault Tolerance | Survive failures        |

---

# Key Distributed Concepts

| Concept              | Purpose                 |
| -------------------- | ----------------------- |
| Sharding             | Split data              |
| Replication          | Copy data               |
| Consensus            | Agree on state          |
| Eventual Consistency | Delayed synchronization |
| Gossip Protocol      | Node communication      |

---

# Why Distributed Data Structures Matter

They power:

* Google Search
* Cloud databases
* Global messaging apps
* Multiplayer systems
* Blockchain
* Collaborative editing

---

# 1. Distributed Hash Tables (DHT)

Very important distributed systems concept.

---

# What is a DHT?

A:

```text id="dd3"
Distributed key-value storage system
```

where:

* Data spread across multiple nodes
* Lookup remains efficient

---

# Normal Hash Table Problem

Single machine stores everything:

```text id="dd4"
Key → hash(key) % tableSize
```

Not scalable globally.

---

# DHT Solution

Distribute keys across:

```text id="dd5"
Multiple servers
```

---

# Example

```text id="dd6"
User Profiles:
Alice → Server A
Bob → Server B
Charlie → Server C
```

---

# Core Idea

Each node stores:

* Part of total hash space

---

# Visualization

```text id="dd7"
Hash Space:

0 -------------------- 100

Server A → 0-30
Server B → 31-60
Server C → 61-100
```

---

# DHT Lookup

To find key:

1. Hash key
2. Determine responsible node
3. Query node

---

# Complexity

Efficient DHTs provide:

```text id="dd8"
O(log n)
```

routing.

---

# Real-Time Applications

| System             | Usage             |
| ------------------ | ----------------- |
| BitTorrent         | Peer lookup       |
| Blockchain         | Node discovery    |
| Distributed caches | Data partitioning |
| P2P networks       | Resource sharing  |

---

# Popular DHT Algorithms

| Algorithm | System             |
| --------- | ------------------ |
| Chord     | Circular DHT       |
| Kademlia  | Distributed lookup |
| Pastry    | Scalable routing   |

---

# 2. Consistent Hash Rings

One of the most important distributed systems concepts.

Extremely important for:

* System Design Interviews
* Databases
* Caching systems

---

# Problem with Normal Hashing

Suppose:

```text id="dd9"
hash(key) % servers
```

If server count changes:

* Almost all keys remap.

Huge disaster.

---

# Example

Before:

```text id="dd10"
4 servers
```

After:

```text id="dd11"
5 servers
```

Most data moves.

---

# Why This is Bad

Causes:

* Massive cache invalidation
* Network overload
* Database reshuffling

---

# Consistent Hashing Solution

Map:

* Servers
* Keys

onto:

```text id="dd12"
Circular hash ring
```

---

# Ring Visualization

```text id="dd13"
         Server A
       /          \
Key X               Server B
       \          /
         Server C
```

---

# Core Rule

Key stored on:

```text id="dd14"
Next clockwise server
```

---

# Major Benefit

Adding/removing server only affects:

```text id="dd15"
Small portion of keys
```

---

# Consistent Hashing Workflow

---

# Virtual Nodes (VNodes)

Very important optimization.

---

# Problem

Uneven server distribution causes:

```text id="dd16"
Hotspots
```

---

# Solution

Each physical server gets:

```text id="dd17"
Multiple virtual nodes
```

---

# Benefits

| Benefit               | Why Important        |
| --------------------- | -------------------- |
| Better load balancing | Uniform distribution |
| Fault tolerance       | Reduced hotspots     |
| Scalability           | Easier expansion     |

---

# Real-Time Applications

| System           | Usage             |
| ---------------- | ----------------- |
| Amazon DynamoDB  | Partitioning      |
| Apache Cassandra | Data distribution |
| Redis Cluster    | Sharding          |
| CDNs             | Request routing   |

---

# Replication in Hash Rings

Usually data stored on:

```text id="dd18"
Multiple neighboring nodes
```

for fault tolerance.

---

# Example

```text id="dd19"
Primary → Replica 1 → Replica 2
```

---

# Benefits

| Benefit           | Why Important     |
| ----------------- | ----------------- |
| High availability | Survive failures  |
| Disaster recovery | Data safety       |
| Faster reads      | Load distribution |

---

# CAP Theorem

Very important distributed systems concept.

Distributed systems can only guarantee TWO of:

| Property            | Meaning                |
| ------------------- | ---------------------- |
| Consistency         | Same data everywhere   |
| Availability        | Always responsive      |
| Partition Tolerance | Survive network splits |

---

# Example

During network failure:

* Choose consistency
  OR
* Choose availability

Impossible to perfectly guarantee both.

---

# 3. CRDTs (Conflict-Free Replicated Data Types)

Very advanced distributed data structure.

---

# Why CRDTs Exist

Distributed systems may update same data:

```text id="dd20"
Simultaneously on different machines
```

without coordination.

---

# Problem

Two users edit same document offline.

How merge safely?

---

# Traditional Solution

Central locking:

```text id="dd21"
Slow and fragile
```

---

# CRDT Solution

Design data structures that:

```text id="dd22"
Automatically merge safely
```

---

# Key Property

CRDT operations are:

* Commutative
* Associative
* Idempotent

---

# Meaning

Updates merge correctly:

```text id="dd23"
Regardless of order
```

---

# Real-World Example

Collaborative editing:

Two users type simultaneously.

CRDT merges changes automatically.

---

# CRDT Types

| Type            | Meaning           |
| --------------- | ----------------- |
| State-based     | Merge full states |
| Operation-based | Merge operations  |

---

# Common CRDT Structures

| CRDT         | Usage                      |
| ------------ | -------------------------- |
| G-Counter    | Distributed counters       |
| OR-Set       | Distributed sets           |
| LWW Register | Last-write-wins            |
| RGA          | Collaborative text editing |

---

# G-Counter Example

Each node keeps local counter.

Merge:

```text id="dd24"
Take maximum per node
```

---

# Why CRDTs Matter

Allow:

* Offline editing
* Eventual consistency
* Multi-region collaboration
* Conflict-free merging

---

# Real-Time Applications

| System                | Usage                 |
| --------------------- | --------------------- |
| Figma                 | Collaborative editing |
| Notion                | Shared documents      |
| Multiplayer games     | Shared state          |
| Distributed databases | Conflict resolution   |

---

# Eventual Consistency

Very important distributed systems concept.

---

# Meaning

Nodes may temporarily differ,
but:

```text id="dd25"
Eventually become consistent
```

---

# Why Important

Global synchronization instantly is impossible at scale.

---

# Example

Instagram likes:

* Count may differ briefly
* Eventually synchronizes

---

# Strong Consistency vs Eventual Consistency

| Feature      | Strong    | Eventual |
| ------------ | --------- | -------- |
| Accuracy     | Immediate | Delayed  |
| Performance  | Slower    | Faster   |
| Availability | Lower     | Higher   |

---

# Distributed Consensus

Very important related topic.

---

# Problem

Multiple nodes must agree on:

```text id="dd26"
Single correct state
```

---

# Consensus Algorithms

| Algorithm | Usage                 |
| --------- | --------------------- |
| Raft      | Simpler consensus     |
| Paxos     | Distributed agreement |
| Zab       | Coordination systems  |

---

# Why Consensus Matters

Needed for:

* Distributed databases
* Leader election
* Replication
* Transactions

---

# Distributed Failures

Unlike local systems,
distributed systems face:

* Node crashes
* Packet loss
* Delayed messages
* Partial failures

---

# Partial Failure Example

```text id="dd27"
Server A alive
Server B unreachable
```

System partially broken.

Very hard problem.

---

# Gossip Protocols

Distributed nodes spread information:

```text id="dd28"
Like rumors spreading socially
```

---

# Real-Time Applications

| System              | Usage                |
| ------------------- | -------------------- |
| Apache Cassandra    | Cluster membership   |
| Blockchain networks | Peer synchronization |
| Service discovery   | Health propagation   |

---

# Distributed Data Structures in System Design

Massive systems depend heavily on them.

---

# Examples

| System          | Structure            |
| --------------- | -------------------- |
| Amazon DynamoDB | Consistent hashing   |
| Redis Cluster   | Hash slots           |
| Google Bigtable | Distributed indexing |
| Blockchain      | Distributed ledgers  |

---

# DHT vs Traditional HashMap

| Feature         | HashMap        | DHT         |
| --------------- | -------------- | ----------- |
| Scope           | Single machine | Distributed |
| Scalability     | Limited        | Massive     |
| Fault tolerance | Poor           | High        |

---

# Consistent Hashing vs Normal Hashing

---

# Important Interview Problems

| Problem                     | Concept              |
| --------------------------- | -------------------- |
| Design Distributed Cache    | Consistent hashing   |
| Collaborative Editing       | CRDT                 |
| Global Chat System          | Eventual consistency |
| Distributed Key-Value Store | DHT                  |
| Multi-region Replication    | Consensus            |

---

# Common Beginner Mistakes

| Mistake                               | Problem            |
| ------------------------------------- | ------------------ |
| Assuming perfect consistency          | CAP violations     |
| Ignoring replication                  | Data loss          |
| Using normal hashing                  | Massive remapping  |
| Underestimating network failures      | System outages     |
| Confusing strong/eventual consistency | Wrong architecture |

---

# Production Engineering Insights

Distributed data structures power:

* Cloud databases
* Global caches
* Multiplayer systems
* Real-time collaboration
* Blockchain
* AI distributed systems

Modern internet-scale systems are impossible without them.

---

# Summary Table

| Topic                | Key Idea                     |
| -------------------- | ---------------------------- |
| Distributed DS       | Multi-machine structures     |
| DHT                  | Distributed key-value lookup |
| Consistent Hashing   | Minimal remapping            |
| Hash Ring            | Circular partitioning        |
| CRDT                 | Conflict-free merging        |
| Replication          | Data redundancy              |
| Eventual Consistency | Delayed synchronization      |
| Consensus            | Distributed agreement        |

---
