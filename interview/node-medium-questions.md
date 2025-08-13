#### 1.Explain how the Event Loop works in Node.js with different phases.

Node.js is single-threaded for JavaScript execution but can handle multiple operations concurrently using the Event Loop.
It’s part of libuv, the library that handles asynchronous I/O in Node.
The Event Loop allows Node.js to:

 - Handle non-blocking I/O.
 - Schedule callbacks.
 - Manage timers.
 - Process networking events.
Think of it as a traffic controller for all async tasks.

2.Life of the Event Loop
The Event Loop works in ticks (iterations).
Each tick has several phases, and each phase has a callback queue.
The loop runs phase by phase, picking up callbacks from queues.

3.The Phases of the Event Loop
Here’s the exact order of phases:

Phase 1: Timers
Handles setTimeout() and setInterval() callbacks.

Timers are not guaranteed to execute exactly at the scheduled time — they run as soon as possible after the delay expires and when the loop reaches this phase.

Example:
```js
setTimeout(() => console.log("Timer callback"), 0);
```
Phase 2: Pending Callbacks
Executes I/O callbacks that were deferred from the previous loop cycle.

These are system-level callbacks (e.g., TCP errors, DNS lookups).

Phase 3: Idle, Prepare
Internal use by Node.js and libuv — not something you typically hook into.

Prepares the loop for the poll phase.

Phase 4: Poll (Most Important)
This is where Node.js waits for new I/O events (like reading files, network data).

Two main things happen here:

If there are callbacks in the poll queue → execute them.

If no callbacks → wait for new I/O or proceed to check phase if setImmediate() is pending.

Phase 5: Check
Executes all setImmediate() callbacks.

setImmediate() is designed to run right after the poll phase.

```js
setImmediate(() => console.log("setImmediate callback"));
```
Phase 6: Close Callbacks
Executes close event callbacks like:
```js
socket.on('close', () => console.log("Socket closed"));

```
Example Flow

```js
setTimeout(() => console.log("Timer"), 0);
setImmediate(() => console.log("Immediate"));

Promise.resolve().then(() => console.log("Promise"));
process.nextTick(() => console.log("NextTick"));

console.log("Start");
```
expected Out Put
```js
Start
NextTick
Promise
Timer
Immediate
```
Reason:

console.log("Start") runs immediately.

process.nextTick() runs before promises.

Promises (then) run next.

Event Loop moves to timers → runs setTimeout.

Then check phase → runs setImmediate.
