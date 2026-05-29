# Rate Limiting

Rate limiting controls the rate of incoming requests to a service, protecting it from abuse, ensuring fair usage, and maintaining service availability.

## Introduction

Rate limiting controls the rate of incoming requests to a service, protecting it from abuse, ensuring fair usage, and maintaining service availability. Rate limiting tracks the number of requests from a user or IP address within a time window and blocks requests that exceed a predefined threshold. Common rate limiting algorithms include Fixed Window (count requests in fixed time intervals), Sliding Window (more precise, avoids burst at boundaries), Token Bucket (allows bursts, smooths out traffic), and Leaky Bucket (constant rate, no bursts). Rate limiting can be implemented at various levels: per user (fair usage), per IP (prevent abuse), per endpoint (protect critical resources), or globally (overall capacity). Distributed rate limiting uses Redis or similar distributed stores to share rate limit state across multiple servers. Rate limiting is essential for API protection from abuse, fair resource allocation, preventing DDoS attacks, and managing service capacity. Key features include configurable limits, different user tiers (free, premium), and proper communication via HTTP headers (X-RateLimit-Limit, X-RateLimit-Remaining, Retry-After).

**Why Rate Limiting Matters:**
- Protects services from abuse and DDoS
- Ensures fair resource allocation
- Prevents service overload
- Enables capacity planning
- Essential for public APIs
- Maintains service availability

**Where It Is Used:**
- Public APIs (Twitter, GitHub)
- Web applications (e-commerce, social media)
- Microservices (service-to-service communication)
- API gateways (rate limiting at gateway)
- Load balancers (rate limiting at edge)
- CDN (rate limiting at edge)

## Core Concept Explanation

Rate limiting tracks and controls the rate of incoming requests to protect services from abuse, ensure fair usage, and maintain availability. The basic concept is to count requests from a user or IP address within a time window and block requests that exceed a threshold. Fixed Window algorithm divides time into fixed intervals (e.g., 1 minute) and counts requests in each interval. Sliding Window algorithm uses a sliding time window for more precise control, avoiding bursts at window boundaries. Token Bucket algorithm uses a bucket of tokens that refills at a constant rate - each request consumes a token, and if the bucket is empty, requests are blocked. Leaky Bucket algorithm processes requests at a constant rate, smoothing out traffic. Rate limiting can be per user (fair usage), per IP (prevent abuse), per endpoint (protect critical resources), or global (overall capacity). Distributed rate limiting uses Redis or similar distributed stores to share rate limit state across multiple servers. Rate limiting communicates limits via HTTP headers (X-RateLimit-Limit, X-RateLimit-Remaining, Retry-After) so clients know their limits and when to retry.

**Step-by-Step Breakdown:**
1. Client sends request
2. Rate limiter checks request count
3. If under limit, allow request
4. Increment request count
5. If over limit, block request
6. Return rate limit headers
7. Client waits and retries
8. Request count resets after window

**Intuition Behind the Concept:**
Think of rate limiting like a bouncer at a club. The bouncer counts how many people enter and allows only a certain number per minute. If too many people try to enter, the bouncer blocks them and tells them to wait. Fixed Window is like counting people per minute - at 12:00, the count resets. Sliding Window is like counting people in the last minute continuously - at 12:00:30, it counts people from 11:59:30 to 12:00:30. Token Bucket is like giving out tickets that refill over time - if you have a ticket, you can enter; if not, you wait for more tickets. Leaky Bucket is like processing people at a constant rate - people line up and enter one by one.

**Visual Thinking:**
```
Fixed Window:
[12:00-12:01] 10 requests → Allowed
[12:01-12:02] 15 requests → Blocked (limit 10)

Sliding Window:
[11:59:30-12:00:30] 8 requests → Allowed
[12:00:00-12:01:00] 12 requests → Blocked (limit 10)

Token Bucket:
Bucket: [Token][Token][Token][Token][Token]
Request: Consume 1 token → 4 tokens remaining
Refill: 1 token per second
```

## Internal Working / Logic

Rate limiting operates through request counting and threshold enforcement. The Fixed Window algorithm divides time into fixed intervals (e.g., 1 minute) and counts requests in each interval. When a request arrives, the rate limiter checks the current time window and counts requests in that window. If the count is below the threshold, the request is allowed and the count is incremented. If the count is at or above the threshold, the request is blocked. The Sliding Window algorithm uses a sliding time window for more precise control - it counts requests in the last N seconds continuously, avoiding bursts at window boundaries. Token Bucket algorithm uses a bucket of tokens that refills at a constant rate - each request consumes a token, and if the bucket is empty, requests are blocked. Leaky Bucket algorithm processes requests at a constant rate, smoothing out traffic by queuing requests and processing them one by one. Distributed rate limiting uses Redis or similar distributed stores to share rate limit state across multiple servers, ensuring consistent rate limiting in distributed systems. Rate limiting communicates limits via HTTP headers (X-RateLimit-Limit, X-RateLimit-Remaining, Retry-After) so clients know their limits and when to retry.

**Operation 1: Fixed Window Rate Limiting**
- Request arrives
- Determine current time window
- Count requests in window
- If count < threshold, allow
- Increment count
- If count >= threshold, block
- Return rate limit headers

**Operation 2: Sliding Window Rate Limiting**
- Request arrives
- Calculate sliding window (last N seconds)
- Count requests in sliding window
- If count < threshold, allow
- Add request timestamp
- If count >= threshold, block
- Return rate limit headers

**Operation 3: Token Bucket Rate Limiting**
- Request arrives
- Calculate elapsed time since last refill
- Refill tokens based on elapsed time
- If tokens >= required, allow
- Consume tokens
- If tokens < required, block
- Return rate limit headers

**Operation 4: Distributed Rate Limiting**
- Request arrives
- Query distributed store for count
- If count < threshold, allow
- Increment count in distributed store
- Set expiration time
- If count >= threshold, block
- Return rate limit headers

**Flow Explanation (Fixed Window):**
1. Client sends request at 12:00:30
2. Rate limiter determines window: 12:00-12:01
3. Rate limiter counts requests in window: 5
4. Threshold is 10
5. Count (5) < threshold (10), allow
6. Increment count to 6
7. Request processed
8. Return headers: X-RateLimit-Limit: 10, X-RateLimit-Remaining: 4

**Decision Making Logic:**
The key decisions are:
- Rate limiting algorithm (fixed, sliding, token bucket, leaky bucket)
- Time window size (1 minute, 1 hour, 1 day)
- Threshold value (10, 100, 1000 requests)
- Scope (per user, per IP, per endpoint, global)
- Storage (in-memory, Redis, distributed)
- Response to exceeded limit (block, throttle, queue)

## Algorithm / Approach

**Fixed Window Algorithm**

```
1. Request arrives
2. Determine current time window
3. Count requests in window
4. If count < threshold:
   a. Allow request
   b. Increment count
5. If count >= threshold:
   a. Block request
   b. Return rate limit headers
6. Reset count at window boundary
```

**Sliding Window Algorithm**

```
1. Request arrives
2. Calculate sliding window (last N seconds)
3. Count requests in sliding window
4. If count < threshold:
   a. Allow request
   b. Add request timestamp
5. If count >= threshold:
   a. Block request
   b. Return rate limit headers
6. Remove timestamps outside window
```

**Token Bucket Algorithm**

```
1. Request arrives
2. Calculate elapsed time since last refill
3. Refill tokens based on elapsed time
4. If tokens >= required:
   a. Allow request
   b. Consume tokens
5. If tokens < required:
   a. Block request
   b. Return rate limit headers
6. Cap tokens at capacity
```

**Leaky Bucket Algorithm**

```
1. Request arrives
2. Add request to queue
3. Process requests at constant rate
4. If queue size < capacity:
   a. Allow request
   b. Add to queue
5. If queue size >= capacity:
   a. Block request
   b. Return rate limit headers
6. Process next request from queue
```

## Implementations

### 1. Fixed Window Rate Limiter

```javascript
class FixedWindowRateLimiter {
  constructor(limit, windowSeconds) {
    this.limit = limit;
    this.windowSeconds = windowSeconds;
    this.requests = new Map();
  }
  
  isAllowed(userId) {
    const now = Date.now();
    const windowStart = now - (this.windowSeconds * 1000);
    const windowEnd = now;
    
    let userRequests = this.requests.get(userId) || [];
    
    // Remove old requests outside window
    userRequests = userRequests.filter(reqTime => reqTime >= windowStart);
    
    if (userRequests.length < this.limit) {
      userRequests.push(now);
      this.requests.set(userId, userRequests);
      return {
        allowed: true,
        remaining: this.limit - userRequests.length,
        resetAt: windowEnd + (this.windowSeconds * 1000)
      };
    }
    
    return {
      allowed: false,
      remaining: 0,
      resetAt: windowEnd + (this.windowSeconds * 1000)
    };
  }
}

// Usage
const rateLimiter = new FixedWindowRateLimiter(10, 60); // 10 requests per minute

function handleRequest(userId) {
  const result = rateLimiter.isAllowed(userId);
  
  if (result.allowed) {
    console.log('Request allowed');
    // Process request
  } else {
    console.log('Request blocked, retry after:', new Date(result.resetAt));
    // Return 429 Too Many Requests
  }
}
```

**Advantages:**
- Simple to implement
- Low memory usage
- Easy to understand
- Good for basic use cases

### 2. Sliding Window Rate Limiter

```javascript
class SlidingWindowRateLimiter {
  constructor(limit, windowSeconds) {
    this.limit = limit;
    this.windowSeconds = windowSeconds;
    this.requests = new Map();
  }
  
  isAllowed(userId) {
    const now = Date.now();
    const windowStart = now - (this.windowSeconds * 1000);
    
    let userRequests = this.requests.get(userId) || [];
    
    // Remove old requests outside sliding window
    userRequests = userRequests.filter(reqTime => reqTime >= windowStart);
    
    if (userRequests.length < this.limit) {
      userRequests.push(now);
      this.requests.set(userId, userRequests);
      return {
        allowed: true,
        remaining: this.limit - userRequests.length,
        resetAt: userRequests[0] + (this.windowSeconds * 1000)
      };
    }
    
    return {
      allowed: false,
      remaining: 0,
      resetAt: userRequests[0] + (this.windowSeconds * 1000)
    };
  }
}

// Usage
const rateLimiter = new SlidingWindowRateLimiter(10, 60); // 10 requests per minute

function handleRequest(userId) {
  const result = rateLimiter.isAllowed(userId);
  
  if (result.allowed) {
    console.log('Request allowed');
    // Process request
  } else {
    console.log('Request blocked, retry after:', new Date(result.resetAt));
    // Return 429 Too Many Requests
  }
}
```

**Advantages:**
- More precise than fixed window
- Avoids burst at boundaries
- Better user experience
- Fairer rate limiting

### 3. Token Bucket Rate Limiter

```javascript
class TokenBucketRateLimiter {
  constructor(capacity, refillRate) {
    this.capacity = capacity;
    this.refillRate = refillRate; // tokens per second
    this.tokens = capacity;
    this.lastRefill = Date.now();
  }
  
  isAllowed(tokens = 1) {
    const now = Date.now();
    const elapsed = (now - this.lastRefill) / 1000;
    
    // Refill tokens
    this.tokens = Math.min(
      this.capacity,
      this.tokens + elapsed * this.refillRate
    );
    this.lastRefill = now;
    
    if (this.tokens >= tokens) {
      this.tokens -= tokens;
      return {
        allowed: true,
        remaining: Math.floor(this.tokens),
        resetAt: now + ((this.capacity - this.tokens) / this.refillRate) * 1000
      };
    }
    
    return {
      allowed: false,
      remaining: 0,
      resetAt: now + ((tokens - this.tokens) / this.refillRate) * 1000
    };
  }
}

// Usage
const rateLimiter = new TokenBucketRateLimiter(10, 1); // 10 tokens, 1 token per second

function handleRequest() {
  const result = rateLimiter.isAllowed(1);
  
  if (result.allowed) {
    console.log('Request allowed');
    // Process request
  } else {
    console.log('Request blocked, retry after:', new Date(result.resetAt));
    // Return 429 Too Many Requests
  }
}
```

**Advantages:**
- Allows bursts
- Smooths out traffic
- Flexible rate limiting
- Good for APIs

### 4. Leaky Bucket Rate Limiter

```javascript
class LeakyBucketRateLimiter {
  constructor(capacity, rate) {
    this.capacity = capacity;
    this.rate = rate; // requests per second
    this.queue = [];
    this.lastLeak = Date.now();
  }
  
  isAllowed() {
    const now = Date.now();
    const elapsed = (now - this.lastLeak) / 1000;
    
    // Leak requests
    const leakCount = Math.floor(elapsed * this.rate);
    this.queue = this.queue.slice(leakCount);
    this.lastLeak = now;
    
    if (this.queue.length < this.capacity) {
      this.queue.push(now);
      return {
        allowed: true,
        remaining: this.capacity - this.queue.length,
        resetAt: now + ((this.capacity - this.queue.length) / this.rate) * 1000
      };
    }
    
    return {
      allowed: false,
      remaining: 0,
      resetAt: now + (this.queue.length / this.rate) * 1000
    };
  }
}

// Usage
const rateLimiter = new LeakyBucketRateLimiter(10, 1); // 10 capacity, 1 request per second

function handleRequest() {
  const result = rateLimiter.isAllowed();
  
  if (result.allowed) {
    console.log('Request allowed');
    // Process request
  } else {
    console.log('Request blocked, retry after:', new Date(result.resetAt));
    // Return 429 Too Many Requests
  }
}
```

**Advantages:**
- Constant rate
- Smooths out traffic
- No bursts
- Good for streaming

### 5. Distributed Rate Limiter with Redis

```javascript
class DistributedRateLimiter {
  constructor(redisClient, limit, windowSeconds) {
    this.redis = redisClient;
    this.limit = limit;
    this.windowSeconds = windowSeconds;
  }
  
  async isAllowed(userId) {
    const key = `ratelimit:${userId}`;
    const now = Date.now();
    const windowStart = now - (this.windowSeconds * 1000);
    
    // Remove old requests
    await this.redis.zremrangebyscore(key, 0, windowStart);
    
    // Count current requests
    const count = await this.redis.zcard(key);
    
    if (count < this.limit) {
      // Add current request
      await this.redis.zadd(key, now, now);
      // Set expiration
      await this.redis.expire(key, this.windowSeconds);
      
      return {
        allowed: true,
        remaining: this.limit - count - 1
      };
    }
    
    // Get oldest request timestamp
    const oldest = await this.redis.zrange(key, 0, 0, 'WITHSCORES');
    const resetAt = oldest[0][1] + (this.windowSeconds * 1000);
    
    return {
      allowed: false,
      remaining: 0,
      resetAt
    };
  }
}

// Usage
const redis = require('redis');
const client = redis.createClient();

const rateLimiter = new DistributedRateLimiter(client, 10, 60); // 10 requests per minute

async function handleRequest(userId) {
  const result = await rateLimiter.isAllowed(userId);
  
  if (result.allowed) {
    console.log('Request allowed');
    // Process request
  } else {
    console.log('Request blocked, retry after:', new Date(result.resetAt));
    // Return 429 Too Many Requests
  }
}
```

**Advantages:**
- Distributed across servers
- Consistent rate limiting
- Redis-backed persistence
- Scalable

## Dry Run

**Example: Fixed Window Rate Limiting**

**Initial State:**
```
Limit: 10 requests per minute
Window: 12:00-12:01
Current count: 0
```

**Step-by-Step Execution:**

```
Step 1: Request at 12:00:10
Step 2: Window: 12:00-12:01
Step 3: Count: 0
Step 4: Count (0) < threshold (10), allow
Step 5: Increment count to 1
Step 6: Request processed
Step 7: Request at 12:00:20
Step 8: Count: 1
Step 9: Count (1) < threshold (10), allow
Step 10: Increment count to 2
Step 11: Request at 12:00:55
Step 12: Count: 9
Step 13: Count (9) < threshold (10), allow
Step 14: Increment count to 10
Step 15: Request at 12:00:58
Step 16: Count: 10
Step 17: Count (10) >= threshold (10), block
Step 18: Return 429 Too Many Requests
```

**Request/Response Table:**

| Time | Count | Threshold | Action | Remaining |
|------|-------|-----------|--------|-----------|
| 12:00:10 | 0 | 10 | Allow | 9 |
| 12:00:20 | 1 | 10 | Allow | 8 |
| 12:00:55 | 9 | 10 | Allow | 0 |
| 12:00:58 | 10 | 10 | Block | 0 |

## Edge Cases

### 1. Clock Synchronization
```javascript
// Clocks out of sync in distributed systems
- Inconsistent rate limiting
// Solution: Use distributed time, NTP
```

### 2. Redis Failure
```javascript
// Redis unavailable
- Rate limiting fails
// Solution: Fallback to local rate limiting
```

### 3. Multiple Concurrent Requests
```javascript
// Concurrent requests exceed limit
- Race conditions
// Solution: Atomic operations, locking
```

### 4. Rate Limit Evasion
```javascript
// Users evade rate limiting
- Multiple IPs, rotating IPs
// Solution: Per-user limits, IP reputation
```

### 5. Time Window Boundary
```javascript
// Burst at window boundary
- Fixed window allows burst
// Solution: Sliding window
```

### 6. Memory Exhaustion
```javascript
// Too many users tracked
- Memory exhausted
// Solution: Evict old entries, use Redis
```

**Why Edge Cases Matter:**
- Clock sync causes inconsistent limiting
- Redis failure causes rate limiting failure
- Concurrent requests cause race conditions
- Evasion causes abuse
- Boundary burst causes unfairness
- Memory exhaustion causes failure

## Variations / Extensions

### 1. Hierarchical Rate Limiting

```javascript
// Multiple levels of limits
- Per-user, per-IP, per-endpoint
// Example: API tiers
```

### 2. Adaptive Rate Limiting

```javascript
// Adjust limits based on load
- Dynamic thresholds
// Example: Auto-scaling
```

### 3. Rate Limiting by Response

```javascript
// Rate limit based on response
- Different limits for different operations
// Example: Read vs write
```

### 4. Rate Limiting with Quotas

```javascript
// Quota-based rate limiting
- Daily/monthly quotas
// Example: API quotas
```

### 5. Rate Limiting with Backoff

```javascript
// Exponential backoff
- Gradual retry
// Example: Client-side retry
```

## Optimization Techniques

### 1. Use Sliding Window

**More Precise:**
```javascript
// Sliding window algorithm
- Better precision
// Fairer rate limiting
```

### 2. Use Redis

**Distributed Storage:**
```javascript
// Redis for distributed rate limiting
- Consistent across servers
// Better scalability
```

### 3. Use Token Bucket

**Allow Bursts:**
```javascript
// Token bucket algorithm
- Allow bursts
// Better user experience
```

### 4. Use Hierarchical Limits

**Multiple Levels:**
```javascript
// Per-user, per-IP, per-endpoint
- More granular control
// Better protection
```

### 5. Trade-offs

**Algorithm Comparison:**

| Algorithm | Precision | Burst Handling | Complexity | Use Case |
|-----------|-----------|----------------|------------|----------|
| Fixed Window | Low | Poor | Low | Simple APIs |
| Sliding Window | High | Medium | Medium | Fair APIs |
| Token Bucket | Medium | Good | Medium | Bursty traffic |
| Leaky Bucket | High | Poor | Medium | Constant rate |

**When to Use Each:**
- Fixed Window: Simple APIs, low complexity
- Sliding Window: Fair APIs, precision needed
- Token Bucket: Bursty traffic, flexibility needed
- Leaky Bucket: Constant rate, streaming

## Complexity Analysis

### Time Complexity

**Fixed Window: O(1)**
- Constant time
- Simple count
- Very fast

**Sliding Window: O(n)**
- n = number of requests in window
- Filter old requests
- Linear with requests

**Token Bucket: O(1)**
- Constant time
- Token calculation
- Very fast

### Space Complexity

**Fixed Window: O(n)**
- n = number of users
- Linear with users
- Memory bound

**Sliding Window: O(n)**
- n = number of requests per user
- Linear with requests
- Memory bound

**Token Bucket: O(1)**
- Constant space
- Token count
- Minimal

**Explanation:**
Fixed Window is O(1) time - constant time for count check. Sliding Window is O(n) where n is the number of requests in window - filter old requests. Token Bucket is O(1) - constant time for token calculation. Space complexity for Fixed Window is O(n) where n is the number of users - linear with users. Sliding Window is O(n) where n is the number of requests per user - linear with requests. Token Bucket is O(1) - constant space for token count. The trade-off is between precision (sliding window) and simplicity (fixed window).

## Real-world Applications

### 1. API Protection

**Public APIs:**
- Prevent abuse
- Example: Twitter API, GitHub API

### 2. Fair Resource Allocation

**Multi-tenant Systems:**
- Fair usage
- Example: SaaS applications

### 3. Preventing DDoS Attacks

**Web Applications:**
- Block abusive traffic
- Example: E-commerce sites

### 4. Managing Service Capacity

**Microservices:**
- Prevent overload
- Example: Service-to-service communication

### 5. API Tiers

**Pricing Tiers:**
- Different limits for different tiers
- Example: Free vs Premium API

### 6. Web Scraping Prevention

**Content Sites:**
- Block scrapers
- Example: News sites

### 7. Login Protection

**Authentication:**
- Prevent brute force
- Example: Login pages

### 8. API Gateway

**Edge Protection:**
- Rate limit at edge
- Example: Cloudflare, AWS API Gateway

## Common Mistakes

### 1. Fixed Window Only

**Mistake:**
```javascript
// Only fixed window
- Burst at boundaries
// Unfair rate limiting
```

**Correct:**
```javascript
// Use sliding window
- More precise
// Fairer rate limiting
```

**Why It Matters:**
- Fixed window = burst at boundaries
- Unfair rate limiting
- Sliding window essential

### 2. No Distributed Storage

**Mistake:**
```javascript
// Local rate limiting only
- Inconsistent across servers
// Poor accuracy
```

**Correct:**
```javascript
// Use Redis for distributed
- Consistent across servers
// Better accuracy
```

**Why It Matters:**
- No distributed storage = inconsistent
- Poor accuracy
- Redis essential

### 3. No Rate Limit Headers

**Mistake:**
```javascript
// No headers
- Clients don't know limits
// Poor UX
```

**Correct:**
```javascript
// Add rate limit headers
- Clients know limits
// Better UX
```

**Why It Matters:**
- No headers = poor UX
- Clients don't know limits
- Headers essential

### 4. Wrong Time Window

**Mistake:**
```javascript
// Window too short or long
- Too strict or too lenient
// Poor user experience
```

**Correct:**
```javascript
// Set appropriate window
- Balance strictness and leniency
// Better UX
```

**Why It Matters:**
- Wrong window = poor UX
- Too strict or too lenient
- Appropriate window essential

### 5. No Fallback

**Mistake:**
```javascript
// No fallback for Redis failure
- Rate limiting fails
// Poor reliability
```

**Correct:**
```javascript
// Implement fallback
- Local rate limiting
// Better reliability
```

**Why It Matters:**
- No fallback = rate limiting fails
- Poor reliability
- Fallback essential

### 6. No Monitoring

**Mistake:**
```javascript
// No rate limit monitoring
- Issues go unnoticed
// Poor visibility
```

**Correct:**
```javascript
// Monitor rate limiting
- Detect issues early
// Better visibility
```

**Why It Matters:**
- No monitoring = issues unnoticed
- Poor visibility
- Monitoring essential

## Advanced Concepts

### 1. Sliding Window Log

**Concept:**
Precise sliding window with logs.

**Features:**
- High precision
- More memory
- Better accuracy

### 2. Distributed Rate Limiting

**Concept:**
Rate limiting across multiple servers.

**Features:**
- Consistent limiting
- Redis-backed
- Scalable

### 3. Adaptive Rate Limiting

**Concept:**
Adjust limits based on load.

**Features:**
- Dynamic thresholds
- Auto-scaling
- Better resource utilization

### 4. Rate Limiting by Response

**Concept:**
Different limits for different operations.

**Features:**
- Granular control
- Resource-based
- Better protection

## Practice Thinking Guide

### How to Design Rate Limiting Strategy

**Key Questions to Ask:**

1. **Precision required?**
   - Low: Fixed window
   - High: Sliding window
   - Example: "Sliding window for fair APIs"

2. **Burst handling?**
   - Yes: Token bucket
   - No: Leaky bucket
   - Example: "Token bucket for bursty traffic"

3. **Distributed?**
   - Yes: Redis-backed
   - No: In-memory
   - Example: "Redis for distributed systems"

4. **Scope?**
   - Per user: Fair usage
   - Per IP: Abuse prevention
   - Example: "Per-user for fair usage"

5. **Response to exceeded limit?**
   - Block: 429 error
   - Throttle: Slow down
   - Example: "Block with 429"

**Pattern Recognition:**

**Pattern 1: Public API**
```
Requirements: Fair usage, abuse prevention
Solution: Sliding window with Redis
Implementation: Per-user limits, rate limit headers
```

**Pattern 2: DDoS Protection**
```
Requirements: High throughput, block abuse
Solution: Fixed window at edge
Implementation: Per-IP limits, block immediately
```

**Pattern 3: Microservices**
```
Requirements: Service-to-service, distributed
Solution: Token bucket with Redis
Implementation: Per-service limits, distributed storage
```

**Pattern 4: Login Protection**
```
Requirements: Prevent brute force
Solution: Leaky bucket
Implementation: Per-IP limits, exponential backoff
```

**Pattern 5: API Tiers**
```
Requirements: Different limits for tiers
Solution: Hierarchical limits
Implementation: Per-tier limits, quota-based
```

**Decision Flowchart:**

```
Rate Limiting Decision:
├─ Precision required?
│        ├─ Low → Fixed window
│        └─ High → Sliding window
├─ Burst handling?
│        ├─ Yes → Token bucket
│        └─ No → Leaky bucket
├─ Distributed?
│        ├─ Yes → Redis-backed
│        └─ No → In-memory
└─ Scope?
         ├─ Per user → Fair usage
         ├─ Per IP → Abuse prevention
         └─ Per endpoint → Resource protection
```

**Example Analysis:**

**Scenario:** "Design rate limiting for public API"

**Analysis:**
1. Requirements: Fair usage, abuse prevention
2. Algorithm: Sliding window
3. Storage: Redis-backed
4. Scope: Per-user
5. Headers: X-RateLimit-Limit, X-RateLimit-Remaining
6. Implementation: Sliding window with Redis

**Scenario:** "Design rate limiting for login page"

**Analysis:**
1. Requirements: Prevent brute force
2. Algorithm: Leaky bucket
3. Storage: In-memory
4. Scope: Per-IP
5. Response: Block with exponential backoff
6. Implementation: Leaky bucket with backoff

## Summary

Rate limiting controls the rate of incoming requests to a service, protecting it from abuse, ensuring fair usage, and maintaining service availability. Rate limiting tracks the number of requests from a user or IP address within a time window and blocks requests that exceed a predefined threshold. Common rate limiting algorithms include Fixed Window (count requests in fixed time intervals), Sliding Window (more precise, avoids burst at boundaries), Token Bucket (allows bursts, smooths out traffic), and Leaky Bucket (constant rate, no bursts). Rate limiting can be implemented at various levels: per user (fair usage), per IP (prevent abuse), per endpoint (protect critical resources), or global (overall capacity). Distributed rate limiting uses Redis or similar distributed stores to share rate limit state across multiple servers. Rate limiting is essential for API protection from abuse, fair resource allocation, preventing DDoS attacks, and managing service capacity. Key features include configurable limits, different user tiers (free, premium), and proper communication via HTTP headers (X-RateLimit-Limit, X-RateLimit-Remaining, Retry-After).

**Key Takeaways:**
- Protects services from abuse and DDoS
- Ensures fair resource allocation
- Prevents service overload
- Multiple algorithms: fixed, sliding, token bucket, leaky bucket
- Distributed rate limiting with Redis
- Rate limit headers for client communication
- Hierarchical limits for granular control
- Essential for public APIs

**Mastery Checklist:**
- ✅ Understand rate limiting concepts
- ✅ Implement fixed window rate limiter
- ✅ Implement sliding window rate limiter
- ✅ Implement token bucket rate limiter
- ✅ Implement leaky bucket rate limiter
- ✅ Implement distributed rate limiting
- ✅ Configure rate limit headers
- ✅ Design rate limiting strategy

