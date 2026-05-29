# API Gateway

API Gateway is a server that acts as an API front-end, receiving API requests, enforcing throttling and security policies, passing requests to the appropriate backend service, and returning responses.

## Introduction

API Gateway is a server that acts as an API front-end, receiving API requests, enforcing throttling and security policies, passing requests to the appropriate backend service, and returning responses. It serves as a single entry point for all client requests, handling cross-cutting concerns like authentication, authorization, rate limiting, caching, request routing, and response aggregation. API Gateway is essential in microservice architectures where clients need to interact with multiple services. It abstracts the backend complexity from clients, providing a unified interface. Popular API Gateway solutions include AWS API Gateway, Kong, NGINX, and Ambassador. API Gateway patterns include the Gateway Aggregation pattern, Backend for Frontend (BFF), and the Gateway Routing pattern.

**Why API Gateway Matters:**
- Single entry point for all APIs
- Centralizes cross-cutting concerns
- Abstracts backend complexity
- Enables microservice architecture
- Improves security and monitoring
- Simplifies client integration

**Where It Is Used:**
- Microservice architectures
- Public API management
- Internal service communication
- Mobile application backends
- Enterprise API platforms
- API monetization platforms

## Core Concept Explanation

API Gateway acts as a reverse proxy that sits between clients and backend services. It receives all client requests and routes them to the appropriate service based on URL patterns, headers, or other routing rules. The gateway handles cross-cutting concerns like authentication (validating tokens), authorization (checking permissions), rate limiting (preventing abuse), caching (improving performance), request/response transformation (protocol translation), and monitoring (logging and metrics). It can also aggregate responses from multiple services into a single response for the client. The gateway maintains a service registry or uses service discovery to find available service instances. This architecture allows backend services to evolve independently without breaking client integrations.

**Step-by-Step Breakdown:**
1. Client sends request to API Gateway
2. Gateway authenticates the request (JWT, OAuth, API key)
3. Gateway authorizes the request (check permissions)
4. Gateway checks rate limits
5. Gateway routes request to appropriate service
6. Service processes request and returns response
7. Gateway transforms response if needed
8. Gateway returns response to client
9. Gateway logs request/response for monitoring

**Intuition Behind the Concept:**
Think of API Gateway like a receptionist at a large company. When you call the company, the receptionist (gateway) answers first. They verify who you are (authentication), check if you're allowed to speak to the person you're asking for (authorization), direct your call to the right department (routing), and may even gather information from multiple departments before giving you a complete answer (aggregation). You don't need to know the internal structure of the company - the receptionist handles all that complexity for you.

**Visual Thinking:**
```
Client → API Gateway → Multiple Services
         ↓              ↓
    Authentication  User Service
    Authorization   Order Service
    Rate Limiting    Product Service
    Routing          Payment Service
    Caching          Inventory Service
    Logging          Notification Service
    Monitoring       Analytics Service

Request Flow:
Client Request → Gateway → Auth Check → Rate Limit → Route → Service → Response → Gateway → Client

Service Discovery:
Gateway → Service Registry → Service Instances
         ↓
    Load Balancer
         ↓
    Healthy Instance
```

## Internal Working / Logic

API Gateway operates through a series of middleware layers that process each request before routing it to the appropriate service. The gateway maintains a service registry or integrates with a service discovery system to find available service instances. Each request passes through authentication, authorization, rate limiting, and routing middleware. The gateway can transform requests and responses, aggregate multiple service calls, and cache responses. It implements circuit breakers to fail fast when services are unavailable and retries for transient failures. The gateway logs all requests and responses for monitoring and debugging purposes.

**Operation 1: Request Processing**
- Client sends HTTP request to gateway
- Gateway extracts authentication credentials
- Gateway validates credentials against auth service
- Gateway checks rate limits (per client, per API)
- Gateway routes request based on URL pattern
- Gateway forwards request to backend service
- Gateway receives response from service
- Gateway transforms response if needed
- Gateway returns response to client

**Operation 2: Service Discovery**
- Gateway queries service registry
- Registry returns available service instances
- Gateway selects instance (round-robin, least connections)
- Gateway forwards request to selected instance
- If instance fails, gateway retries with another instance
- Gateway marks unhealthy instances for circuit breaker

**Operation 3: Request Aggregation**
- Client requests data requiring multiple services
- Gateway splits request into sub-requests
- Gateway sends sub-requests to multiple services in parallel
- Gateway waits for all responses
- Gateway aggregates responses into single response
- Gateway returns aggregated response to client

**Operation 4: Circuit Breaker**
- Gateway tracks service failure rate
- If failure rate exceeds threshold, open circuit
- Open circuit: fail fast without calling service
- After timeout, attempt to close circuit (half-open)
- If request succeeds, close circuit
- If request fails, keep circuit open

**Flow Explanation (Request Processing):**
1. Client sends request to gateway endpoint
2. Authentication middleware validates credentials
3. Authorization middleware checks permissions
4. Rate limiter checks request count
5. Router matches URL to service
6. Service discovery finds healthy instance
7. Gateway forwards request to service
8. Service processes and returns response
9. Gateway logs request/response
10. Gateway returns response to client

**Decision Making Logic:**
The key decisions are:
- Which service to route to (based on URL, headers, parameters)
- Whether to allow request (auth, rate limit, circuit breaker)
- How to transform request/response (protocol translation)
- Whether to cache response (based on endpoint, headers)
- Whether to aggregate multiple service calls
- How to handle failures (retry, circuit breaker, fallback)

## Algorithm / Approach

**API Gateway Routing Algorithm**

```
1. Receive request from client
2. Extract authentication credentials
3. Validate credentials
4. Check rate limits
5. Match URL pattern to service
6. Discover service instance
7. Forward request to service
8. Receive response
9. Transform response if needed
10. Return response to client
```

**Service Discovery Algorithm**

```
1. Query service registry
2. Get list of available instances
3. Filter healthy instances
4. Select instance (round-robin, least connections)
5. Return instance address
6. Monitor instance health
```

**Rate Limiting Algorithm**

```
1. Extract client identifier (IP, API key, user ID)
2. Get current request count
3. Check if count exceeds limit
4. If exceeded, return 429 Too Many Requests
5. If not exceeded, increment count
6. Set expiration for count
```

**Circuit Breaker Algorithm**

```
1. Track service failure rate
2. If failure rate > threshold, open circuit
3. Open circuit: fail fast without calling service
4. After timeout, attempt half-open state
5. If request succeeds, close circuit
6. If request fails, keep circuit open
```

## Implementations

### 1. Simple API Gateway with Express

```javascript
const express = require('express');
const http = require('http');
const app = express();

app.use(express.json());

// Service registry
const services = {
  users: 'http://localhost:3001',
  orders: 'http://localhost:3002',
  products: 'http://localhost:3003'
};

// Rate limiting (in-memory)
const rateLimit = new Map();
const RATE_LIMIT = 100; // requests per minute

function checkRateLimit(req, res, next) {
  const ip = req.ip;
  const now = Date.now();
  const requests = rateLimit.get(ip) || [];
  
  // Remove old requests (older than 1 minute)
  const recent = requests.filter(t => now - t < 60000);
  
  if (recent.length >= RATE_LIMIT) {
    return res.status(429).json({ error: 'Rate limit exceeded' });
  }
  
  recent.push(now);
  rateLimit.set(ip, recent);
  next();
}

// Proxy to service
function proxyRequest(service, req, res) {
  const options = {
    hostname: new URL(services[service]).hostname,
    port: new URL(services[service]).port,
    path: req.url,
    method: req.method,
    headers: req.headers
  };
  
  const proxyReq = http.request(options, (proxyRes) => {
    res.writeHead(proxyRes.statusCode, proxyRes.headers);
    proxyRes.pipe(res);
  });
  
  req.pipe(proxyReq);
}

// Route to user service
app.use('/api/users', checkRateLimit, (req, res) => {
  proxyRequest('users', req, res);
});

// Route to order service
app.use('/api/orders', checkRateLimit, (req, res) => {
  proxyRequest('orders', req, res);
});

// Route to product service
app.use('/api/products', checkRateLimit, (req, res) => {
  proxyRequest('products', req, res);
});

app.listen(3000, () => console.log('API Gateway running on port 3000'));
```

**Advantages:**
- Single entry point
- Centralized rate limiting
- Simple routing
- Easy to implement

### 2. API Gateway with Authentication

```javascript
const express = require('express');
const jwt = require('jsonwebtoken');
const http = require('http');
const app = express();

app.use(express.json());

const SECRET_KEY = 'your-secret-key';
const services = {
  users: 'http://localhost:3001',
  orders: 'http://localhost:3002'
};

// Authentication middleware
function authenticateToken(req, res, next) {
  const authHeader = req.headers['authorization'];
  const token = authHeader && authHeader.split(' ')[1];
  
  if (!token) {
    return res.status(401).json({ error: 'Access token required' });
  }
  
  jwt.verify(token, SECRET_KEY, (err, user) => {
    if (err) {
      return res.status(403).json({ error: 'Invalid token' });
    }
    req.user = user;
    next();
  });
}

// Public endpoint (no auth)
app.get('/api/public', (req, res) => {
  res.json({ message: 'Public endpoint' });
});

// Protected endpoint (requires auth)
app.use('/api/users', authenticateToken, (req, res) => {
  proxyRequest('users', req, res);
});

app.use('/api/orders', authenticateToken, (req, res) => {
  proxyRequest('orders', req, res);
});

function proxyRequest(service, req, res) {
  const options = {
    hostname: new URL(services[service]).hostname,
    port: new URL(services[service]).port,
    path: req.url,
    method: req.method,
    headers: { ...req.headers, 'x-user-id': req.user.id }
  };
  
  const proxyReq = http.request(options, (proxyRes) => {
    res.writeHead(proxyRes.statusCode, proxyRes.headers);
    proxyRes.pipe(res);
  });
  
  req.pipe(proxyReq);
}

app.listen(3000, () => console.log('API Gateway running on port 3000'));
```

**Advantages:**
- Centralized authentication
- JWT token validation
- User context propagation
- Protected endpoints

### 3. API Gateway with Circuit Breaker

```javascript
const express = require('express');
const http = require('http');
const app = express();

app.use(express.json());

const services = {
  users: 'http://localhost:3001',
  orders: 'http://localhost:3002'
};

// Circuit breaker state
const circuitBreakers = {
  users: { failures: 0, lastFailure: 0, state: 'closed' },
  orders: { failures: 0, lastFailure: 0, state: 'closed' }
};

const FAILURE_THRESHOLD = 5;
const TIMEOUT = 60000; // 1 minute

function checkCircuitBreaker(service) {
  const breaker = circuitBreakers[service];
  const now = Date.now();
  
  // Reset if timeout passed
  if (breaker.state === 'open' && now - breaker.lastFailure > TIMEOUT) {
    breaker.state = 'half-open';
    breaker.failures = 0;
  }
  
  // Open circuit: fail fast
  if (breaker.state === 'open') {
    return false;
  }
  
  return true;
}

function recordFailure(service) {
  const breaker = circuitBreakers[service];
  breaker.failures++;
  breaker.lastFailure = Date.now();
  
  if (breaker.failures >= FAILURE_THRESHOLD) {
    breaker.state = 'open';
  }
}

function recordSuccess(service) {
  const breaker = circuitBreakers[service];
  breaker.failures = 0;
  breaker.state = 'closed';
}

function proxyWithCircuitBreaker(service, req, res) {
  if (!checkCircuitBreaker(service)) {
    return res.status(503).json({ error: 'Service unavailable' });
  }
  
  const options = {
    hostname: new URL(services[service]).hostname,
    port: new URL(services[service]).port,
    path: req.url,
    method: req.method,
    headers: req.headers
  };
  
  const proxyReq = http.request(options, (proxyRes) => {
    recordSuccess(service);
    res.writeHead(proxyRes.statusCode, proxyRes.headers);
    proxyRes.pipe(res);
  });
  
  proxyReq.on('error', () => {
    recordFailure(service);
    res.status(503).json({ error: 'Service unavailable' });
  });
  
  req.pipe(proxyReq);
}

app.use('/api/users', (req, res) => {
  proxyWithCircuitBreaker('users', req, res);
});

app.use('/api/orders', (req, res) => {
  proxyWithCircuitBreaker('orders', req, res);
});

app.listen(3000, () => console.log('API Gateway running on port 3000'));
```

**Advantages:**
- Fail fast for failing services
- Automatic recovery
- Prevents cascading failures
- Improved resilience

### 4. API Gateway with Response Aggregation

```javascript
const express = require('express');
const app = express();

app.use(express.json());

const services = {
  users: 'http://localhost:3001',
  orders: 'http://localhost:3002',
  products: 'http://localhost:3003'
};

// Aggregate user data from multiple services
async function aggregateUserData(userId) {
  const [user, orders, recommendations] = await Promise.all([
    fetch(`${services.users}/users/${userId}`).then(r => r.json()),
    fetch(`${services.orders}/orders?userId=${userId}`).then(r => r.json()),
    fetch(`${services.products}/recommendations?userId=${userId}`).then(r => r.json())
  ]);
  
  return {
    user,
    orders,
    recommendations
  };
}

app.get('/api/v1/user/:id/complete', async (req, res) => {
  try {
    const userId = req.params.id;
    const data = await aggregateUserData(userId);
    res.json(data);
  } catch (error) {
    res.status(500).json({ error: 'Failed to aggregate data' });
  }
});

app.listen(3000, () => console.log('API Gateway running on port 3000'));
```

**Advantages:**
- Single request for multiple services
- Reduced client complexity
- Parallel service calls
- Unified response format

### 5. API Gateway with Caching

```javascript
const express = require('express');
const NodeCache = require('node-cache');
const http = require('http');
const app = express();

app.use(express.json());

const services = {
  products: 'http://localhost:3003'
};

const cache = new NodeCache({ stdTTL: 300 }); // 5 minutes

function proxyWithCache(service, req, res) {
  const cacheKey = `${service}:${req.method}:${req.url}`;
  const cachedResponse = cache.get(cacheKey);
  
  if (cachedResponse) {
    return res.json(cachedResponse);
  }
  
  const options = {
    hostname: new URL(services[service]).hostname,
    port: new URL(services[service]).port,
    path: req.url,
    method: req.method,
    headers: req.headers
  };
  
  const proxyReq = http.request(options, (proxyRes) => {
    let data = '';
    
    proxyRes.on('data', chunk => {
      data += chunk;
    });
    
    proxyRes.on('end', () => {
      const parsed = JSON.parse(data);
      cache.set(cacheKey, parsed);
      res.json(parsed);
    });
  });
  
  req.pipe(proxyReq);
}

app.use('/api/products', (req, res) => {
  if (req.method === 'GET') {
    proxyWithCache('products', req, res);
  } else {
    // Don't cache non-GET requests
    proxyRequest('products', req, res);
  }
});

function proxyRequest(service, req, res) {
  const options = {
    hostname: new URL(services[service]).hostname,
    port: new URL(services[service]).port,
    path: req.url,
    method: req.method,
    headers: req.headers
  };
  
  const proxyReq = http.request(options, (proxyRes) => {
    res.writeHead(proxyRes.statusCode, proxyRes.headers);
    proxyRes.pipe(res);
  });
  
  req.pipe(proxyReq);
}

app.listen(3000, () => console.log('API Gateway running on port 3000'));
```

**Advantages:**
- Reduced backend load
- Faster response times
- Lower latency
- Improved scalability

## Dry Run

**Example: API Gateway Request Flow**

**Request:**
```
GET /api/users/123
Headers: {
  "Authorization": "Bearer eyJhbGciOiJIUzI1NiIs...",
  "Content-Type": "application/json"
}
```

**Step-by-Step Execution:**

```
1. Client sends GET /api/users/123 to API Gateway
2. Gateway receives request
3. Authentication middleware validates JWT token
   - Token valid → Proceed
   - Token invalid → Return 401 Unauthorized
4. Rate limiter checks request count for client IP
   - Under limit → Proceed
   - Over limit → Return 429 Too Many Requests
5. Router matches /api/users to user service
6. Circuit breaker checks user service health
   - Circuit closed → Proceed
   - Circuit open → Return 503 Service Unavailable
7. Gateway forwards request to user service
8. User service processes request and returns user data
9. Gateway receives response from user service
10. Gateway logs request/response
11. Gateway returns response to client
```

**Request/Response Table:**

| Step | Component | Action | Status |
|------|-----------|--------|--------|
| 1 | Client | Send GET /api/users/123 | - |
| 2 | Gateway | Receive request | - |
| 3 | Auth Middleware | Validate JWT | Valid |
| 4 | Rate Limiter | Check rate limit | Under limit |
| 5 | Router | Match to user service | Matched |
| 6 | Circuit Breaker | Check service health | Closed |
| 7 | Gateway | Forward to user service | - |
| 8 | User Service | Process request | Success |
| 9 | Gateway | Receive response | - |
| 10 | Gateway | Log request/response | - |
| 11 | Gateway | Return to client | 200 OK |

## Edge Cases

### 1. Gateway Bottleneck
```javascript
// High traffic overwhelms gateway
// Gateway becomes bottleneck
// Scale horizontally
```

### 2. Service Failure
```javascript
// Backend service unavailable
// Circuit breaker opens
// Return cached response or error
```

### 3. Authentication Failure
```javascript
// Invalid or expired token
// Return 401 Unauthorized
// Client should refresh token
```

### 4. Rate Limit Exceeded
```javascript
// Client exceeds rate limit
// Return 429 Too Many Requests
// Include Retry-After header
```

### 5. Timeout
```javascript
// Service takes too long
// Gateway times out
// Return 504 Gateway Timeout
```

### 6. Service Discovery Failure
```javascript
// Service registry unavailable
// Gateway cannot find service
// Return 503 Service Unavailable
```

**Why Edge Cases Matter:**
- Gateway is single point of failure
- Must handle service failures gracefully
- Rate limiting prevents abuse
- Authentication is security critical
- Timeouts prevent hanging requests
- Service discovery essential for dynamic environments

## Variations / Extensions

### 1. Backend for Frontend (BFF)

```javascript
// Separate gateway per client type
// Mobile gateway, web gateway
// Optimized for each client
```

### 2. API Gateway with WebSocket Support

```javascript
// Gateway handles WebSocket connections
// Routes to appropriate service
- Maintains connection state
```

### 3. API Gateway with GraphQL

```javascript
// Gateway as GraphQL endpoint
// Resolvers call backend services
- Schema stitching
```

### 4. API Gateway with Service Mesh Integration

```javascript
// Gateway integrates with service mesh
// Uses sidecar proxies
- Advanced routing
```

### 5. API Gateway with API Versioning

```javascript
// Gateway handles version routing
// /api/v1/users → v1 service
// /api/v2/users → v2 service
```

## Optimization Techniques

### 1. Connection Pooling

**Reuse Backend Connections:**
```javascript
// Pool connections to backend services
// Reduce connection overhead
- Improve performance
```

### 2. Response Compression

**Compress Responses:**
```javascript
// Gzip compression
// Reduce payload size
- Faster transfer
```

### 3. HTTP/2

**Use HTTP/2:**
```javascript
// Multiplexing
// Header compression
- Better performance
```

### 4. Edge Caching

**Cache at Edge:**
```javascript
// Use CDN for caching
// Reduce latency
- Better user experience
```

### 5. Trade-offs

**API Gateway vs Direct Service Access:**

| Aspect | API Gateway | Direct Access |
|--------|-------------|---------------|
| Complexity | High | Low |
| Flexibility | High | Low |
| Performance | Lower (extra hop) | Higher |
| Security | Centralized | Distributed |
| Monitoring | Centralized | Distributed |

**When to Use API Gateway:**
- Multiple microservices
- Need centralized auth
- Need rate limiting
- Public APIs
- Complex routing needs

## Complexity Analysis

### Time Complexity

**Request Processing: O(1) to O(n)**
- Simple routing: O(1)
- With aggregation: O(n) where n = number of services
- Authentication: O(1)
- Rate limiting: O(1)

**Service Discovery: O(1) to O(n)**
- Static registry: O(1)
- Dynamic discovery: O(n) where n = number of instances
- Health checks: O(n)

### Space Complexity

**Rate Limiting: O(n)**
- n = number of clients
- In-memory storage
- Can use Redis for distributed

**Circuit Breaker: O(m)**
- m = number of services
- Minimal state storage
- O(1) per service

**Explanation:**
API Gateway adds minimal overhead to request processing. The main complexity comes from authentication (O(1)), rate limiting (O(1)), and routing (O(1)). Aggregation adds O(n) where n is the number of services called. Service discovery can be O(1) with static registry or O(n) with dynamic discovery. Space complexity is primarily for rate limiting (O(n) clients) and circuit breaker state (O(m) services).

## Real-world Applications

### 1. Microservice Platforms

**Service Communication:**
- Netflix API Gateway
- Amazon API Gateway
- Google Cloud Endpoints
- Example: Netflix Zuul

### 2. Public API Platforms

**API Management:**
- Stripe API
- Twilio API
- SendGrid API
- Example: Stripe's API Gateway

### 3. Mobile Applications

**Backend for Frontend:**
- Uber API Gateway
- Airbnb API Gateway
- Instagram API Gateway
- Example: Uber's BFF pattern

### 4. Enterprise Systems

**Internal APIs:**
- Service mesh gateways
- Internal API management
- Legacy system integration
- Example: Enterprise API Gateway

### 5. E-commerce

**API Orchestration:**
- Product catalog
- Inventory management
- Order processing
- Example: Amazon API Gateway

### 6. Financial Services

**Secure APIs:**
- Trading APIs
- Banking APIs
- Payment processing
- Example: PayPal API Gateway

### 7. IoT Platforms

**Device APIs:**
- Device management
- Data collection
- Command execution
- Example: AWS IoT Gateway

### 8. Healthcare

**Data APIs:**
- Patient records
- Medical devices
- Lab results
- Example: Healthcare API Gateway

## Common Mistakes

### 1. Gateway as Single Point of Failure

**Mistake:**
```javascript
// Single gateway instance
// No redundancy
// Gateway failure = system failure
```

**Correct:**
```javascript
// Deploy multiple gateway instances
// Use load balancer
// High availability
```

**Why It Matters:**
- Gateway is critical path
- Must be highly available
- Single point of failure unacceptable

### 2. No Rate Limiting

**Mistake:**
```javascript
// Unlimited requests
- Can abuse backend services
- Denial of service
- Resource exhaustion
```

**Correct:**
```javascript
// Implement rate limiting
- Protect backend services
- Fair usage
- Prevent abuse
```

**Why It Matters:**
- Protects backend services
- Prevents abuse
- Ensures fair usage

### 3. No Circuit Breaker

**Mistake:**
```javascript
// No circuit breaker
- Cascading failures
- Slow failures
- Poor user experience
```

**Correct:**
```javascript
// Implement circuit breaker
- Fail fast
- Prevent cascading failures
- Better resilience
```

**Why It Matters:**
- Prevents cascading failures
- Improves resilience
- Better user experience

### 4. No Monitoring

**Mistake:**
```javascript
// No logging or metrics
- No visibility
- Hard to debug
- Can't detect issues
```

**Correct:**
```javascript
// Implement comprehensive monitoring
- Log all requests
- Track metrics
- Set up alerts
```

**Why It Matters:**
- Visibility essential
- Debugging requires logs
- Metrics for optimization

### 5. No Authentication

**Mistake:**
```javascript
// Public endpoints that should be private
// No authentication
// Security risk
```

**Correct:**
```javascript
// Implement authentication
- JWT, OAuth, API keys
- Protect sensitive endpoints
```

**Why It Matters:**
- Security critical
- Protect user data
- Prevent unauthorized access

### 6. Over-Aggregation

**Mistake:**
```javascript
// Aggregate too many services
- Slow responses
- High latency
- Poor user experience
```

**Correct:**
```javascript
// Aggregate only when needed
- Parallel calls
- Cache results
- Timeout appropriately
```

**Why It Matters:**
- Latency affects UX
- Too many calls slow responses
- Balance aggregation with performance

## Advanced Concepts

### 1. Service Mesh

**Concept:**
Dedicated infrastructure for service-to-service communication.

**Features:**
- Sidecar proxies
- Traffic management
- Security
- Observability

### 2. GraphQL Gateway

**Concept:**
Gateway that handles GraphQL queries.

**Features:**
- Schema stitching
- Query planning
- Federation

### 3. API Gateway with WAF

**Concept:**
Web Application Firewall integration.

**Features:**
- DDoS protection
- SQL injection prevention
- XSS protection

### 4. API Gateway with API Management

**Concept:**
Full API lifecycle management.

**Features:**
- API versioning
- Developer portal
- API keys
- Usage analytics

## Practice Thinking Guide

### How to Design an API Gateway

**Key Questions to Ask:**

1. **What services need to be exposed?**
   - Identify all backend services
   - Define API surface
   - Example: "Users, Orders, Products"

2. **What cross-cutting concerns?**
   - Authentication, authorization, rate limiting
   - Caching, logging, monitoring
   - Example: "JWT auth, rate limiting, caching"

3. **What routing rules?**
   - URL patterns, header-based routing
   - Version routing
   - Example: "/api/v1/users → user service v1"

4. **How to handle failures?**
   - Circuit breaker, retries, fallbacks
   - Graceful degradation
   - Example: "Circuit breaker with fallback"

5. **How to scale?**
   - Horizontal scaling, load balancing
   - Caching, connection pooling
   - Example: "Multiple instances with load balancer"

**Pattern Recognition:**

**Pattern 1: Microservice Gateway**
```
Services: Multiple microservices
Operations: Routing, auth, rate limiting
Solution: API Gateway with service discovery
```

**Pattern 2: BFF Pattern**
```
Clients: Mobile, web, desktop
Operations: Client-specific optimization
Solution: Separate gateway per client type
```

**Pattern 3: Aggregation Gateway**
```
Services: Multiple services needed for single response
Operations: Parallel calls, aggregation
Solution: Gateway with request aggregation
```

**Pattern 4: Public API Gateway**
```
Services: Internal services
Operations: API management, monetization
Solution: Gateway with API management features
```

**Pattern 5: GraphQL Gateway**
```
Services: Multiple data sources
Operations: Schema stitching, query resolution
Solution: GraphQL gateway with federation
```

**Decision Flowchart:**

```
API Gateway Decision:
├─ Multiple services?
│        ├─ Yes → Need API Gateway
│        └─ No → May not need gateway
├─ Public API?
│        ├─ Yes → Need API Gateway
│        └─ No → May use simpler routing
├─ Need centralized auth?
│        ├─ Yes → Need API Gateway
│        └─ No → May handle per service
└─ Need rate limiting?
         ├─ Yes → Need API Gateway
         └─ No → May handle per service
```

**Example Analysis:**

**Scenario:** "Design API Gateway for e-commerce platform"

**Analysis:**
1. Services: Users, Products, Orders, Payments, Inventory
2. Cross-cutting: JWT auth, rate limiting, caching, logging
3. Routing: URL-based, version-based
4. Failures: Circuit breaker, retries, fallbacks
5. Scaling: Horizontal scaling, load balancing, caching
6. Solution: Full-featured API Gateway

**Scenario:** "Design BFF for mobile app"

**Analysis:**
1. Services: Optimized for mobile
2. Cross-cutting: Mobile-specific auth, compression
3. Routing: Mobile-specific endpoints
4. Failures: Graceful degradation
5. Scaling: CDN integration, edge caching
6. Solution: Mobile BFF with optimization

## Summary

API Gateway is a server that acts as an API front-end, receiving API requests, enforcing throttling and security policies, passing requests to the appropriate backend service, and returning responses. It serves as a single entry point for all client requests, handling cross-cutting concerns like authentication, authorization, rate limiting, caching, request routing, and response aggregation. API Gateway is essential in microservice architectures where clients need to interact with multiple services. It abstracts backend complexity from clients, providing a unified interface. Key features include service discovery, circuit breakers, request aggregation, and comprehensive monitoring. The gateway must be highly available and scalable to avoid becoming a bottleneck.

**Key Takeaways:**
- Single entry point for APIs
- Centralizes cross-cutting concerns
- Routes requests to microservices
- Handles authentication and rate limiting
- Aggregates responses from multiple services
- Implements circuit breakers for resilience
- Essential for microservice architecture
- Must be highly available and scalable

**Mastery Checklist:**
- ✅ Understand API Gateway patterns
- ✅ Implement request routing
- ✅ Implement authentication
- ✅ Implement rate limiting
- ✅ Implement circuit breaker
- ✅ Implement service discovery
- ✅ Implement response aggregation
- ✅ Design for high availability

