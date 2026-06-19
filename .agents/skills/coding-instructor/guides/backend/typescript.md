# TypeScript Backend Guide

## Phase 1 — Language Foundation Concept Priorities

| Lesson | Key Concepts to Cover | DSA Task Patterns |
|--------|----------------------|-------------------|
| Hello World | `console.log()`, running with `ts-node`/`bun`, types, `tsconfig.json` | — |
| Data Types | `string`, `number`, `boolean`, `null`, `undefined`, `any`, type annotations | Type coercion awareness, template literals |
| Collections | `Array<T>`, `Map<K,V>`, `Set<T>`, tuples, spread/rest operators | Frequency counting, grouping, deduplication |
| Control Flow | `if/else`, `for`, `for...of`, `while`, `switch`, ternary | Pattern generation, iteration |
| Functions | Function declarations/expressions, arrow functions, generics, optional params | Pure utility functions |
| Classes & OOP | `class`, constructor, methods, `extends`, `implements`, `interface`, access modifiers | Model entities with interfaces |
| DSA Fundamentals | `Array` as stack/queue, recursion, sorting with `Array.sort()`, searching | Implement linked list, binary search, basic sorting |

## Phase 2 — Backend Domain (12 Lessons)

| # | Lesson | Key Concepts | Language Nuances | Testing |
|---|--------|-------------|------------------|---------|
| 8 | Framework Setup & Hello Server | Express scaffold, `app.listen()`, route definitions, `ts-node-dev` for hot reload, logging | Use Express + TypeScript. `ts-node-dev` for dev. `tsconfig.json` for paths | `vitest` + `supertest`. Unit: app config. Integration: GET / returns |
| 9 | Environment Config | `dotenv`, `process.env`, config module, validation, graceful shutdown on missing PORT | `dotenv` at entry point. Typed config interface. Validate PORT presence | Test config parser with/without env. Integration: PORT env on/off |
| 10 | Health Check + Docker | `GET /health`, `res.json()`, status codes, Dockerfile (node:20-alpine), docker-compose, multi-stage build | Async handler pattern. `express.json()` middleware. Docker multi-stage for TS: build then run | Integration: supertest hits /health. Docker: image builds and runs |
| 11 | Error Handling & Safety | Express error middleware `(err, req, res, next)`, custom error classes, `try/catch` in async handlers, process-level `uncaughtException` | Wrap async routes with error catcher utility. Express error middleware at end of chain. `process.on('unhandledRejection')` | Unit: custom errors. Integration: 400/404/500. Crash test: malformed JSON, invalid types |
| 12 | Database (Single DB) | Connect to PostgreSQL via env variable. DB connection in a separate file. Server starts only when DB connects. | `drizzle-orm` with `pg` for SQL. Type-safe schema. Separate `db/` module with connection pool | Unit: mocked DB. Integration: test container (Postgres). Connection failure test |
| 13 | Dual DB & Repository Abstraction | Add MongoDB or alternative via env switch. Repository interface abstracts both. DI selects implementation. | `mongoose` for Mongo. Repository interface + two implementations. `drizzle` for SQL, `mongoose` for Mongo | Unit via interface mocks. Integration: test containers for both DBs. Env switching test |
| 14 | CRUD + 3-Layer | Controller (routes), Service (business logic), Repository (DB access). Directory structure. Request validation (`zod`) | `routes/`, `services/`, `repositories/` dirs. `zod` for validation. Service depends on repository interface | Unit per layer with mocks (vitest mock functions). Integration: supertest CRUD |
| 15 | Auth Middleware | Express middleware, JWT (`jsonwebtoken`), token generation, `Authorization` header parsing, 401/422 | Middleware function in `middleware/` dir. `express.Request` extension for user payload. Auth as composable middleware | Unit: token verify. Integration: token flow, missing/expired/invalid token |
| 16 | Redis Cache | `ioredis`, cache-aside pattern, TTL, connection management, env config, cache on read, invalidate on write | `ioredis` singleton. JSON serialize values. Cache middleware or service layer | Unit: mock ioredis. Integration: test container Redis. Hit/miss/invalidation |
| 17 | Async Task Queue | `amqplib` (RabbitMQ) or Bull/Queue (Redis-based), producer endpoint, consumer worker, task state, durable queues | Bull for Redis-based queue (simpler). `amqplib` for RabbitMQ. Worker as separate process or in-app consumer | Unit: mock queue. Integration: test container RabbitMQ/Bull. Enqueue/process/durability |
| 18 | gRPC Services | `@grpc/grpc-js`, proto files, gRPC server/client, 2 services, sync gRPC + async queue | Proto in `protos/` dir. `grpc-tools` TS code gen. Async gRPC with promises | Unit: stub tests. Integration: two services. Contract: proto validation |
| 19 | Gateway + Microservices | Express/Fastify gateway, 3 services (orchestrator, auth, user), gateway proxy/routing, inter-service HTTP/gRPC | Gateway as reverse proxy or route distributor. Each service independent Express app. Shared types library | Integration through gateway. Service-level tests. End-to-end flow |

## Recommended Frameworks

- **Express** (standard, widely used)
- **Bun** runtime + built-in HTTP server (faster, modern)

## Testing

Framework: `vitest` with `supertest` for API tests. Test containers via `testcontainers` package.