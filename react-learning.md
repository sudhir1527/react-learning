# ⚛️ React.js Tough Interview — Master Roadmap

> A comprehensive, senior-level React interview checklist covering JavaScript foundations, React internals, hooks, state management, performance, rendering, TypeScript, security, deployment, architecture, and staff/principal-level system design.

![Sections](https://img.shields.io/badge/sections-23-4f46e5?style=for-the-badge) ![Topics](https://img.shields.io/badge/topics-308-0891b2?style=for-the-badge) ![Level](https://img.shields.io/badge/level-Advanced%20to%20Principal-7c3aed?style=for-the-badge)

## How to use this roadmap

- [ ] Read each topic and explain it in your own words.
- [ ] Implement or demonstrate the concept where practical.
- [ ] Prepare trade-offs, failure modes, and real-world examples for senior-level topics.
- [ ] Revisit unchecked topics before mock interviews.
- [ ] Track your progress by checking items off directly in this Markdown file.

> **Interview tip:** For advanced questions, structure answers around the problem, options considered, trade-offs, failure modes, observability, and measurable outcomes.

## Table of contents

01. [JavaScript & Browser Foundations (Prerequisite Layer)](#javascript--browser-foundations-prerequisite-layer)
02. [React Core Fundamentals](#react-core-fundamentals)
03. [Fiber Architecture, Reconciliation & Rendering Internals](#fiber-architecture-reconciliation--rendering-internals)
04. [Hooks — Full Depth](#hooks--full-depth)
05. [Component Design Patterns & Composition](#component-design-patterns--composition)
06. [State Management](#state-management)
07. [Data Fetching & Server State](#data-fetching--server-state)
08. [Performance Optimization](#performance-optimization)
09. [Streaming Data, Real-Time & Large File Handling (Advanced)](#streaming-data-real-time--large-file-handling-advanced)
10. [Rendering Strategies: CSR / SSR / SSG / ISR / RSC](#rendering-strategies-csr--ssr--ssg--isr--rsc)
11. [Routing](#routing)
12. [Forms](#forms)
13. [Testing](#testing)
14. [TypeScript (General + React-Specific)](#typescript-general--react-specific)
15. [Security](#security)
16. [Build Tools, Bundling & Compilation](#build-tools-bundling--compilation)
17. [Environment Configuration](#environment-configuration)
18. [Deployment & Hosting Infrastructure](#deployment--hosting-infrastructure)
19. [Monorepo Architecture](#monorepo-architecture)
20. [Micro-Frontend Architecture](#micro-frontend-architecture)
21. [Accessibility (a11y)](#accessibility-a11y)
22. [Architecture, System Design & Org-Level Concerns](#architecture-system-design--org-level-concerns)
23. [Compiled "Elite" System-Design & Mock-Scenario Prompts](#compiled-elite-system-design--mock-scenario-prompts)

---

## 01. JavaScript & Browser Foundations (Prerequisite Layer)

- [ ] Closures, scope, hoisting, `this` binding — and how closures cause stale closures/memory leaks in hooks & Redux listeners
- [ ] Prototypal inheritance, `Object.create`
- [ ] Event loop: microtasks vs macrotasks; why React batching/state updates coordinate with the paint loop vs `setTimeout`/fetch macrotasks
- [ ] Promises, async/await, generators (`function*`, `yield`, iterator `.next()` — foundation of Redux-Saga)
- [ ] Debounce/throttle implementation from scratch
- [ ] ES6+: destructuring, spread/rest, optional chaining, nullish coalescing, Map/Set, WeakMap/WeakRef
- [ ] Immutability patterns, structural sharing, shallow vs deep equality
- [ ] V8 engine internals: hidden classes & inline caches, garbage collection / GC thrashing, memory leak archetypes (detached DOM, uncleared listeners, stale closures, unbounded caches)
- [ ] Browser rendering pipeline: parse → style → layout → paint → composite
- [ ] Browser storage comparison: cookies, localStorage, sessionStorage, IndexedDB, Cache API
- [ ] Web Components interop with React

---

## 02. React Core Fundamentals

- [ ] JSX compilation (Babel → `React.createElement` → jsx-runtime)
- [ ] Elements vs Components vs Instances
- [ ] Functional vs Class components
- [ ] Props, state, controlled vs uncontrolled components
- [ ] Conditional/list rendering; `key` prop semantics (why index-as-key breaks reconciliation)
- [ ] Fragments, Portals (DOM decoupling vs event bubbling preservation)
- [ ] Synthetic Event System: root-container event delegation, historical pooling, perf vs native DOM events

---

## 03. Fiber Architecture, Reconciliation & Rendering Internals

- [ ] Fiber nodes, work-in-progress tree, double buffering (current vs WIP tree)
- [ ] Work loop: `beginWork` / `completeWork`, split/pause/resume
- [ ] Reconciliation/diffing heuristics (O(n) vs theoretical O(n³))
- [ ] Render phase (pure, interruptible) vs Commit phase (synchronous DOM mutation)
- [ ] The Scheduler package: polyfilling `requestIdleCallback` via `MessageChannel`/`requestAnimationFrame`
- [ ] Priority lanes / task prioritization (NoPriority, Immediate, UserBlocking, Normal, Idle), expiration & starvation prevention
- [ ] Yielding to main thread (~5ms slicing) for responsiveness
- [ ] Batching: legacy vs React 18 automatic batching
- [ ] Concurrent rendering, interruptible rendering, time-slicing
- [ ] `React.memo`, `PureComponent`, shallow comparison pitfalls
- [ ] Bailing out of updates — exact conditions for early bailout
- [ ] Suspense internals (throwing promises), Suspense boundaries & commit-phase interaction
- [ ] Error boundaries — internals (`componentDidCatch`, `getDerivedStateFromError`)
- [ ] Source-level `react-reconciler` understanding, lanes model (staff/principal level)

---

## 04. Hooks — Full Depth

### Core

- [ ] `useState` — batching, functional updates, lazy initialization
- [ ] `useReducer` — reducer patterns, when to prefer over `useState`
- [ ] `useEffect` — async-after-paint execution, cleanup, dependency-array pitfalls, stale closures
- [ ] `useLayoutEffect` — sync pre-paint execution, layout measurement, flicker prevention
- [ ] `useInsertionEffect` — pre-DOM-mutation timing (CSS-in-JS style injection)
- [ ] `useMemo` / `useCallback` — genuine use cases vs premature optimization; no guaranteed cache retention
- [ ] `useRef` — mutable refs, DOM refs, avoiding re-renders, closures over stale state
- [ ] `useContext` — re-render cascade traps, selector/splitting mitigation
- [ ] `useImperativeHandle` + `forwardRef` — exposing restricted imperative APIs
- [ ] `useId` — stable, collision-free IDs consistent across SSR/hydration
- [ ] `useSyncExternalStore` — solving "tearing" when reading external mutable stores (Redux/Zustand/history API)
- [ ] `useTransition` / `useDeferredValue` — concurrent, non-blocking updates
- [ ] `useOptimistic` (React 19) — optimistic UI with automatic rollback
- [ ] `useActionState` (formerly `useFormState`) / `useFormStatus` — native async form state, pending/error tracking
- [ ] Custom hooks — design, composition, race-condition handling in data-fetching hooks
- [ ] Rules of Hooks — *why* they exist: hook linked-list architecture on the Fiber node (can't be in loops/conditionals)
- [ ] Implementing a simplified `useState`/`useEffect` yourself (fiber-lite understanding)

---

## 05. Component Design Patterns & Composition

- [ ] Higher-Order Components (HOCs) — limitations, why hooks largely replaced them
- [ ] Render Props (legacy, still asked)
- [ ] Compound Components — Context-driven communication (` `)
- [ ] Container/Presentational pattern
- [ ] Controlled vs Uncontrolled — dynamic transitions, complex validation
- [ ] Custom hook composition patterns
- [ ] Atomic design, feature-based folder structure
- [ ] Polymorphic components (`as` prop pattern) — typing challenge

---

## 06. State Management

### Local/Global Decision Making

- [ ] Local vs lifted vs Context vs global — staff-level decision matrix
- [ ] State colocation principles

### Context API

- [ ] Performance pitfalls, splitting contexts, selector patterns, memoized context value

### Redux — Core

- [ ] Three principles, unidirectional flow, `createStore`(legacy), `combineReducers`
- [ ] Pure reducers, immutability without Immer (spread/`Object.assign`), normalization
- [ ] Middleware signature `store => next => action`, custom middleware, execution order, enhancers vs middleware
- [ ] `connect()` (legacy) vs hooks (`useSelector`, `useDispatch`, `useStore`) — re-render behavior, `shallowEqual`
- [ ] Selectors & Reselect (`createSelector`), memoization internals, parametrized selectors

### Redux Thunk

- [ ] Function-as-action, `getState` access, chaining, error handling, cancellation limitations, testing thunks

### Redux-Saga

- [ ] Generator-driven middleware, declarative effects (plain objects, easy mocking)
- [ ] Effects: `call`, `put`, `take`, `takeEvery`, `takeLatest`, `takeLeading`, `fork` vs `spawn` (attached vs detached), `cancel`/`cancelled`, `race`, `all`, `delay`
- [ ] `actionChannel` (buffering), `eventChannel` (WebSockets/timers/geolocation bridge), custom `channel` (inter-saga comms)
- [ ] Root saga composition, watcher/worker pattern, supervisor/global error-boundary patterns
- [ ] Saga testing (step-through yielded-effect assertions)
- [ ] Real-world: token auth flow (`take` pull-loop), parallel dashboard loads with error isolation, file-upload progress via `eventChannel`, search typeahead with `race` cancellation, WebSocket chat sync, polling engines, exponential-backoff retry engine, offline action queueing

### Redux Toolkit (RTK)

- [ ] `configureStore` internals (auto middleware, DevTools, serializability checks)
- [ ] `createSlice`, Immer under the hood (Proxies enabling "mutating" syntax)
- [ ] `prepare` callback for custom payloads
- [ ] `createReducer` (builder vs map notation), `createAction`
- [ ] `createAsyncThunk` lifecycle (pending/fulfilled/rejected), `extraReducers`, `unwrap()`, `rejectWithValue`, `condition`, AbortController cancellation
- [ ] `createEntityAdapter` — normalized ID-to-record state, CRUD utilities, memoized selectors

### RTK Query

- [ ] `createApi`, `fetchBaseQuery`/custom baseQuery, query vs mutation endpoints, auto-generated hooks
- [ ] Cache keys, cache lifetimes (`keepUnusedDataFor`), tag-based invalidation (`providesTags`/`invalidatesTags`)
- [ ] Polling, refetch strategies, optimistic updates (`onQueryStarted` + manual rollback), prefetching (hover/focus/intent)
- [ ] Streaming cache updates (`onCacheEntryAdded` — SSE/WebSockets), `injectEndpoints` code-splitting
- [ ] RTK Query vs React Query/SWR — architectural differences

### Other State Libraries

- [ ] Zustand, Jotai, Recoil — atomic state models, transient updates
- [ ] XState / Finite State Machines — when FSMs beat boolean flags; modeling multi-step wizards/checkout flows

### Real-World Redux Use Cases (all levels)

- [ ] Session mgmt & logout store reset, multi-step wizards, feature flags/theme sync
- [ ] Normalized e-commerce dashboards, debounced search, optimistic "like" button
- [ ] Real-time collaborative workspace (OT + WebSockets), infinite undo/redo history stack, cross-tab/window sync via BroadcastChannel
- [ ] Micro-frontend state isolation, offline-first analytics sync engine with IndexedDB queue

---

## 07. Data Fetching & Server State

- [ ] `fetch`/Axios patterns, race conditions, `AbortController` cancellation, idempotency
- [ ] React Query / TanStack Query — caching, stale-while-revalidate, invalidation
- [ ] SWR
- [ ] Suspense-based data fetching; Render-as-You-Fetch vs Fetch-on-Render vs Fetch-then-Render (waterfalls)
- [ ] Server state vs client state distinction
- [ ] Optimistic updates & rollback strategies
- [ ] HTTP caching (Cache-Control, ETag) vs client-side memory caching boundaries

---

## 08. Performance Optimization

- [ ] Identifying unnecessary re-renders (React DevTools Profiler, flame graphs)
- [ ] Memoization strategy — when it backfires (memory vs compute tradeoff)
- [ ] Reference-equality pitfalls (inline objects/functions breaking memoization)
- [ ] Splitting components / moving state down to limit re-render blast radius
- [ ] Code splitting: `React.lazy`, dynamic `import()`, chunk-failure handling
- [ ] Virtualization: `react-window`, `react-virtualized`, `@tanstack/virtual`; windowing trade-offs
- [ ] Web Vitals in React context: LCP, INP (replaced FID), CLS, TTFB, FCP, TTI, TBT/long tasks (>50ms)
- [ ] Bundle analysis & tree-shaking (`sideEffects` field, ESM imports, barrel-file risks)
- [ ] Image/font loading strategies, lazy loading, SVGO
- [ ] Avoiding prop drilling / render cascades
- [ ] Concurrent features for perf: automatic batching, `useTransition`, `useDeferredValue`, Suspense coordination
- [ ] Memory management: leak diagnosis, heap snapshots, unbounded cache growth (RTK Query/React Query `gcTime`)
- [ ] CSS & layout performance: layout thrashing, CSS-in-JS runtime cost, `will-change`/GPU-accelerated props, CSS Containment (`contain: content`, `content-visibility: auto`)
- [ ] Performance budgets in CI, alerting on Web Vitals regressions, correlating perf with business metrics
- [ ] Prioritized scheduling via `scheduler.postTask()`; Web Workers for main-thread inversion
- [ ] System-design style: diagnose a slow 10k-row table, cut a 5MB bundle, debug high INP, 15-widget dashboard without waterfalls

---

## 09. Streaming Data, Real-Time & Large File Handling (Advanced)

- [ ] Real-time stream pipeline: incoming stream → worker/in-memory buffer → throttled batched dispatch → Fiber update
- [ ] SSE vs WebSockets vs WebTransport (HTTP/3/QUIC) trade-offs
- [ ] HTTP/2 & HTTP/3 multiplexing/prioritization
- [ ] Never pushing high-frequency data directly into React/Redux state — buffer + rAF-timed batched dispatch (60/120fps)
- [ ] Chunked/multipart file uploads (`File.slice()`), concurrent upload pool with concurrency limits, resumable uploads with client-side hashing (MD5/SHA-256) via Web Worker
- [ ] `ReadableStream` API for large downloads; File System Access API for direct-to-disk streaming; Object URL memory-safe downloads (`createObjectURL`/`revokeObjectURL`)
- [ ] Global `AbortController` cancel-all orchestration
- [ ] CSS Houdini/Paint Worklets, OffscreenCanvas, Intersection/Resize Observer custom hooks
- [ ] Mock system design: real-time collaborative financial dashboard, video-processing workspace with chunked upload + live WebSocket chart

---

## 10. Rendering Strategies: CSR / SSR / SSG / ISR / RSC

- [ ] Rendering strategy comparison and TTFB/FCP/TTI impact per strategy; SEO implications
- [ ] `renderToString`, `renderToStaticMarkup`, `renderToPipeableStream`/`renderToReadableStream` (streaming SSR)
- [ ] Hydration mechanics — attaching listeners/reconciling to existing DOM (not re-rendering)
- [ ] Hydration mismatches (browser-only APIs, `Date.now()`, `typeof window` conditionals), `suppressHydrationWarning`
- [ ] Selective/partial hydration, progressive hydration, streaming out-of-order via Suspense
- [ ] Resumability (Qwik) as a conceptual contrast to hydration
- [ ] Data fetching for SSR: waterfalls, parallel fetch/preloading, dehydrate/hydrate caching pattern
- [ ] React Server Components (RSC): server vs client component boundary (`"use client"`), what can/can't run where, serialization constraints, RSC payload wire format, bundle-size reduction, composition rules
- [ ] Next.js as reference implementation: Pages Router (`getServerSideProps`/`getStaticProps`/`getStaticPaths`) vs App Router (Server Components by default, layouts, loading/error file conventions), ISR & on-demand revalidation, Middleware/edge runtime, Route handlers, Server Actions, Next.js caching layers (Data/Full Route/Router cache)
- [ ] Other frameworks for contrast: Remix (loaders/actions), Gatsby (SSG+GraphQL), Astro (islands architecture)
- [ ] SSR performance: avoiding blocking Node event loop, full-page/edge caching, component-level RSC caching, N+1 avoidance
- [ ] State across server/client boundary: per-request store instantiation, `window.__PRELOADED_STATE__` pattern, avoiding cross-request contamination
- [ ] Auth/cookies in SSR — reading session pre-render, avoiding auth flicker, CSRF w/ Server Actions
- [ ] Error handling & timeouts in SSR context
- [ ] SSR deployment: Node server vs serverless (cold starts), Edge SSR constraints, horizontal scaling costs
- [ ] Debugging a production hydration mismatch — diagnosis walkthrough

---

## 11. Routing

- [ ] React Router — nested routes, dynamic routing, v6.4+ data APIs (loaders/actions)
- [ ] Route-based code splitting
- [ ] Protected routes & auth flows
- [ ] Deep linking & browser-history handling across composed apps

---

## 12. Forms

- [ ] Controlled vs uncontrolled forms
- [ ] Formik vs React Hook Form — why RHF avoids re-renders internally
- [ ] Validation strategies: Yup, Zod
- [ ] Complex dynamic forms
- [ ] React 19 native form handling: `useActionState`, `useFormStatus`, Server Actions, automatic rollback on failure, request dedup

---

## 13. Testing

- [ ] Jest fundamentals
- [ ] React Testing Library philosophy — behavior over implementation
- [ ] Mocking API calls & timers; Mocking Service Worker (MSW) for network-layer interception
- [ ] Snapshot testing pros/cons
- [ ] Cypress / Playwright for E2E
- [ ] Testing hooks in isolation
- [ ] Testing thunks (mock `dispatch`/`getState`, `redux-mock-store`)
- [ ] Testing sagas step-by-step (`redux-saga-test-plan`)
- [ ] Testing concurrent features — asserting mid-`useTransition` behavior, deterministic `act()` usage
- [ ] Visual regression testing (Chromatic, Percy, Storybook)
- [ ] Contract testing (micro-frontend shell ↔ remotes)
- [ ] Automated a11y testing (axe-core, jest-axe)

---

## 14. TypeScript (General + React-Specific)

### Foundations

- [ ] Structural typing (duck typing), inference vs explicit annotation, `any` vs `unknown` vs `never` vs `void`
- [ ] Type assertions (`as`) vs casting, `as const`
- [ ] Arrays/tuples, interfaces vs type aliases, enums & pitfalls, literal types

### Composition & Narrowing

- [ ] Union/intersection types, discriminated unions + exhaustiveness (`never`) checks
- [ ] Narrowing: `typeof`/`instanceof`/`in`, custom type guards (`is`), assertion functions (`asserts`)

### Generics & Meta-Programming

- [ ] Generic functions/classes/constraints (`extends`), default generic params, inference & variance
- [ ] `keyof`, lookup types, mapped types (+key remapping via `as`)
- [ ] Conditional types, `infer` keyword, distributive conditional types, recursive types
- [ ] Utility types under the hood: `Pick`, `Omit`, `Partial`, `Required`, `Record`, `Extract`, `Exclude`, `ReturnType`, `Parameters`, `InstanceType`, `Awaited`, `NonNullable`
- [ ] Template literal types (type-safe routes/CSS/event names)

### OOP, Modules, Declarations

- [ ] Access modifiers, parameter properties, abstract classes, `override`, static blocks
- [ ] `import type`/`export type`, namespaces vs modules, declaration merging, ambient modules/`.d.ts`, module augmentation
- [ ] `tsconfig.json` deep dive: `strict`, `noImplicitAny`, `strictNullChecks`, `strictFunctionTypes`, `noUncheckedIndexedAccess`, module resolution, path mapping, project references/composite builds

### Null Safety & Error Patterns

- [ ] `strictNullChecks`, `?.`/`??`, non-null assertion (`!`), definite assignment (`!:`)
- [ ] Result/Either pattern, exhaustiveness with `switch`+`never`, discriminated-union API response modeling

### Interop & Runtime Safety

- [ ] Typing untyped libs, `allowJs`/`checkJs`, runtime validation (Zod/io-ts) vs compile-time types

### TypeScript + React

- [ ] Typing props/state/refs/events (`React.MouseEvent ` etc.)
- [ ] `React.FC` debate, `ComponentProps`/`ComponentPropsWithoutRef`/`PropsWithChildren`
- [ ] Typing hooks: `useState `, `useRef `, `useReducer` with discriminated action unions
- [ ] Generic components (` () =>` gotcha in `.tsx`), typing HOCs/render props generically
- [ ] Typing context (`createContext ` pattern)
- [ ] Polymorphic components (`as` prop) typing

### Branded/Nominal Typing & Security

- [ ] Branded/opaque types simulating nominal typing (e.g., `UserId`, `SanitizedHTML`)
- [ ] `unique symbol`

### Compiler Internals (staff/principal)

- [ ] Structural assignability checking, AST representation, type widening/narrowing internals, declaration emit, deferred vs immediate conditional-type evaluation, compile-time performance pitfalls of deep generic chains

### System-Design-Style TS

- [ ] Type-safe REST client, type-safe form validation library, type-safe router (inferred path params), plugin system with type-safe extensibility, `DeepPartial `/`DeepReadonly `, Object-Path-Getter via template literals, dynamic Redux slice action typings, type-safe i18n translation function

---

## 15. Security

- [ ] XSS: stored/reflected/DOM-based; React's built-in JSX escaping and its exact bypass vectors (`javascript:` URLs)
- [ ] `dangerouslySetInnerHTML` — ESLint blocking + DOMPurify sanitization; SVG-based XSS vectors
- [ ] Content Security Policy: eliminating `unsafe-inline`, nonces/hashes, Trusted Types API, report-only rollout mode
- [ ] CSRF: tokens (double-submit, synchronizer), `SameSite` cookies, Server Actions built-in protections
- [ ] Token storage matrix: localStorage/sessionStorage vs cookies, `HttpOnly`/`Secure`/`SameSite` flags
- [ ] Backend-for-Frontend (BFF) pattern — moving token/cookie handling off the client entirely
- [ ] OAuth 2.1 + PKCE for SPAs (why implicit flow is deprecated)
- [ ] Session teardown & cross-tab sync (BroadcastChannel/storage events) on logout
- [ ] Authorization: client-side gating is UX only; real enforcement is server-side; role-based UI vs actual permission enforcement
- [ ] TypeScript compile-time security: branded/tainted-string types, exhaustive `never` checks for new roles/flags, strict serialization (Zod/TypeBox) stripping unexpected API properties
- [ ] State/memory security: prototype-pollution prevention in deep-merges, nullifying sensitive closures, malicious Redux DevTools/extension action injection
- [ ] Supply chain: SBOM, dependency poisoning/typosquatting, lockfile integrity, `npm audit`/Snyk/Dependabot
- [ ] Subresource Integrity (SRI) for third-party scripts/fonts
- [ ] Clickjacking defenses: `X-Frame-Options`, `frame-ancestors`
- [ ] Other security headers: `X-Content-Type-Options`, `Referrer-Policy`, `Permissions-Policy`, HSTS
- [ ] CORS from the frontend-consumer perspective (credentials mode, allowed origins)
- [ ] Third-party scripts/iframes: `sandbox` attribute, `postMessage` origin validation
- [ ] Input validation: client-side as UX-only, schema validation at boundaries (Zod/Yup)
- [ ] Security testing: SAST in CI, pen-testing mindset, OWASP Top 10 mapping to frontend
- [ ] Elite scenario: zero-data-exfiltration architecture for a regulated medical dashboard (Trusted Types + DOMPurify + BFF + strict CSP)

---

## 16. Build Tools, Bundling & Compilation

- [ ] Dev vs prod builds (minification, dead-code elimination, `NODE_ENV`)
- [ ] CRA (and its deprecation) vs Vite vs Next.js build pipeline
- [ ] Source maps: generation, private upload to Sentry/Bugsnag, production exclusion for security
- [ ] Tree-shaking mechanics, `sideEffects` field, barrel-file risks
- [ ] Code-splitting at build time (route/component-based)
- [ ] Bundle analysis (`webpack-bundle-analyzer`, `vite-bundle-visualizer`, `source-map-explorer`)
- [ ] Asset optimization: image compression, font subsetting, SVG optimization
- [ ] Output hashing/fingerprinting (`[contenthash]`) for cache busting
- [ ] Differential loading (modern ESM vs legacy `nomodule` fallback bundles)
- [ ] Babel JSX transforms, ESLint/Prettier + `eslint-plugin-react-hooks`
- [ ] The React Compiler ("React Forget") — automatic memoization, obsoleting manual `useMemo`/`useCallback`
- [ ] `"use client"` / `"use server"` directive boundary handling
- [ ] Document metadata/asset loading (React 19 native ` `/` `/` ` hoisting, `preload`/`preinit`)

---

## 17. Environment Configuration

- [ ] `.env`/`.env.local`/`.env.production` precedence
- [ ] Build-time vs runtime env vars — critical distinction; `REACT_APP_`/`VITE_` prefix security rationale
- [ ] Runtime config injection patterns (`window.__env__`, config fetched at boot) for one-build-many-environments
- [ ] Secrets management — never ship secrets to the client
- [ ] Multi-environment strategy (dev/staging/QA/UAT/prod)
- [ ] Feature flags: LaunchDarkly/Unleash/homemade; build-time vs runtime flags
- [ ] Config validation/fail-fast at startup

---

## 18. Deployment & Hosting Infrastructure

- [ ] Static hosting/Jamstack (S3/Cloudflare Pages/Vercel/Netlify/GitHub Pages/Firebase/Azure SWA)
- [ ] SPA routing on static hosts — 404-fallback-to-index.html / CDN rewrite rules
- [ ] Cache-Control strategy: immutable fingerprinted assets vs `no-cache` entry HTML
- [ ] Atomic deployments & origin pinning (avoiding stale-chunk mismatches during release)
- [ ] Edge Computing/ESR (Cloudflare Workers, Vercel Edge, CloudFront Functions) — constraints, use cases
- [ ] Containerization: multi-stage Docker builds, Nginx/Caddy SPA-fallback + gzip/brotli config, Docker Compose, container registries
- [ ] Orchestration: Kubernetes basics, ECS/Fargate, AWS/Azure/GCP hosting options, load balancing & auto-scaling for SSR
- [ ] CI/CD pipeline stages (lint → typecheck → test → security scan → build → deploy), GitHub Actions/GitLab CI/Jenkins/CircleCI
- [ ] Dependency caching in CI, PR preview deployments, semantic-release/automated versioning
- [ ] Deployment gates/manual approval, rollback strategy (N previous builds, one-click revert)
- [ ] Deployment strategies: blue-green, canary (weighted DNS/Route 53), rolling, feature-flag-gated releases
- [ ] SSR/SSG deployment specifics: `next export` static export, Vercel serverless-per-route model, ISR revalidation, edge vs serverless cold starts
- [ ] Production observability: RUM/Web Vitals, Sentry/Bugsnag + source-map upload, APM (Datadog/New Relic), structured SSR logging (ELK/CloudWatch), synthetic uptime checks, alerting
- [ ] Security in deployment: CSP/HSTS/`X-Frame-Options` headers, dependency & secrets scanning in CI, CORS config, SRI
- [ ] Versioning & release management: semver, GitFlow/trunk-based dev, release-note automation, frontend/backend API compatibility
- [ ] Multi-tenant/multi-region: latency-driven multi-region deploys, white-labeling/per-tenant config, i18n build strategy (runtime switch vs per-locale builds)
- [ ] Local dev/prod parity: Docker Compose mirroring, `.nvmrc`, lockfile discipline (`npm ci`)
- [ ] Package manager strategy: npm vs Yarn vs pnpm (strict/symlinked `node_modules`), private registries, peer-dependency conflicts

---

## 19. Monorepo Architecture

- [ ] Monorepo vs polyrepo trade-offs; when justified vs overengineering
- [ ] Workspace support: npm/Yarn(Classic & Berry/PnP)/pnpm workspaces, hoisting & phantom-dependency risk, `workspace:*` protocol
- [ ] Tooling: Nx (project graph, computation caching, `nx affected`, generators/executors), Turborepo (pipeline config, remote caching), Lerna, Rush, Bazel (conceptual) — comparison
- [ ] Build graph & task orchestration, affected/changed detection, parallelization
- [ ] Caching: local vs remote/distributed (Nx Cloud, Turborepo Remote Cache), cache-key inputs, invalidation correctness
- [ ] Code sharing: shared `ui`/`utils`/`config`/`types` packages, barrel-file trade-offs, internal versioning (always-latest vs independent), public API boundary discipline
- [ ] Dependency management: single-version policy vs drift, circular-dependency prevention, module-boundary lint rules
- [ ] Testing: affected-only test runs, cross-package integration, shared test config, multi-app E2E
- [ ] CI/CD: affected-based pipelines, independent per-app deploys, matrix builds, Changesets for versioning/changelogs
- [ ] Ownership/governance: CODEOWNERS, architectural-boundary enforcement, multi-team scaling
- [ ] Micro-frontends inside a monorepo: Module Federation + Nx/Turborepo patterns, shared design-system consumption, build isolation
- [ ] TypeScript in monorepos: project references/composite builds, path aliases, type-check performance at scale
- [ ] Migration: merging polyrepos (git subtree/filter-repo), incrementally adopting Nx/Turborepo, splitting an over-large package
- [ ] Common pitfalls: phantom dependencies, over/under-granular packages, stale-cache-induced false-green CI
- [ ] System design: 3-app monorepo (web/admin/mobile-web) w/ shared component lib, affected-only CI for 10-app repo w/ remote caching, module-boundary rules (checkout vs admin), org-wide monorepo vs domain-split vs polyrepo trade-off (200-engineer org)

---

## 20. Micro-Frontend Architecture

- [ ] Motivation: independent deployability, team autonomy, tech-stack independence, Conway's Law; honest cost trade-offs vs a well-structured monorepo SPA
- [ ] Decomposition: vertical (domain) vs horizontal (page-region) split, DDD bounded contexts, single-spa "applications" vs "parcels"
- [ ] Integration approaches: build-time (npm packages) vs runtime-JS (Module Federation/SystemJS) vs iframes (isolation, why largely avoided) vs server-side/Edge-Side Includes composition
- [ ] Webpack Module Federation: host/remote, `exposes`/`remotes`, singleton shared deps (React/ReactDOM), version-mismatch handling (`strictVersion`), dynamic remote resolution at runtime, bidirectional host+remote apps; Vite federation-plugin differences
- [ ] Orchestration frameworks: single-spa lifecycle (bootstrap/mount/unmount), qiankun sandboxing, Piral pilet architecture, hand-rolled shells
- [ ] Routing: shell-owned top-level routing + delegated sub-routes, route-based lazy loading, shared-router vs independent-router+URL-sync, cross-app deep linking, multi-app browser-history handling
- [ ] Inter-app communication: CustomEvents/pub-sub bus, shared injected store (coupling trade-off), URL/query-param state, props from shell, avoiding tight coupling
- [ ] Styling isolation: CSS collision problems, CSS Modules/CSS-in-JS scoping, Shadow DOM, shared design tokens, namespacing conventions
- [ ] Shared dependencies/versioning: avoiding duplicate framework copies, singleton strategies/import maps, independent vs enforced-shared versions, design-system distribution & breaking-change handling
- [ ] Cross-boundary state: why global Redux is tricky across independently-deployed apps, per-app vs shared/cross-cutting state (auth/session/theme/notifications), avoiding a shared store as a hidden coupling point
- [ ] Team/ownership: one team per MFE end-to-end, independent CI/CD, versioned shell↔remote contracts, shared design-system governance
- [ ] Independent deployability: single-MFE deploy w/o redeploying shell/siblings, dynamic remote-entry resolution, versioned/pinned vs always-latest remotes, feature-flag-gated MFE visibility
- [ ] Testing: isolated unit/integration, contract testing (shell↔remote), composed-system E2E, standalone/"parcel" mode
- [ ] Performance: bundle-duplication risk, lazy-loading remotes by route, network-waterfall risk (manifest→chunks), remote-entry caching, holistic Web Vitals across a multi-team composed app
- [ ] Security: trust boundary (remote MFE has full host-page access unlike iframes), CSP across dynamically-loaded cross-origin remotes, sanitizing inter-MFE data, SSO/token propagation
- [ ] SSR with MFEs: composing server-rendered fragments from multiple services, ESI/fragment caching, Next.js + Module Federation immaturity/trade-offs, cross-pipeline hydration challenges
- [ ] MFE circuit breakers: detecting remote timeout/script-load failure, auto-unmount + local fallback; Service-Worker interception serving cached stable versions during deploy failures
- [ ] Common pitfalls: "distributed monolith" anti-pattern, shared-library bottlenecks, inconsistent UX without design-system discipline, over-fragmentation, version drift
- [ ] System design: e-commerce MFE split (search/product/cart/checkout/account), shell responsibility boundary (auth/nav/theming/error boundaries), rollback strategy for a remote breaking prod, cross-MFE checkout communication (cart team A ↔ payment team B), Module Federation vs iframes vs server-side composition trade-off

---

## 21. Accessibility (a11y)

- [ ] Semantic HTML in JSX, ARIA roles, focus management, keyboard navigation
- [ ] WCAG conformance levels (A/AA/AAA) — org-wide enforcement expectations
- [ ] Baking a11y into the design system so teams get it "for free"
- [ ] Automated testing (axe-core/jest-axe) vs manual/screen-reader testing
- [ ] Complex widget patterns: focus trapping (modals), ARIA live regions, accessible comboboxes/data tables

---

## 22. Architecture, System Design & Org-Level Concerns

### API Layer

- [ ] REST vs GraphQL vs tRPC trade-offs; Apollo Client/Relay normalized cache & fragment colocation
- [ ] Backend-for-Frontend (BFF) pattern rationale
- [ ] API versioning, contract-first design (OpenAPI/GraphQL schema), schema stitching/federation, N+1/DataLoader pattern

### Design Systems

- [ ] Design tokens (color/spacing/typography), Storybook, headless (Radix/React Aria) vs fully-styled (MUI/Chakra)
- [ ] Versioning/distributing across teams, governance/contribution model, visual regression testing (Chromatic/Percy)

### i18n & l10n

- [ ] react-intl/i18next architecture, runtime vs per-locale builds, RTL/logical CSS properties, `Intl` pluralization/date/number formatting, translation-management workflows, locale-file bundle-size impact

### PWA & Offline-First

- [ ] Service workers, caching strategies (cache-first/network-first/SWR), Workbox, offline sync/background sync, IndexedDB persistence, manifest/installability, when it's actually worth it

### Native/Cross-Platform

- [ ] React Native code-sharing strategy, Expo vs bare workflow, when to extend web architecture to mobile

### Resilience & Observability

- [ ] Error-boundary placement strategy, graceful degradation, circuit-breaker pattern, exponential-backoff retries
- [ ] Structured logging correlated with backend trace IDs, distributed tracing (OpenTelemetry), dashboards tying errors/perf to business KPIs, alerting/on-call runbooks

### Governance & Decision-Making

- [ ] Architecture Decision Records (ADRs), tech-evaluation POC→pilot→rollout process, technical RFCs
- [ ] Tech-debt vs feature-velocity prioritization/justification to leadership
- [ ] Org-wide standards/linting/architecture rule enforcement

### Legacy Migration

- [ ] Strangler Fig pattern, running two frameworks side-by-side (MFE/iframe bridge), class→hooks codemods at scale, state-management migration strategies

### Cost & Team

- [ ] CDN/bandwidth cost of bundle size, serverless/edge cost models vs always-on, CI infra cost vs cache strategy, justifying spend to non-technical stakeholders
- [ ] Mentoring/code-review philosophy, autonomy vs consistency tension, onboarding into complex codebases, cross-functional collaboration, communicating technical risk

### Forward-Looking

- [ ] React Compiler implications, Signals-based reactivity (Preact Signals/Solid) vs React's re-render model, Server Actions maturity, View Transitions API, WebAssembly's realistic fit in a React app

---

## 23. Compiled "Elite" System-Design & Mock-Scenario Prompts

- [ ] Real-Time Collaborative Financial Dashboard (WebSockets + `useTransition` + `createEntityAdapter` + optimistic comments)
- [ ] Enterprise Micro-Frontend Shell with dynamically-registered isolated state slices
- [ ] Offline-First Analytics Sync Engine (IndexedDB queue + Thunk drain on reconnect)
- [ ] Browser-based Video Processing Workspace (chunked 4GB upload w/ pause/resume + live WebSocket analytics, 60fps)
- [ ] Regulated Medical Dashboard requiring zero data exfiltration under active XSS attack
- [ ] Atomic Zero-Downtime Global Deployment Pipeline (40 countries, edge-localized routing)
- [ ] Design an SSR architecture for an SEO+personalization product page
- [ ] Design a data table with sorting/filtering/pagination/virtualization
- [ ] Design an infinite-scroll feed and a real-time notification system
- [ ] Trade-off drills: CSR vs SSR vs SSG vs ISR; Thunk vs Saga vs RTK Query for cancel-on-keystroke search; Module Federation vs iframes vs server-side composition; single monorepo vs domain-split vs polyrepo for a 200-engineer org

---

## Progress checklist

- [ ] Complete all 23 sections
- [ ] Practice coding and implementation questions
- [ ] Complete at least 3 full mock interviews
- [ ] Prepare architecture stories from real projects

*Converted from the supplied HTML roadmap. The original 23 sections and 308 topics are preserved; interactive browser features such as search, theme switching, and saved progress are replaced with standard Markdown checkboxes and links.*
