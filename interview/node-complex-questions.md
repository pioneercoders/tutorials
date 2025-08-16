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
