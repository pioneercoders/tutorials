# Concurrent Data Structures

Concurrent Data Structures are designed to work safely when:

```text id="cd1"
Multiple threads access data simultaneously
```

They are foundational in:

* Operating systems
* Databases
* Cloud infrastructure
* Distributed systems
* High-frequency trading
* Multiplayer systems
* Real-time analytics

---

# Why Concurrent Data Structures Exist

Normal data structures are NOT thread-safe.

Example:

Two threads updating queue simultaneously:

```text id="cd2"
Thread A → enqueue(10)
Thread B → dequeue()
```

Without synchronization:

* Data corruption
* Race conditions
* Crashes
* Inconsistent states

can occur.

---

# Real-World Analogy

Imagine:

* Multiple bank employees editing same account balance simultaneously.

Without coordination:

```text id="cd3"
Money corruption
```

Same issue occurs in memory.

---

# Core Problem: Race Condition

---

# Example

```js id="cd4"
count = count + 1;
```

Looks simple.

Internally:

```text id="cd5"
1. Read count
2. Increment
3. Write back
```

If two threads execute simultaneously:

* Updates may be lost.

---

# Visualization

```text id="cd6"
Thread A reads 5
Thread B reads 5

Thread A writes 6
Thread B writes 6

Expected:
7

Actual:
6
```

---

# Why This Matters

Race conditions can cause:

* Banking errors
* Database corruption
* System crashes
* Deadlocks
* Security vulnerabilities

---

# Key Concepts in Concurrency

| Concept          | Meaning                   |
| ---------------- | ------------------------- |
| Thread Safety    | Safe parallel access      |
| Mutual Exclusion | Only one thread at a time |
| Atomic Operation | Indivisible operation     |
| Lock             | Synchronization mechanism |
| Lock-Free        | No blocking locks         |
| Wait-Free        | Guaranteed progress       |

---

# Thread Safety

A data structure is thread-safe if:

```text id="cd7"
Multiple threads can access it safely
```

without corruption.

---

# Approaches to Thread Safety

| Approach             | Idea                     |
| -------------------- | ------------------------ |
| Locks/Mutexes        | One thread at a time     |
| Atomic Operations    | Hardware-level safety    |
| Lock-Free Algorithms | Non-blocking concurrency |

---

# 1. Thread Safe Queue

One of the most important concurrent structures.

---

# Why Queues Matter

Queues power:

* Task scheduling
* Thread pools
* Message brokers
* Job systems
* Streaming pipelines

---

# Problem in Normal Queue

Two threads may:

* Insert simultaneously
* Remove simultaneously

causing corruption.

---

# Example Problem

```text id="cd8"
Front/Rear pointers updated incorrectly
```

---

# Lock-Based Thread Safe Queue

Uses:

```text id="cd9"
Mutex / Lock
```

---

# Workflow

```text id="cd10"
Lock Queue
↓
Perform enqueue/dequeue
↓
Unlock Queue
```

---

# Simplified JavaScript Example

(JavaScript itself is single-threaded normally,
but conceptually:)

```js id="cd11"
class ThreadSafeQueue {
  constructor() {
    this.queue = [];
  }

  enqueue(item) {
    // lock

    this.queue.push(item);

    // unlock
  }

  dequeue() {
    // lock

    const item = this.queue.shift();

    // unlock

    return item;
  }
}
```

---

# Real Implementations

Languages like:

* Java
* C++
* Rust
* Go

provide true thread-safe queues.

---

# Complexity

| Operation | Complexity |
| --------- | ---------- |
| Enqueue   | O(1)       |
| Dequeue   | O(1)       |

---

# Real-Time Applications

| System        | Usage          |
| ------------- | -------------- |
| Apache Kafka  | Message queues |
| RabbitMQ      | Job processing |
| Thread pools  | Task execution |
| OS schedulers | Process queues |

---

# Blocking Queue vs Non-Blocking Queue

| Type         | Behavior           |
| ------------ | ------------------ |
| Blocking     | Wait if empty/full |
| Non-Blocking | Immediate return   |

---

# Producer-Consumer Pattern

Very important concurrency model.

---

# Workflow

```text id="cd12"
Producer → Queue → Consumer
```

---

# Example

```text id="cd13"
User uploads image
↓
Queue stores task
↓
Worker processes image
```

---

# Why Queues Matter Here

Benefits:

* Scalability
* Load balancing
* Async processing
* Fault isolation

---

# 2. Lock-Free Stack

Advanced concurrent data structure.

---

# Why Lock-Free?

Locks cause:

* Contention
* Delays
* Deadlocks
* Context switching overhead

Lock-free algorithms improve performance.

---

# Core Idea

Use:

```text id="cd14"
Atomic Compare-And-Swap (CAS)
```

instead of locks.

---

# Compare-And-Swap (CAS)

Atomic CPU instruction.

---

# CAS Workflow

```text id="cd15"
If value unchanged:
    update it
Else:
    retry
```

---

# Stack Push Example

Normal stack:

```text id="cd16"
top → 30 → 20 → 10
```

Push:

```text id="cd17"
40
```

CAS safely updates top pointer.

---

# Why Lock-Free Matters

Benefits:

* High throughput
* Low latency
* Better CPU scalability

---

# Real-Time Applications

| System              | Usage             |
| ------------------- | ----------------- |
| Trading systems     | Ultra-low latency |
| Game engines        | Parallel systems  |
| Real-time analytics | High concurrency  |

---

# Lock-Free vs Lock-Based

---

# ABA Problem

Very important lock-free issue.

---

# Problem

Value changes:

```text id="cd18"
A → B → A
```

CAS thinks:

```text id="cd19"
Nothing changed
```

but state actually changed.

---

# Solutions

| Solution        | Idea                 |
| --------------- | -------------------- |
| Versioning      | Attach counters      |
| Hazard pointers | Safe memory handling |

---

# Memory Reclamation Problem

Lock-free structures must safely free memory.

Very difficult problem in systems programming.

---

# Why?

Thread may still access node while another thread deletes it.

---

# Advanced Techniques

| Technique          | Usage            |
| ------------------ | ---------------- |
| Hazard Pointers    | Safe reclamation |
| Epoch GC           | Deferred cleanup |
| Reference Counting | Shared ownership |

---

# 3. Concurrent HashMap

One of the most important production data structures.

---

# Problem

Normal HashMap is unsafe under concurrent modification.

---

# Issues

Multiple threads may:

* Resize simultaneously
* Overwrite buckets
* Corrupt chains

---

# Example

```text id="cd20"
Two threads insert into same bucket
```

can corrupt structure.

---

# Concurrent HashMap Solution

Uses:

* Fine-grained locking
* Lock striping
* Atomic operations

---

# Lock Striping

Instead of locking whole map:

```text id="cd21"
Lock only specific bucket
```

---

# Benefits

* Better concurrency
* Reduced contention
* Higher throughput

---

# Concurrent HashMap Architecture

```text id="cd22"
Bucket 1 → Lock 1
Bucket 2 → Lock 2
Bucket 3 → Lock 3
```

Threads can work independently.

---

# Java ConcurrentHashMap

Very famous implementation.

Uses:

* CAS
* Bucket-level synchronization
* Tree bins for collisions

---

# Complexity

| Operation | Complexity |
| --------- | ---------- |
| Insert    | O(1) avg   |
| Search    | O(1) avg   |
| Delete    | O(1) avg   |

---

# Real-Time Applications

| System             | Usage               |
| ------------------ | ------------------- |
| Web servers        | Session storage     |
| Distributed caches | Shared state        |
| Microservices      | Concurrent metadata |
| Game servers       | Player state        |

---

# Concurrent HashMap vs HashMap

| Feature     | HashMap | ConcurrentHashMap |
| ----------- | ------- | ----------------- |
| Thread Safe | No      | Yes               |
| Locking     | None    | Fine-grained      |
| Scalability | Poor    | Excellent         |

---

# Lock Granularity

Very important concurrency concept.

---

# Coarse-Grained Locking

```text id="cd23"
One big lock
```

Simple but slow.

---

# Fine-Grained Locking

```text id="cd24"
Multiple smaller locks
```

Better parallelism.

---

# Comparison

---

# Deadlocks

Very important concurrency issue.

---

# What is Deadlock?

Two threads waiting forever.

---

# Example

```text id="cd25"
Thread A holds Lock 1
waiting for Lock 2

Thread B holds Lock 2
waiting for Lock 1
```

System freezes.

---

# Deadlock Prevention

| Technique            | Purpose              |
| -------------------- | -------------------- |
| Lock ordering        | Consistent locking   |
| Timeouts             | Avoid infinite waits |
| Lock-free algorithms | Eliminate locks      |

---

# Starvation

Thread never gets CPU/resources.

---

# Example

High-priority threads always dominate.

Low-priority thread never executes.

---

# Livelock

Threads keep retrying but make no progress.

---

# Concurrent Data Structures in System Design

Massive distributed systems depend heavily on concurrency.

---

# Examples

| System       | Concurrent Structure |
| ------------ | -------------------- |
| Redis        | Shared caches        |
| Apache Kafka | Concurrent queues    |
| MongoDB      | Concurrent indexes   |
| Kubernetes   | Scheduling queues    |

---

# Wait-Free vs Lock-Free

| Type      | Guarantee               |
| --------- | ----------------------- |
| Lock-Free | Some thread progresses  |
| Wait-Free | Every thread progresses |

---

# Why Wait-Free is Rare

Very difficult to implement efficiently.

Usually used in:

* Ultra-low latency systems
* Aerospace
* High-frequency trading

---

# Important Interview Problems

| Problem             | Concept           |
| ------------------- | ----------------- |
| Producer Consumer   | Thread-safe queue |
| Dining Philosophers | Deadlock          |
| Readers Writers     | Synchronization   |
| Concurrent Cache    | ConcurrentHashMap |
| Lock-Free Stack     | CAS               |

---

# Common Beginner Mistakes

| Mistake                    | Problem                 |
| -------------------------- | ----------------------- |
| Forgetting synchronization | Race conditions         |
| Overusing locks            | Performance bottlenecks |
| Ignoring deadlocks         | System freeze           |
| Unsafe memory access       | Crashes                 |
| Wrong lock ordering        | Deadlock                |

---

# Production Engineering Insights

Concurrent data structures power:

* Google infrastructure
* Cloud computing
* Databases
* Trading systems
* Real-time analytics
* Distributed caches

Modern multi-core systems rely heavily on efficient concurrency.

---

# Summary Table

| Topic                | Key Idea                 |
| -------------------- | ------------------------ |
| Concurrent DS        | Safe parallel access     |
| Thread Safe Queue    | Locked queue             |
| Lock-Free Stack      | CAS-based stack          |
| ConcurrentHashMap    | Parallel hash map        |
| CAS                  | Atomic compare-and-swap  |
| Lock Striping        | Bucket-level locks       |
| Deadlocks            | Circular waiting         |
| Lock-Free Algorithms | Non-blocking concurrency |

---
