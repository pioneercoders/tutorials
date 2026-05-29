# Distributed Transactions

Distributed transactions involve multiple operations across different databases or services that must all succeed or all fail together, maintaining data consistency across distributed systems.

## Introduction

Distributed transactions involve multiple operations across different databases or services that must all succeed or all fail together, maintaining data consistency across distributed systems. In a distributed system where operations span multiple services or databases, ensuring ACID (Atomicity, Consistency, Isolation, Durability) properties becomes challenging. Distributed transaction patterns like Two-Phase Commit (2PC), Saga pattern, TCC (Try-Confirm-Cancel), and Event Sourcing provide different approaches to maintaining consistency. Two-Phase Commit uses a coordinator to ensure all participants agree before committing, providing strong consistency but blocking availability. Saga pattern breaks transactions into a sequence of local transactions with compensating actions, providing availability with eventual consistency. TCC uses business-level compensation with try, confirm, and cancel phases. Event Sourcing uses event-driven consistency by storing events instead of current state. The choice depends on consistency requirements, availability needs, and transaction complexity. Distributed transactions are essential for financial systems, e-commerce, inventory management, and any system requiring cross-service consistency.

**Why Distributed Transactions Matter:**
- Ensures cross-service consistency
- Maintains ACID properties across distributed systems
- Prevents partial failures
- Essential for financial transactions
- Critical for e-commerce systems
- Foundation for distributed data integrity

**Where It Is Used:**
- Bank transfers (money movement)
- Order processing (inventory, payment, shipping)
- Inventory management (stock updates)
- Payment processing (payment gateway, ledger)
- Financial systems (trading, accounting)
- E-commerce platforms

## Core Concept Explanation

Distributed transactions ensure that multiple operations across different services or databases either all succeed or all fail together, maintaining data consistency. In a monolithic system, transactions are handled by a single database with built-in ACID support. In distributed systems, operations span multiple services and databases, making coordination challenging. Two-Phase Commit (2PC) uses a coordinator that asks all participants to prepare (lock resources and confirm they can commit). If all participants agree, the coordinator asks them to commit. If any participant disagrees, the coordinator asks all to rollback. This provides strong consistency but blocks during the prepare phase and has a single point of failure (the coordinator). Saga pattern breaks a distributed transaction into a sequence of local transactions, each with a compensating action that undoes the transaction if needed. If any step fails, compensating actions are executed in reverse order to rollback. This provides availability with eventual consistency. TCC (Try-Confirm-Cancel) is similar to Saga but uses business-level compensation with explicit try, confirm, and cancel phases. Event Sourcing stores events instead of current state, allowing reconstruction of state and event-driven consistency.

**Step-by-Step Breakdown:**
1. Transaction coordinator initiates distributed transaction
2. Coordinator identifies all participants (services/databases)
3. For 2PC: Prepare phase - ask all participants to prepare
4. Participants lock resources and confirm they can commit
5. If all agree, commit phase - ask all to commit
6. If any disagree, rollback phase - ask all to rollback
7. For Saga: Execute steps sequentially with compensating actions
8. If any step fails, execute compensating actions in reverse
9. Transaction completes (committed or rolled back)

**Intuition Behind the Concept:**
Think of distributed transactions like a group project where everyone must either complete their part or no one does. Two-Phase Commit is like a project manager asking everyone if they can complete their task. If everyone says yes, the manager tells everyone to proceed. If anyone says no, the manager tells everyone to stop. Saga pattern is like completing tasks one by one, and if any task fails, undoing all completed tasks in reverse order.

**Visual Thinking:**
```
Two-Phase Commit (2PC):
Coordinator → Participant 1: Prepare?
             → Participant 2: Prepare?
             → Participant 3: Prepare?
             
All agree → Coordinator → Participant 1: Commit
                      → Participant 2: Commit
                      → Participant 3: Commit

Any fail → Coordinator → Participant 1: Rollback
                      → Participant 2: Rollback
                      → Participant 3: Rollback

Saga Pattern:
Step 1: Execute action → Success
Step 2: Execute action → Success
Step 3: Execute action → FAIL
Step 4: Compensate step 2
Step 5: Compensate step 1
```

## Internal Working / Logic

Distributed transactions operate through different patterns depending on the consistency and availability requirements. Two-Phase Commit (2PC) uses a coordinator to manage the transaction. In the prepare phase, the coordinator sends prepare requests to all participants. Participants lock resources, perform validations, and respond with "prepare" or "abort". If all participants respond with "prepare", the coordinator enters the commit phase and sends commit requests to all participants. If any participant responds with "abort" or times out, the coordinator sends rollback requests to all participants. Participants then commit or rollback their local transactions. Saga pattern executes steps sequentially. Each step is a local transaction with a compensating action that undoes the step. If a step fails, compensating actions are executed in reverse order to rollback the transaction. TCC (Try-Confirm-Cancel) uses three phases: Try (reserve resources), Confirm (confirm transaction), or Cancel (release resources). Event Sourcing stores events instead of current state, allowing reconstruction of state by replaying events.

**Operation 1: 2PC Prepare Phase**
- Coordinator sends prepare request to all participants
- Participants lock resources
- Participants validate they can commit
- Participants respond with prepare or abort
- Coordinator collects all responses
- If all prepare, proceed to commit phase
- If any abort, proceed to rollback phase

**Operation 2: 2PC Commit Phase**
- Coordinator sends commit request to all participants
- Participants commit their local transactions
- Participants release locks
- Participants acknowledge commit
- Transaction completed successfully

**Operation 3: 2PC Rollback Phase**
- Coordinator sends rollback request to all participants
- Participants rollback their local transactions
- Participants release locks
- Participants acknowledge rollback
- Transaction rolled back

**Operation 4: Saga Execution**
- Execute first step (local transaction)
- If success, proceed to next step
- If failure, execute compensating actions in reverse
- Continue until all steps complete or rollback completes
- Transaction completed (committed or rolled back)

**Flow Explanation (2PC):**
1. Coordinator initiates transaction
2. Coordinator sends prepare to participant 1
3. Participant 1 locks resources, validates, responds prepare
4. Coordinator sends prepare to participant 2
5. Participant 2 locks resources, validates, responds prepare
6. Coordinator sends prepare to participant 3
7. Participant 3 locks resources, validates, responds prepare
8. All participants prepared
9. Coordinator sends commit to all participants
10. Participants commit and release locks
11. Transaction committed

**Decision Making Logic:**
The key decisions are:
- Which pattern to use (2PC, Saga, TCC, Event Sourcing)
- Strong consistency or eventual consistency
- Blocking or non-blocking
- Coordinator-based or decentralized
- Compensation strategy
- Timeout and retry handling

## Algorithm / Approach

**Two-Phase Commit Algorithm**

```
1. Coordinator sends prepare to all participants
2. Wait for all responses
3. If all respond prepare:
   a. Send commit to all participants
   b. Wait for all acknowledgments
   c. Transaction committed
4. If any respond abort or timeout:
   a. Send rollback to all participants
   b. Wait for all acknowledgments
   c. Transaction rolled back
```

**Saga Pattern Algorithm**

```
1. Execute first step (local transaction)
2. If success, execute next step
3. Repeat until all steps complete
4. If any step fails:
   a. Execute compensating actions in reverse order
   b. Rollback completed steps
5. Transaction completed (committed or rolled back)
```

**TCC Algorithm**

```
1. Try phase: Reserve resources for all participants
2. If all try succeed:
   a. Confirm phase: Confirm transaction
   b. Release resources
3. If any try fails:
   a. Cancel phase: Cancel transaction
   b. Release resources
4. Transaction completed
```

**Event Sourcing Algorithm**

```
1. Generate event for operation
2. Append event to event store
3. Publish event to subscribers
4. Subscribers update their state
5. If any subscriber fails:
   a. Retry event delivery
   b. Use dead letter queue for failures
6. Event processed successfully
```

## Implementations

### 1. Two-Phase Commit (2PC)

```javascript
class TwoPhaseCommit {
  constructor(participants) {
    this.participants = participants;
  }
  
  async execute(operations) {
    // Phase 1: Prepare
    const prepared = [];
    for (let i = 0; i < this.participants.length; i++) {
      const participant = this.participants[i];
      const operation = operations[i];
      
      try {
        const canCommit = await participant.prepare(operation);
        if (canCommit) {
          prepared.push(participant);
        } else {
          // Abort all prepared participants
          for (const p of prepared) {
            await p.rollback();
          }
          return { success: false, message: 'Participant aborted' };
        }
      } catch (error) {
        // Abort all prepared participants on error
        for (const p of prepared) {
          await p.rollback();
        }
        return { success: false, message: error.message };
      }
    }
    
    // Phase 2: Commit
    try {
      for (const participant of prepared) {
        await participant.commit();
      }
      return { success: true, message: 'Transaction committed' };
    } catch (error) {
      // Attempt rollback on commit failure
      for (const participant of prepared) {
        await participant.rollback();
      }
      return { success: false, message: error.message };
    }
  }
}

// Participant interface
class DatabaseParticipant {
  constructor(db, transactionId) {
    this.db = db;
    this.transactionId = transactionId;
  }
  
  async prepare(operation) {
    // Start transaction, lock resources, validate
    await this.db.query('BEGIN');
    await this.db.query(operation.query, operation.params);
    return true; // Can commit
  }
  
  async commit() {
    // Commit transaction
    await this.db.query('COMMIT');
  }
  
  async rollback() {
    // Rollback transaction
    await this.db.query('ROLLBACK');
  }
}

// Usage
const participants = [
  new DatabaseParticipant(db1, 'tx-1'),
  new DatabaseParticipant(db2, 'tx-1'),
  new DatabaseParticipant(db3, 'tx-1')
];
const coordinator = new TwoPhaseCommit(participants);

const operations = [
  { query: 'UPDATE accounts SET balance = balance - 100 WHERE id = 1', params: [] },
  { query: 'UPDATE accounts SET balance = balance + 100 WHERE id = 2', params: [] },
  { query: 'INSERT INTO transactions (from_id, to_id, amount) VALUES ($1, $2, $3)', params: [1, 2, 100] }
];

const result = await coordinator.execute(operations);
console.log(result);
```

**Advantages:**
- Strong consistency
- All or nothing semantics
- ACID properties
- Widely used

### 2. Saga Pattern

```javascript
class Saga {
  constructor() {
    this.steps = [];
  }
  
  addStep(action, compensation) {
    this.steps.push({ action, compensation });
  }
  
  async execute() {
    const executed = [];
    
    for (const step of this.steps) {
      try {
        await step.action();
        executed.push(step);
      } catch (error) {
        // Compensate executed steps in reverse order
        for (const executedStep of executed.reverse()) {
          try {
            await executedStep.compensation();
          } catch (compensationError) {
            console.error('Compensation failed:', compensationError);
            // Continue compensating other steps
          }
        }
        throw error;
      }
    }
    
    return { success: true, message: 'Saga completed' };
  }
}

// Usage: Order processing saga
const saga = new Saga();

// Step 1: Reserve inventory
saga.addStep(
  async () => {
    console.log('Reserving inventory...');
    // Reserve inventory in inventory service
    await inventoryService.reserve(orderId, items);
  },
  async () => {
    console.log('Releasing inventory...');
    // Release inventory in inventory service
    await inventoryService.release(orderId, items);
  }
);

// Step 2: Process payment
saga.addStep(
  async () => {
    console.log('Processing payment...');
    // Process payment in payment service
    await paymentService.charge(customerId, amount);
  },
  async () => {
    console.log('Refunding payment...');
    // Refund payment in payment service
    await paymentService.refund(customerId, amount);
  }
);

// Step 3: Create order
saga.addStep(
  async () => {
    console.log('Creating order...');
    // Create order in order service
    await orderService.create(orderId, customerId, items);
  },
  async () => {
    console.log('Cancelling order...');
    // Cancel order in order service
    await orderService.cancel(orderId);
  }
);

// Step 4: Ship order
saga.addStep(
  async () => {
    console.log('Shipping order...');
    // Ship order in shipping service
    await shippingService.ship(orderId, address);
  },
  async () => {
    console.log('Cancelling shipment...');
    // Cancel shipment in shipping service
    await shippingService.cancel(orderId);
  }
);

try {
  const result = await saga.execute();
  console.log(result);
} catch (error) {
  console.error('Saga failed:', error);
}
```

**Advantages:**
- Non-blocking
- High availability
- Eventual consistency
- Long-running transactions

### 3. TCC (Try-Confirm-Cancel)

```javascript
class TCC {
  constructor() {
    this.participants = [];
  }
  
  addParticipant(participant) {
    this.participants.push(participant);
  }
  
  async execute() {
    // Try phase
    const tried = [];
    for (const participant of this.participants) {
      try {
        const result = await participant.try();
        if (result.success) {
          tried.push(participant);
        } else {
          // Cancel all tried participants
          for (const p of tried) {
            await p.cancel();
          }
          return { success: false, message: 'Try phase failed' };
        }
      } catch (error) {
        // Cancel all tried participants
        for (const p of tried) {
          await p.cancel();
        }
        return { success: false, message: error.message };
      }
    }
    
    // Confirm phase
    try {
      for (const participant of tried) {
        await participant.confirm();
      }
      return { success: true, message: 'Transaction confirmed' };
    } catch (error) {
      // Cancel all tried participants on confirm failure
      for (const participant of tried) {
        await participant.cancel();
      }
      return { success: false, message: error.message };
    }
  }
}

// Participant interface
class PaymentParticipant {
  constructor(paymentService, amount) {
    this.paymentService = paymentService;
    this.amount = amount;
  }
  
  async try() {
    // Reserve payment amount
    return await this.paymentService.reserve(this.amount);
  }
  
  async confirm() {
    // Confirm payment
    return await this.paymentService.confirm(this.amount);
  }
  
  async cancel() {
    // Release reserved amount
    return await this.paymentService.release(this.amount);
  }
}

// Usage
const tcc = new TCC();
tcc.addParticipant(new PaymentParticipant(paymentService, 100));
tcc.addParticipant(new InventoryParticipant(inventoryService, items));

const result = await tcc.execute();
console.log(result);
```

**Advantages:**
- Business-level compensation
- Flexible compensation logic
- Good for complex business rules
- Explicit phases

### 4. Event Sourcing

```javascript
class EventSourcing {
  constructor(eventStore) {
    this.eventStore = eventStore;
  }
  
  async execute(event) {
    // Append event to event store
    await this.eventStore.append(event);
    
    // Publish event to subscribers
    await this.eventStore.publish(event);
    
    return { success: true, message: 'Event appended' };
  }
  
  async replay(aggregateId) {
    // Replay events to reconstruct state
    const events = await this.eventStore.getEvents(aggregateId);
    let state = {};
    
    for (const event of events) {
      state = this.applyEvent(state, event);
    }
    
    return state;
  }
  
  applyEvent(state, event) {
    // Apply event to state
    switch (event.type) {
      case 'ORDER_CREATED':
        return { ...state, orderId: event.orderId, status: 'created' };
      case 'PAYMENT_PROCESSED':
        return { ...state, status: 'paid' };
      case 'ORDER_SHIPPED':
        return { ...state, status: 'shipped' };
      default:
        return state;
    }
  }
}

// Event store
class EventStore {
  constructor() {
    this.events = [];
    this.subscribers = [];
  }
  
  async append(event) {
    event.id = crypto.randomUUID();
    event.timestamp = Date.now();
    this.events.push(event);
    return event;
  }
  
  async publish(event) {
    for (const subscriber of this.subscribers) {
      try {
        await subscriber.handle(event);
      } catch (error) {
        console.error('Subscriber error:', error);
        // Retry or send to dead letter queue
      }
    }
  }
  
  subscribe(subscriber) {
    this.subscribers.push(subscriber);
  }
  
  async getEvents(aggregateId) {
    return this.events.filter(e => e.aggregateId === aggregateId);
  }
}

// Usage
const eventStore = new EventStore();
const eventSourcing = new EventSourcing(eventStore);

// Subscribe to events
eventStore.subscribe({
  handle: async (event) => {
    if (event.type === 'ORDER_CREATED') {
      await orderService.create(event.orderId, event.customerId);
    }
  }
});

eventStore.subscribe({
  handle: async (event) => {
    if (event.type === 'PAYMENT_PROCESSED') {
      await paymentService.process(event.paymentId, event.amount);
    }
  }
});

// Execute transaction by appending events
await eventSourcing.execute({
  type: 'ORDER_CREATED',
  aggregateId: 'order-123',
  orderId: 'order-123',
  customerId: 'customer-456'
});

await eventSourcing.execute({
  type: 'PAYMENT_PROCESSED',
  aggregateId: 'order-123',
  paymentId: 'payment-789',
  amount: 100
});
```

**Advantages:**
- Event-driven consistency
- Audit trail
- Temporal queries
- Event replay

### 5. Saga Orchestrator

```javascript
class SagaOrchestrator {
  constructor() {
    this.sagas = new Map();
  }
  
  registerSaga(name, saga) {
    this.sagas.set(name, saga);
  }
  
  async execute(name, data) {
    const saga = this.sagas.get(name);
    if (!saga) {
      throw new Error(`Saga ${name} not found`);
    }
    
    return await saga.execute(data);
  }
}

// Order processing saga orchestrator
const orchestrator = new SagaOrchestrator();

orchestrator.registerSaga('order-processing', async (data) => {
  const saga = new Saga();
  
  saga.addStep(
    async () => await inventoryService.reserve(data.orderId, data.items),
    async () => await inventoryService.release(data.orderId, data.items)
  );
  
  saga.addStep(
    async () => await paymentService.charge(data.customerId, data.amount),
    async () => await paymentService.refund(data.customerId, data.amount)
  );
  
  saga.addStep(
    async () => await orderService.create(data.orderId, data.customerId, data.items),
    async () => await orderService.cancel(data.orderId)
  );
  
  return await saga.execute();
});

// Usage
const result = await orchestrator.execute('order-processing', {
  orderId: 'order-123',
  customerId: 'customer-456',
  items: [{ productId: 'prod-1', quantity: 2 }],
  amount: 100
});
```

**Advantages:**
- Centralized saga management
- Reusable sagas
- Easy to monitor
- Better organization

## Dry Run

**Example: Two-Phase Commit for Bank Transfer**

**Initial State:**
```
Account A: $1000
Account B: $500
Transfer: $200 from A to B
```

**Step-by-Step Execution:**

```
Step 1: Coordinator initiates transaction
Step 2: Coordinator sends prepare to Account A DB
Step 3: Account A DB: BEGIN TRANSACTION
Step 4: Account A DB: UPDATE accounts SET balance = balance - 200 WHERE id = A
Step 5: Account A DB: Validate balance >= 0
Step 6: Account A DB responds: PREPARE
Step 7: Coordinator sends prepare to Account B DB
Step 8: Account B DB: BEGIN TRANSACTION
Step 9: Account B DB: UPDATE accounts SET balance = balance + 200 WHERE id = B
Step 10: Account B DB: Validate no constraints violated
Step 11: Account B DB responds: PREPARE
Step 12: All participants prepared
Step 13: Coordinator sends commit to Account A DB
Step 14: Account A DB: COMMIT
Step 15: Account A DB releases locks
Step 16: Account A DB acknowledges commit
Step 17: Coordinator sends commit to Account B DB
Step 18: Account B DB: COMMIT
Step 19: Account B DB releases locks
Step 20: Account B DB acknowledges commit
Step 21: Transaction committed
Step 22: Final state: Account A: $800, Account B: $700
```

**Request/Response Table:**

| Step | Coordinator | Participant | Action | Response |
|------|-------------|-------------|--------|----------|
| 1 | Initiate | - | Start transaction | - |
| 2 | Send prepare | Account A | Prepare | PREPARE |
| 3 | Send prepare | Account B | Prepare | PREPARE |
| 4 | Send commit | Account A | Commit | ACK |
| 5 | Send commit | Account B | Commit | ACK |
| 6 | Complete | - | Transaction committed | - |

## Edge Cases

### 1. Coordinator Failure
```javascript
// Coordinator crashes during transaction
- Participants left in prepared state
// Solution: Timeout and recovery, participant-initiated recovery
```

### 2. Participant Failure
```javascript
// Participant crashes during transaction
- Cannot respond to coordinator
// Solution: Timeout, rollback, retry
```

### 3. Network Partition
```javascript
// Network partition between coordinator and participant
- Communication lost
// Solution: Timeout, rollback, retry
```

### 4. Timeout Handling
```javascript
// Participant doesn't respond within timeout
- Transaction hangs
// Solution: Timeout, rollback, retry
```

### 5. Partial Failure
```javascript
// Some participants commit, others rollback
- Inconsistent state
// Solution: Recovery logs, reconciliation
```

### 6. Long-Running Transaction
```javascript
// Transaction takes too long
- Resources locked too long
// Solution: Use Saga pattern instead of 2PC
```

**Why Edge Cases Matter:**
- Coordinator failure causes resource locks
- Participant failure prevents completion
- Network partition breaks communication
- Timeout causes transaction hangs
- Partial failure causes inconsistency
- Long transactions block resources

## Variations / Extensions

### 1. Three-Phase Commit

```javascript
// Additional pre-commit phase
- Reduces blocking
// Example: High availability systems
```

### 2. Optimistic Concurrency Control

```javascript
// Version-based conflict detection
- No locking
// Example: Low contention systems
```

### 3. Pessimistic Concurrency Control

```javascript
// Lock-based conflict prevention
- Strong consistency
// Example: High contention systems
```

### 4. Compensation-Based Transactions

```javascript
// Saga with compensation
- Eventual consistency
// Example: Long-running transactions
```

### 5. Eventual Consistency

```javascript
// Accept temporary inconsistency
- High availability
// Example: Social media feeds
```

## Optimization Techniques

### 1. Timeout Management

**Set Appropriate Timeouts:**
```javascript
// Set timeouts for each phase
- Prevent hanging
// Better availability
```

### 2. Retry Logic

**Exponential Backoff:**
```javascript
// Retry with increasing delay
- Handle transient failures
// Better reliability
```

### 3. Idempotent Operations

**Make Operations Idempotent:**
```javascript
// Safe to retry
- Handle duplicate requests
// Better reliability
```

### 4. Parallel Execution

**Execute in Parallel:**
```javascript
// Parallel prepare/commit phases
- Reduce latency
// Better performance
```

### 5. Trade-offs

**Pattern Comparison:**

| Pattern | Consistency | Availability | Complexity | Use Case |
|---------|-------------|-------------|------------|----------|
| 2PC | Strong | Low | Medium | Financial systems |
| Saga | Eventual | High | High | Long-running |
| TCC | Strong | Medium | High | Business logic |
| Event Sourcing | Eventual | High | High | Audit trails |

**When to Use Each:**
- 2PC: Strong consistency, short transactions
- Saga: Long-running, high availability
- TCC: Complex business rules
- Event Sourcing: Audit trails, event-driven

## Complexity Analysis

### Time Complexity

**2PC: O(n)**
- n = number of participants
- Sequential prepare/commit
- Blocking

**Saga: O(n)**
- n = number of steps
- Sequential execution
- Non-blocking

**TCC: O(n)**
- n = number of participants
- Sequential try/confirm
- Non-blocking

### Space Complexity

**2PC: O(n)**
- n = number of participants
- Lock resources
- Transaction logs

**Saga: O(n)**
- n = number of steps
- Compensation actions
- Execution history

**Explanation:**
2PC is O(n) time complexity where n is the number of participants, with sequential prepare and commit phases. It's blocking and has lower availability. Saga is O(n) where n is the number of steps, with sequential execution but non-blocking. TCC is O(n) where n is the number of participants, with sequential try and confirm phases. Space complexity is O(n) for all patterns, storing transaction state, locks, or compensation actions. The trade-off is between consistency (2PC, TCC) and availability (Saga, Event Sourcing).

## Real-world Applications

### 1. Bank Transfers

**Money Movement:**
- Debit source account
- Credit destination account
- Example: Wire transfers

### 2. Order Processing

**E-commerce Orders:**
- Reserve inventory
- Process payment
- Create order
- Ship order
- Example: Online shopping

### 3. Inventory Management

**Stock Updates:**
- Update inventory across warehouses
- Prevent overselling
- Example: Multi-warehouse systems

### 4. Payment Processing

**Payment Gateway:**
- Charge customer
- Update ledger
- Notify services
- Example: Payment systems

### 5. Financial Trading

**Stock Trading:**
- Execute trade
- Update positions
- Clear settlement
- Example: Trading platforms

### 6. Travel Booking

**Flight Booking:**
- Reserve seat
- Process payment
- Issue ticket
- Example: Travel sites

### 7. Healthcare

**Patient Records:**
- Update multiple systems
- Maintain consistency
- Example: EHR systems

### 8. Supply Chain

**Order Fulfillment:**
- Update inventory
- Process shipment
- Update accounting
- Example: Logistics

## Common Mistakes

### 1. No Timeout Handling

**Mistake:**
```javascript
// No timeout for participant response
- Transaction hangs
// Poor availability
```

**Correct:**
```javascript
// Set timeout for each phase
- Timeout and rollback
// Better availability
```

**Why It Matters:**
- No timeout = transaction hangs
- Poor availability
- Timeout essential

### 2. No Idempotency

**Mistake:**
```javascript
// Operations not idempotent
- Retry causes duplicate actions
// Data corruption
```

**Correct:**
```javascript
// Make operations idempotent
- Safe to retry
// Better reliability
```

**Why It Matters:**
- No idempotency = duplicate actions
- Data corruption
- Idempotency essential

### 3. Wrong Pattern Choice

**Mistake:**
```javascript
// Use 2PC for long-running transaction
- Resources locked too long
// Poor performance
```

**Correct:**
```javascript
// Use Saga for long-running
- Non-blocking
// Better performance
```

**Why It Matters:**
- Wrong pattern = poor performance
- Resources locked too long
- Match pattern to use case

### 4. No Compensation Logic

**Mistake:**
```javascript
// No compensation in Saga
- Cannot rollback
// Inconsistent state
```

**Correct:**
```javascript
// Implement compensation for each step
- Can rollback
// Better consistency
```

**Why It Matters:**
- No compensation = cannot rollback
- Inconsistent state
- Compensation essential

### 5. No Recovery Mechanism

**Mistake:**
```javascript
// No recovery from failures
- Inconsistent state persists
// Data corruption
```

**Correct:**
```javascript
// Implement recovery mechanism
- Recover from failures
// Better reliability
```

**Why It Matters:**
- No recovery = inconsistent state
- Data corruption
- Recovery essential

### 6. Ignoring Network Partitions

**Mistake:**
```javascript
// No handling for network partitions
- Transaction hangs
// Poor availability
```

**Correct:**
```javascript
// Handle network partitions
- Timeout and retry
// Better availability
```

**Why It Matters:**
- Network partitions = communication lost
- Transaction hangs
- Partition handling essential

## Advanced Concepts

### 1. Three-Phase Commit

**Concept:**
Additional pre-commit phase.

**Features:**
- Reduces blocking
- Better availability
- More complex

### 2. Optimistic Concurrency Control

**Concept:**
Version-based conflict detection.

**Features:**
- No locking
- Better performance
- Conflict resolution

### 3. Pessimistic Concurrency Control

**Concept:**
Lock-based conflict prevention.

**Features:**
- Strong consistency
- Locking overhead
- Better for high contention

### 4. Event Sourcing

**Concept:**
Store events, not state.

**Features:**
- Audit trail
- Event replay
- Temporal queries

## Practice Thinking Guide

### How to Design Distributed Transaction Strategy

**Key Questions to Ask:**

1. **Strong or eventual consistency?**
   - Strong for financial
   - Eventual for social
   - Example: "Strong for bank transfers"

2. **Short or long-running?**
   - Short for 2PC
   - Long for Saga
   - Example: "Saga for order processing"

3. **High availability required?**
   - Yes for Saga/Event Sourcing
   - No for 2PC
   - Example: "Saga for e-commerce"

4. **Complex business rules?**
   - Yes for TCC
   - No for 2PC
   - Example: "TCC for payment processing"

5. **Audit trail needed?**
   - Yes for Event Sourcing
   - No for 2PC
   - Example: "Event Sourcing for financial"

**Pattern Recognition:**

**Pattern 1: Bank Transfer**
```
Requirements: Strong consistency, short transaction
Solution: Two-Phase Commit
Implementation: 2PC with coordinator
```

**Pattern 2: Order Processing**
```
Requirements: Long-running, high availability
Solution: Saga Pattern
Implementation: Saga with compensation
```

**Pattern 3: Payment Processing**
```
Requirements: Complex business rules
Solution: TCC
Implementation: Try-Confirm-Cancel
```

**Pattern 4: Audit Trail**
```
Requirements: Audit trail, event-driven
Solution: Event Sourcing
Implementation: Event store with subscribers
```

**Pattern 5: Inventory Update**
```
Requirements: High availability, eventual consistency
Solution: Saga or Event Sourcing
Implementation: Saga with compensation
```

**Decision Flowchart:**

```
Distributed Transaction Decision:
├─ Strong or eventual consistency?
│        ├─ Strong → 2PC or TCC
│        └─ Eventual → Saga or Event Sourcing
├─ Short or long-running?
│        ├─ Short → 2PC
│        └─ Long → Saga
├─ High availability?
│        ├─ Yes → Saga or Event Sourcing
│        └─ No → 2PC
└─ Audit trail needed?
         ├─ Yes → Event Sourcing
         └─ No → 2PC or Saga
```

**Example Analysis:**

**Scenario:** "Design transaction for bank transfer"

**Analysis:**
1. Requirements: Strong consistency, short transaction
2. Pattern: Two-Phase Commit
3. Coordinator: Transaction coordinator
4. Participants: Source account DB, destination account DB
5. Timeout: 5 seconds per phase
6. Implementation: 2PC with retry logic

**Scenario:** "Design transaction for order processing"

**Analysis:**
1. Requirements: Long-running, high availability
2. Pattern: Saga
3. Steps: Reserve inventory, process payment, create order, ship
4. Compensation: Release inventory, refund payment, cancel order, cancel shipment
5. Timeout: 30 seconds per step
6. Implementation: Saga with compensation

## Summary

Distributed transactions involve multiple operations across different databases or services that must all succeed or all fail together, maintaining data consistency across distributed systems. Common patterns include Two-Phase Commit (2PC), Saga pattern, TCC (Try-Confirm-Cancel), and Event Sourcing. Two-Phase Commit uses a coordinator to ensure all participants agree before committing, providing strong consistency but blocking availability. Saga pattern breaks transactions into a sequence of local transactions with compensating actions, providing availability with eventual consistency. TCC uses business-level compensation with try, confirm, and cancel phases. Event Sourcing stores events instead of current state, allowing reconstruction of state and event-driven consistency. The choice depends on consistency requirements, availability needs, and transaction complexity. Distributed transactions are essential for financial systems, e-commerce, inventory management, and any system requiring cross-service consistency.

**Key Takeaways:**
- Ensures cross-service consistency
- 2PC provides strong consistency but blocks
- Saga provides availability with eventual consistency
- TCC uses business-level compensation
- Event Sourcing provides audit trail
- Choose pattern based on requirements
- Handle timeouts and failures
- Implement recovery mechanisms

**Mastery Checklist:**
- ✅ Understand distributed transaction patterns
- ✅ Implement Two-Phase Commit
- ✅ Implement Saga pattern
- ✅ Implement TCC
- ✅ Implement Event Sourcing
- ✅ Handle timeouts and failures
- ✅ Design compensation logic
- ✅ Choose appropriate pattern

