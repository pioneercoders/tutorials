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


#### 2.How does Node.js handle asynchronous operations?

Node.js handles asynchronous operations using an event-driven, non-blocking I/O model powered by the event loop and callback queue.

Here’s how it works step-by-step:

1. Single-threaded Execution
 - Node.js runs JavaScript code in a single thread (the main thread).

 - Instead of blocking for slow operations (like file reading, network calls, or database queries), it delegates them to the system kernel or background threads.

2. Asynchronous APIs
 - Node.js provides asynchronous APIs (e.g., fs.readFile, http.get, setTimeout) that immediately return control to the main thread.

 - These APIs accept callbacks (or use Promises/async-await) to run after the operation finishes.

3. Libuv and Thread Pool
 - Node.js uses the libuv library for handling asynchronous tasks.

 - Some tasks (like file I/O, DNS lookup) are handled in a thread pool to avoid blocking the main thread.

4. Event Loop
 - The event loop constantly checks:

   - If the call stack is empty.

   - If there are any pending callbacks/events ready to run.

   - When an asynchronous operation finishes, its callback is pushed into the callback queue.

The event loop moves these callbacks to the call stack when the main thread is free.

5. Example:
```javascript
console.log("Start");

setTimeout(() => {
  console.log("Async operation complete");
}, 2000);

console.log("End");

```
Execution flow:

  - "Start" is printed immediately.

  - setTimeout is registered, and the timer runs in the background.

  - "End" is printed.

  - After 2 seconds, the callback from setTimeout is added to the queue.

  - Event loop executes it → "Async operation complete" is printed.

6. Key Benefits

 - Non-blocking: Other tasks can run while waiting for slow operations.

 - Efficient I/O handling: Ideal for real-time applications (e.g., chats, streaming).

#### 3.Explain the concept of backpressure in streams.

In Node.js streams, backpressure refers to a situation where the data is being produced faster than it can be consumed.

If the readable stream pushes data quicker than the writable stream can handle, the writable stream’s internal buffer starts filling up. If this is not handled properly, it can lead to memory bloat and even application crashes.

How It Happens

-  Readable stream emits data chunks continuously.

-  Writable stream has a limited internal buffer size.

-  If writable is still busy processing the previous chunk, new chunks start queuing.

-  This “queue” growth is backpressure.

Example
```javascript
const fs = require("fs");

const readable = fs.createReadStream("large-file.txt");
const writable = fs.createWriteStream("output.txt");

readable.on("data", (chunk) => {
  const canWrite = writable.write(chunk);
  if (!canWrite) {
    console.log("Backpressure detected! Pausing readable stream...");
    readable.pause();
  }
});

writable.on("drain", () => {
  console.log("Buffer drained! Resuming readable stream...");
  readable.resume();
});

```
Explanation:

 - writable.write(chunk) returns false when the internal buffer is full → Backpressure detected.

 - We pause the readable stream to stop receiving more data.

 - When the buffer drains, the drain event triggers, and we resume reading.

Automatic Handling with .pipe()
Node.js pipe() automatically handles backpressure:
```javascript
fs.createReadStream("large-file.txt")
  .pipe(fs.createWriteStream("output.txt"));
```
Here, Node.js pauses and resumes the readable stream internally when backpressure occurs.
