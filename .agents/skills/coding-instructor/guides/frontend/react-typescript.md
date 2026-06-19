# React + TypeScript Frontend Guide

## Phase 1 — Language Foundation Concept Priorities

| Lesson | Key Concepts to Cover | DSA Task Patterns |
|--------|----------------------|-------------------|
| Hello World | `console.log()`, `.tsx` files, `tsconfig.json`, running with Vite | — |
| Data Types | `string`, `number`, `boolean`, `null`, `undefined`, type annotations, interfaces | Template literals, string methods |
| Collections | `Array<T>`, `Map<K,V>`, `Set<T>`, tuple types, spread/rest | Frequency counting, grouping |
| Control Flow | `if/else`, `for`, `for...of`, `while`, ternary, && short-circuit | Iteration, pattern generation |
| Functions | Arrow functions, generics, optional/rest params, callbacks | Pure utility functions |
| Classes & OOP | `class`, constructor, methods, `extends`, `implements`, access modifiers | Model entities |
| DSA Fundamentals | Recursion, sorting, searching, `Array` as stack/queue | Implement linked list, binary search |

## Phase 2 — Frontend Domain (13 Lessons)

| # | Lesson | Key Concepts | Framework Nuances | Testing |
|---|--------|-------------|-------------------|---------|
| 8 | Framework Setup & First Render | Vite scaffold, `npm create vite@latest`, `App.tsx`, `main.tsx`, `createRoot()`, dev server | `npm create vite@latest my-app -- --template react-ts`. Default component renders | `@testing-library/react`: `render(<App />)`. Check text appears. Framework-provided smoke test |
| 9 | First Page — Content Only | Clear template, render specific text, image placeholder (`<img>` with placeholder), `<h1>`-`<h3>` headings, semantic HTML | Remove boilerplate. Use `<main>` wrapper. Placeholder image from `picsum.photos` or div | Snapshot test. `getByText()` for content. Check heading hierarchy |
| 10 | Layouts & Alignment | CSS Grid: `grid-template-columns`, `grid-area`, `gap`. Header, 4-column body, 3-section footer. Flexbox for nesting | CSS module per component. Or inline style object for simplicity early. CSS Grid in `App.css` | Render layout, check DOM structure. Test grid columns via computed styles (vitest + jsdom) |
| 11 | Responsive Design | Media queries (`@media`), breakpoints (480/768/1024), `grid-template-columns: 1fr`, mobile-first, responsive images | `useMediaQuery` hook or CSS-only. Prefer CSS-only (`@media`) for separation of concerns | Test with different viewport sizes via `window.resizeTo()` or jsdom mock. Check column counts |
| 12 | Theming & Color Systems | CSS custom properties (`--color-primary`), light/dark mode via `[data-theme]`, `var()` function, theme toggle button | `:root` vars + `[data-theme="dark"]` overrides. Button toggles `data-theme` on `<html>`. At least 5 tokens defined | `fireEvent.click` on toggle. Check CSS custom property values change. Snapshot per theme |
| 13 | Complex UI Components | `<table>` semantic structure, `<details>/<summary>` for accordion, tab pattern (button + conditional render), `<div class="card">` pattern | Accordion: state-driven expand. Tabs: active tab state + conditional content. Card: composed div pattern | Each component renders with test data. Tabs: click tab, verify content changes. Accordion: toggle |
| 14 | Routing & Navigation | `react-router-dom`, `BrowserRouter`, `Routes`, `Route`, `Link`, `useNavigate`, `useParams`, 404 route | Wrap app in `<BrowserRouter>`. `<Routes>` with `<Route path="/" element={<Home />}>`. `<Link>` for nav | `MemoryRouter` with initial entries. Test both routes render. Test navigation. Test unknown route → 404 |
| 15 | Component Modularization | Extract `Card`, `Accordion`, `DataTable` as reusable components. `interface Props` per component. `children` prop. Directory: `components/` | Props interface for config. `React.PropsWithChildren` or `{children: React.ReactNode}`. `.tsx` extension | Test each component with different props. Test composition. Test default props |
| 16 | Dynamic Forms | Field definition array: `{name, type, label, required?, options?}`. Controlled inputs. Validation on submit. Form state management | `useState` for form data + validation errors. `onChange` handler per field type. Submit handler emits form data | Render form from field defs. Fill and submit. Check emitted data. Test validation errors |
| 17 | Mock API Integration | MSW (Mock Service Worker), handlers definition, fetch/axios, `useEffect` fetch, loading/error/empty/success states | `msw` browser worker. Handlers in `mocks/handlers.ts`. `VITE_API_URL` env var | Test all 4 states via MSW handler variations. Loading → spinner. Error → error message. Empty → empty state. Success → data renders |
| 18 | Global State Management | Zustand store (or Context API), store definition, actions, selectors, Provider-free (Zustand), cross-page shared state | Zustand: `create<Store>()` with `set()`. Import `useStore` in any component. Theme state in store | Test store in isolation. Test components with store. Verify state persists across pages |
| 19 | Advanced Components (Modals, Animations) | Portal (`createPortal`), overlay/dialog, open/close state, focus trap, `aria-modal`, `aria-hidden`, `role="dialog"`, ESC to close, CSS transitions | `createPortal(modal, document.body)`. `useEffect` for focus trap. `useEffect` for ESC listener. CSS `transition` or `framer-motion` | Test open/close. Test focus trap (tab cycles inside). Test ESC closes. Test backdrop click closes |
| 20 | Capstone — Full App | Combines: routing, global state, MSW API, dynamic form, modal, responsive, theming, reusable components. 3+ pages | Separate page components, shared layout. Feature modules. All states handled | Full integration test: navigate through app, submit form, toggle theme, check responsive breakpoints |

## ⚠️ Important

Phase 1 (language foundation) should be done in plain `.ts` files. Only introduce `.tsx` and React at Phase 2. This separates learning TypeScript fundamentals from learning React.

## Recommended Setup

- **Vite** for project scaffolding
- **React Router** for routing
- **Zustand** (lightweight) or Context API (no deps) for state management
- **MSW** for mock API

## Testing

Framework: `vitest` + `@testing-library/react` + `@testing-library/user-event` + `@testing-library/jest-dom` + `msw`.