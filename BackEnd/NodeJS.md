# Node.js Cheatsheet

## Node.js Basics

### Basic Script

```javascript
// hello.js
// Simple console output
console.log('Hello, Node.js!');

// Run: node hello.js
```

### Module Export/Import (CommonJS - Primary)

```javascript
// math.js
// CommonJS: Synchronous, widely used
module.exports = {
  add: (a, b) => a + b,
  subtract: (a, b) => a - b,
};

// app.js
const math = require('./math');
console.log(math.add(2, 3)); // 5
```

### Module Export/Import (ES Modules - Alternative)

```javascript
// math.mjs
// ES Modules: Modern, async-friendly
export const add = (a, b) => a + b;
export const subtract = (a, b) => a - b;

// app.mjs
import { add } from './math.mjs';
console.log(add(2, 3)); // 5

// Requires "type": "module" in package.json or .mjs extension
```

### TypeScript Alternative

```typescript
// math.ts
export const add = (a: number, b: number): number => a + b;
export const subtract = (a: number, b: number): number => a - b;

// app.ts
import { add } from './math';
console.log(add(2, 3)); // 5

// Run: ts-node app.ts or compile with tsc
```

- **Node.js Overview**: JavaScript runtime on V8 engine, non-blocking I/O for server-side apps.
- **Modules**:
  - **CommonJS**: Default, synchronous, mature ecosystem.
  - **ES Modules**: Modern, supports tree-shaking, async imports.
  - **TypeScript**: Type-safe, compiles to JavaScript, growing adoption.
- **Setup**:
  - Install via `nvm` for version management.
  - Initialize with `npm init -y` or `yarn init`.
  - TypeScript requires `tsconfig.json` and `ts-node` or `tsc`.
- **Best Practices**:
  - Use ES Modules for new projects; CommonJS for legacy.
  - Use TypeScript for large apps to catch errors early.
  - Avoid global scope; encapsulate logic in modules.

**Explanation**:

- CommonJS is reliable but blocks during module loading.
- ES Modules align with browser standards, supporting dynamic imports.
- TypeScript enhances maintainability with static types, ideal for teams.
- `nvm` simplifies switching Node versions for compatibility.

---

## Core Modules

### File System (fs - Async vs. Sync)

```javascript
// Synchronous (fs.readFileSync)
const fs = require('fs');

try {
  // Blocks event loop, use for scripts
  const data = fs.readFileSync('file.txt', 'utf8');
  console.log(data);
} catch (err) {
  console.error('Error:', err);
}

// Asynchronous (fs.promises)
const fsPromises = require('fs').promises;

async function readFile() {
  try {
    // Non-blocking, preferred for servers
    const data = await fsPromises.readFile('file.txt', 'utf8');
    console.log(data);
  } catch (err) {
    console.error('Error:', err);
  }
}
readFile();
```

### Path Module

```javascript
const path = require('path');

// Cross-platform path operations
const filePath = path.join(__dirname, 'data', 'file.txt'); // e.g., /app/data/file.txt
const ext = path.extname(filePath); // '.txt'
const base = path.basename(filePath); // 'file.txt'
console.log({ filePath, ext, base });
```

### HTTP Module (Basic Server)

```javascript
const http = require('http');

// Simple HTTP server
const server = http.createServer((req, res) => {
  res.writeHead(200, { 'Content-Type': 'text/plain' });
  res.end('Hello, Node.js!');
});

server.listen(3000, () => console.log('Server on http://localhost:3000'));
```

- **Core Modules**:
  - **fs**: File operations (`readFile`, `writeFile`, `appendFile`).
  - **path**: Path manipulation (`join`, `resolve`, `dirname`).
  - **http**: HTTP servers/clients, base for frameworks.
  - Others: `os` (system info), `url` (URL parsing), `crypto` (encryption), `events` (event emitters).
- **Approaches**:
  - **Sync fs**: Simple for CLI tools, blocks event loop.
  - **Async fs**: Non-blocking, use `fs.promises` for modern syntax.
- **Best Practices**:
  - Prefer async `fs` methods for performance.
  - Use `path` for OS-agnostic file paths.
  - Avoid raw `http` in production; use Express or Fastify.

**Explanation**:

- Sync `fs` is convenient but unsuitable for high-concurrency apps.
- `fs.promises` integrates with async/await, reducing callback hell.
- `path` ensures portability across Windows/Linux/Mac.
- `http` is foundational but lacks routing; frameworks add abstractions.

---

## Event Loop (Understanding Node.js Core)

### Basic Example

```javascript
// Demonstrates event loop behavior
console.log('Start');

setTimeout(() => console.log('Timeout'), 0);
Promise.resolve().then(() => console.log('Promise'));

console.log('End');

// Output: Start, End, Promise, Timeout
```

### Detailed Phases

```javascript
const fs = require('fs');

// Simulate event loop phases
console.log('1: Start (main script)');

setTimeout(() => console.log('2: Timer callback'), 0); // Timers phase
fs.readFile('file.txt', () => console.log('3: I/O callback')); // I/O polling phase
Promise.resolve().then(() => console.log('4: Microtask')); // Microtask queue

process.nextTick(() => console.log('5: Next tick')); // Next tick queue
console.log('6: End (main script)');
```

- **Event Loop Overview**: Manages asynchronous operations via phases:
  - **Timers**: Executes `setTimeout`/`setInterval` callbacks.
  - **I/O Callbacks**: Handles I/O operations (e.g., `fs.readFile`).
  - **Idle/Prepare**: Internal Node.js tasks.
  - **Poll**: Retrieves new I/O events.
  - **Check**: Executes `setImmediate` callbacks.
  - **Close**: Handles close events (e.g., socket closure).
  - **Microtasks**: `Promise.then`, `process.nextTick` (higher priority).
- **Best Practices**:
  - Avoid blocking the event loop with CPU-intensive tasks.
  - Use `process.nextTick` for immediate async tasks, sparingly.
  - Understand microtask vs. macrotask precedence for debugging.

**Explanation**:

- The event loop is Node.js’s core mechanism for non-blocking I/O.
- Microtasks (`Promise`, `nextTick`) run before timers, causing `Promise` to log before `setTimeout`.
- Blocking operations (e.g., `while(true)`) stall the loop, degrading performance.
- Use tools like `libuv` documentation to understand low-level details.

---

## Express.js for Web Development

### Express Server (Primary)

```javascript
const express = require('express');
const app = express();

// Middleware: Parse JSON
app.use(express.json());

// GET route
app.get('/', (req, res) => res.send('Hello, Express!'));

// POST route with params
app.post('/users/:id', (req, res) => {
  const { id } = req.params;
  const { name } = req.body;
  res.json({ id, name });
});

// Error middleware
app.use((err, req, res, next) => {
  console.error(err.stack);
  res.status(500).json({ error: 'Server error' });
});

app.listen(3000, () => console.log('Server on http://localhost:3000'));
```

### Fastify (Alternative)

```javascript
const fastify = require('fastify')({ logger: true });

// GET route
fastify.get('/', async (request, reply) => 'Hello, Fastify!');

// POST route with schema validation
fastify.post('/users/:id', {
  schema: {
    params: { id: { type: 'string' } },
    body: { name: { type: 'string' } },
  },
}, async (request, reply) => {
  const { id } = request.params;
  const { name } = request.body;
  return { id, name };
});

// Error handler
fastify.setErrorHandler((error, request, reply) => {
  reply.status(500).send({ error: 'Server error' });
});

fastify.listen({ port: 3000 }, err => {
  if (err) console.error(err);
  console.log('Server on http://localhost:3000');
});
```

### Koa (Alternative)

```javascript
const Koa = require('koa');
const Router = require('koa-router');
const bodyParser = require('koa-bodyparser');
const app = new Koa();
const router = new Router();

// Middleware
app.use(bodyParser());

// Routes
router.get('/', ctx => {
  ctx.body = 'Hello, Koa!';
});
router.post('/users/:id', ctx => {
  const { id } = ctx.params;
  const { name } = ctx.request.body;
  ctx.body = { id, name };
});

// Error handling
app.use(async (ctx, next) => {
  try {
    await next();
  } catch (err) {
    ctx.status = 500;
    ctx.body = { error: 'Server error' };
  }
});

app.use(router.routes());
app.listen(3000, () => console.log('Server on http://localhost:3000'));
```

- **Frameworks**:
  - **Express**: Popular, middleware-based, large ecosystem.
  - **Fastify**: High-performance, schema-driven, modern.
  - **Koa**: Minimal, async-focused, uses middleware composition.
- **Best Practices**:
  - Use middleware for logging (`morgan`), security (`helmet`), CORS (`cors`).
  - Validate inputs with `joi`, `zod`, or framework schemas.
  - Structure routes in separate files for scalability.

**Explanation**:

- Express is beginner-friendly but slower for high loads.
- Fastify excels in performance with built-in validation.
- Koa leverages async/await natively, reducing callback complexity.
- Choose Express for community support, Fastify for speed, Koa for minimalism.

---

## Asynchronous Programming

### Callbacks (Legacy)

```javascript
const fs = require('fs');

// Callback-based
fs.readFile('file.txt', 'utf8', (err, data) => {
  if (err) return console.error('Error:', err);
  console.log(data);
});
```

### Promises

```javascript
const fs = require('fs').promises;

// Promise-based
fs.readFile('file.txt', 'utf8')
  .then(data => console.log(data))
  .catch(err => console.error('Error:', err));
```

### Async/Await (Preferred)

```javascript
const fs = require('fs').promises;

async function readFile() {
  try {
    const data = await fs.readFile('file.txt', 'utf8');
    console.log(data);
  } catch (err) {
    console.error('Error:', err);
  }
}
readFile();
```

### Promisify (Bridge Callbacks to Promises)

```javascript
const fs = require('fs');
const util = require('util');

// Convert callback-based to Promise
const readFile = util.promisify(fs.readFile);

async function readFileAsync() {
  try {
    const data = await readFile('file.txt', 'utf8');
    console.log(data);
  } catch (err) {
    console.error('Error:', err);
  }
}
readFileAsync();
```

- **Approaches**:
  - **Callbacks**: Error-prone, leads to nesting.
  - **Promises**: Chainable, better error handling.
  - **Async/Await**: Readable, standard for modern Node.js.
  - **Promisify**: Adapts legacy APIs to Promises.
- **Best Practices**:
  - Use async/await for clarity.
  - Handle errors with try-catch or `.catch`.
  - Use `Promise.all` for parallel operations.

**Explanation**:

- Callbacks cause callback hell; avoid in new code.
- Promises improve flow but require chaining.
- Async/await is syntactic sugar over Promises, most maintainable.
- `util.promisify` bridges old APIs, preserving compatibility.

---

## Database Integration

### MongoDB with Mongoose (NoSQL)

```javascript
const mongoose = require('mongoose');

// Connect
mongoose.connect('mongodb://localhost:27017/mydb', {
  useNewUrlParser: true,
  useUnifiedTopology: true,
});

// Schema
const userSchema = new mongoose.Schema({
  name: String,
  age: Number,
});
const User = mongoose.model('User', userSchema);

// CRUD
async function manageUsers() {
  await User.create({ name: 'Suman', age: 25 });
  const users = await User.find();
  await User.updateOne({ name: 'Suman' }, { age: 26 });
  await User.deleteOne({ name: 'Suman' });
  console.log(users);
}
manageUsers();
```

### PostgreSQL with Sequelize (SQL)

```javascript
const { Sequelize, DataTypes } = require('sequelize');

const sequelize = new Sequelize('postgres://user:pass@localhost:5432/mydb');

const User = sequelize.define('User', {
  name: { type: DataTypes.STRING, allowNull: false },
  age: { type: DataTypes.INTEGER },
});

async function manageUsers() {
  await sequelize.sync({ force: true });
  await User.create({ name: 'Suman', age: 25 });
  const users = await User.findAll();
  await User.update({ age: 26 }, { where: { name: 'Suman' } });
  await User.destroy({ where: { name: 'Suman' } });
  console.log(users);
}
manageUsers();
```

### Raw Queries with pg (Alternative)

```javascript
const { Pool } = require('pg');
const pool = new Pool({
  user: 'user',
  host: 'localhost',
  database: 'mydb',
  password: 'pass',
  port: 5432,
});

async function manageUsers() {
  const client = await pool.connect();
  try {
    await client.query('CREATE TABLE IF NOT EXISTS users (name TEXT, age INTEGER)');
    await client.query('INSERT INTO users (name, age) VALUES ($1, $2)', ['Suman', 25]);
    const res = await client.query('SELECT * FROM users');
    await client.query('UPDATE users SET age = $1 WHERE name = $2', [26, 'Suman']);
    await client.query('DELETE FROM users WHERE name = $1', ['Suman']);
    console.log(res.rows);
  } finally {
    client.release();
  }
}
manageUsers();
```

- **Approaches**:
  - **Mongoose**: ORM for MongoDB, schema-based.
  - **Sequelize**: ORM for SQL, supports relations.
  - **Raw Queries (pg)**: Direct control, high performance.
- **Best Practices**:
  - Use ORMs for productivity; raw queries for speed.
  - Use parameterized queries to prevent SQL injection.
  - Implement connection pooling for scalability.

**Explanation**:

- Mongoose simplifies NoSQL with schemas, ideal for flexible data.
- Sequelize handles SQL relationships but adds overhead.
- `pg` offers low-level control, suitable for custom queries.
- Pooling (`Pool`) manages connections efficiently under load.

---

## Environment Variables

### Using dotenv

```javascript
// .env
// DATABASE_URL=mongodb://localhost:27017/mydb

// app.js
require('dotenv').config();
const dbUrl = process.env.DATABASE_URL;
console.log('Connecting to:', dbUrl);
```

### yargs for CLI Arguments

```javascript
const yargs = require('yargs');

const argv = yargs
  .option('db', {
    alias: 'database',
    description: 'Database URL',
    type: 'string',
  })
  .argv;

const dbUrl = argv.db || 'mongodb://localhost:27017/mydb';
console.log('Connecting to:', dbUrl);

// Run: node app.js --db mongodb://localhost:27017/otherdb
```

### envalid for Validation

```javascript
const { cleanEnv, str, url } = require('envalid');
require('dotenv').config();

// Validate environment variables
const env = cleanEnv(process.env, {
  DATABASE_URL: url(),
  API_KEY: str(),
});

console.log('Connecting to:', env.DATABASE_URL);
```

- **Approaches**:
  - **dotenv**: Standard for `.env` files.
  - **yargs**: CLI-based, dynamic configuration.
  - **envalid**: Validates `.env` variables at runtime.
- **Best Practices**:
  - Exclude `.env` from version control.
  - Validate critical variables with `envalid` or similar.
  - Use defaults for non-sensitive configs.

**Explanation**:

- `dotenv` is simple, widely adopted for environment configs.
- `yargs` suits scripts with variable inputs.
- `envalid` ensures type safety and prevents runtime errors.
- Secure sensitive data with environment-specific `.env` files.

---

## Error Handling

### Try-Catch with Async/Await

```javascript
async function fetchData() {
  try {
    const response = await fetch('https://api.example.com/data');
    if (!response.ok) throw new Error('Network error');
    const data = await response.json();
    console.log(data);
  } catch (err) {
    console.error('Error:', err.message);
  }
}
fetchData();
```

### Express Error Middleware

```javascript
const express = require('express');
const app = express();

app.get('/data', async (req, res, next) => {
  try {
    const data = await fetch('https://api.example.com/data').then(res => res.json());
    res.json(data);
  } catch (err) {
    next(err);
  }
});

app.use((err, req, res, next) => {
  console.error(err.stack);
  res.status(500).json({ error: 'Server error' });
});

app.listen(3000);
```

### Global Uncaught Exception Handler

```javascript
process.on('uncaughtException', err => {
  console.error('Uncaught Exception:', err.message);
  process.exit(1);
});

process.on('unhandledRejection', (reason, promise) => {
  console.error('Unhandled Rejection at:', promise, 'reason:', reason);
  process.exit(1);
});

// Example: Trigger unhandled rejection
Promise.reject(new Error('Test error'));
```

- **Approaches**:
  - **Try-Catch**: Standard for async code.
  - **Express Middleware**: Centralized for web apps.
  - **Global Handlers**: Catch unhandled errors/rejections.
- **Best Practices**:
  - Log errors with structured logging (Winston, Pino).
  - Gracefully shut down on fatal errors.
  - Use `express-async-errors` for async route errors.

**Explanation**:

- Try-catch is explicit and integrates with async/await.
- Express middleware consolidates error handling.
- Global handlers prevent crashes but should exit after logging.
- Structured logging aids debugging in production.

---

## Streams

### Readable/Writable Streams

```javascript
const fs = require('fs');

const readStream = fs.createReadStream('largefile.txt', 'utf8');
const writeStream = fs.createWriteStream('output.txt');

readStream.pipe(writeStream);
readStream.on('data', chunk => console.log('Chunk:', chunk.length));
readStream.on('end', () => console.log('Done'));
```

### Transform Stream

```javascript
const { Transform } = require('stream');
const fs = require('fs');

const upperCaseTransform = new Transform({
  transform(chunk, encoding, callback) {
    this.push(chunk.toString().toUpperCase());
    callback();
  },
});

fs.createReadStream('largefile.txt')
  .pipe(upperCaseTransform)
  .pipe(fs.createWriteStream('output.txt'));
```

### Using stream.pipeline

```javascript
const { pipeline } = require('stream');
const fs = require('fs');
const zlib = require('zlib');

pipeline(
  fs.createReadStream('largefile.txt'),
  zlib.createGzip(),
  fs.createWriteStream('largefile.txt.gz'),
  err => {
    if (err) console.error('Pipeline failed:', err);
    else console.log('Pipeline succeeded');
  }
);
```

- **Streams**: Process data in chunks, ideal for large files or real-time.
- **Approaches**:
  - **Readable/Writable**: Basic file/network streaming.
  - **Transform**: Modify data (e.g., compression).
  - **pipeline**: Robust piping with error handling.
- **Best Practices**:
  - Use `pipeline` for safe stream chaining.
  - Handle stream errors with `on('error')`.
  - Monitor backpressure for performance.

**Explanation**:

- Streams reduce memory usage compared to loading entire files.
- Transform streams enable real-time data processing.
- `pipeline` ensures proper cleanup, preventing memory leaks.
- Use libraries like `fs-extra` for simpler stream operations.

---

## Worker Threads

### Basic Worker Thread

```javascript
const { Worker, isMainThread, parentPort, workerData } = require('worker_threads');

if (isMainThread) {
  // Main thread: Spawn worker
  const worker = new Worker(__filename, { workerData: { num: 42 } });
  worker.on('message', msg => console.log('Result:', msg));
  worker.on('error', err => console.error('Error:', err));
  worker.on('exit', code => console.log('Worker exited with code:', code));
} else {
  // Worker: Perform CPU-intensive task
  const result = workerData.num * 2;
  parentPort.postMessage(result);
}
```

### Alternative: Child Processes

```javascript
const { fork } = require('child_process');

const child = fork('worker.js');
child.send({ num: 42 });
child.on('message', msg => console.log('Result:', msg));
child.on('error', err => console.error('Error:', err));
child.on('exit', code => console.log('Child exited with code:', code));

// worker.js
process.on('message', msg => {
  const result = msg.num * 2;
  process.send(result);
});
```

- **Approaches**:
  - **Worker Threads**: Run JavaScript in parallel threads, share memory.
  - **Child Processes**: Run separate processes, higher overhead.
- **Best Practices**:
  - Use worker threads for CPU-intensive tasks (e.g., image processing).
  - Use child processes for external scripts or isolation.
  - Limit workers to CPU core count.

**Explanation**:

- Worker threads are lighter than child processes, sharing memory via `SharedArrayBuffer`.
- Child processes are isolated, suitable for running non-JavaScript tasks.
- Both offload work from the event loop, improving responsiveness.
- Use `piscina` for a high-level worker thread pool.

---

## Clustering

### Cluster Module

```javascript
const cluster = require('cluster');
const http = require('http');
const numCPUs = require('os').cpus().length;

if (cluster.isMaster) {
  console.log(`Master ${process.pid} running`);
  for (let i = 0; i < numCPUs; i++) {
    cluster.fork();
  }
  cluster.on('exit', (worker) => {
    console.log(`Worker ${worker.process.pid} died`);
    cluster.fork();
  });
} else {
  http
    .createServer((req, res) => {
      res.writeHead(200);
      res.end('Hello from worker ' + process.pid);
    })
    .listen(3000);
  console.log(`Worker ${process.pid} started`);
}
```

### PM2 (Alternative)

```javascript
// app.js
const express = require('express');
const app = express();
app.get('/', (req, res) => res.send('Hello'));
app.listen(3000);

// Run: pm2 start app.js -i max
```

- **Approaches**:
  - **Cluster**: Built-in, manual worker management.
  - **PM2**: Automates clustering, monitoring, restarts.
- **Best Practices**:
  - Cluster for high-concurrency apps.
  - Use PM2 for production with zero-downtime reloads.
  - Ensure stateless workers; use Redis for state.

**Explanation**:

- Clustering utilizes multiple CPU cores, improving throughput.
- PM2 simplifies management with logging and scaling.
- Stateless design prevents data loss during worker restarts.
- Combine with load balancers (e.g., Nginx) for high traffic.

---

## WebSockets

### Using ws

```javascript
const WebSocket = require('ws');
const server = new WebSocket.Server({ port: 8080 });

server.on('connection', ws => {
  ws.on('message', message => {
    console.log('Received:', message.toString());
    ws.send(`Echo: ${message}`);
  });
  ws.on('close', () => console.log('Client disconnected'));
});

console.log('WebSocket server on ws://localhost:8080');
```

### Socket.IO (Alternative)

```javascript
const express = require('express');
const { createServer } = require('http');
const { Server } = require('socket.io');

const app = express();
const httpServer = createServer(app);
const io = new Server(httpServer);

io.on('connection', socket => {
  socket.on('message', msg => {
    console.log('Received:', msg);
    socket.emit('message', `Echo: ${msg}`);
  });
  socket.on('disconnect', () => console.log('Client disconnected'));
});

httpServer.listen(8080, () => console.log('Server on http://localhost:8080'));
```

- **Approaches**:
  - **ws**: Lightweight, low-level WebSocket library.
  - **Socket.IO**: Higher-level, supports rooms and events.
- **Best Practices**:
  - Use WebSockets for real-time apps (e.g., chat, gaming).
  - Implement reconnection logic for reliability.
  - Secure with `wss://` in production.

**Explanation**:

- `ws` is minimal, ideal for custom protocols.
- Socket.IO adds features like rooms and fallbacks, easier for complex apps.
- Both require secure connections (TLS) in production.
- Scale WebSockets with Redis for distributed systems.

---

## GraphQL with Apollo

### Apollo Server

```javascript
const { ApolloServer, gql } = require('apollo-server');

const typeDefs = gql`
  type User {
    id: ID!
    name: String!
  }
  type Query {
    users: [User]
  }
`;

const resolvers = {
  Query: {
    users: () => [{ id: '1', name: 'Suman' }],
  },
};

const server = new ApolloServer({ typeDefs, resolvers });

server.listen(4000).then(({ url }) => console.log(`GraphQL server on ${url}`));
```

### REST Alternative (Express)

```javascript
const express = require('express');
const app = express();

app.use(express.json());
app.get('/users', (req, res) => res.json([{ id: '1', name: 'Suman' }]));

app.listen(4000, () => console.log('REST server on http://localhost:4000'));
```

- **Approaches**:
  - **GraphQL (Apollo)**: Flexible queries, single endpoint.
  - **REST (Express)**: Traditional, multiple endpoints.
- **Best Practices**:
  - Use GraphQL for complex data relationships.
  - Implement caching (e.g., DataLoader) for GraphQL performance.
  - Secure GraphQL with depth limiting and authentication.

**Explanation**:

- GraphQL reduces over/under-fetching compared to REST.
- Apollo simplifies GraphQL setup with schema and resolvers.
- REST is simpler for basic APIs but less flexible.
- Combine GraphQL with subscriptions for real-time updates.

---

## Microservices Patterns

### Basic Microservice with Express

```javascript
const express = require('express');
const app = express();

app.use(express.json());
app.get('/users', (req, res) => res.json([{ id: '1', name: 'Suman' }]));

// Communicate with other services via HTTP
app.post('/notify', async (req, res) => {
  const response = await fetch('http://localhost:3001/log', {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify(req.body),
  });
  res.json(await response.json());
});

app.listen(3000, () => console.log('User service on http://localhost:3000'));
```

### Message Queue with RabbitMQ

```javascript
const amqp = require('amqplib');

async function publishMessage() {
  const connection = await amqp.connect('amqp://localhost');
  const channel = await connection.createChannel();
  const queue = 'user_events';

  await channel.assertQueue(queue, { durable: true });
  channel.sendToQueue(queue, Buffer.from(JSON.stringify({ id: '1', name: 'Suman' })));
  console.log('Message sent');

  await channel.close();
  await connection.close();
}

async function consumeMessage() {
  const connection = await amqp.connect('amqp://localhost');
  const channel = await connection.createChannel();
  const queue = 'user_events';

  await channel.assertQueue(queue, { durable: true });
  channel.consume(queue, msg => {
    console.log('Received:', JSON.parse(msg.content.toString()));
    channel.ack(msg);
  });
}

publishMessage();
consumeMessage();
```

- **Approaches**:
  - **HTTP Microservices**: Simple, REST-based communication.
  - **Message Queues (RabbitMQ)**: Decoupled, async communication.
- **Best Practices**:
  - Use message queues for high-throughput, decoupled services.
  - Implement service discovery with tools like Consul.
  - Monitor with Prometheus and Grafana.

**Explanation**:

- HTTP microservices are easy to set up but tightly coupled.
- RabbitMQ enables asynchronous, resilient communication.
- Microservices increase complexity; ensure clear boundaries.
- Use Kubernetes or Docker for orchestration in production.

---

## Debugging and Profiling

### Node.js Inspector

```javascript
// app.js
console.log('Debug me');

// Run: node --inspect app.js
// Open chrome://inspect in Chrome
```

### Clinic.js for Profiling

```javascript
// Install: npm install clinic
// Run: clinic doctor -- node app.js

const http = require('http');
http.createServer((req, res) => {
  res.end('Hello');
}).listen(3000);
```

- **Approaches**:
  - **Inspector**: Built-in, Chrome DevTools integration.
  - **Clinic.js**: Visualizes performance bottlenecks (e.g., CPU, I/O).
- **Best Practices**:
  - Use `--inspect` for runtime debugging.
  - Profile with Clinic.js to identify bottlenecks.
  - Log with structured formats for traceability.

**Explanation**:

- Inspector is ideal for debugging logic errors.
- Clinic.js provides insights into performance (e.g., event loop delays).
- Combine with logging (Pino) for comprehensive diagnostics.
- Use in development to catch issues early.

---

## Docker Integration

### Dockerfile

```dockerfile
# Use official Node.js image
FROM node:18

# Set working directory
WORKDIR /app

# Copy package.json and install dependencies
COPY package*.json ./
RUN npm install

# Copy source code
COPY . .

# Expose port
EXPOSE 3000

# Run app
CMD ["node", "app.js"]
```

### Docker Compose

```yaml
version: '3'
services:
  app:
    build: .
    ports:
      - "3000:3000"
    environment:
      - DATABASE_URL=mongodb://mongo:27017/mydb
  mongo:
    image: mongo
    ports:
      - "27017:27017"
```

- **Docker**: Containerizes Node.js apps for consistent deployment.
- **Best Practices**:
  - Use multi-stage builds for smaller images.
  - Define environment variables in `docker-compose.yml`.
  - Use `.dockerignore` to exclude unnecessary files.

**Explanation**:

- Docker ensures consistent environments across development and production.
- Docker Compose simplifies multi-container setups (e.g., app + database).
- Optimize images with `node:alpine` for smaller footprints.
- Use orchestrators like Kubernetes for scaling.

---

## Security Best Practices

### Helmet for Headers

```javascript
const express = require('express');
const helmet = require('helmet');
const app = express();

app.use(helmet());
app.get('/', (req, res) => res.send('Secure'));

app.listen(3000);
```

### Validation with Zod

```javascript
const express = require('express');
const z = require('zod');
const app = express();

app.use(express.json());
const schema = z.object({
  name: z.string().min(3),
  age: z.number().int().nonnegative(),
});

app.post('/users', (req, res) => {
  try {
    const value = schema.parse(req.body);
    res.json(value);
  } catch (err) {
    res.status(400).json({ error: err.errors });
  }
});

app.listen(3000);
```

### JWT Authentication

```javascript
const express = require('express');
const jwt = require('jsonwebtoken');
const app = express();

app.use(express.json());
const SECRET = 'mysecret';

// Login route
app.post('/login', (req, res) => {
  const { username } = req.body;
  const token = jwt.sign({ username }, SECRET, { expiresIn: '1h' });
  res.json({ token });
});

// Protected route
app.get('/protected', (req, res) => {
  const token = req.headers.authorization?.split(' ')[1];
  try {
    const decoded = jwt.verify(token, SECRET);
    res.json({ message: `Hello, ${decoded.username}` });
  } catch (err) {
    res.status(401).json({ error: 'Unauthorized' });
  }
});

app.listen(3000);
```

- **Practices**:
  - **Helmet**: Secure headers (XSS, CSP).
  - **Zod**: Type-safe validation, TypeScript-friendly.
  - **JWT**: Stateless authentication for APIs.
  - Others: Rate limiting (`express-rate-limit`), CSRF (`csurf`).
- **Best Practices**:
  - Use HTTPS with TLS certificates.
  - Hash passwords with `bcrypt`.
  - Audit dependencies with `npm audit`.

**Explanation**:

- Helmet mitigates common web vulnerabilities.
- Zod ensures robust input validation, reducing injection risks.
- JWT is lightweight for APIs but requires secure token management.
- Regular security updates are critical to prevent exploits.

---

## Testing

### Jest

```javascript
// math.js
module.exports = { add: (a, b) => a + b };

// math.test.js
const { add } = require('./math');
test('adds 2 + 3', () => {
  expect(add(2, 3)).toBe(5);
});
```

### Mocha + Chai

```javascript
const { expect } = require('chai');
const { add } = require('./math');

describe('Math', () => {
  it('adds 2 + 3', () => {
    expect(add(2, 3)).to.equal(5);
  });
});
```

### Supertest for APIs

```javascript
const request = require('supertest');
const express = require('express');
const app = express();

app.get('/api', (req, res) => res.json({ message: 'Hello' }));

test('GET /api', async () => {
  const response = await request(app).get('/api');
  expect(response.status).toBe(200);
  expect(response.body.message).toBe('Hello');
});
```

- **Approaches**:
  - **Jest**: Zero-config, unit testing.
  - **Mocha + Chai**: Flexible, custom setups.
  - **Supertest**: API testing, integrates with Jest/Mocha.
- **Best Practices**:
  - Mock dependencies with `jest.mock` or `sinon`.
  - Test edge cases and errors.
  - Use coverage tools (`nyc`, `c8`).

**Explanation**:

- Jest is ideal for quick setup and mocking.
- Mocha + Chai suit complex test suites.
- Supertest ensures APIs behave as expected.
- High coverage (80%+) ensures reliability.

---

## Common Node.js APIs & Modules

- **Core**: `fs`, `path`, `http`, `https`, `url`, `os`, `crypto`, `events`, `stream`, `worker_threads`, `child_process`.
- **NPM**:
  - **Web**: `express`, `fastify`, `koa`, `apollo-server`.
  - **Database**: `mongoose`, `sequelize`, `pg`, `knex`.
  - **Utilities**: `lodash`, `axios`, `dotenv`, `nodemon`.
  - **Security**: `helmet`, `joi`, `zod`, `bcrypt`, `jsonwebtoken`.
  - **Testing**: `jest`, `mocha`, `chai`, `supertest`.
- **Process**: `process.env`, `process.on`, `process.exit`.

**Explanation**:

- Core modules minimize dependencies for basic tasks.
- NPM packages enhance functionality; vet for security.
- `process` APIs manage runtime and errors.

---

## Cheat Codes

```javascript
// Debug with console
console.dir(obj, { depth: null });

// Auto-restart with nodemon
// package.json: "scripts": { "dev": "nodemon app.js" }

// Graceful shutdown
process.on('SIGTERM', () => {
  server.close(() => process.exit(0));
});

// Memory usage
console.log(process.memoryUsage());

// Async Express handler
const asyncHandler = fn => (req, res, next) =>
  Promise.resolve(fn(req, res, next)).catch(next);
```

**Explanation**:

- `console.dir` aids deep object inspection.
- `nodemon` boosts development speed.
- Graceful shutdown prevents resource leaks.
- `asyncHandler` streamlines async routes.

---

## Best Practices

- **Code**: Structure with `src/controllers`, `src/routes`, use linters (ESLint).
- **Performance**: Use streams, clustering, caching (Redis).
- **Security**: Validate inputs, secure headers, HTTPS.
- **Testing**: Unit, integration, and API tests.
- **Deployment**: Docker, PM2, CI/CD pipelines.
- **Monitoring**: Prometheus, Grafana, structured logging.

**Explanation**:

- Best practices ensure scalable, secure, and maintainable apps.
- Linting and testing catch errors early.
- Monitoring and CI/CD improve reliability in production.