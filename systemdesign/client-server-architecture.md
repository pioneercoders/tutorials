# Client-Server Architecture

Client-Server Architecture is a distributed application structure that partitions tasks between providers of resources or services (servers) and service requesters (clients).

## Introduction

Client-Server Architecture is a distributed application structure that partitions tasks between providers of resources or services (servers) and service requesters (clients). In this architecture, clients initiate requests for services or resources, and servers provide those services or resources. The client and server communicate over a network using a request-response model, typically using protocols like HTTP, TCP, or UDP. This separation of concerns enables independent development, scaling, and maintenance of client and server components. Client-server architecture is the foundation of modern web applications, REST APIs, microservices, and cloud computing. It provides benefits like centralized resource management, improved security, easier maintenance, and horizontal scalability. Common implementations include web browsers (clients) communicating with web servers, mobile apps communicating with backend APIs, and desktop applications connecting to database servers.

**Why Client-Server Architecture Matters:**
- Separates concerns between clients and servers
- Enables independent scaling and development
- Centralized resource management
- Improved security through controlled access
- Foundation for modern web applications
- Essential for distributed systems

**Where It Is Used:**
- Web applications (browsers to web servers)
- Mobile apps (apps to backend APIs)
- REST APIs and GraphQL
- Microservices architecture
- Database client-server model
- Cloud computing

## Core Concept Explanation

Client-Server Architecture partitions application functionality into two distinct roles: clients and servers. Clients are the front-end components that initiate requests for services or resources. They are typically user-facing applications like web browsers, mobile apps, or desktop applications. Servers are back-end components that provide services or resources in response to client requests. They handle business logic, data storage, and resource management. The communication follows a request-response model where the client sends a request and the server returns a response. This architecture enables separation of concerns, as clients focus on user interface and interaction while servers focus on business logic and data management. Servers can be stateless (no client state between requests) or stateful (maintain session information). The architecture supports horizontal scaling by adding more servers to handle increased load, and vertical scaling by upgrading server resources.

**Step-by-Step Breakdown:**
1. Client initiates request to server
2. Request travels over network to server
3. Server receives and processes request
4. Server performs business logic
5. Server accesses data/resources if needed
6. Server generates response
7. Response travels over network to client
8. Client processes and displays response
9. Connection may be closed or kept alive

**Intuition Behind the Concept:**
Think of client-server architecture like a restaurant. The customer (client) orders food from the menu (request). The kitchen (server) receives the order, prepares the food (processes request), and serves it to the customer (response). The customer doesn't need to know how the food is prepared, and the kitchen doesn't need to know who the customer is. This separation allows the kitchen to serve many customers efficiently, and customers can order from any restaurant that serves the food they want.

**Visual Thinking:**
```
Client-Server Communication:
Client                    Server
  |                          |
  |--- Request ------------->|
  |                          | Process Request
  |                          | Access Data
  |                          | Generate Response
  |<-- Response -------------|
  |                          |
  | Display Response         |

Multiple Clients:
Client1                     Server
  |                          |
  |--- Request1 ------------>|
  |                          |
Client2                     |
  |                          |
  |--- Request2 ------------>|
  |                          |
Client3                     |
  |                          |
  |--- Request3 ------------>|
  |                          |
  |<-- Response1 ------------|
  |<-- Response2 ------------|
  |<-- Response3 ------------|
```

## Internal Working / Logic

Client-Server Architecture operates through a request-response cycle over a network. The client initiates a request by constructing a message containing the desired operation, parameters, and any necessary authentication. This request is sent over the network using a protocol like HTTP, TCP, or UDP. The server receives the request, parses it, and validates it. The server then processes the request by executing business logic, accessing databases or other resources, and generating a response. The response is sent back over the network to the client. The client receives the response, parses it, and updates the user interface or performs other actions based on the response. The connection may be closed after the response (stateless) or kept alive for subsequent requests (stateful). Servers can handle multiple concurrent requests using threading, event loops, or async I/O. Load balancers can distribute requests across multiple servers for scalability and high availability.

**Operation 1: Client Request**
- User interacts with client application
- Client constructs request
- Client adds authentication if needed
- Client sends request over network
- Client waits for response

**Operation 2: Server Processing**
- Server receives request
- Server parses and validates request
- Server authenticates client if needed
- Server executes business logic
- Server accesses data/resources
- Server generates response

**Operation 3: Response Delivery**
- Server sends response over network
- Client receives response
- Client parses response
- Client updates UI or performs action
- Client handles errors if any

**Operation 4: Connection Management**
- Connection established (TCP handshake)
- Request sent over connection
- Response sent over connection
- Connection closed or kept alive
- Connection pooling for efficiency

**Flow Explanation (HTTP Request):**
1. Client constructs HTTP request (method, URL, headers, body)
2. Client sends request to server over TCP connection
3. Server receives request and parses HTTP
4. Server routes request to appropriate handler
5. Handler processes request and generates response
6. Server sends HTTP response (status, headers, body)
7. Client receives response and parses HTTP
8. Client updates UI based on response

**Decision Making Logic:**
The key decisions are:
- Whether to use stateless or stateful design
- Which communication protocol to use (HTTP, TCP, UDP)
- How to handle authentication and authorization
- How to scale (horizontal vs vertical)
- How to handle concurrent requests
- How to manage connections (keep-alive, pooling)

## Algorithm / Approach

**Client Request Algorithm**

```
1. User triggers action in client
2. Client validates input
3. Client constructs request
4. Client adds authentication
5. Client sends request to server
6. Client waits for response
7. Client receives response
8. Client processes response
9. Client updates UI
10. Client handles errors
```

**Server Processing Algorithm**

```
1. Server receives request
2. Server parses request
3. Server validates request
4. Server authenticates client
5. Server authorizes operation
6. Server executes business logic
7. Server accesses data/resources
8. Server generates response
9. Server sends response to client
10. Server logs request
```

**Connection Management Algorithm**

```
1. Establish connection (TCP handshake)
2. Send request over connection
3. Receive response over connection
4. Close connection or keep alive
5. Pool connections for reuse
6. Handle connection errors
7. Retry failed requests
```

**Load Balancing Algorithm**

```
1. Load balancer receives request
2. Load balancer selects server
3. Load balancer forwards request
4. Server processes request
5. Server returns response
6. Load balancer returns response to client
```

## Implementations

### 1. Simple HTTP Server

```javascript
const http = require('http');

const server = http.createServer((req, res) => {
  // Set CORS headers
  res.setHeader('Access-Control-Allow-Origin', '*');
  res.setHeader('Access-Control-Allow-Methods', 'GET, POST, PUT, DELETE');
  res.setHeader('Access-Control-Allow-Headers', 'Content-Type, Authorization');
  
  // Handle preflight requests
  if (req.method === 'OPTIONS') {
    res.writeHead(200);
    res.end();
    return;
  }
  
  // Route requests
  if (req.url === '/api/data' && req.method === 'GET') {
    res.writeHead(200, { 'Content-Type': 'application/json' });
    res.end(JSON.stringify({ message: 'Hello from server!', timestamp: Date.now() }));
  } else if (req.url === '/api/data' && req.method === 'POST') {
    let body = '';
    req.on('data', chunk => body += chunk);
    req.on('end', () => {
      const data = JSON.parse(body);
      res.writeHead(201, { 'Content-Type': 'application/json' });
      res.end(JSON.stringify({ message: 'Data received', data }));
    });
  } else {
    res.writeHead(404, { 'Content-Type': 'application/json' });
    res.end(JSON.stringify({ error: 'Not Found' }));
  }
});

server.listen(3000, () => {
  console.log('Server running on port 3000');
});
```

**Advantages:**
- Simple implementation
- Built-in HTTP support
- Easy to understand
- Good for learning

### 2. Express.js Server

```javascript
const express = require('express');
const app = express();

// Middleware
app.use(express.json());
app.use(express.urlencoded({ extended: true }));

// CORS middleware
app.use((req, res, next) => {
  res.header('Access-Control-Allow-Origin', '*');
  res.header('Access-Control-Allow-Methods', 'GET, POST, PUT, DELETE');
  res.header('Access-Control-Allow-Headers', 'Content-Type, Authorization');
  next();
});

// Routes
app.get('/api/data', (req, res) => {
  res.json({ message: 'Hello from server!', timestamp: Date.now() });
});

app.post('/api/data', (req, res) => {
  const { name, value } = req.body;
  res.status(201).json({ message: 'Data received', data: { name, value } });
});

app.get('/api/users/:id', (req, res) => {
  const { id } = req.params;
  res.json({ userId: id, name: `User ${id}` });
});

// Error handling
app.use((err, req, res, next) => {
  console.error(err.stack);
  res.status(500).json({ error: 'Internal Server Error' });
});

// 404 handler
app.use((req, res) => {
  res.status(404).json({ error: 'Not Found' });
});

app.listen(3000, () => {
  console.log('Server running on port 3000');
});
```

**Advantages:**
- Rich routing features
- Middleware support
- Easy API development
- Large ecosystem

### 3. WebSocket Server

```javascript
const WebSocket = require('ws');

const wss = new WebSocket.Server({ port: 8080 });

wss.on('connection', (ws) => {
  console.log('Client connected');
  
  // Send welcome message
  ws.send(JSON.stringify({ type: 'welcome', message: 'Connected to server' }));
  
  // Handle messages from client
  ws.on('message', (message) => {
    const data = JSON.parse(message);
    console.log('Received:', data);
    
    // Echo message back
    ws.send(JSON.stringify({ type: 'echo', data }));
    
    // Broadcast to all clients
    wss.clients.forEach((client) => {
      if (client !== ws && client.readyState === WebSocket.OPEN) {
        client.send(JSON.stringify({ type: 'broadcast', data }));
      }
    });
  });
  
  // Handle disconnection
  ws.on('close', () => {
    console.log('Client disconnected');
  });
  
  // Handle errors
  ws.on('error', (error) => {
    console.error('WebSocket error:', error);
  });
});

console.log('WebSocket server running on port 8080');
```

**Advantages:**
- Real-time communication
- Bidirectional messaging
- Low latency
- Good for live updates

### 4. REST API Client

```javascript
class APIClient {
  constructor(baseURL) {
    this.baseURL = baseURL;
    this.token = null;
  }
  
  setToken(token) {
    this.token = token;
  }
  
  async get(endpoint) {
    const response = await fetch(`${this.baseURL}${endpoint}`, {
      method: 'GET',
      headers: {
        'Content-Type': 'application/json',
        'Authorization': this.token ? `Bearer ${this.token}` : ''
      }
    });
    
    if (!response.ok) {
      throw new Error(`HTTP error! status: ${response.status}`);
    }
    
    return response.json();
  }
  
  async post(endpoint, data) {
    const response = await fetch(`${this.baseURL}${endpoint}`, {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
        'Authorization': this.token ? `Bearer ${this.token}` : ''
      },
      body: JSON.stringify(data)
    });
    
    if (!response.ok) {
      throw new Error(`HTTP error! status: ${response.status}`);
    }
    
    return response.json();
  }
  
  async put(endpoint, data) {
    const response = await fetch(`${this.baseURL}${endpoint}`, {
      method: 'PUT',
      headers: {
        'Content-Type': 'application/json',
        'Authorization': this.token ? `Bearer ${this.token}` : ''
      },
      body: JSON.stringify(data)
    });
    
    if (!response.ok) {
      throw new Error(`HTTP error! status: ${response.status}`);
    }
    
    return response.json();
  }
  
  async delete(endpoint) {
    const response = await fetch(`${this.baseURL}${endpoint}`, {
      method: 'DELETE',
      headers: {
        'Content-Type': 'application/json',
        'Authorization': this.token ? `Bearer ${this.token}` : ''
      }
    });
    
    if (!response.ok) {
      throw new Error(`HTTP error! status: ${response.status}`);
    }
    
    return response.json();
  }
}

// Usage
const client = new APIClient('http://localhost:3000');
client.setToken('your-jwt-token');

// GET request
const data = await client.get('/api/data');
console.log(data);

// POST request
const result = await client.post('/api/data', { name: 'John', value: 100 });
console.log(result);
```

**Advantages:**
- Reusable API client
- Authentication support
- Error handling
- Type-safe requests

### 5. GraphQL Server

```javascript
const { ApolloServer, gql } = require('apollo-server');

// Type definitions
const typeDefs = gql`
  type User {
    id: ID!
    name: String!
    email: String!
  }
  
  type Query {
    user(id: ID!): User
    users: [User]
  }
  
  type Mutation {
    createUser(name: String!, email: String!): User
  }
`;

// Sample data
const users = [
  { id: '1', name: 'John Doe', email: 'john@example.com' },
  { id: '2', name: 'Jane Smith', email: 'jane@example.com' }
];

// Resolvers
const resolvers = {
  Query: {
    user: (_, { id }) => users.find(user => user.id === id),
    users: () => users
  },
  Mutation: {
    createUser: (_, { name, email }) => {
      const newUser = {
        id: String(users.length + 1),
        name,
        email
      };
      users.push(newUser);
      return newUser;
    }
  }
};

// Create server
const server = new ApolloServer({ typeDefs, resolvers });

server.listen().then(({ url }) => {
  console.log(`Server ready at ${url}`);
});
```

**Advantages:**
- Flexible queries
- Single endpoint
- Type-safe
- Efficient data fetching

## Dry Run

**Example: REST API Request-Response**

**Request:**
```
GET /api/users/1
Host: localhost:3000
Authorization: Bearer token123
```

**Step-by-Step Execution:**

```
1. Client constructs HTTP GET request
2. Client adds Authorization header
3. Client sends request to server
4. Server receives request
5. Server parses request headers
6. Server validates token
7. Server routes to /api/users/:id handler
8. Handler extracts id from params
9. Handler queries database for user
10. Database returns user data
11. Handler generates JSON response
12. Server sends HTTP 200 response
13. Client receives response
14. Client parses JSON
15. Client displays user data
```

**Request/Response Table:**

| Step | Component | Action | Status |
|------|-----------|--------|--------|
| 1 | Client | Construct GET request | - |
| 2 | Client | Add Authorization header | Bearer token123 |
| 3 | Client | Send to server | localhost:3000 |
| 4 | Server | Receive request | - |
| 5 | Server | Parse headers | - |
| 6 | Server | Validate token | Valid |
| 7 | Server | Route to handler | /api/users/:id |
| 8 | Handler | Extract id | 1 |
| 9 | Handler | Query database | - |
| 10 | Database | Return user data | `{id: 1, name: "John"}` |
| 11 | Handler | Generate response | JSON |
| 12 | Server | Send 200 response | - |
| 13 | Client | Receive response | - |
| 14 | Client | Parse JSON | - |
| 15 | Client | Display data | User shown |

## Edge Cases

### 1. Server Failure
```javascript
// Server goes down
// Client requests fail
// Solution: Retry, fallback, error handling
```

### 2. Network Partition
```javascript
// Network connection lost
// Requests timeout
// Solution: Retry logic, offline mode
```

### 3. High Concurrency
```javascript
// Too many concurrent requests
// Server overwhelmed
// Solution: Rate limiting, load balancing
```

### 4. Security Vulnerabilities
```javascript
// Authentication bypass
// Data exposure
// Solution: Proper auth, encryption, validation
```

### 5. Slow Response
```javascript
// Server response slow
- Poor user experience
// Solution: Timeout, async processing, caching
```

### 6. Data Inconsistency
```javascript
// Client and server data out of sync
- Incorrect information
// Solution: Versioning, sync mechanisms
```

**Why Edge Cases Matter:**
- Server failures cause downtime
- Network partitions affect availability
- High concurrency overwhelms servers
- Security vulnerabilities expose data
- Slow responses degrade UX
- Data inconsistency causes errors

## Variations / Extensions

### 1. Three-Tier Architecture

```javascript
// Presentation, Application, Data layers
- Better separation
- More scalable
```

### 2. Microservices

```javascript
// Multiple small services
- Independent deployment
- Better scalability
```

### 3. Serverless

```javascript
// Function as a Service
- No server management
- Auto-scaling
```

### 4. Peer-to-Peer

```javascript
// No central server
- Decentralized
- Resilient
```

### 5. Event-Driven

```javascript
// Event-based communication
- Async processing
- Better scalability
```

## Optimization Techniques

### 1. Connection Pooling

**Reuse Connections:**
```javascript
// Pool database connections
- Reduce overhead
- Better performance
```

### 2. Caching

**Cache Responses:**
```javascript
// Cache frequently accessed data
- Reduce server load
- Faster responses
```

### 3. Compression

**Compress Data:**
```javascript
// Use gzip, brotli
- Smaller payloads
- Faster transfer
```

### 4. Keep-Alive

**Persistent Connections:**
```javascript
// Keep connections alive
- Reduce connection overhead
- Faster requests
```

### 5. Trade-offs

**Architecture Comparison:**

| Architecture | Scalability | Complexity | Use Case |
|--------------|-------------|------------|----------|
| Client-Server | Medium | Low | General purpose |
| Three-Tier | High | Medium | Enterprise apps |
| Microservices | Very High | High | Large scale |
| Serverless | Very High | Medium | Event-driven |
| P2P | High | High | Decentralized |

**When to Use Each:**
- Client-Server: General purpose, simple apps
- Three-Tier: Enterprise, separation of concerns
- Microservices: Large scale, independent services
- Serverless: Event-driven, auto-scaling
- P2P: Decentralized, resilient

## Complexity Analysis

### Time Complexity

**Request Processing: O(n)**
- n = request processing time
- Depends on business logic
- Database queries add complexity

**Response Time: O(n + m)**
- n = processing time
- m = network latency
- Total round-trip time

### Space Complexity

**Server Memory: O(k)**
- k = concurrent requests
- Each request uses memory
- Connection pooling reduces overhead

**Explanation:**
Client-server request processing time is O(n) where n is the time to process the request, including business logic and database queries. Response time is O(n + m) where m is network latency. Server memory usage is O(k) where k is the number of concurrent requests. Connection pooling and caching can reduce both time and space complexity by reusing resources and avoiding redundant processing.

## Real-world Applications

### 1. Web Applications

**Browser to Web Server:**
- HTTP/HTTPS communication
- REST APIs
- Example: E-commerce sites

### 2. Mobile Applications

**App to Backend API:**
- REST or GraphQL
- Authentication
- Example: Social media apps

### 3. Desktop Applications

**Desktop to Server:**
- TCP/UDP communication
- Custom protocols
- Example: Games, enterprise software

### 4. Database Access

**Application to Database:**
- SQL queries
- Connection pooling
- Example: Any data-driven app

### 5. File Transfer

**Client to File Server:**
- FTP, SFTP
- Large file transfers
- Example: Cloud storage

### 6. Email

**Email Client to Server:**
- IMAP, SMTP, POP3
- Email protocols
- Example: Email clients

### 7. Gaming

**Game Client to Server:**
- Real-time communication
- WebSockets, UDP
- Example: Multiplayer games

### 8. IoT

**Device to Cloud Server:**
- MQTT, HTTP
- Sensor data
- Example: Smart home devices

## Common Mistakes

### 1. No Error Handling

**Mistake:**
```javascript
// No error handling
// Requests fail silently
// Poor user experience
```

**Correct:**
```javascript
// Implement error handling
// Show user-friendly errors
// Retry failed requests
```

**Why It Matters:**
- No error handling = poor UX
- Silent failures confuse users
- Proper error handling essential

### 2. No Authentication

**Mistake:**
```javascript
// No authentication
// Unauthorized access
// Security vulnerability
```

**Correct:**
```javascript
// Implement authentication
// Use JWT, OAuth
- Secure endpoints
```

**Why It Matters:**
- No authentication = security risk
- Unauthorized access to data
- Authentication essential for security

### 3. Tight Coupling

**Mistake:**
```javascript
// Client tightly coupled to server
- Hard to change
// Poor maintainability
```

**Correct:**
```javascript
// Use contracts, versioning
- Loose coupling
// Better maintainability
```

**Why It Matters:**
- Tight coupling = hard to change
- Changes break clients
- Loose coupling enables evolution

### 4. No Validation

**Mistake:**
```javascript
// No input validation
// Invalid data processed
- Security vulnerability
```

**Correct:**
```javascript
// Validate all inputs
// Sanitize data
- Secure processing
```

**Why It Matters:**
- No validation = security risk
- Invalid data causes errors
- Validation essential for security

### 5. Synchronous Processing

**Mistake:**
```javascript
// Synchronous processing
// Blocks on long operations
- Poor performance
```

**Correct:**
```javascript
// Use async processing
- Non-blocking
// Better performance
```

**Why It Matters:**
- Synchronous = poor performance
- Blocks other requests
- Async processing essential

### 6. No Rate Limiting

**Mistake:**
```javascript
// No rate limiting
// Abuse possible
- Server overwhelmed
```

**Correct:**
```javascript
// Implement rate limiting
- Protect server
// Fair usage
```

**Why It Matters:**
- No rate limiting = abuse risk
- Server can be overwhelmed
- Rate limiting protects resources

## Advanced Concepts

### 1. Three-Tier Architecture

**Concept:**
Presentation, Application, Data layers.

**Features:**
- Better separation of concerns
- Scalable layers
- Easier maintenance

### 2. Microservices

**Concept:**
Decompose into small services.

**Features:**
- Independent deployment
- Technology diversity
- Better scalability

### 3. Serverless

**Concept:**
Function as a Service.

**Features:**
- No server management
- Auto-scaling
- Pay per use

### 4. Event-Driven Architecture

**Concept:**
Event-based communication.

**Features:**
- Async processing
- Loose coupling
- Better scalability

## Practice Thinking Guide

### How to Design Client-Server Architecture

**Key Questions to Ask:**

1. **Stateless or stateful?**
   - Stateless for scalability
   - Stateful for session persistence
   - Example: "Stateless for API, stateful for chat"

2. **Which protocol?**
   - HTTP for web APIs
   - WebSocket for real-time
   - TCP for custom protocols
   - Example: "HTTP for REST, WebSocket for chat"

3. **How to authenticate?**
   - JWT, OAuth, API keys
   - Based on security requirements
   - Example: "JWT for mobile apps, OAuth for web"

4. **How to scale?**
   - Horizontal (more servers)
   - Vertical (bigger servers)
   - Example: "Horizontal with load balancer"

5. **How to handle errors?**
   - Retry logic
   - Fallback mechanisms
   - User-friendly errors
   - Example: "Retry with exponential backoff"

**Pattern Recognition:**

**Pattern 1: REST API**
```
Requirements: Standard web API
Protocol: HTTP/HTTPS
Solution: RESTful API with JSON
```

**Pattern 2: Real-time**
```
Requirements: Live updates
Protocol: WebSocket
Solution: WebSocket server with bidirectional messaging
```

**Pattern 3: Mobile Backend**
```
Requirements: Mobile app backend
Protocol: HTTP/HTTPS
Solution: REST API with JWT authentication
```

**Pattern 4: High Traffic**
```
Requirements: Handle high traffic
Scaling: Horizontal
Solution: Load balancer with multiple servers
```

**Pattern 5: Enterprise**
```
Requirements: Enterprise application
Architecture: Three-tier
Solution: Presentation, Application, Data layers
```

**Decision Flowchart:**

```
Client-Server Decision:
├─ Stateless or stateful?
│        ├─ Stateless → Easier scaling
│        └─ Stateful → Session persistence
├─ Which protocol?
│        ├─ HTTP → REST APIs
│        ├─ WebSocket → Real-time
│        └─ TCP → Custom protocols
├─ Authentication?
│        ├─ JWT → Mobile apps
│        ├─ OAuth → Web apps
│        └─ API Keys → Service-to-service
└─ Scaling strategy?
         ├─ Horizontal → Load balancer
         └─ Vertical → Bigger servers
```

**Example Analysis:**

**Scenario:** "Design backend for mobile app"

**Analysis:**
1. Requirements: Mobile app backend, high traffic
2. Protocol: HTTP/HTTPS (REST API)
3. Authentication: JWT (mobile-friendly)
4. Scaling: Horizontal with load balancer
5. State: Stateless for scalability
6. Solution: REST API with JWT, load balanced

**Scenario:** "Design real-time chat application"

**Analysis:**
1. Requirements: Real-time messaging
2. Protocol: WebSocket (bidirectional)
3. Authentication: JWT or session
4. Scaling: Horizontal with sticky sessions
5. State: Stateful (connection state)
6. Solution: WebSocket server with session persistence

## Summary

Client-Server Architecture is a distributed application structure that partitions tasks between providers of resources or services (servers) and service requesters (clients). In this architecture, clients initiate requests for services or resources, and servers provide those services or resources. The client and server communicate over a network using a request-response model, typically using protocols like HTTP, TCP, or UDP. This separation of concerns enables independent development, scaling, and maintenance of client and server components. Client-server architecture is the foundation of modern web applications, REST APIs, microservices, and cloud computing. It provides benefits like centralized resource management, improved security, easier maintenance, and horizontal scalability.

**Key Takeaways:**
- Separates concerns between clients and servers
- Request-response communication model
- Foundation for modern web applications
- Enables scalability and separation of concerns
- Essential for distributed systems
- Supports multiple protocols (HTTP, WebSocket, TCP)
- Stateless vs stateful design choices
- Authentication and security critical

**Mastery Checklist:**
- ✅ Understand client-server architecture
- ✅ Implement HTTP server
- ✅ Implement HTTP client
- ✅ Use REST APIs
- ✅ Implement WebSocket server
- ✅ Handle authentication
- ✅ Design for scalability
- ✅ Handle errors gracefully

