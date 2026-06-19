# Java Backend Guide

## Phase 1 — Language Foundation Concept Priorities

| Lesson | Key Concepts to Cover | DSA Task Patterns |
|--------|----------------------|-------------------|
| Hello World | `public class`, `public static void main`, project setup (Maven/Gradle), `System.out.println` | — |
| Data Types | `int`, `long`, `double`, `boolean`, `char`, `String`, wrapper classes (Integer, etc.), autoboxing | String manipulation, `StringBuilder` |
| Collections | `ArrayList<T>`, `HashMap<K,V>`, `HashSet<T>`, generics, `Collections` utility | Frequency counting, grouping, deduplication |
| Control Flow | `if/else`, `for`, `for-each`, `while`, `switch`, `break`/`continue` | Iteration patterns |
| Functions | **Methods** — access modifiers, `static`, return types, parameters, varargs, method overloading | Utility methods |
| Classes & OOP | `class`, constructors, `this`, `extends`, `super`, `interface`, `abstract`, `final`, `static`, encapsulation (getters/setters) | Model entities |
| DSA Fundamentals | `ArrayList` as stack/queue, recursion, `Arrays.sort`, `Collections.sort`, binary search (`Collections.binarySearch`) | Implement linked list (custom class), binary search |

## ⚠️ Java Project Setup

For Phase 1 basics, use simple single-file approach with `javac`/`java`. Introduce Maven/Gradle at start of Phase 2.

## Phase 2 — Backend Domain (12 Lessons)

| # | Lesson | Key Concepts | Language Nuances | Testing |
|---|--------|-------------|------------------|---------|
| 8 | Framework Setup & Hello Server | Spring Initializr (`start.spring.io`), Maven/Gradle, `@SpringBootApplication`, `SpringApplication.run()`, embedded Tomcat, `application.properties`, log output | Maven `pom.xml` with spring-boot-starter-web. `mvn spring-boot:run`. Main class annotation | `@SpringBootTest` with `WebEnvironment.RANDOM_PORT`. `TestRestTemplate` for integration |
| 9 | Environment Config | `application.yml`, `application.properties`, `@Value`, `Environment` interface, `@ConfigurationProperties`, `@ConditionalOnProperty`, graceful startup failure | `@ConfigurationProperties(prefix="app")` for grouped config. Profile-based config (`application-dev.yml`). `System.getenv()` | Test with `@TestPropertySource`. Integration: start with/without PORT env |
| 10 | Health Check + Docker | `@RestController`, `GET /health`, `ResponseEntity`, `@GetMapping`, Dockerfile (maven build + eclipse-temurin JRE), docker-compose | `@RestController` returns object (auto-serialized to JSON). Docker multi-stage: Maven build → JRE runtime | `MockMvc` for controller. Docker: image builds and container starts |
| 11 | Error Handling & Safety | `@ControllerAdvice`, `@ExceptionHandler`, custom exception classes, `ResponseEntity` for error responses, `@Valid` and validation | `@ControllerAdvice` global handler. `ResponseEntityExceptionHandler` extension. `MethodArgumentNotValidException` handling | Unit: exception classes. Integration: 400 (invalid input), 404 (not found), 500 (internal). Crash test |
| 12 | Database (Single DB) | Connect to PostgreSQL via env variable. DB connection in a separate `config/` file. Server starts only when DB connects. | H2 for dev, PostgreSQL for prod. `spring-boot-starter-data-jpa`, `DataSource` bean, profile-based config | `@DataJpaTest` with test container. Connection failure test |
| 13 | Dual DB & Repository Abstraction | Add MongoDB or alternative via env switch. Repository interface abstracts both. Profile-based DI selects implementation. | `spring-boot-starter-data-mongodb`. `@Profile("sql")`/`@Profile("mongo")`. Interface with two `@Repository` impls | `@DataJpaTest` and `@DataMongoTest`. Profile switching integration test |
| 14 | CRUD + 3-Layer | `@RestController` (controller), `@Service` (service), `@Repository` (repository). `@Autowired` constructor injection. DTO pattern, `@Valid` request bodies | `controller/`, `service/`, `repository/` packages. DTO classes for request/response. `@Entity` for DB models. `ModelMapper` or manual mapping | Unit per layer (`@WebMvcTest`, `@DataJpaTest`, mock service). Integration: `@SpringBootTest` CRUD |
| 15 | Auth Middleware | Spring Security (`spring-boot-starter-security`), `SecurityFilterChain` bean, JWT (`jjwt`), `UsernamePasswordAuthenticationToken`, `SecurityContextHolder`, `@PreAuthorize`, 401/403/422 | `SecurityConfig` class with `@EnableWebSecurity`. `OncePerRequestFilter` for JWT. `AuthenticationManager` for token gen | `@WebMvcTest` with `@MockBean` for security. Integration: token flow, invalid token |
| 16 | Redis Cache | `spring-boot-starter-data-redis`, `@Cacheable`, `@CacheEvict`, `@EnableCaching`, `RedisTemplate`/`StringRedisTemplate`, TTL, connection config | `@EnableCaching` on config. `@Cacheable(cacheNames="items")`. `application.properties` for Redis host/port | `@SpringBootTest` with embedded Redis or test container. Cache hit/miss/invalidation |
| 17 | Async Task Queue | RabbitMQ (`spring-boot-starter-amqp`), `RabbitTemplate`, `@RabbitListener`, `Queue`, `Exchange`, `Binding`, `@EnableRabbit` | `RabbitConfig` class declares queues/exchanges. `@Async` for background processing. `MessagePostProcessor` for persistence | `@SpringBootTest` with test container RabbitMQ. Enqueue/dequeue/durability |
| 18 | gRPC Services | Spring gRPC (`net.devh:grpc-server-spring-boot-starter`), proto files, `@GrpcService`, gRPC client stub, 2 services, sync + async | `protobuf-maven-plugin` for codegen. `@GrpcService` for server. `@GrpcClient` for client injection | Unit: stub tests. Integration: two gRPC services. Contract: proto validation |
| 19 | Gateway + Microservices | Spring Cloud Gateway (`spring-cloud-starter-gateway`), 3 services (orchestrator, auth, user), `@LoadBalanced`, `WebClient`, route definitions | `application.yml` with `spring.cloud.gateway.routes`. Eureka discovery or static URLs. Each service as independent Spring Boot app | Integration through gateway. Each service `@SpringBootTest`. End-to-end with docker-compose |

## Recommended Frameworks

- **Spring Boot** (standard for Java backend)
- Use `start.spring.io` for project initialization (Maven or Gradle)

## Testing

Framework: JUnit 5 + Mockito for unit tests, `MockMvc` for controller tests, `@SpringBootTest` for integration. Test containers via `testcontainers-java`.