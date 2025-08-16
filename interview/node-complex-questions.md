#### 1.Explain memory management and garbage collection in Node.js.

Node.js is built on V8 (Google’s JavaScript engine), so memory management works mostly like in JavaScript in browsers.

Memory management in Node.js

Node.js uses the V8 engine, which automatically handles memory allocation and cleanup.

  - Memory is divided into stack (for function calls and primitives) and heap (for objects).

  - Node.js has a default memory limit (about 1.5–2 GB per process).

  - As developers, we must avoid memory leaks (like unused global variables, unremoved event listeners, or large objects kept in memory).

garbage collection in Node.js

Node.js uses automatic garbage collection provided by V8.

It works on a mark-and-sweep algorithm → finds unreachable objects and frees them.

Uses generational GC:

 - New space: for short-lived objects (collected quickly).

 - Old space: for long-lived objects (collected less frequently).


#### 2.How would you scale a Node.js application on multiple cores and multiple servers?

By default, Node.js runs on a single thread, so to fully use system resources we need to scale it.

1. Scaling on Multiple Cores (same machine)

   Use the Cluster module or PM2 process manager.

   They create multiple worker processes that share the same server port.

   This way, Node.js can utilize all CPU cores.
```js
const cluster = require('cluster');
const os = require('os');

if (cluster.isMaster) {
  const numCPUs = os.cpus().length;
  for (let i = 0; i < numCPUs; i++) {
    cluster.fork();
  }
} else {
  require('./app'); // worker runs the app
}
```

2. Scaling on Multiple Servers

Use a load balancer (like NGINX, HAProxy, or AWS ELB) in front of multiple Node.js servers.

Requests are distributed across servers.

Use a shared session store (e.g., Redis, MongoDB) so that session/state is available to all servers.

3. Additional Scaling Practices

Use containerization (Docker + Kubernetes) for orchestration.

Implement caching (Redis, CDN) for performance.

Use horizontal scaling (add more servers) + vertical scaling (increase CPU/RAM).
