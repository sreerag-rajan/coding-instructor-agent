# Vue Frontend Guide

## Phase 1 — Language Foundation Concept Priorities

| Lesson | Key Concepts to Cover | DSA Task Patterns |
|--------|----------------------|-------------------|
| Hello World | `console.log()`, ES module syntax, running with Vite | — |
| Data Types | `string`, `number`, `boolean`, `null`, `undefined`, `typeof`, `===` | String methods, number operations |
| Collections | `Array`, `Object`, `Map`, `Set`, destructuring, spread | Frequency counting, grouping |
| Control Flow | `if/else`, `for`, `for...of`, `while`, ternary, switch | Iteration, pattern generation |
| Functions | Arrow functions, callbacks, default params, rest/spread | Pure utility functions |
| Classes & OOP | `class`, constructor, methods, `extends`, getters/setters | Model entities |
| DSA Fundamentals | Recursion, sorting, searching, `Array` as stack/queue | Implement linked list, binary search |

## Phase 2 — Frontend Domain (13 Lessons)

| # | Lesson | Key Concepts | Framework Nuances | Testing |
|---|--------|-------------|-------------------|---------|
| 8 | Framework Setup & First Render | `npm create vue@latest`, Vite + Vue 3, `createApp()`, SFC (`.vue`), `<template>/<script>/<style>`, dev server | Composition API with `<script setup>` preferred. Default App.vue renders | `@vue/test-utils`: `mount(App)`. Check text. Framework-provided smoke test |
| 9 | First Page — Content Only | Clear template, render specific text, image placeholder (`<img>`), `<h1>`-`<h3>`, semantic HTML | Remove boilerplate. `<template>` with semantic `<main>`, `<section>`, `<header>` | Snapshot test. `find()` or `getByText()`. Check heading hierarchy |
| 10 | Layouts & Alignment | CSS Grid in SFC `<style scoped>`, `grid-template-columns: 1fr 1fr 1fr 1fr`. Header/body/footer sections | Scoped styles in SFC. CSS Grid. Flexbox for footer | `mount()` component, check DOM structure. CSS class assertions |
| 11 | Responsive Design | `@media` queries in Vue SFC, breakpoints (480/768/1024), `grid-template-columns: 1fr`, mobile-first | Scoped media queries. `useMediaQuery` composable or CSS-only. CSS-only preferred | Test with `window.resizeTo()`. Check column layout changes |
| 12 | Theming & Color Systems | CSS custom properties in `:root`, `[data-theme="dark"]`, `var()`, toggle button, 5+ design tokens | Set `data-theme` on `<html>` via `document.documentElement.dataset.theme`. Toggle in component | Test theme toggle effect. Snapshot per theme. Check CSS variable values |
| 13 | Complex UI Components | Table (`<table>`), accordion (`v-if`/`v-show` toggle), tabs (component state + `v-if`), card (`<div>` composable) | Vue `v-if`/`v-else` for tab content. `@click` for toggle. `<Transition>` for expand/collapse (optional) | `mount()` each. `trigger('click')`. Verify content visibility changes. Tab switching |
| 14 | Routing & Navigation | `vue-router`, `createRouter`, `<router-view>`, `<router-link>`, `useRoute()`, `useRouter()`, nested routes, 404 | `src/router/index.ts`. `router-link` for nav. `useRoute()` for params. `<router-view>` in `App.vue` | `mount()` with `global.plugins = [router]`. Test navigation. Test 404 route |
| 15 | Component Modularization | Extract `Card.vue`, `AccordionItem.vue`, `DataTable.vue`. `defineProps` for inputs. `components/` dir. Slots for composition | `<script setup>` with `defineProps<{...}>()`. Slots for flexible content. Default slot | Test with different props. Test slot content renders. Test `v-for` rendering |
| 16 | Dynamic Forms | Field definition array, `v-model` with computed setter, dynamic input type, validation, reset, `reactive()` form state | `reactive()` for form data. `computed` for validation. `v-for` over field defs. Dynamic `:type` binding | Fill form, submit, check emitted data. Validate errors. Reset |
| 17 | Mock API Integration | MSW (browser worker), `fetch`/`axios`, `onMounted()` async, loading/error/empty state, env-based `VITE_API_URL` | `msw` browser worker. Fetch in `onMounted` or composable. `ref()` for loading/error/data | MSW handler variations. Test all 4 states: loading, error, empty, success |
| 18 | Global State Management | Pinia, `defineStore()`, `state`, `getters`, `actions`, store composition, cross-page shared state | `defineStore('theme', ...)`. `storeToRefs()` for reactivity. Pinia instance in `main.ts` | Test store in isolation. Test components with `setActivePinia(createPinia())` |
| 19 | Advanced Components (Modals, Animations) | Teleport (`<Teleport to="body">`), modal state, Vue `<Transition>`, focus trap, ESC close, `aria-modal` | `<Teleport>` for overlay. `<Transition name="modal">` for animation. `watch` for ESC key | `<Transition>` mocked or actual. Test open/close state. Test focus trapping. Test ESC key |
| 20 | Capstone — Full App | Combines: routing, Pinia, MSW API, dynamic form, modal, responsive, theming, reusable components. 3+ pages | Page views in `views/`. Layout component. Feature folders. All states handled | Full integration test: navigate app, submit form, toggle theme, check responsive |

## ⚠️ Important

Phase 1 should be done in plain `.js`/`.ts` files. Introduce Vue SFC and `.vue` files only in Phase 2.

## Recommended Setup

- **Vite** + Vue 3 with `<script setup>` (Composition API preferred over Options API)
- **Vue Router** for routing
- **Pinia** for state management
- **MSW** for mock API

## Testing

Framework: `vitest` + `@vue/test-utils` + `msw`. Prefer Composition API patterns.