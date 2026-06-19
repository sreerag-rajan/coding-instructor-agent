# Coding Instructor — Agent-Guided Coding Tutor

This repository is a **strict, agent-guided coding tutor** for learning web development — backend or frontend. You write every line of code. The agent guides, explains, reviews, and tests — but **never writes code**.

## How It Works

1. **Set up**: Run `/setup` and choose **backend** (Python, TS, JS, Go, Rust, Java) or **frontend** (React+TS, Vue, Flutter)
2. **Learn**: Each lesson has a `concepts.md` (theory) and `task.md` (hands-on build)
3. **Code**: You write the solution yourself. The agent explains and guides — never codes
4. **Review**: Submit with `/review @<file>` — the agent runs automated tests (unit + integration), executes a mandatory 30-point code review checklist, and provides detailed feedback
5. **Progress**: Pass all tests + code review to unlock the next lesson

## Slash Commands

| Command | What It Does |
|---------|-------------|
| `/setup` | Initialize path, language/framework, scaffold curriculum, verify toolchain |
| `/lesson` | Show current lesson details and status |
| `/review @<file>` | Submit work for automated testing + mandatory code review |
| `/hint` | Get a gentle nudge (4-level escalation, never full code) |
| `/progress` | Show overall completion and lesson status |
| `/status` | Show current config, active lesson, and blockers |
| `/doctor` | Verify toolchain — runtime, compiler, Docker daemon (backend) |
| `/help` | List all commands |

## The Cardinal Rule

**The agent never writes code.** Not a single line. Not even fixes. The agent explains, guides, and reviews — the user writes everything. This is how you learn.

## Philosophy

AI generates code effortlessly today, but when it breaks or needs understanding, only human skill matters. This curriculum is designed to make you **capable enough to self-develop, self-debug, and self-improve** in your chosen stack. Every concept is applied through code you write yourself.

## Supported Paths

### Backend
| Language | Frameworks |
|----------|-----------|
| Python | FastAPI / Flask |
| TypeScript | Express / Bun |
| JavaScript | Express |
| Go | net/http + chi |
| Rust | Axum / Actix-web |
| Java | Spring Boot |

### Frontend
| Framework | Tooling |
|-----------|---------|
| React + TypeScript | Vite + React Router + Zustand + MSW |
| Vue | Vue 3 + Pinia + Vue Router + MSW |
| Flutter (Dart) | Provider/Riverpod + go_router |

## Curriculum Arc

### Phase 1 — Language Foundation (7 lessons)
Hello World → Data Types → Collections → Control Flow → Functions → Classes & OOP → DSA Fundamentals

### Phase 2 — Backend Domain (12 lessons)

| # | Lesson | Core Concepts |
|---|--------|---------------|
| 8 | Framework Setup & Hello Server | Scaffold, start server, log port |
| 9 | Environment Config | .env, PORT variable, graceful failure |
| 10 | Health Check + Docker | GET /health, JSON, Dockerfile |
| 11 | Error Handling & Safety | 400/404/500, app must not crash |
| 12 | Database (Single DB) | PostgreSQL/SQLite via env, separate db module |
| 13 | Dual DB & Repository Abstraction | MongoDB via env switch, interface-based abstraction |
| 14 | CRUD + 3-Layer Architecture | Controller → Service → Repository, full CRUD |
| 15 | Auth Middleware | JWT, Authorization header, 401/422 |
| 16 | Redis Cache | Cache-aside, TTL, read/write caching |
| 17 | Async Task Queue | RabbitMQ/Redis, producer/consumer |
| 18 | gRPC Services | 2 services, sync gRPC + async queue |
| 19 | Gateway + Microservices | Gateway + 3 services (orchestrator, auth, user) |

### Phase 2 — Frontend Domain (13 lessons)

| # | Lesson | Core Concepts |
|---|--------|---------------|
| 8 | Framework Setup & First Render | Scaffold, dev server, default page |
| 9 | First Page (Content Only) | Text, images, headings, semantic HTML |
| 10 | Layouts & Alignment | CSS Grid, header/body/footer layout |
| 11 | Responsive Design | Breakpoints, mobile-first, adaptive columns |
| 12 | Theming & Color Systems | Light/dark mode, CSS custom properties |
| 13 | Complex UI Components | Table, accordion, tabs, cards |
| 14 | Routing & Navigation | Client-side router, 2 pages, 404 |
| 15 | Component Modularization | Reusable components with props |
| 16 | Dynamic Forms | Field definition arrays, validation, submit |
| 17 | Mock API Integration | MSW, loading/error/empty/success states |
| 18 | Global State Management | Store, cross-page state, theme in store |
| 19 | Advanced Components | Modal, animations, focus trap, a11y |
| 20 | Capstone — Multi-Page App | All concepts combined, 3+ pages |

## Testing Strategy

The agent generates tests per lesson using a tiered approach:

| Phase | Test Types | Coverage |
|-------|-----------|----------|
| Phase 1 | Unit tests only | Positive + negative + edge cases |
| Phase 2 (lessons 1-4) | Unit + integration + crash tests | App must never crash |
| Phase 2 (lessons 5+) | Unit + integration + test containers | Real DB, Redis, RabbitMQ |
| Phase 2 (lessons 18-19) | Unit + integration + contract tests | gRPC, multi-service flows |

Every review includes 30 mandatory code review checks across: **Correctness, Readability, Idiomatic Patterns, Error Handling, Structure & Architecture, and Testing**.

## Getting Started

```bash
# Clone the repo
git clone <this-repo>
cd coding-instructor

# Open with any agent (Zed, Claude Code, OpenCode, Cursor, etc.)
# Run /setup and follow the prompts
```
