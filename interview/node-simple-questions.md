#### 1.What is Node.js?
Node.js is an open-source, cross-platform JavaScript runtime environment that allows you to run JavaScript on the server side.

#### 2.What is the main advantage of Node.js?
It is asynchronous and non-blocking, which makes it efficient for handling multiple requests simultaneously.

#### 3.Is Node.js single-threaded or multi-threaded?
Node.js uses a single-threaded event loop for handling requests but can use background worker threads for heavy tasks.

#### 4.What is the difference between JavaScript in the browser and Node.js?
Browser JavaScript: Runs in a browser, mainly used for frontend.

Node.js: Runs on the server, can interact with files, databases, etc.

#### 5.What is npm in Node.js?
npm (Node Package Manager) is used to install, update, and manage third-party packages for Node.js.

#### 6.What is the difference between npm install and npm install --save-dev?
--save (default): Installs as a production dependency.

--save-dev: Installs as a development dependency.

#### 7.What is the role of the package.json file?
It contains metadata about the project and lists dependencies.

#### 8.What is the difference between synchronous and asynchronous code in Node.js?
Synchronous: Code executes line by line, blocking further execution until finished.

Asynchronous: Code executes without blocking, using callbacks/promises.

#### 9.How do you import a module in Node.js?

```javascript
const fs = require('fs'); // CommonJS
```
### 10. What is the difference between CommonJS and ES Modules in Node.js?
CommonJS: Uses require and module.exports.

ES Modules: Uses import and export.

#### 11.What is a callback function in Node.js?
A function passed as an argument to another function, executed after the first function finishes.
```javascript
fs.readFile('file.txt', (err, data) => {
    if (err) throw err;
    console.log(data.toString());
});
```
#### 12.What are Promises in Node.js?
A Promise in JavaScript is an object that represents the eventual result (or error) of an asynchronous operation.
Promises represent the eventual completion (or failure) of an asynchronous operation.

It can be in one of three states:

Pending → operation still running

Fulfilled → operation finished successfully (resolve)

Rejected → operation failed (reject)

```javascript
fetchData().then(result => console.log(result)).catch(err => console.log(err));
```

#### 13.What is async/await in Node.js? explain in detail
Async/await in Node.js is JavaScript’s built-in way to write asynchronous code that looks synchronous. It’s just syntax sugar over Promises—nothing magical—but it makes async flows easier to read, compose, and handle errors.

What it is (in one line)

- async function ⇒ always returns a Promise (even if you return a value).

- await expr ⇒ pauses inside that async function until expr’s Promise settles, then:

  - if fulfilled: gives you the value

  - if rejected: throws an exception you can try/catch
 
Why it matters in Node.js

Node is single-threaded and event-loop driven. I/O (files, DB, HTTP) must be non-blocking to keep throughput high. Async/await lets you write non-blocking I/O code in a top-to-bottom style without callback pyramids or deeply chained .then() calls.

#### 14.What is the difference between readFile and readFileSync in Node.js?
readFile: Asynchronous (non-blocking).

readFileSync: Synchronous (blocking).

#### 15.What is the difference between process.nextTick() and setImmediate()?
deep dive into process.nextTick() vs setImmediate() in Node.js—what they are, where they sit in the event loop, how they schedule work, and when to use each, with runnable examples.

process.nextTick(fn): runs immediately after the current JavaScript stack clears, before the event loop continues to the next phase. It has higher priority than Promise microtasks in Node and can starve the event loop if overused.

setImmediate(fn): runs on the next iteration of the event loop in the check phase, i.e., after I/O callbacks are processed. It yields to the event loop and avoids starvation.

Key differences explained
| Aspect              | `process.nextTick(fn)`                                                      | `setImmediate(fn)`                                        |
| ------------------- | --------------------------------------------------------------------------- | --------------------------------------------------------- |
| Event loop relation | **Not a phase**; runs **before** the loop continues                         | Runs in the **check** phase on the **next iteration**     |
| Priority            | **Highest** (drained before Promise microtasks)                             | Lower (after poll, before timers on the next tick)        |
| Typical use         | Make a callback truly async, finish work **right after** current call stack | Yield back to the loop; run **after I/O**, avoid blocking |
| Risk                | **Starvation** if you schedule many (`while (true) nextTick(...)`)          | No starvation; naturally yields                           |
| Browser support     | Node-only                                                                   | Node-only (not in browsers)                               |

When to use which

Use process.nextTick() when:

 - You need to defer an action just beyond the current call stack so consumers can attach listeners first.

- You want to normalize sync/async behavior (“Zalgo-proofing”) of a callback or EventEmitter.

Use setImmediate() when:

- You want to yield to the event loop and let I/O and timers progress.

- You’re breaking up heavy CPU work into chunks without blocking I/O.

- You’re inside an I/O callback and want your continuation to run immediately after that I/O turn.

