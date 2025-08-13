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
Promises represent the eventual completion (or failure) of an asynchronous operation.
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
