# Node JS

## Okta Integration Guide
- [OktaDev - Youtube](https://www.youtube.com/watch?v=1XxQBXl4Lv8)

## Interview Questions

[Link](https://zerotomastery.io/blog/node-js-interview-questions/)

1. What is Node JS
- JS Runtime environment that allows JS to run outside of Browser
- Built upon Chrome V8 Engine
- Non blocking & Event Driven Architecture

2. Event Loop
- Single Threaded
- Does not wait for a Task to Complete
- Delegates Task to OS and moves to other task
- Once Task is completed event loop picks the result & executes Callback

3. NPM & package.json
- NPM - Node Package Manager is a tool to manage dependencies in Node JS projects
- Helps to install, update & remove packages with ease
- Package.json file serves as the blueprint for your project
- Includes essential details like Project name, Version, Dependencies & Scripts

4. Difference between require & import
- Require is part of ES5
- Default for Node JS environments and works without additional config
- Its Synchronous
- Import is part of ES6
- Modern & consise
- Asynchronous and requires adding type: Module to package.json

5. FS module
- File System module
-
```js 
readFile("example.txt", "utf-8", (err, data)=> {})
```
- readFileSync

6. Modules in Node JS
- Core modules - http, fs, path
- Local modules - Custom modules created inside a project
- 3rd Party modules - Express JS

7. Streams
- Process data piece-by-piece making the process memory efficient for handling large data sets
- Types
	1. Readable - file
	2. Writable - file
	3. Duplex - Sockets (both Read & Write)
	4. Transform - Modifies data as it flows; Eg: Compression
	
8. Middleware
- Middleware has access to Request, Response & Next functions
- Commonly used for Logging, Authentication, Error Handling
- Executed before Request handler

9. Error Handling
- Using Callbacks with err param
-
```js
fs.readFile('file.txt', 'utf8', (err, data) => {
  if (err) {
	console.error('Error reading file:', err.message);
	return;
  }
  console.log(data);
});
```
- Using Promises with catch
- 
```js
fs.promises.readFile('file.txt', 'utf8')
  .then((data) => console.log(data))
  .catch((err) => console.error('Error:', err.message));
```
- Using Async Await with Try catch
```js
async function readFile() {
  try {
	const data = await fs.promises.readFile('file.txt', 'utf8');
	console.log(data);
  } catch (err) {
	console.error('Error:', err.message);
  }
}
readFile();
```

10. Environment variables
- Using Dot Env package
- 
```js
require('dotenv').config();
const dbHost = process.env.DB_HOST;
```

- Using Flags (Node 20.6.0+)
- 
```js
node --env-file=.env app.js
```

11. Clustering
- Creating multiple instances of your application to take advantage of multi-core processors
- Clustering is ideal for high traffic applications
- The master process forks a worker process for each CPU core
- Each worker handles incoming requests, distributing the load and improving performance
- 
```js
const cluster = require('cluster');
const http = require('http');
const os = require('os');

if (cluster.isMaster) {
  const numCPUs = os.cpus().length;
  for (let i = 0; i < numCPUs; i++) {
	cluster.fork(); // Create a worker process
  }
} else {
  http.createServer((req, res) => {
	res.writeHead(200);
	res.end('Hello, World!');
  }).listen(3000);
}
```

12. Worker Threads
- Run code in parallel threads & useful for CPU intensive tasks
- Share memory with the main thread making it more efficient

13. Event Loop Starvation
- Occurs when long running tasks block the event loop
- Can be prevented using Worker threads, Asynchronous operations

14. process.nextTick() vs setImmediate()
- process.nextTick() - Executes callbacks at the end of the current operation, before I/O events
- setImmediate() - Executes callbacks at the end of the current operation, after I/O events
- 
```js
(()=>{
    let stockPrice=1000;
    console.log(`Stock Price: ${stockPrice}`);
    setTimeout(()=>{
        console.log(`Stock Price: ${stockPrice+10}`)
    },0)
    setImmediate(()=>{
        console.log('Stock sales increase after increase in Price')
    })
    process.nextTick(()=>{
        console.log(`Stock Price Opening for Day: ${stockPrice+2}`)
    })
})();

/* Output
Stock Price: 1000
Stock Price Opening for Day: 1002
Stock Price: 1010
Stock sales increase after increase in Price
*/
```
