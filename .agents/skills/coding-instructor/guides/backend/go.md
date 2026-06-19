# Go Backend Guide

## Phase 1 — Language Foundation Concept Priorities

| Lesson | Key Concepts to Cover | DSA Task Patterns |
|--------|----------------------|-------------------|
| Hello World | `package main`, `func main()`, `fmt.Println`, `go run`, `go build` | — |
| Data Types | `int`, `float64`, `string`, `bool`, `var`, `:=` short declaration, zero values | String formatting, type conversion |
| Collections | `[]T` (slice), `map[K]V`, `make()`, `append()`, slice operations | Frequency counting, grouping, deduplication |
| Control Flow | `if`, `for` (Go has no while), `switch`, `range`, `break`/`continue` | Slice iteration, pattern generation |
| Functions | `func`, parameters, return values (multiple), named returns, variadic, first-class functions | Utility functions |
| Classes & OOP | **No classes** — structs, methods (receiver functions), interfaces, embedding | Model entities with structs |
| DSA Fundamentals | Slice as stack/queue, recursion, `sort` package, searching | Implement linked list (with structs), binary search |

## Phase 2 — Backend Domain (12 Lessons)

| # | Lesson | Key Concepts | Language Nuances | Testing |
|---|--------|-------------|------------------|---------|
| 8 | Framework Setup & Hello Server | `net/http`, `http.ListenAndServe`, `http.HandlerFunc`, `log.Printf`, `go run` | Use stdlib `net/http` first. `chi` router introduced later. Handler function signature | `net/http/httptest` for test server. Unit: handler returns. Integration: test server |
| 9 | Environment Config | `os.Getenv`, `os.LookupEnv`, `fmt.Sprintf` for error messages, config struct | Go has no built-in .env reader. Use `os.Getenv` directly. Validate at startup | Test config with env set/unset. `t.Setenv` for test env vars |
| 10 | Health Check + Docker | `GET /health`, `w.WriteHeader(http.StatusOK)`, `encoding/json`, Dockerfile (golang:1.22-alpine), multi-stage build | `json.NewEncoder(w).Encode()`. Docker multi-stage: build in golang, run in scratch/alpine | `httptest` for handler. Docker: build and run test |
| 11 | Error Handling & Safety | Go error handling (`if err != nil`), custom error types, `http.Error`, `defer` for cleanup, `recover()` for panic safety | Go has no try/catch — errors as values. `recover()` in middleware or `defer` in main. `log.Fatal` vs `log.Printf` | Unit: error types. Integration: 400/404/500. Crash test: trigger panic, verify recovery |
| 12 | Database (Single DB) | Connect to PostgreSQL via env variable. DB connection in a separate file. Server starts only when DB connects. | `database/sql` + `pgx/v5`. Separate `db/` package. `sql.Open`/`Connect` with connection pool | Unit: mock interfaces. Integration: test container (Postgres). Connection failure |
| 13 | Dual DB & Repository Abstraction | Add MongoDB or alternative via env switch. Repository interface abstracts both. DI selects implementation. | `mongo-driver` for Mongo. Interface with two struct implementations. Constructor-based DI | Unit via interface mocks. Integration: test containers for both. Env switching test |
| 14 | CRUD + 3-Layer | `handlers/`, `service/`, `repository/` packages. Interface-based DI. Struct constructors. Clean architecture | Go interfaces as contracts. Repository interface → multiple implementations. Handler struct with service field | Unit per layer with mock implementations. Integration: httptest CRUD |
| 15 | Auth Middleware | Middleware pattern (`func(http.Handler) http.Handler`), JWT (`golang-jwt/jwt`), `context.WithValue`, 401/422 | Go middleware wraps handler. `context` package for request-scoped data. `chi` router has `With` and middleware | Unit: middleware returns 401. Integration: token flow, invalid token |
| 16 | Redis Cache | `go-redis`/`rueidis`, cache-aside pattern, TTL, connection pool, env config, struct serialization (JSON) | `go-redis/v9` recommended. Marshal struct to JSON. Redis as injectable interface | Unit: mock redis. Integration: test container Redis. Hit/miss/invalidation |
| 17 | Async Task Queue | `amqp091-go` (RabbitMQ) or `asynq` (Redis-based), producer handler, consumer goroutine, task lifecycle | Go goroutines as natural workers. `asynq` for Redis queue with task scheduling. Signal handling (`os.Signal`) for graceful shutdown | Unit: mock queue. Integration: test container. Enqueue/process/durability |
| 18 | gRPC Services | `google.golang.org/grpc`, proto files with `protoc`, gRPC server/client, 2 services, sync + async queue | `protoc` codegen. Go gRPC with streams. Interceptors for logging/auth. Proto in `proto/` dir | Unit: stub/interface tests. Integration: two gRPC services. Contract: proto compile |
| 19 | Gateway + Microservices | `chi`/`net/http` gateway, 3 services (orchestrator, auth, user), gateway routing, `http.ReverseProxy` or gRPC gateway | Go's `ReverseProxy` for HTTP. gRPC gateway plugin. Each service as `cmd/service-name/main.go` | Integration through gateway. Each service testable independently. End-to-end flow |

## Recommended Frameworks

- **Standard library** + `chi` or `gorilla/mux` (lightweight)
- **gRPC** with `protobuf` and `connect-go`

## Testing

Framework: `go test` (stdlib) with table-driven test patterns. Test containers via `testcontainers-go`.