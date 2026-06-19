# Python Backend Guide

## Phase 1 — Language Foundation Concept Priorities

| Lesson | Key Concepts to Cover | DSA Task Patterns |
|--------|----------------------|-------------------|
| Hello World | `print()`, running `.py` files, variables, comments | — |
| Data Types | `int`, `float`, `str`, `bool`, `None`, `type()`, conversion | Convert types, format strings |
| Collections | `list`, `dict`, `tuple`, `set`, indexing, slicing, comprehensions | Frequency counting, grouping, lookups, deduplication |
| Control Flow | `if/elif/else`, `for`, `while`, `range()`, `enumerate()`, `zip()` | Pattern printing, nested loops, iteration patterns |
| Functions | `def`, parameters, return values, default args, `*args`/`**kwargs`, scope | Pure functions, data transformations |
| Classes & OOP | `class`, `__init__`, methods, inheritance, `super()`, dunder methods | Model entities (e.g., BankAccount, Library) |
| DSA Fundamentals | `list` as stack/queue, recursion, sorting (built-in), searching (linear/binary) | Implement linked list, binary search, basic sorting |

## Phase 2 — Backend Domain (12 Lessons)

| # | Lesson | Key Concepts | Language Nuances | Testing |
|---|--------|-------------|------------------|---------|
| 8 | Framework Setup & Hello Server | FastAPI/Flask scaffold, `uvicorn`, router, first route, `print` vs logger | Use FastAPI (async) or Flask. Decorator-based routing. `uvicorn.run()` | `httpx.AsyncClient` or `TestClient`. Unit: server starts. Integration: GET / returns |
| 9 | Environment Config | `python-dotenv`, `os.getenv`, `pydantic-settings`, config class, graceful exit on missing PORT | Prefer `pydantic-settings` for type-safe config. Validate PORT is int | Test config parser. Integration: with/without .env file |
| 10 | Health Check + Docker | `GET /health`, JSONResponse, status codes, Dockerfile (python:3.x-slim), docker-compose | Use Pydantic response model. `docker-compose.yml` with port mapping | Integration: `httpx` hits `/health` and validates JSON. Docker build test |
| 11 | Error Handling & Safety | `try/except` in handlers, custom exception classes, `HTTPException`, app lifecycle (lifespan), crash resilience | FastAPI exception handlers. `@app.exception_handler`. Flask `@app.errorhandler` | Unit: custom exceptions. Integration: 400/404/500 responses. Crash test: send garbage input, verify app stays up |
| 12 | Database (Single DB) | Connect to PostgreSQL or SQLite via env variable. DB connection in a separate file. Server starts only when DB connects. | SQLAlchemy async (`asyncpg`) for PG or `aiosqlite` for SQLite. `pydantic-settings` for DB URL. Alembic for migrations | Unit: mocked connection. Integration: test container (Postgres or SQLite). Connection failure test |
| 13 | Dual DB & Repository Abstraction | Add MongoDB or alternative via env switch. Repository pattern abstracts both. DI selects implementation. | `motor` for Mongo. Abstract repository class. FastAPI `Depends` or factory for DI. Env variable selects impl | Unit via abstract base class mocks. Integration: test containers for both DBs. Env switching test |
| 14 | CRUD + 3-Layer | Controller (router), Service (business logic), Repository (DB). FastAPI `Depends` for DI. Request/response models | `router/`, `service/`, `repository/` directories. Pydantic for validation. Dependency injection via `Depends()` | Unit per layer with mocks. Integration: full CRUD via httpx. Test all 4 operations |
| 15 | Auth Middleware | `@app.middleware` or `@router.dependencies`, JWT (PyJWT), token generation/validation, `Authorization` header, 401/422 | FastAPI `Depends` for auth. `python-jose` or `PyJWT`. Middleware vs dependency per-route | Unit: token encode/decode. Integration: flow with and without token. Expired token test |
| 16 | Redis Cache | `redis-py` async, cache-aside pattern, TTL, connection pool, env-based config, cache on read, invalidate on write | `aioredis` or `redis.asyncio`. Connection pool as dependency. Serialize with JSON | Unit: mock Redis. Integration: test container Redis. Cache hit/miss/invalidation tests |
| 17 | Async Task Queue | `aio-pika` (RabbitMQ) or `redis` as queue, producer endpoint, background consumer, task status tracking, durable queues | Prefer `aio-pika` for RabbitMQ. `fastapi.BackgroundTasks` is too simple — need real queue. Consumer as separate process or `asyncio.create_task` | Unit: mock queue. Integration: test container RabbitMQ. Enqueue/dequeue/durability tests |
| 18 | gRPC Services | `grpcio`, proto files, gRPC server/client, 2 services, sync gRPC + async queue, proto versioning | `grpcio-tools` for code gen. Async gRPC with `grpcio.aio`. Proto in `protos/` dir | Unit: stub tests. Integration: two services communicate. Contract: proto validation |
| 19 | Gateway + Microservices | API Gateway (FastAPI), 3 services (orchestrator, auth, user), gateway routes, service orchestration, circuit breaker awareness | Gateway as entry point. Services as separate FastAPI apps. `httpx.AsyncClient` for inter-service. Shared proto lib | Integration through gateway. Service-level tests. Full flow end-to-end |

## Recommended Frameworks

Start framework-less for HTTP basics. Then:
- **FastAPI** (preferred) — async, modern, auto-docs
- **Flask** — simpler, more explicit

## Testing

Framework: `pytest` with `pytest-cov` and `httpx` for API tests. Test containers via `testcontainers-python`.