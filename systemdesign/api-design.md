# API Design

API (Application Programming Interface) design creates interfaces for different software systems to communicate.

## Introduction

API Design is the process of creating interfaces that enable different software systems to communicate with each other. A well-designed API is crucial for building maintainable, scalable, and developer-friendly systems. APIs define the methods and data formats that applications can use to request and exchange information. The three main API paradigms are REST (Representational State Transfer), GraphQL, and gRPC, each with distinct advantages for different use cases. Good API design principles include consistency, simplicity, proper error handling, versioning, and comprehensive documentation. APIs are the backbone of modern software architecture, enabling microservices, third-party integrations, and client-server communication.

**Why API Design Matters:**
- Enables system integration and communication
- Determines developer experience and adoption
- Impacts system scalability and maintainability
- Critical for microservice architecture
- Essential for third-party integrations
- Affects performance and security

**Where It Is Used:**
- Microservice communication
- Web and mobile application backends
- Third-party service integrations
- Public APIs for developers
- Internal service boundaries
- API gateways and proxies

## Core Concept Explanation

API design revolves around creating clear, consistent, and intuitive interfaces for software communication. REST APIs use standard HTTP methods (GET, POST, PUT, DELETE, PATCH) to operate on resources identified by URLs. GraphQL uses a query language to allow clients to request exactly the data they need. gRPC uses Protocol Buffers for high-performance, type-safe communication between services. Key principles include using nouns for resource names (not verbs), proper HTTP status codes, consistent response formats, and versioning for breaking changes. APIs should be stateless, cacheable, and follow the principle of least surprise for developers.

**Step-by-Step Breakdown:**
1. Identify resources and their relationships
2. Choose appropriate API paradigm (REST, GraphQL, gRPC)
3. Design resource endpoints and naming conventions
4. Define request/response formats
5. Implement authentication and authorization
6. Add pagination, filtering, and sorting
7. Implement error handling and status codes
8. Add rate limiting and monitoring
9. Document the API comprehensively
10. Version the API for future changes

**Intuition Behind the Concept:**
Think of API design like designing a menu for a restaurant. The menu (API) should be clear, consistent, and easy to understand. Each dish (endpoint) should have a descriptive name, the ingredients (parameters) should be clearly listed, and the presentation (response format) should be consistent. Just as a good menu makes ordering easy, a good API makes integration straightforward. Versioning is like offering seasonal menus - you can introduce changes without breaking existing customers' habits.

**Visual Thinking:**
```
REST API Structure:
Client → HTTP Request → API Gateway → Service → Database
                    ↓
                 Response

Resource Hierarchy:
/api/v1/users              (Collection)
/api/v1/users/123          (Specific user)
/api/v1/users/123/posts    (Nested resource)
/api/v1/posts              (Related collection)

HTTP Methods Mapping:
GET    /users     → List all users
GET    /users/123 → Get specific user
POST   /users     → Create new user
PUT    /users/123 → Update entire user
PATCH  /users/123 → Partial update
DELETE /users/123 → Delete user

GraphQL Query Structure:
query {
  user(id: "123") {
    name
    email
    posts {
      title
      comments {
        author {
          name
        }
      }
    }
  }
}
```

## Internal Working / Logic

APIs work through a request-response cycle where clients send requests to endpoints, servers process them, and return responses. REST APIs use HTTP methods to indicate the action being performed on resources. The server validates the request, processes it (often interacting with databases or other services), and returns an appropriate response with a status code. GraphQL uses a single endpoint where clients send queries describing the data they need, and the server resolves the query by fetching data from various sources. gRPC uses Protocol Buffers to serialize data and HTTP/2 for efficient communication between services.

**Operation 1: REST Request Processing**
- Client sends HTTP request with method, URL, headers, and body
- API gateway routes request to appropriate service
- Service validates authentication and authorization
- Service processes request (CRUD operations)
- Service returns response with appropriate status code
- Response includes data, metadata, and error information if applicable

**Operation 2: GraphQL Query Resolution**
- Client sends query to single endpoint
- Server parses query and validates against schema
- Server resolves each field in the query
- Data may come from multiple sources (databases, services)
- Server aggregates results and returns structured response
- Client receives exactly the data requested

**Operation 3: gRPC Communication**
- Client and server share Protocol Buffer definition (.proto file)
- Client serializes request using Protocol Buffers
- Request sent over HTTP/2 for efficient transport
- Server deserializes and processes request
- Response serialized and sent back
- Binary format is more efficient than JSON

**Flow Explanation (REST Request):**
1. Client constructs HTTP request with method, URL, headers, body
2. Request sent to API endpoint
3. API gateway authenticates and authorizes request
4. Request routed to appropriate service
5. Service validates request data
6. Service performs operation (query/update database)
7. Service constructs response with appropriate status code
8. Response sent back to client
9. Client processes response

**Decision Making Logic:**
The key decisions are:
- Which API paradigm to use (REST, GraphQL, gRPC)
- How to structure resources and endpoints
- Which HTTP methods to use for each operation
- How to handle authentication and authorization
- How to version the API for breaking changes
- How to implement pagination, filtering, sorting
- How to handle errors consistently

## Algorithm / Approach

**REST API Design Algorithm**

```
1. Identify resources (nouns, not verbs)
2. Design resource hierarchy
3. Map CRUD operations to HTTP methods
4. Design request/response formats
5. Implement authentication/authorization
6. Add pagination, filtering, sorting
7. Implement error handling
8. Add rate limiting
9. Document API
10. Version API
```

**GraphQL Schema Design Algorithm**

```
1. Define types and relationships
2. Design queries and mutations
3. Implement resolvers for each field
4. Add authentication context
5. Implement data loaders for efficiency
6. Add validation
7. Document schema
8. Version schema
```

**gRPC Service Design Algorithm**

```
1. Define Protocol Buffer schema (.proto)
2. Define service methods and messages
3. Generate server and client code
4. Implement service methods
5. Add interceptors for auth/logging
6. Implement error handling
7. Document service
8. Version service
```

**API Versioning Algorithm**

```
1. Choose versioning strategy (URL, header, parameter)
2. Document breaking changes
3. Maintain old version for deprecation period
4. Communicate changes to consumers
5. Sunset old version after transition period
```

## Implementations

### 1. REST API with Express

```javascript
const express = require('express');
const app = express();

app.use(express.json());

// In-memory data store
let users = [
  { id: 1, name: 'John Doe', email: 'john@example.com' },
  { id: 2, name: 'Jane Smith', email: 'jane@example.com' }
];

// GET /api/v1/users - List all users with pagination
app.get('/api/v1/users', (req, res) => {
  const page = parseInt(req.query.page) || 1;
  const perPage = parseInt(req.query.per_page) || 10;
  const start = (page - 1) * perPage;
  const end = start + perPage;
  
  res.json({
    data: users.slice(start, end),
    pagination: {
      page,
      per_page: perPage,
      total: users.length,
      total_pages: Math.ceil(users.length / perPage)
    }
  });
});

// GET /api/v1/users/:id - Get specific user
app.get('/api/v1/users/:id', (req, res) => {
  const user = users.find(u => u.id === parseInt(req.params.id));
  
  if (!user) {
    return res.status(404).json({ error: 'User not found' });
  }
  
  res.json(user);
});

// POST /api/v1/users - Create new user
app.post('/api/v1/users', (req, res) => {
  const { name, email } = req.body;
  
  if (!name || !email) {
    return res.status(400).json({ error: 'Name and email are required' });
  }
  
  const newUser = {
    id: users.length + 1,
    name,
    email
  };
  
  users.push(newUser);
  res.status(201).json(newUser);
});

// PUT /api/v1/users/:id - Update entire user
app.put('/api/v1/users/:id', (req, res) => {
  const id = parseInt(req.params.id);
  const userIndex = users.findIndex(u => u.id === id);
  
  if (userIndex === -1) {
    return res.status(404).json({ error: 'User not found' });
  }
  
  const { name, email } = req.body;
  
  if (!name || !email) {
    return res.status(400).json({ error: 'Name and email are required' });
  }
  
  users[userIndex] = { id, name, email };
  res.json(users[userIndex]);
});

// PATCH /api/v1/users/:id - Partial update
app.patch('/api/v1/users/:id', (req, res) => {
  const id = parseInt(req.params.id);
  const userIndex = users.findIndex(u => u.id === id);
  
  if (userIndex === -1) {
    return res.status(404).json({ error: 'User not found' });
  }
  
  users[userIndex] = { ...users[userIndex], ...req.body };
  res.json(users[userIndex]);
});

// DELETE /api/v1/users/:id - Delete user
app.delete('/api/v1/users/:id', (req, res) => {
  const id = parseInt(req.params.id);
  const userIndex = users.findIndex(u => u.id === id);
  
  if (userIndex === -1) {
    return res.status(404).json({ error: 'User not found' });
  }
  
  users.splice(userIndex, 1);
  res.status(204).send();
});

app.listen(3000, () => console.log('Server running on port 3000'));
```

**Advantages:**
- Standard HTTP methods
- Easy to understand and use
- Built-in caching support
- Wide tooling support

### 2. GraphQL API with Apollo Server

```javascript
const { ApolloServer, gql } = require('apollo-server');

const typeDefs = gql`
  type User {
    id: ID!
    name: String!
    email: String!
    posts: [Post]
  }
  
  type Post {
    id: ID!
    title: String!
    content: String!
    author: User
  }
  
  type Query {
    user(id: ID!): User
    users: [User]
    post(id: ID!): Post
    posts: [Post]
  }
  
  type Mutation {
    createUser(name: String!, email: String!): User
    createPost(title: String!, content: String!, authorId: ID!): Post
  }
`;

const users = [
  { id: '1', name: 'John Doe', email: 'john@example.com' },
  { id: '2', name: 'Jane Smith', email: 'jane@example.com' }
];

const posts = [
  { id: '1', title: 'First Post', content: 'Hello World', authorId: '1' },
  { id: '2', title: 'Second Post', content: 'GraphQL is great', authorId: '2' }
];

const resolvers = {
  Query: {
    user: (parent, { id }) => users.find(u => u.id === id),
    users: () => users,
    post: (parent, { id }) => posts.find(p => p.id === id),
    posts: () => posts
  },
  Mutation: {
    createUser: (parent, { name, email }) => {
      const newUser = {
        id: String(users.length + 1),
        name,
        email
      };
      users.push(newUser);
      return newUser;
    },
    createPost: (parent, { title, content, authorId }) => {
      const newPost = {
        id: String(posts.length + 1),
        title,
        content,
        authorId
      };
      posts.push(newPost);
      return newPost;
    }
  },
  User: {
    posts: (user) => posts.filter(p => p.authorId === user.id)
  },
  Post: {
    author: (post) => users.find(u => u.id === post.authorId)
  }
};

const server = new ApolloServer({ typeDefs, resolvers });

server.listen().then(({ url }) => {
  console.log(`Server ready at ${url}`);
});
```

**Advantages:**
- Flexible data fetching
- Single endpoint
- Strongly typed schema
- No over-fetching or under-fetching

### 3. gRPC Service with Node.js

```javascript
// user.proto
syntax = "proto3";

package user;

service UserService {
  rpc GetUser(GetUserRequest) returns (User);
  rpc ListUsers(Empty) returns (UserList);
  rpc CreateUser(CreateUserRequest) returns (User);
}

message User {
  int32 id = 1;
  string name = 2;
  string email = 3;
}

message GetUserRequest {
  int32 id = 1;
}

message CreateUserRequest {
  string name = 1;
  string email = 2;
}

message UserList {
  repeated User users = 1;
}

message Empty {}

// server.js
const grpc = require('@grpc/grpc-js');
const protoLoader = require('@grpc/proto-loader');

const packageDefinition = protoLoader.loadSync('user.proto', {});
const userProto = grpc.loadPackageDefinition(packageDefinition).user;

const users = [
  { id: 1, name: 'John Doe', email: 'john@example.com' },
  { id: 2, name: 'Jane Smith', email: 'jane@example.com' }
];

const server = new grpc.Server();

server.addService(userProto.UserService.service, {
  GetUser: (call, callback) => {
    const user = users.find(u => u.id === call.request.id);
    if (!user) {
      callback(new Error('User not found'));
    } else {
      callback(null, user);
    }
  },
  ListUsers: (call, callback) => {
    callback(null, { users });
  },
  CreateUser: (call, callback) => {
    const newUser = {
      id: users.length + 1,
      name: call.request.name,
      email: call.request.email
    };
    users.push(newUser);
    callback(null, newUser);
  }
});

server.bindAsync('0.0.0.0:50051', grpc.ServerCredentials.createInsecure(), () => {
  server.start();
  console.log('gRPC server running on port 50051');
});
```

**Advantages:**
- High performance with Protocol Buffers
- Type-safe communication
- Efficient binary serialization
- Built-in streaming support

### 4. API with Authentication (JWT)

```javascript
const express = require('express');
const jwt = require('jsonwebtoken');
const app = express();

app.use(express.json());

const SECRET_KEY = 'your-secret-key';

// Middleware to verify JWT
const authenticateToken = (req, res, next) => {
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
};

// Login endpoint
app.post('/api/v1/login', (req, res) => {
  const { username, password } = req.body;
  
  // Validate credentials (in production, check against database)
  if (username === 'admin' && password === 'password') {
    const token = jwt.sign({ username }, SECRET_KEY, { expiresIn: '1h' });
    res.json({ token });
  } else {
    res.status(401).json({ error: 'Invalid credentials' });
  }
});

// Protected endpoint
app.get('/api/v1/protected', authenticateToken, (req, res) => {
  res.json({ message: 'This is protected data', user: req.user });
});

app.listen(3000, () => console.log('Server running on port 3000'));
```

**Advantages:**
- Secure authentication
- Stateless tokens
- Easy integration
- Standard approach

### 5. API with Rate Limiting

```javascript
const express = require('express');
const rateLimit = require('express-rate-limit');
const app = express();

app.use(express.json());

// Rate limiter configuration
const limiter = rateLimit({
  windowMs: 15 * 60 * 1000, // 15 minutes
  max: 100, // limit each IP to 100 requests per windowMs
  message: 'Too many requests from this IP, please try again later',
  standardHeaders: true,
  legacyHeaders: false
});

// Apply rate limiter to all API routes
app.use('/api/', limiter);

// Stricter rate limiter for expensive operations
const strictLimiter = rateLimit({
  windowMs: 15 * 60 * 1000,
  max: 10,
  message: 'Too many expensive operations'
});

app.get('/api/v1/users', (req, res) => {
  res.json({ users: [] });
});

app.post('/api/v1/expensive-operation', strictLimiter, (req, res) => {
  res.json({ result: 'Operation completed' });
});

app.listen(3000, () => console.log('Server running on port 3000'));
```

**Advantages:**
- Prevents abuse
- Protects resources
- Configurable limits
- Standard headers

## Dry Run

**Example: REST API Request Flow**

**Request:**
```
GET /api/v1/users/123
Headers: {
  "Authorization": "Bearer eyJhbGciOiJIUzI1NiIs...",
  "Content-Type": "application/json"
}
```

**Step-by-Step Execution:**

```
1. Client sends HTTP GET request to /api/v1/users/123
2. API Gateway receives request
3. Authentication middleware validates JWT token
   - Token valid → Proceed
   - Token invalid → Return 401 Unauthorized
4. Request routed to user service
5. Service extracts user ID from URL parameter: 123
6. Service queries database for user with ID 123
7. Database returns user data
8. Service constructs response:
   {
     "id": 123,
     "name": "John Doe",
     "email": "john@example.com"
   }
9. Service returns response with status 200 OK
10. Client receives response
```

**Request/Response Table:**

| Step | Component | Action | Status |
|------|-----------|--------|--------|
| 1 | Client | Send GET /api/v1/users/123 | - |
| 2 | API Gateway | Receive request | 200 OK |
| 3 | Auth Middleware | Validate JWT | Valid |
| 4 | Router | Route to user service | - |
| 5 | Service | Extract ID 123 | - |
| 6 | Database | Query user | Found |
| 7 | Service | Construct response | - |
| 8 | Service | Return 200 OK + data | - |
| 9 | Client | Receive response | - |

## Edge Cases

### 1. Authentication Failure
```javascript
// Invalid or missing token
// Return 401 Unauthorized
// Include error message
```

### 2. Resource Not Found
```javascript
// GET /api/v1/users/999
// User doesn't exist
// Return 404 Not Found
```

### 3. Invalid Request Data
```javascript
// POST with missing required fields
// Return 400 Bad Request
// Include validation errors
```

### 4. Rate Limit Exceeded
```javascript
// Too many requests
// Return 429 Too Many Requests
// Include Retry-After header
```

### 5. Server Error
```javascript
// Internal server error
// Return 500 Internal Server Error
// Log error for debugging
```

### 6. Version Mismatch
```javascript
// Client using deprecated version
// Return 410 Gone or deprecation warning
// Include upgrade path
```

**Why Edge Cases Matter:**
- Robust error handling essential
- Clear error messages help developers
- Proper status codes indicate issues
- Rate limiting prevents abuse
- Versioning ensures backward compatibility
- Security requires proper auth handling

## Variations / Extensions

### 1. API Gateway Pattern

```javascript
// API Gateway routes requests to multiple services
// Handles authentication, rate limiting, logging
// Single entry point for all APIs
```

### 2. WebSocket API

```javascript
const WebSocket = require('ws');

const wss = new WebSocket.Server({ port: 8080 });

wss.on('connection', (ws) => {
  ws.on('message', (message) => {
    console.log('Received:', message);
    ws.send('Message received');
  });
});
```

### 3. Event-Driven API (Webhooks)

```javascript
// Server sends events to registered webhooks
// Client receives notifications
// Asynchronous communication
```

### 4. Batch Operations

```javascript
// Process multiple operations in single request
// Reduce round trips
// Atomic operations
```

### 5. GraphQL Subscriptions

```javascript
const typeDefs = gql`
  type Subscription {
    userUpdated: User
  }
`;

const resolvers = {
  Subscription: {
    userUpdated: {
      subscribe: () => pubsub.asyncIterator(['USER_UPDATED'])
    }
  }
};
```

## Optimization Techniques

### 1. Caching

**Implement Response Caching:**
```javascript
const NodeCache = require('node-cache');
const cache = new NodeCache({ stdTTL: 600 }); // 10 minutes

app.get('/api/v1/users/:id', async (req, res) => {
  const cacheKey = `user:${req.params.id}`;
  const cachedUser = cache.get(cacheKey);
  
  if (cachedUser) {
    return res.json(cachedUser);
  }
  
  const user = await getUserFromDB(req.params.id);
  cache.set(cacheKey, user);
  res.json(user);
});
```

### 2. Compression

**Enable Gzip Compression:**
```javascript
const compression = require('compression');
app.use(compression());
```

### 3. Connection Pooling

**Reuse Database Connections:**
```javascript
// Use connection pooling
// Reduce connection overhead
- Improve performance
```

### 4. Pagination

**Implement Cursor-based Pagination:**
```javascript
// More efficient than offset-based
- Works with large datasets
- Consistent results
```

### 5. Trade-offs

**REST vs GraphQL vs gRPC:**

| Aspect | REST | GraphQL | gRPC |
|--------|------|---------|------|
| Simplicity | High | Medium | Low |
| Flexibility | Low | High | Medium |
| Performance | Medium | Medium | High |
| Browser Support | Excellent | Good | Poor |
| Caching | Built-in | Custom | Custom |
| Type Safety | Low | High | High |

**When to Use Each:**
- REST: Simple CRUD, public APIs, caching needed
- GraphQL: Complex data needs, mobile apps, flexible queries
- gRPC: Microservices, high performance, internal APIs

## Complexity Analysis

### Time Complexity

**REST API: O(1) to O(n)**
- Simple queries: O(1)
- Complex queries with joins: O(n)
- Depends on database complexity

**GraphQL: O(1) to O(n)**
- Depends on query complexity
- N+1 problem if not optimized
- Data loaders can optimize to O(1)

**gRPC: O(1) to O(n)**
- Similar to REST
- Binary serialization faster
- Depends on operation complexity

### Space Complexity

**REST: O(1) to O(n)**
- Response size varies
- Can over-fetch data
- JSON overhead

**GraphQL: O(1) to O(n)**
- Fetches exactly requested data
- No over-fetching
- Query parsing overhead

**gRPC: O(1) to O(n)**
- Binary format more compact
- Protocol Buffers efficient
- Less overhead than JSON

**Explanation:**
API complexity depends on the operations performed and data returned. REST can over-fetch data, leading to larger responses. GraphQL fetches exactly what's requested, reducing payload size. gRPC uses binary Protocol Buffers, which are more efficient than JSON. The actual complexity is often dominated by database operations rather than API processing.

## Real-world Applications

### 1. Public APIs

**Developer Platforms:**
- GitHub API
- Twitter API
- Google Maps API
- Example: GitHub's REST API

### 2. Microservices

**Service Communication:**
- Internal service APIs
- gRPC for inter-service
- REST for external
- Example: Netflix microservices

### 3. Mobile Applications

**Backend APIs:**
- GraphQL for flexible data
- REST for simple operations
- Optimized for bandwidth
- Example: Facebook's GraphQL API

### 4. E-commerce

**Product APIs:**
- Product catalog
- Inventory management
- Order processing
- Example: Amazon's APIs

### 5. Financial Services

**Trading APIs:**
- Real-time data
- High-performance gRPC
- Secure authentication
- Example: Trading platforms

### 6. Social Media

**Content APIs:**
- User profiles
- Posts and comments
- Real-time updates
- Example: Instagram's API

### 7. IoT

**Device APIs:**
- Device management
- Data collection
- Command execution
- Example: Smart home APIs

### 8. Healthcare

**Data APIs:**
- Patient records
- Medical devices
- Lab results
- Example: Healthcare APIs

## Common Mistakes

### 1. Using Verbs in URLs

**Mistake:**
```javascript
// Bad
GET /api/v1/getUsers
POST /api/v1/createUser
```

**Correct:**
```javascript
// Good
GET /api/v1/users
POST /api/v1/users
```

**Why It Matters:**
- REST uses nouns for resources
- HTTP methods indicate actions
- Consistent with REST principles

### 2. Wrong HTTP Status Codes

**Mistake:**
```javascript
// Always returning 200
// Using 200 for errors
// Confusing for clients
```

**Correct:**
```javascript
// Use proper status codes
// 200 for success
// 400 for client errors
// 500 for server errors
```

**Why It Matters:**
- Status codes indicate result
- Clients rely on them
- Standard HTTP semantics

### 3. Not Versioning APIs

**Mistake:**
```javascript
// No versioning
// Breaking changes break clients
// No migration path
```

**Correct:**
```javascript
// Version from start
// /api/v1/users
// /api/v2/users
// Maintain old versions
```

**Why It Matters:**
- Breaking changes inevitable
- Need migration path
- Don't break existing clients

### 4. Inconsistent Response Formats

**Mistake:**
```javascript
// Different formats for different endpoints
// Inconsistent error responses
// Hard for clients to parse
```

**Correct:**
```javascript
// Consistent response format
// Standard error structure
// Easy for clients
```

**Why It Matters:**
- Consistency reduces complexity
- Easier for developers
- Better developer experience

### 5. Missing Authentication

**Mistake:**
```javascript
// Public endpoints that should be private
// No authentication
// Security risk
```

**Correct:**
```javascript
// Implement authentication
// JWT, OAuth, API keys
- Protect sensitive endpoints
```

**Why It Matters:**
- Security critical
- Protect user data
- Prevent unauthorized access

### 6. No Rate Limiting

**Mistake:**
```javascript
// Unlimited requests
- Can abuse API
- Denial of service
- Resource exhaustion
```

**Correct:**
```javascript
// Implement rate limiting
- Protect resources
- Fair usage
- Prevent abuse
```

**Why It Matters:**
- Prevents abuse
- Protects resources
- Ensures fair usage

## Advanced Concepts

### 1. API Gateway

**Concept:**
Single entry point for all APIs.

**Features:**
- Request routing
- Authentication
- Rate limiting
- Load balancing

### 2. GraphQL Federation

**Concept:**
Compose multiple GraphQL services.

**Features:**
- Distributed GraphQL
- Schema stitching
- Cross-service queries

### 3. API Documentation

**Concept:**
Automated API documentation.

**Features:**
- OpenAPI/Swagger
- Interactive docs
- Code generation

### 4. API Testing

**Concept:**
Automated API testing.

**Features:**
- Contract testing
- Integration testing
- Load testing

## Practice Thinking Guide

### How to Design an API

**Key Questions to Ask:**

1. **What are the resources?**
   - Identify nouns (users, posts, comments)
   - Define relationships
   - Example: "User has many posts"

2. **What operations are needed?**
   - CRUD operations
   - Custom operations
   - Example: "Create, read, update, delete users"

3. **Which API paradigm?**
   - REST for simple CRUD
   - GraphQL for complex data
   - gRPC for high performance
   - Example: "REST for public API"

4. **How to authenticate?**
   - JWT, OAuth, API keys
   - Public vs private endpoints
   - Example: "JWT for user authentication"

5. **How to version?**
   - URL versioning
   - Header versioning
   - Example: "/api/v1/users"

**Pattern Recognition:**

**Pattern 1: CRUD API**
```
Resources: Users, Posts
Operations: Create, Read, Update, Delete
Solution: REST with standard HTTP methods
```

**Pattern 2: Complex Data Relationships**
```
Resources: Users, Posts, Comments, Likes
Operations: Nested queries, relationships
Solution: GraphQL for flexible queries
```

**Pattern 3: High-Performance Service**
```
Resources: Internal services
Operations: Frequent communication
Solution: gRPC for performance
```

**Pattern 4: Public API**
```
Resources: Public data
Operations: Read-heavy, some writes
Solution: REST with caching
```

**Pattern 5: Mobile Backend**
```
Resources: Various data types
Operations: Bandwidth-constrained
Solution: GraphQL for efficient data fetching
```

**Decision Flowchart:**

```
API Design Decision:
├─ Public or Private?
│        ├─ Public → REST or GraphQL
│        └─ Private → REST, GraphQL, or gRPC
├─ Simple CRUD or Complex?
│        ├─ Simple → REST
│        └─ Complex → GraphQL
├─ Performance Critical?
│        ├─ Yes → gRPC
│        └─ No → REST or GraphQL
└─ Browser Client?
         ├─ Yes → REST or GraphQL
         └─ No → Any paradigm
```

**Example Analysis:**

**Scenario:** "Design a social media API"

**Analysis:**
1. Resources: Users, Posts, Comments, Likes, Follows
2. Operations: CRUD, complex relationships, real-time updates
3. Public API for developers, private for internal services
4. GraphQL for flexible data fetching
5. REST for simple operations
6. WebSocket for real-time
7. Solution: Hybrid approach

**Scenario:** "Design a payment processing API"

**Analysis:**
1. Resources: Transactions, Accounts, Payments
2. Operations: Create payment, refund, status checks
3. Security critical
4. High performance required
5. Internal service communication
6. Solution: gRPC for internal, REST for external

## Summary

API Design is the process of creating interfaces that enable different software systems to communicate with each other. The three main paradigms are REST, GraphQL, and gRPC, each with distinct advantages. REST uses standard HTTP methods and is simple and cacheable. GraphQL allows flexible data fetching with a single endpoint. gRPC provides high-performance, type-safe communication using Protocol Buffers. Good API design principles include consistency, proper error handling, versioning, authentication, rate limiting, and comprehensive documentation. APIs are fundamental to modern software architecture, enabling microservices, third-party integrations, and client-server communication.

**Key Takeaways:**
- REST: Simple, cacheable, widely supported
- GraphQL: Flexible, efficient, single endpoint
- gRPC: High performance, type-safe, binary format
- Use proper HTTP methods and status codes
- Implement authentication and rate limiting
- Version APIs for breaking changes
- Document APIs comprehensively
- Choose paradigm based on requirements

**Mastery Checklist:**
- ✅ Understand REST principles
- ✅ Design RESTful APIs
- ✅ Understand GraphQL schema design
- ✅ Implement GraphQL resolvers
- ✅ Understand gRPC and Protocol Buffers
- ✅ Implement authentication
- ✅ Implement rate limiting
- ✅ Choose appropriate API paradigm

