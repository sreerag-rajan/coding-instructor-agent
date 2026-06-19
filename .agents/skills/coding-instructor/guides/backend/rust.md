# Rust Backend Guide

## Phase 1 — Language Foundation Concept Priorities

| Lesson | Key Concepts to Cover | DSA Task Patterns |
|--------|----------------------|-------------------|
| Hello World | `fn main()`, `println!`, `cargo new`, `cargo run`, `cargo build` | — |
| Data Types | `i32`, `u64`, `f64`, `bool`, `char`, `&str`, `String`, type inference | String manipulation, type conversion |
| Collections | `Vec<T>`, `HashMap<K,V>`, `HashSet<T>`, `vec![]`, iteration | Frequency counting, grouping, deduplication |
| Control Flow | `if/else`, `loop`, `while`, `for`, `match` (key!), `if let` | Pattern matching exercises |
| Functions | `fn`, parameters, return types, expressions vs statements, ownership basics | Pure functions |
| Classes & OOP | **Ownership + Borrowing** (teach first!) — structs, `impl`, methods, traits, enums | Model entities, implement a trait |
| DSA Fundamentals | Recursion, slices, sorting (`Vec::sort`), searching, lifetime basics | Implement linked list (with `Box`), binary search |

## ⚠️ Critical — Ownership, Borrowing, Lifetimes

Rust's unique concepts require special attention:
- Lesson order matters: Ownership must come before references, references before lifetimes
- The DSA lesson should include practical work with ownership boundaries (e.g., implementing a function that takes ownership vs borrows)
- For structs + methods: emphasize `self`, `&self`, `&mut self` distinction

## Phase 2 — Backend Domain (12 Lessons)

| # | Lesson | Key Concepts | Language Nuances | Testing |
|---|--------|-------------|------------------|---------|
| 8 | Framework Setup & Hello Server | `cargo init` (or `cargo new` for Axum), Axum `Router`, `tokio::main`, `TcpListener`, `axum::serve`, logging | Axum uses `tokio` runtime. `#[tokio::main]` on main. `TcpListener::bind()` + `axum::serve()` | `axum::test` helpers. Unit: router mounts. Integration: `reqwest` to running server |
| 9 | Environment Config | `dotenvy` or `dotenv` crate, `std::env::var`, config struct with `serde`, `Result` for validation, graceful error | `dotenvy` loads .env. `env::var("PORT")` returns `Result`. `expect()` or match on missing | Test config: with/without env. Error path for missing vars |
| 10 | Health Check + Docker | `GET /health`, `Json<Value>`, `StatusCode`, Dockerfile (rust:1.78-slim, multi-stage), docker-compose | Axum: handler returns `Json(serde_json::json!({...}))`. Docker: build from rust, final in debian-slim | Integration: `reqwest` to /health. Docker: `cargo build --release` then run |
| 11 | Error Handling & Safety | `Result<T, E>` in handlers, `anyhow`/`thiserror`, `IntoResponse` for errors, `panic` catching, `tower_http` catch-panic middleware | `thiserror` for error types, `anyhow` for application-level. `impl IntoResponse` for custom errors. Axum error responses | Unit: `thiserror` variants. Integration: send garbage, verify app stays up |
| 12 | Database (Single DB) | Connect to PostgreSQL or SQLite via env variable. DB connection in a separate file. Server starts only when DB connects. | `sqlx` (async PostgreSQL or SQLite), `sqlx::PgPool`/`SqlitePool`, `dotenvy`, separate `db/` module | Unit: mock pool. Integration: test container. Connection failure test |
| 13 | Dual DB & Repository Abstraction | Add MongoDB or alternative via env switch. Repository trait abstracts both. DI selects implementation. | `mongodb` crate, `#[async_trait]` for repository trait, `Arc<dyn Repository>` for DI. Two implementations | Unit via trait contract mocks. Integration: test containers for both. Env switching test |
| 14 | CRUD + 3-Layer | Axum Router + handler (controller), Service struct, Repository trait. `Arc<AppState>` for DI. Extractors | `Arc<AppState>` holds service/repository. Handler extracts state via `State<Arc<AppState>>`. Repository as trait | Unit per layer with mock traits. Integration: `reqwest` CRUD |
| 15 | Auth Middleware | Axum middleware (`Middleware` from `tower`), JWT (`jsonwebtoken` crate), `Authorization` header extractor, 401/422 | Axum middleware via `tower::ServiceBuilder`. Custom extractor for JWT claims. `axum::http::HeaderMap` | Unit: middleware layer. Integration: token generation, valid/invalid/expired token |
| 16 | Redis Cache | `redis-rs` async, cache-aside pattern, TTL, connection manager, env config, serialize data | `redis::aio::ConnectionManager`. `serde_json` for value serialization. `Arc<ConnectionManager>` in app state | Unit: mock `ConnectionManager`. Integration: test container Redis. Cache hit/miss/invalidation |
| 17 | Async Task Queue | `lapin` (RabbitMQ, async) or `celery-rs`/`bull`, producer endpoint, background task (tokio::spawn), queue durability | `lapin` for RabbitMQ (async). `tokio::spawn` for consumer. Channel management. Graceful shutdown with `tokio::signal` | Unit: mock channel. Integration: test container RabbitMQ. Enqueue/process/durability |
| 18 | gRPC Services | `tonic` crate, proto files, gRPC server/client, 2 services, sync gRPC + async queue, `prost`/`tonic-build` | `tonic` as gRPC framework. `prost` for proto codegen via `build.rs`. Proto in `proto/` dir | Unit: tonic mock. Integration: two services. Contract: proto compile step |
| 19 | Gateway + Microservices | Axum or `reqwest` gateway, 3 services (orchestrator, auth, user), `reqwest` for inter-service HTTP, tonic for gRPC | Gateway as Axum app that proxies. Each service as separate crate in workspace (`services/auth`, `services/user`, `services/orchestrator`) | Integration through gateway. Each service testable. End-to-end with `docker-compose` |

## Recommended Frameworks

- **Axum** (preferred — modern, async, Tower ecosystem)
- **Actix-web** (battle-tested, actor-based)

## Testing

Framework: `cargo test` (stdlib) with `axum::test` helpers or `reqwest` for integration tests. Test containers via `testcontainers` crate.