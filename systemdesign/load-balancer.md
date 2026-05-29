# Load Balancer

A Load Balancer distributes incoming network traffic across multiple servers to ensure no single server bears too much demand, improving responsiveness and availability.

## Introduction

A Load Balancer distributes incoming network traffic across multiple servers to ensure no single server bears too much demand, improving responsiveness and availability. Load balancers act as a reverse proxy, sitting between clients and backend servers, distributing incoming requests based on various algorithms like round-robin, least connections, IP hash, and weighted distribution. They perform health checks to detect unhealthy servers and automatically route traffic away from them, ensuring high availability. Load balancers also handle SSL termination, session persistence, and can operate at Layer 4 (transport layer) or Layer 7 (application layer). Popular load balancers include Nginx, HAProxy, AWS ELB, and hardware load balancers from F5 and Citrix. Load balancing is essential for horizontal scaling, high availability, and handling high traffic loads in modern distributed systems.

**Why Load Balancer Matters:**
- Distributes traffic across multiple servers
- Ensures no single server is overwhelmed
- Provides high availability through failover
- Enables horizontal scaling
- Handles SSL termination
- Improves application performance

**Where It Is Used:**
- Web application scaling
- API gateway traffic distribution
- Microservice communication
- Database read replica routing
- CDN edge server selection
- Cloud load balancing

## Core Concept Explanation

Load balancers distribute incoming network traffic across multiple backend servers using various algorithms. They act as a single entry point for clients, hiding the complexity of multiple backend servers. When a request arrives, the load balancer selects a backend server based on the configured algorithm and forwards the request. The load balancer continuously performs health checks on backend servers, removing unhealthy ones from the rotation and adding them back when they recover. This ensures high availability and automatic failover. Load balancers can operate at Layer 4 (TCP/UDP) for faster performance or Layer 7 (HTTP) for content-aware routing. They also handle SSL termination, decrypting HTTPS traffic and forwarding plaintext to backend servers, reducing the cryptographic load on backend servers.

**Step-by-Step Breakdown:**
1. Client sends request to load balancer
2. Load balancer selects backend server based on algorithm
3. Load balancer forwards request to selected server
4. Backend server processes request
5. Backend server returns response to load balancer
6. Load balancer returns response to client
7. Load balancer performs health checks on all servers
8. Unhealthy servers are removed from rotation
9. Load balancer monitors performance metrics

**Intuition Behind the Concept:**
Think of a load balancer like a receptionist at a busy restaurant. When customers arrive, the receptionist (load balancer) directs them to available tables (servers) based on availability. If a waiter (server) is busy or unavailable, the receptionist directs customers to other waiters. This ensures no single waiter is overwhelmed and customers are served efficiently. The receptionist also checks if waiters are available (health checks) and directs customers away from unavailable ones.

**Visual Thinking:**
```
Request Flow:
Client → Load Balancer → Backend Servers
         ↓                  ↓
    Algorithm Selection  Server 1
         ↓                  ↓
    Health Check         Server 2
         ↓                  ↓
    SSL Termination      Server 3
         ↓                  ↓
    Forward Request      Server 4

Load Balancing Algorithms:
Round Robin: 1, 2, 3, 4, 1, 2, 3, 4...
Least Connections: Server with fewest active connections
IP Hash: Hash client IP, map to server
Weighted: Distribute based on server capacity
```

## Internal Working / Logic

Load balancers operate by maintaining a pool of backend servers and distributing incoming requests based on a configured algorithm. The load balancer continuously performs health checks on all backend servers, typically by sending HTTP requests or TCP connections to a health endpoint. Servers that fail health checks are marked as unhealthy and removed from the rotation. When a request arrives, the load balancer selects a backend server based on the algorithm, forwards the request, and returns the response to the client. The load balancer can also perform SSL termination, decrypting HTTPS traffic and forwarding plaintext to backend servers. Session persistence can be implemented using IP hash, cookies, or session affinity to ensure that requests from the same client are routed to the same backend server.

**Operation 1: Request Routing**
- Client sends request to load balancer
- Load balancer receives request
- Load balancer selects backend server based on algorithm
- Load balancer forwards request to selected server
- Backend server processes request
- Backend server returns response to load balancer
- Load balancer returns response to client

**Operation 2: Health Checking**
- Load balancer sends health check to server
- Server responds to health check
- Load balancer marks server as healthy or unhealthy
- Unhealthy servers removed from rotation
- Healthy servers added to rotation
- Continuous health checking ensures availability

**Operation 3: SSL Termination**
- Client sends HTTPS request to load balancer
- Load balancer decrypts SSL/TLS
- Load balancer forwards plaintext to backend
- Backend server processes request
- Backend server returns plaintext response
- Load balancer encrypts response
- Load balancer returns HTTPS response to client

**Operation 4: Session Persistence**
- Client sends request with session cookie
- Load balancer extracts session identifier
- Load balancer hashes session identifier
- Load balancer routes to consistent backend server
- Future requests with same session routed to same server
- Maintains session state on single server

**Flow Explanation (Request Routing):**
1. Client sends HTTP request to load balancer
2. Load balancer parses request
3. Load balancer selects backend server based on algorithm
4. Load balancer forwards request to backend server
5. Backend server processes request
6. Backend server returns response
7. Load balancer returns response to client
8. Load balancer logs request for monitoring

**Decision Making Logic:**
The key decisions are:
- Which load balancing algorithm to use (round-robin, least connections, IP hash)
- Whether to use Layer 4 or Layer 7 load balancing
- How to handle SSL (termination or pass-through)
- Whether to implement session persistence
- Health check interval and timeout
- How to handle server failures (failover, retry)

## Algorithm / Approach

**Round Robin Algorithm**

```
1. Maintain list of healthy servers
2. Maintain current index
3. On request, select server at current index
4. Increment index (wrap around at end)
5. Return selected server
```

**Least Connections Algorithm**

```
1. Track active connections per server
2. On request, select server with fewest connections
3. Increment connection count for selected server
4. Return selected server
5. Decrement connection count when request completes
```

**IP Hash Algorithm**

```
1. Extract client IP address
2. Hash IP address
3. Map hash to server index
4. Return selected server
5. Same IP always maps to same server
```

**Weighted Round Robin Algorithm**

```
1. Assign weight to each server
2. On request, select server based on weight
3. Higher weight = more requests
4. Return selected server
5. Distribute proportionally to capacity
```

## Implementations

### 1. Round Robin Load Balancer

```javascript
class RoundRobinLoadBalancer {
  constructor(servers) {
    this.servers = servers;
    this.healthy = new Set(servers);
    this.currentIndex = 0;
  }
  
  getNextServer() {
    if (this.healthy.size === 0) {
      throw new Error("No healthy servers available");
    }
    
    const healthyServers = Array.from(this.healthy);
    const server = healthyServers[this.currentIndex];
    this.currentIndex = (this.currentIndex + 1) % healthyServers.length;
    return server;
  }
  
  markUnhealthy(server) {
    this.healthy.delete(server);
  }
  
  markHealthy(server) {
    if (this.servers.includes(server)) {
      this.healthy.add(server);
    }
  }
}

// Usage
const lb = new RoundRobinLoadBalancer(['server1', 'server2', 'server3']);
console.log(lb.getNextServer()); // server1
console.log(lb.getNextServer()); // server2
console.log(lb.getNextServer()); // server3
console.log(lb.getNextServer()); // server1
```

**Advantages:**
- Simple implementation
- Even distribution
- No server state needed
- Fair distribution

### 2. Least Connections Load Balancer

```javascript
class LeastConnectionsLoadBalancer {
  constructor(servers) {
    this.servers = servers;
    this.healthy = new Set(servers);
    this.connections = new Map();
    servers.forEach(server => this.connections.set(server, 0));
  }
  
  getNextServer() {
    if (this.healthy.size === 0) {
      throw new Error("No healthy servers available");
    }
    
    return Array.from(this.healthy).reduce((minServer, server) => {
      const currentConnections = this.connections.get(server) || 0;
      const minConnections = this.connections.get(minServer) || 0;
      return currentConnections < minConnections ? server : minServer;
    });
  }
  
  incrementConnections(server) {
    const current = this.connections.get(server) || 0;
    this.connections.set(server, current + 1);
  }
  
  decrementConnections(server) {
    const current = this.connections.get(server) || 0;
    this.connections.set(server, Math.max(0, current - 1));
  }
  
  markUnhealthy(server) {
    this.healthy.delete(server);
  }
  
  markHealthy(server) {
    if (this.servers.includes(server)) {
      this.healthy.add(server);
    }
  }
}

// Usage
const lb = new LeastConnectionsLoadBalancer(['server1', 'server2', 'server3']);
lb.incrementConnections('server1');
lb.incrementConnections('server1');
console.log(lb.getNextServer()); // server2 or server3 (fewer connections)
```

**Advantages:**
- Accounts for server load
- Better for variable request duration
- More efficient distribution
- Adapts to current load

### 3. IP Hash Load Balancer

```javascript
class IPHashLoadBalancer {
  constructor(servers) {
    this.servers = servers;
    this.healthy = new Set(servers);
  }
  
  _hash(ip) {
    let hash = 0;
    for (let i = 0; i < ip.length; i++) {
      hash = ((hash << 5) - hash) + ip.charCodeAt(i);
      hash |= 0;
    }
    return Math.abs(hash);
  }
  
  getServer(clientIP) {
    if (this.healthy.size === 0) {
      throw new Error("No healthy servers available");
    }
    
    const healthyServers = Array.from(this.healthy);
    const hash = this._hash(clientIP);
    const index = hash % healthyServers.length;
    return healthyServers[index];
  }
  
  markUnhealthy(server) {
    this.healthy.delete(server);
  }
  
  markHealthy(server) {
    if (this.servers.includes(server)) {
      this.healthy.add(server);
    }
  }
}

// Usage
const lb = new IPHashLoadBalancer(['server1', 'server2', 'server3']);
console.log(lb.getServer('192.168.1.1')); // Always same server for same IP
console.log(lb.getServer('192.168.1.1')); // Same server as above
```

**Advantages:**
- Session persistence
- Same client to same server
- Simple implementation
- Good for stateful applications

### 4. Weighted Round Robin Load Balancer

```javascript
class WeightedRoundRobinLoadBalancer {
  constructor(servers) {
    this.servers = servers.map((server, index) => ({
      server,
      weight: 1,
      currentWeight: 0
    }));
    this.healthy = new Set(servers);
    this.totalWeight = servers.length;
  }
  
  setWeight(server, weight) {
    const serverObj = this.servers.find(s => s.server === server);
    if (serverObj) {
      serverObj.weight = weight;
      this.totalWeight = this.servers.reduce((sum, s) => sum + s.weight, 0);
    }
  }
  
  getNextServer() {
    if (this.healthy.size === 0) {
      throw new Error("No healthy servers available");
    }
    
    const healthyServers = this.servers.filter(s => this.healthy.has(s.server));
    
    // Add weight to current
    healthyServers.forEach(s => {
      s.currentWeight += s.weight;
    });
    
    // Find server with highest current weight
    let selected = healthyServers[0];
    healthyServers.forEach(s => {
      if (s.currentWeight > selected.currentWeight) {
        selected = s;
      }
    });
    
    // Subtract total weight from selected
    selected.currentWeight -= this.totalWeight;
    
    return selected.server;
  }
  
  markUnhealthy(server) {
    this.healthy.delete(server);
  }
  
  markHealthy(server) {
    if (this.servers.some(s => s.server === server)) {
      this.healthy.add(server);
    }
  }
}

// Usage
const lb = new WeightedRoundRobinLoadBalancer(['server1', 'server2', 'server3']);
lb.setWeight('server1', 3); // Higher capacity
lb.setWeight('server2', 1); // Lower capacity
lb.setWeight('server3', 1); // Lower capacity
console.log(lb.getNextServer()); // More likely to be server1
```

**Advantages:**
- Accounts for server capacity
- Proportional distribution
- Better resource utilization
- Handles heterogeneous servers

### 5. Load Balancer with Health Checks

```javascript
class LoadBalancerWithHealthChecks {
  constructor(servers, healthCheckInterval = 5000) {
    this.servers = servers;
    this.healthy = new Set(servers);
    this.healthCheckInterval = healthCheckInterval;
    this.startHealthChecks();
  }
  
  async healthCheck(server) {
    try {
      const response = await fetch(`${server}/health`, {
        method: 'GET',
        timeout: 2000
      });
      return response.ok;
    } catch (error) {
      return false;
    }
  }
  
  async checkAllServers() {
    for (const server of this.servers) {
      const isHealthy = await this.healthCheck(server);
      if (isHealthy) {
        this.healthy.add(server);
      } else {
        this.healthy.delete(server);
      }
    }
  }
  
  startHealthChecks() {
    setInterval(() => {
      this.checkAllServers();
    }, this.healthCheckInterval);
  }
  
  getNextServer() {
    if (this.healthy.size === 0) {
      throw new Error("No healthy servers available");
    }
    
    const healthyServers = Array.from(this.healthy);
    const index = Math.floor(Math.random() * healthyServers.length);
    return healthyServers[index];
  }
}

// Usage
const lb = new LoadBalancerWithHealthChecks(
  ['http://server1:3000', 'http://server2:3000', 'http://server3:3000'],
  5000 // Check every 5 seconds
);
```

**Advantages:**
- Automatic failover
- High availability
- Self-healing
- Reduced downtime

## Dry Run

**Example: Round Robin Load Balancing**

**Initial State:**
```
Servers: server1, server2, server3
All servers healthy
Current index: 0
```

**Step-by-Step Execution:**

```
Request 1:
1. Client sends request to load balancer
2. Load balancer selects server at index 0
3. Load balancer forwards to server1
4. Server1 processes request
5. Server1 returns response
6. Load balancer returns response to client
7. Index incremented to 1

Request 2:
1. Client sends request to load balancer
2. Load balancer selects server at index 1
3. Load balancer forwards to server2
4. Server2 processes request
5. Server2 returns response
6. Load balancer returns response to client
7. Index incremented to 2

Request 3:
1. Client sends request to load balancer
2. Load balancer selects server at index 2
3. Load balancer forwards to server3
4. Server3 processes request
5. Server3 returns response
6. Load balancer returns response to client
7. Index wrapped to 0

Request 4:
1. Client sends request to load balancer
2. Load balancer selects server at index 0
3. Load balancer forwards to server1
4. Server1 processes request
5. Server1 returns response
6. Load balancer returns response to client
7. Index incremented to 1
```

**Request/Response Table:**

| Request | Selected Server | Index | Status |
|---------|----------------|--------|--------|
| 1 | server1 | 0 | Success |
| 2 | server2 | 1 | Success |
| 3 | server3 | 2 | Success |
| 4 | server1 | 0 | Success |
| 5 | server2 | 1 | Success |

## Edge Cases

### 1. All Servers Unhealthy
```javascript
// No healthy servers available
// Cannot serve requests
// Solution: Return error, use fallback
```

### 2. Server Failure During Request
```javascript
// Server fails while processing
// Request lost or error
// Solution: Retry, failover
```

### 3. Slow Server Detection
```javascript
// Server responding slowly
- Degraded performance
// Solution: Health check timeout, remove
```

### 4. Network Partitions
```javascript
// Load balancer cannot reach servers
- Requests fail
// Solution: Multiple load balancers, failover
```

### 5. Thundering Herd
```javascript
// All requests to one server after failover
- Server overwhelmed
// Solution: Gradual reintroduction
```

### 6. Session Loss
```javascript
// Session persistence broken
- User logged out
// Solution: Sticky sessions, distributed sessions
```

**Why Edge Cases Matter:**
- All servers down = complete outage
- Server failures during requests cause errors
- Slow servers degrade performance
- Network partitions cause downtime
- Thundering herd overwhelms servers
- Session loss affects user experience

## Variations / Extensions

### 1. Layer 7 Load Balancing

```javascript
// HTTP-aware routing
- Based on URL, headers, cookies
- Content-aware distribution
```

### 2. Global Server Load Balancing

```javascript
// Geographic routing
- Route to nearest datacenter
- DNS-based routing
```

### 3. Software Load Balancer

```javascript
// Nginx, HAProxy
- Flexible configuration
- Cost-effective
```

### 4. Hardware Load Balancer

```javascript
// F5, Citrix
- High performance
- Expensive
```

### 5. Cloud Load Balancer

```javascript
// AWS ELB, GCP Load Balancing
- Managed service
- Auto-scaling integration
```

## Optimization Techniques

### 1. Connection Pooling

**Reuse Connections:**
```javascript
// Pool connections to backend servers
- Reduce connection overhead
- Better performance
```

### 2. Keep-Alive Connections

**Persistent Connections:**
```javascript
// Keep connections alive
- Reduce connection overhead
- Faster requests
```

### 3. HTTP/2

**Use HTTP/2:**
```javascript
// Multiplexing, header compression
- Better performance
- Lower latency
```

### 4. Caching

**Cache Responses:**
```javascript
// Cache responses at load balancer
- Reduce backend load
- Faster responses
```

### 5. Trade-offs

**Load Balancing Algorithms Comparison:**

| Algorithm | Distribution | Complexity | Use Case |
|-----------|--------------|------------|----------|
| Round Robin | Even | Low | General purpose |
| Least Connections | Load-aware | Medium | Variable load |
| IP Hash | Session-sticky | Low | Stateful apps |
| Weighted | Capacity-aware | Medium | Heterogeneous servers |

**When to Use Each:**
- Round Robin: General purpose, similar servers
- Least Connections: Variable request duration
- IP Hash: Session persistence required
- Weighted: Heterogeneous server capacities

## Complexity Analysis

### Time Complexity

**Round Robin: O(1)**
- Simple index increment
- Constant time selection
- No server state needed

**Least Connections: O(n)**
- n = number of servers
- Find minimum connections
- Linear scan

**IP Hash: O(1)**
- Hash computation
- Modulo operation
- Constant time

**Weighted Round Robin: O(n)**
- n = number of servers
- Find maximum weight
- Linear scan

### Space Complexity

**Server State: O(n)**
- n = number of servers
- Track health, connections, weights
- Minimal overhead

**Explanation:**
Round Robin and IP Hash are O(1) time complexity - simple operations with constant time. Least Connections and Weighted Round Robin are O(n) where n is the number of servers, requiring a linear scan to find the minimum or maximum. Space complexity is O(n) for tracking server state (health, connections, weights). The trade-off is between algorithm complexity and distribution quality.

## Real-world Applications

### 1. Web Applications

**Web Server Load Balancing:**
- Nginx, HAProxy
- HTTP traffic distribution
- Example: E-commerce websites

### 2. API Gateways

**API Traffic Distribution:**
- AWS API Gateway
- Kong, Ambassador
- Example: REST APIs

### 3. Microservices

**Service-to-Service Communication:**
- Service mesh
- Sidecar proxies
- Example: Kubernetes services

### 4. Database

**Read Replica Routing:**
- Database read replicas
- Query distribution
- Example: MySQL read replicas

### 5. Cloud Platforms

**Cloud Load Balancing:**
- AWS ELB, GCP LB
- Auto-scaling integration
- Example: Cloud applications

### 6. CDN

**Edge Server Selection:**
- Geographic routing
- Anycast
- Example: Content delivery

### 7. Gaming

**Game Server Load Balancing:**
- Player distribution
- Session persistence
- Example: Multiplayer games

### 8. Streaming

**Media Server Load Balancing:**
- Video streaming
- Adaptive bitrate
- Example: Netflix, YouTube

## Common Mistakes

### 1. No Health Checks

**Mistake:**
```javascript
// No health checks
// Unhealthy servers in rotation
// Poor availability
```

**Correct:**
```javascript
// Implement health checks
// Remove unhealthy servers
// High availability
```

**Why It Matters:**
- No health checks = poor availability
- Unhealthy servers cause errors
- Health checks ensure reliability

### 2. Wrong Algorithm

**Mistake:**
```javascript
// Use round-robin for stateful app
// Sessions lost
// Poor user experience
```

**Correct:**
```javascript
// Use IP hash for stateful app
// Session persistence
// Better user experience
```

**Why It Matters:**
- Wrong algorithm = poor distribution
- Session loss affects users
- Match algorithm to use case

### 3. No SSL Termination

**Mistake:**
```javascript
// Pass-through SSL
// Backend handles encryption
- High backend load
```

**Correct:**
```javascript
// Terminate SSL at load balancer
- Reduce backend load
// Better performance
```

**Why It Matters:**
- SSL termination reduces backend load
- Better performance
- Centralized certificate management

### 4. Single Load Balancer

**Mistake:**
```javascript
// Single load balancer
- Single point of failure
// Outage affects all
```

**Correct:**
```javascript
// Multiple load balancers
- High availability
// Failover capability
```

**Why It Matters:**
- Single LB = single point of failure
- Outage affects all traffic
- Multiple LBs ensure availability

### 5. No Monitoring

**Mistake:**
```javascript
// No monitoring
// Don't know performance
// Can't optimize
```

**Correct:**
```javascript
// Monitor load balancer
// Track metrics
// Set up alerts
```

**Why It Matters:**
- Monitoring essential for optimization
- Metrics indicate performance
- Alerts catch issues early

### 6. Ignoring Weights

**Mistake:**
```javascript
// All servers equal weight
// Heterogeneous servers
// Uneven load
```

**Correct:**
```javascript
// Use weighted distribution
- Proportional to capacity
// Better resource utilization
```

**Why It Matters:**
- Heterogeneous servers need weights
- Equal weights = uneven load
- Weighted distribution = better balance

## Advanced Concepts

### 1. Layer 7 Load Balancing

**Concept:**
HTTP-aware routing.

**Features:**
- URL-based routing
- Header-based routing
- Content-aware distribution

### 2. Global Server Load Balancing

**Concept:**
Geographic routing.

**Features:**
- DNS-based routing
- Anycast
- Geographic proximity

### 3. Service Mesh

**Concept:**
Service-to-service load balancing.

**Features:**
- Sidecar proxies
- Service discovery
- Traffic management

### 4. Consistent Hashing

**Concept:**
Hash-based routing.

**Features:**
- Minimal remapping
- Session persistence
- Cache-friendly

## Practice Thinking Guide

### How to Design Load Balancing Strategy

**Key Questions to Ask:**

1. **Which algorithm to use?**
   - Round-robin, least connections, IP hash
   - Based on application needs
   - Example: "Round-robin for stateless, IP hash for stateful"

2. **Layer 4 or Layer 7?**
   - Layer 4 for performance
   - Layer 7 for content-aware routing
   - Example: "Layer 4 for API, Layer 7 for web"

3. **SSL termination?**
   - Terminate at load balancer
   - Pass-through to backend
   - Example: "Terminate at LB for performance"

4. **Session persistence?**
   - Sticky sessions needed?
   - Use IP hash or cookies
   - Example: "IP hash for stateful app"

5. **Health check strategy?**
   - HTTP endpoint, TCP connection
   - Interval and timeout
   - Example: "HTTP health check every 5 seconds"

**Pattern Recognition:**

**Pattern 1: Stateless Web App**
```
Requirements: No session state, high traffic
Algorithm: Round-robin
Solution: Layer 4 load balancer with round-robin
```

**Pattern 2: Stateful Application**
```
Requirements: Session persistence
Algorithm: IP hash or cookie-based
Solution: Layer 7 load balancer with sticky sessions
```

**Pattern 3: Variable Load**
```
Requirements: Variable request duration
Algorithm: Least connections
Solution: Layer 7 load balancer with least connections
```

**Pattern 4: Heterogeneous Servers**
```
Requirements: Different server capacities
Algorithm: Weighted round-robin
Solution: Weighted distribution based on capacity
```

**Pattern 5: Global Application**
```
Requirements: Geographic distribution
Algorithm: Geographic routing
Solution: Global server load balancing with DNS
```

**Decision Flowchart:**

```
Load Balancing Decision:
├─ Stateful or stateless?
│        ├─ Stateful → IP hash, sticky sessions
│        └─ Stateless → Round-robin, least connections
├─ Layer 4 or Layer 7?
│        ├─ Layer 4 → Performance, simple routing
│        └─ Layer 7 → Content-aware, complex routing
├─ SSL termination?
│        ├─ Yes → Terminate at LB
│        └─ No → Pass-through to backend
└─ Heterogeneous servers?
         ├─ Yes → Weighted distribution
         └─ No → Equal weight distribution
```

**Example Analysis:**

**Scenario:** "Design load balancing for e-commerce site"

**Analysis:**
1. Requirements: High traffic, some stateful operations
2. Algorithm: Round-robin for most, IP hash for checkout
3. Layer: Layer 7 for content-aware routing
4. SSL: Terminate at load balancer
5. Health checks: HTTP endpoint every 5 seconds
6. Solution: Layer 7 LB with mixed algorithms

**Scenario:** "Design load balancing for API service"

**Analysis:**
1. Requirements: High throughput, stateless
2. Algorithm: Least connections (variable load)
3. Layer: Layer 4 for performance
4. SSL: Terminate at load balancer
5. Health checks: TCP connection every 10 seconds
6. Solution: Layer 4 LB with least connections

## Summary

Load balancers distribute incoming network traffic across multiple backend servers to ensure no single server bears too much demand, improving responsiveness and availability. They act as a single entry point for clients, hiding the complexity of multiple backend servers. Load balancers use various algorithms like round-robin, least connections, IP hash, and weighted distribution to route requests. They perform health checks to detect unhealthy servers and automatically route traffic away from them, ensuring high availability. Load balancers can operate at Layer 4 (transport layer) or Layer 7 (application layer) and handle SSL termination to reduce cryptographic load on backend servers. Session persistence can be implemented using IP hash, cookies, or session affinity. Load balancing is essential for horizontal scaling, high availability, and handling high traffic loads.

**Key Takeaways:**
- Distributes traffic across multiple servers
- Ensures no single server is overwhelmed
- Provides high availability through failover
- Enables horizontal scaling
- Handles SSL termination
- Multiple algorithms for different use cases
- Health checks ensure reliability
- Session persistence for stateful applications

**Mastery Checklist:**
- ✅ Understand load balancing algorithms
- ✅ Implement round-robin load balancer
- ✅ Implement least connections load balancer
- ✅ Implement IP hash load balancer
- ✅ Implement weighted distribution
- ✅ Configure health checks
- ✅ Handle SSL termination
- ✅ Design for high availability

