# JavaScript Backend Guide

## Phase 1 — Language Foundation Concept Priorities

| Lesson | Key Concepts to Cover | DSA Task Patterns |
|--------|----------------------|-------------------|
| Hello World | `console.log()`, running with Node, `let`/`const`/`var`, ES modules vs CommonJS | — |
| Data Types | `string`, `number`, `boolean`, `null`, `undefined`, `symbol`, `typeof`, `===` vs `==` | String methods, number coercion awareness |
| Collections | `Array`, `Object` as map, `Map`, `Set`, destructuring, spread/rest | Frequency counting, grouping, deduplication |
| Control Flow | `if/else`, `for`, `for...of`, `while`, `switch`, short-circuit | Iteration, pattern generation |
| Functions | Function declarations/expressions, arrow functions, closures, callbacks, default params | Utility functions, higher-order functions |
| Classes & OOP | `class`, constructor, methods, `extends`, `super`, `#private` fields, getters/setters | Model entities |
| DSA Fundamentals | `Array` as stack/queue, recursion, sorting (`Array.sort()`), searching | Implement linked list, binary search, basic sorting |

## Phase 2 — Backend Domain (12 Lessons)

| # | Lesson | Key Concepts | Language Nuances | Testing |
|---|--------|-------------|------------------|---------|
| 8 | Framework Setup & Hello Server | Express scaffold, `app.listen()`, `--watch` flag (Node 18+), route setup, console logging | ESM (`import` syntax) preferred. `node --watch` for dev reload | `vitest` + `supertest`. Unit: server config. Integration: GET |
| 9 | Environment Config | `dotenv` package, `process.env`, config object, `process.exit()` on missing PORT | `dotenv/config` at entry. Config module with validation | Test config with/without env. Crash on missing PORT |
| 10 | Health Check + Docker | `GET /health`, `res.json()`, Dockerfile (node:20-alpine), docker-compose | CommonJS vs ESM Docker considerations. Multi-stage (optional) | Integration: supertest /health. Docker build |
| 11 | Error Handling & Safety | Express error middleware, custom error classes, `try/catch` in async handlers, `process.on('uncaughtException')` | `express-async-errors` import (auto-wrap). Error middleware at end of chain | Unit: custom errors. Integration: 400/404/500. Crash test |
| 12 | Database (Single DB) | Connect to PostgreSQL via env variable. DB connection in a separate file. Server starts only when DB connects. | `pg` pool for SQL. Separate `db/` module. `.env` for DB URL | Unit: mocked DB. Integration: test container (Postgres). Connection fail |
| 13 | Dual DB & Repository Abstraction | Add MongoDB or alternative via env switch. Repository interface abstracts both. DI selects implementation. | `mongoose` for Mongo. Repository interface + two implementations | Unit via interface mocks. Integration: test containers for both. Env switching test |
| 14 | CRUD + 3-Layer | Controller (routes), Service (business logic), Repository (DB access). Directory structure. Validation | `routes/`, `services/`, `repositories/` dirs. `express-validator` or Joi for validation | Unit per layer (mocks). Integration: supertest CRUD |
| 15 | Auth Middleware | Express middleware, JWT (`jsonwebtoken`), token generation, `Authorization` header, 401/422 | Middleware in `middleware/` dir. Attach user to `req`. Express middleware order | Unit: token verify. Integration: token flow |
| 16 | Redis Cache | `ioredis`, cache-aside pattern, TTL, connection pool, env config, cache on read, invalidate on write | `ioredis` singleton. JSON serialize. Cache-aside on service layer | Unit: mock ioredis. Integration: test container Redis |
| 17 | Async Task Queue | `amqplib` (RabbitMQ) or Bull (Redis), producer endpoint, consumer worker, task state, durable queues | Bull for Redis-based (simpler). `amqplib` for RabbitMQ. Worker as separate process | Unit: mock queue. Integration: test container |
| 18 | gRPC Services | `@grpc/grpc-js`, proto files, gRPC server/client, 2 services, sync + async | Proto in `protos/`. Dynamic codegen with `@grpc/proto-loader` | Unit: stubs. Integration: two services. Contract |
| 19 | Gateway + Microservices | Express/Fastify gateway, 3 services, gateway routing, inter-service HTTP | Each service independent. Gateway proxies. Shared types | Through gateway. Service-level. End-to-end |

## Testing

Framework: `vitest` with `supertest` for API tests. Test containers via `testcontainers`.