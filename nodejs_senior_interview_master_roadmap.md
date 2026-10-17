# 🧠 Node.js Microservices on GCP/GKE — Senior Interview Master Roadmap

> A consolidated, checkbox-driven preparation roadmap for senior/staff-level interviews. Covers Node.js internals, distributed systems, microservices, APIs, data, messaging, performance, security, GCP/GKE, production operations, system design, and engineering leadership.

![Level](https://img.shields.io/badge/level-senior%2Fstaff-blueviolet)
![Stack](https://img.shields.io/badge/stack-Node.js%20%7C%20GKE%20%7C%20GCP-4285F4)
![Duration](https://img.shields.io/badge/interview-90--120%20min-informational)

> **How to use this roadmap:** Work through each checklist, prepare a production example for every major area, and practise the scenario questions aloud. Mark a topic complete only when you can explain the trade-offs, failure modes, and operational implications—not just define the term.

---

## 📑 Table of Contents

- [1. Node.js Core & Advanced Runtime](#1-nodejs-core--advanced-runtime)
- [2. Microservices Architecture & Design](#2-microservices-architecture--design)
- [3. API & Communication Design](#3-api--communication-design)
- [4. Data Layer](#4-data-layer)
- [5. Messaging & Event-Driven Systems](#5-messaging--event-driven-systems)
- [6. Performance Engineering (Steady State)](#6-performance-engineering-steady-state)
- [6B. Handling Massive Traffic / Sudden Load Spikes](#6b-handling-massive-traffic--sudden-load-spikes-deep-dive)
- [7. Security](#7-security)
- [8. Kubernetes / GKE Deep Dive](#8-kubernetes--gke-deep-dive)
- [9. CI/CD & Deployment Strategies](#9-cicd--deployment-strategies)
- [10. Observability](#10-observability)
- [11. Resilience & Fault Tolerance](#11-resilience--fault-tolerance)
- [12. Testing Strategy](#12-testing-strategy)
- [13. System Design & Real-World Scenarios](#13-system-design--real-world-scenario-questions-senior)
- [14. Leadership / Engineering Maturity](#14-leadership--engineering-maturity-expected-at-12-yrs)
- [Suggested Interview Structure](#-suggested-interview-structure-90120-min-senior-candidate)
- [15. Advanced Node.js Runtime & Diagnostics](#15-advanced-nodejs-runtime--diagnostics)
- [16. Distributed Systems Foundations](#16-distributed-systems-foundations)
- [17. Advanced Microservices Architecture](#17-advanced-microservices-architecture)
- [18. Advanced API & Communication](#18-advanced-api--communication)
- [19. Advanced Database Engineering](#19-advanced-database-engineering)
- [20. Advanced Messaging & Event Streaming](#20-advanced-messaging--event-streaming)
- [21. Advanced Performance Engineering](#21-advanced-performance-engineering)
- [22. Advanced Security](#22-advanced-security)
- [23. GCP Architecture & Networking](#23-gcp-architecture--networking)
- [24. Kubernetes Internals](#24-kubernetes-internals)
- [25. Production Debugging & Incident Response](#25-production-debugging--incident-response)
- [26. Architecture Trade-off Questions](#26-architecture-trade-off-questions)
- [27. Additional Senior+ System Design Scenarios](#27-additional-senior-system-design-scenarios)
- [Senior-Level Interview Answer Pattern](#senior-level-interview-answer-pattern)

---

## 1. Node.js Core & Advanced Runtime

- [ ] Event loop phases (timers, pending callbacks, idle/prepare, poll, check, close)
- [ ] **Microtask vs Macrotask queue** — `process.nextTick` vs `Promise.then` vs `setImmediate` vs `setTimeout(fn, 0)`, and event-loop starvation risk
- [ ] libuv thread pool sizing (`UV_THREADPOOL_SIZE`) for crypto/fs/DNS/compression
- [ ] Blocking vs non-blocking I/O; identifying and fixing event-loop-blocking code
- [ ] Streams (Readable/Writable/Duplex/Transform), backpressure handling
- [ ] Buffer internals, memory allocation
- [ ] `async/await` vs Promises vs callbacks — error propagation differences
- [ ] Worker Threads vs Cluster module vs child_process — multi-core scaling inside one container vs letting K8s scale pods
- [ ] **V8 memory layout**: Young Generation (Scavenge) vs Old Generation (Mark-Sweep-Compact) vs Large Object Space
- [ ] Heap snapshot diffing, allocation timelines, `node --inspect` against a live GKE pod
- [ ] **AsyncLocalStorage** for request-scoped trace/correlation context propagation
- [ ] CommonJS vs ESM interop issues in production
- [ ] Node.js LTS upgrade strategy across a service fleet
- [ ] Native addons / N-API — when justified
- [ ] Error handling: operational vs programmer errors, centralized error boundaries
- [ ] Graceful shutdown (`SIGTERM`/`SIGINT`, draining connections, finishing in-flight requests)
- [ ] Event-loop lag detection in production (`perf_hooks`, exported as a Prometheus metric)

## 2. Microservices Architecture & Design

- [ ] Service decomposition (DDD bounded contexts, strangler fig pattern)
- [ ] Sync (REST/gRPC) vs async (event-driven/Pub/Sub/Kafka) trade-offs
- [ ] API Gateway vs Backend-for-Frontend (BFF)
- [ ] Service discovery in Kubernetes (DNS-based, headless services)
- [ ] Data ownership per service; avoiding shared databases
- [ ] **Saga pattern** (choreography vs orchestration) vs **2PC anti-pattern**
- [ ] Outbox pattern to avoid the dual-write problem
- [ ] CQRS and event sourcing — when justified vs over-engineering
- [ ] Idempotency keys for retried requests
- [ ] API versioning strategy
- [ ] Contract testing (Pact) between services
- [ ] Monorepo vs polyrepo trade-offs (Nx, Lerna, Turborepo)
- [ ] Strangling a monolith into microservices — real migration experience
- [ ] Anti-patterns: distributed monolith, chatty services, shared-database coupling

## 3. API & Communication Design

- [ ] REST maturity model, HATEOAS practicality
- [ ] **gRPC over HTTP/2**: multiplexing, protobuf design, streaming types, deadlines, interceptors
- [ ] GraphQL federation vs REST (N+1 problem, DataLoader)
- [ ] Pagination (offset vs cursor/keyset)
- [ ] Rate limiting (token bucket, sliding window) — gateway vs service level
- [ ] OpenAPI/Swagger, contract-first development
- [ ] Backward compatibility / deprecation strategy
- [ ] Request validation (Joi/Zod/class-validator) and sanitization

## 4. Data Layer

- [ ] SQL (Cloud SQL) vs NoSQL (Firestore, Bigtable) vs **Cloud Spanner** — selection criteria
- [ ] Connection pooling (pg-pool, Cloud SQL Auth Proxy, PgBouncer) — `pods × pool_size` vs DB max-connections math
- [ ] ORMs (TypeORM, Prisma, Sequelize) — N+1 queries, migration strategy
- [ ] Read replicas, connection routing, failover handling
- [ ] Caching (Memorystore/Redis) — cache-aside vs write-through vs write-behind
- [ ] Cache stampede prevention, TTL jitter
- [ ] Zero-downtime DB migrations (expand/contract pattern)
- [ ] Multi-tenancy data isolation
- [ ] Eventual consistency handling in client code

## 5. Messaging & Event-Driven Systems

- [ ] **Cloud Pub/Sub**: at-least-once delivery, ordering keys, DLQ, exactly-once semantics
- [ ] Push vs pull subscriptions
- [ ] Kafka on GCP vs Pub/Sub trade-offs
- [ ] Schema evolution (Avro/Protobuf), schema registry
- [ ] Poison-message handling, retry with backoff **+ jitter**, DLQ reprocessing
- [ ] Idempotent consumers
- [ ] Event ordering, partition/ordering-key design
- [ ] Outbox pattern implementation
- [ ] Backpressure handling when consumers lag

## 6. Performance Engineering (Steady State)

- [ ] Profiling: `--prof`, `clinic.js`, `0x`, Chrome DevTools on a live container
- [ ] CPU flame graphs — finding hot paths
- [ ] Memory leak hunting (`EventEmitter` max-listener leaks, detached closures)
- [ ] Load testing (k6, Artillery, autocannon) — reading p50/p95/p99
- [ ] Node's single-threaded ceiling — cluster workers per pod vs scaling pod count
- [ ] Connection reuse: HTTP keep-alive, gRPC channel reuse
- [ ] Compression trade-offs (gzip/br) — gateway vs app layer
- [ ] JSON serialization cost — protobuf/msgpack alternatives
- [ ] GC tuning (`--max-old-space-size`) aligned with container memory limits
- [ ] Load shedding when downstream is overwhelmed

## 6B. Handling Massive Traffic / Sudden Load Spikes (Deep Dive)

**Edge Layer**
- [ ] Cloud Load Balancing absorbing volumetric spikes before the cluster
- [ ] Cloud CDN for cacheable GETs
- [ ] Cloud Armor for DDoS/bot mitigation and edge rate limiting

**Autoscaling Under Burst**
- [ ] HPA lag on sudden spikes — custom/external metrics (queue depth, req rate) for faster reaction
- [ ] Pre-warming / minimum replica floors vs pure reactive scaling
- [ ] Cluster Autoscaler node provisioning lag (30–90s+) — buffer node pools / low-priority placeholder pods
- [ ] Pod startup optimization (slim images, lazy-loaded deps)
- [ ] PodDisruptionBudgets + readiness gates

**Application Level**
- [ ] Single-threaded ceiling per pod, real concurrent-connection headroom
- [ ] Backpressure signaling, `server.maxConnections`
- [ ] No blocking calls on the hot path
- [ ] Load shedding: fast `429 + Retry-After` for low-priority requests
- [ ] Aggressive timeouts to free held connections

**Database & State — usually the real breaking point**
- [ ] Connection pool exhaustion math (`pods × pool_size` vs DB max connections)
- [ ] Read replicas + read/write splitting
- [ ] Memorystore (Redis) cache-aside to protect the DB
- [ ] Cache stampede protection under concurrent hot-key expiry
- [ ] Buffering writes through Pub/Sub as a shock absorber
- [ ] Per-tenant/per-key rate limiting (Redis token bucket)

**Queue-Based Load Leveling**
- [ ] Accept-fast/return-202/process-async pattern
- [ ] Autoscaling consumers on queue depth, not CPU

**Graceful Degradation**
- [ ] Circuit breakers serving cached/stale/default responses
- [ ] Feature flags disabling non-critical functionality under load
- [ ] Prioritizing critical endpoints over non-critical ones

**Validate before it happens in prod**
- [ ] Load testing to find the real per-pod breaking point
- [ ] Chaos/game-day drills simulating a 10x spike

> **Scenario question:** *"We just got featured on the homepage and traffic went 50x in 2 minutes. Walk me through what happens at every layer, where it breaks first, and how you'd have designed for it beforehand."*
> A strong answer traces edge → autoscaling lag → pod capacity → DB connection pool → queue-based leveling → degradation, and correctly names the **database** (not the app tier) as the usual first bottleneck.

## 7. Security

**Application-Level**
- [ ] OWASP Top 10 in Node.js context
- [ ] **Prototype pollution** and **ReDoS** as named JS-specific vulnerability classes
- [ ] Input validation & output encoding
- [ ] Dependency scanning (`npm audit`, Snyk, Trivy) and supply-chain risk
- [ ] Secrets via Secret Manager + Workload Identity (never plaintext env vars)
- [ ] JWT handling: algorithm-confusion attacks, short-lived tokens, refresh rotation
- [ ] OAuth2/OIDC, service-to-service auth (mTLS vs JWT)
- [ ] CORS misconfiguration risks
- [ ] Helmet.js / security headers, CSP
- [ ] Body-parsing size limits (large-payload DoS)
- [ ] Rate limiting & brute-force protection
- [ ] SSRF prevention for user-supplied URLs

**Infrastructure / GCP-Level**
- [ ] Workload Identity (K8s SA → GCP SA binding)
- [ ] IAM least-privilege, custom vs predefined roles
- [ ] VPC-native GKE clusters, private clusters
- [ ] Binary Authorization + **Cosign** image signing
- [ ] Artifact Registry vulnerability scanning
- [ ] Network Policies (Calico / **GKE Dataplane V2 — eBPF**)
- [ ] gRPC mTLS via Istio/Cloud Service Mesh
- [ ] Shielded GKE nodes, node auto-upgrade
- [ ] Distroless/multi-stage builds, non-root, `readOnlyRootFilesystem`, dropped capabilities
- [ ] Kubernetes RBAC design
- [ ] Secret sync: External Secrets Operator vs CSI Secret Store Driver vs native Secrets
- [ ] Pod Security Standards (restricted profile)
- [ ] Cloud Audit Logs for compliance

## 8. Kubernetes / GKE Deep Dive

- [ ] GKE Autopilot vs Standard — cost vs control
- [ ] Deployments/ReplicaSets/StatefulSets — when a Node.js service needs the latter
- [ ] Readiness vs liveness vs startup probes (avoiding kills during GC pauses)
- [ ] Resource requests/limits — CPU throttling vs libuv thread pool interplay
- [ ] HPA (CPU/memory + custom/external metrics) and VPA
- [ ] Cluster Autoscaler, node pools, Spot/preemptible VMs
- [ ] Node Affinity/Anti-Affinity, Taints and Tolerations
- [ ] ConfigMaps vs Secrets; hot-reload strategies
- [ ] Init containers for migrations/warm-up
- [ ] Sidecar pattern (Envoy / Cloud SQL Proxy) vs native drivers
- [ ] PodDisruptionBudgets
- [ ] Ingress (GKE Ingress/Gateway API) vs Istio Gateway, Cloud Armor integration, TLS termination
- [ ] Internal DNS / CoreDNS tuning for high-throughput resolution
- [ ] CNI performance — Dataplane V2 (eBPF)
- [ ] Multi-cluster/multi-region GKE for DR
- [ ] Namespace strategy, resource quotas
- [ ] Cost optimization: bin packing, right-sizing, Autopilot pricing
- [ ] Helm / Kustomize
- [ ] Debugging crashlooping pods
- [ ] OOMKilled troubleshooting (Node heap vs container memory limit mismatch)

## 9. CI/CD & Deployment Strategies

- [ ] Cloud Build / GitHub Actions / GitLab CI for a Node.js monorepo
- [ ] Multi-stage Docker builds — minimal size, distroless, non-root
- [ ] Artifact Registry tagging (immutable tags, semver, digest pinning), Cosign signing
- [ ] Blue-green, canary, rolling deployments (Istio/Argo Rollouts)
- [ ] Progressive delivery + automated rollback on error-rate/SLO-burn
- [ ] GitOps with ArgoCD / FluxCD / Config Sync
- [ ] DB migration coordination with rolling deploys
- [ ] Feature flags (LaunchDarkly/Unleash) to decouple deploy from release
- [ ] Environment promotion via Cloud Deploy pipelines
- [ ] Runtime secret injection, never baked into images
- [ ] Testing pyramid in CI: unit, integration, contract, e2e, load
- [ ] Pre-prod smoke tests / synthetic monitoring gating release

## 10. Observability

- [ ] Structured JSON logging to Cloud Logging, correlation/trace IDs
- [ ] OpenTelemetry auto-instrumentation + custom metrics/spans
- [ ] Distributed tracing (Cloud Trace / Jaeger), trace-ID propagation across HTTP/gRPC
- [ ] Prometheus metrics via Cloud Managed Service for Prometheus
- [ ] SLI/SLO/error-budget definition, burn-rate alerting
- [ ] Cloud Monitoring dashboards, alerting policies, on-call runbooks
- [ ] Log-based metrics vs app-emitted metrics
- [ ] Debugging without SSH (`kubectl exec`, ephemeral debug containers)
- [ ] Chaos engineering to validate alerts actually fire

## 11. Resilience & Fault Tolerance

- [ ] Circuit breaker pattern (Opossum)
- [ ] Retry strategies: exponential backoff + jitter, retry budgets
- [ ] Timeouts at every network hop
- [ ] Bulkhead isolation per dependency
- [ ] Graceful degradation / fallback responses
- [ ] Failure injection (Istio fault injection, Chaos Mesh)
- [ ] Multi-region failover: active-active vs active-passive
- [ ] Partial-failure handling in fan-out calls (`Promise.allSettled`)
- [ ] **Cascading failure prevention** — timeouts + circuit breakers + bulkheads working together

## 12. Testing Strategy

- [ ] Unit testing (Jest/Mocha/Vitest) with GCP SDK mocking
- [ ] Integration testing with Testcontainers (Postgres/Redis/Pub-Sub emulator)
- [ ] Contract testing (Pact)
- [ ] Load/performance testing as CI gates
- [ ] Mutation testing
- [ ] K8s manifest testing (kubeval, conftest/OPA)
- [ ] Ephemeral per-PR namespace for e2e testing

## 13. System Design & Real-World Scenario Questions (Senior+)

- [ ] Design a rate limiter usable across 50 microservices with Redis
- [ ] Design an idempotent payment processing service on GKE
- [ ] Design a multi-tenant SaaS backend with data isolation
- [ ] Design a real-time notification system (WebSockets/SSE + Pub/Sub)
- [ ] Handle a thundering herd on cache expiry across thousands of pods
- [ ] Design zero-downtime schema migration for a high-traffic service
- [ ] Diagnose a sudden p99 latency spike after a deploy
- [ ] Design DR for a GKE-hosted platform (RTO/RPO targets)
- [ ] GKE bill doubled — walk through the cost audit
- [ ] Design service-to-service auth for 100+ microservices
- [ ] "Traffic went 50x in 2 minutes" — full-stack trace (see §6B)
- [ ] **Event-loop-delay scenario**: *"Pod latency is high but CPU is 35% and RAM is stable — how do you instrument and debug Event Loop Delay live in a K8s pod?"*
- [ ] **Cascading failure scenario**: *"Service A calls Service B; B's DB slows down; within 2 minutes the whole system degrades. How do you prevent this?"*
- [ ] **Zero-downtime deploy with long-lived connections**: *"How do you roll-update a Node.js service on GKE holding long-lived HTTP/2 or gRPC streams without dropping connections or losing state?"*
- [ ] **Graceful shutdown lifecycle**: *"Walk through the exact sequence when a GKE pod terminates — SIGTERM, preStop hook, readiness probe flip, connection draining — and how the process should exit cleanly."*

## 14. Leadership / Engineering Maturity (expected at 12 yrs)

- [ ] Trade-off articulation: build-vs-buy, monolith-vs-microservices
- [ ] Mentoring approach, code review philosophy
- [ ] Blameless incident postmortem facilitation
- [ ] Driving architecture decisions with ADRs
- [ ] Balancing tech debt vs feature delivery with stakeholders
- [ ] Capacity planning and GCP cost forecasting
- [ ] Cross-team API contract negotiation experience

---

## ⏱ Suggested Interview Structure (90–120 min, senior candidate)

| Round | Focus | Duration |
|---|---|---|
| 1 | Node.js internals + event loop/perf deep dive | 30 min |
| 2 | Microservices architecture + system design (whiteboard) | 40 min |
| 3 | GKE/GCP infra, security & deployment | 30 min |
| 4 | Scenario walkthroughs + leadership/behavioral | 20 min |

> **Tip:** For a 12-year candidate, weight questions toward *trade-off reasoning and past real incidents* rather than textbook definitions — ask "walk me through a time you debugged X in production" instead of "what is X." The four scenario questions in §13 are especially strong signal because they can't be answered from memorized definitions alone.

---

## 15. Advanced Node.js Runtime & Diagnostics

- [ ] V8 JIT compilation — interpreter, bytecode, TurboFan, deoptimization
- [ ] Hidden classes / Shapes and inline caching
- [ ] Advanced garbage collection — incremental/concurrent GC and GC pauses
- [ ] `WeakMap`, `WeakSet`, `WeakRef`, `FinalizationRegistry`
- [ ] `AbortController` and cancellation of async operations
- [ ] `async_hooks` and async resource lifecycle
- [ ] DNS behavior — `dns.lookup()` vs `dns.resolve()`
- [ ] HTTP Agent / connection-pool tuning
- [ ] Node.js diagnostics and `diagnostics_channel`
- [ ] Native memory vs V8 heap memory
- [ ] File descriptor exhaustion (`EMFILE`) and OS-level limits
- [ ] TCP sockets, ephemeral ports and connection exhaustion

## 16. Distributed Systems Foundations

- [ ] CAP theorem in practical systems
- [ ] PACELC
- [ ] Strong vs eventual consistency
- [ ] Linearizability, sequential consistency and causal consistency
- [ ] Distributed consensus — Raft fundamentals
- [ ] Leader election
- [ ] Split-brain and network partitions
- [ ] Clock synchronization
- [ ] Logical clocks / Lamport timestamps
- [ ] Vector clocks
- [ ] Distributed locking
- [ ] Distributed ID generation — UUID/ULID/Snowflake concepts
- [ ] Exactly-once vs at-least-once processing in real systems
- [ ] Request deduplication
- [ ] Distributed transactions and their practical limits

## 17. Advanced Microservices Architecture

- [ ] Distributed transactions beyond Saga
- [ ] API composition / aggregation patterns
- [ ] Fan-out / fan-in architecture
- [ ] Dependency graph management
- [ ] Service ownership and Team Topologies
- [ ] Distributed configuration management
- [ ] Service mesh vs application-level communication
- [ ] Correlation ID vs Trace ID vs Span ID
- [ ] Leader-election-based service coordination
- [ ] Distributed locking patterns
- [ ] Practical exactly-once processing
- [ ] Cross-service request deduplication

## 18. Advanced API & Communication

- [ ] HTTP caching semantics — Cache-Control, ETag, If-None-Match
- [ ] Conditional requests
- [ ] HTTP status-code design
- [ ] Long-running APIs — `202 Accepted`, polling and webhooks
- [ ] Webhooks — retries, signatures and replay protection
- [ ] WebSockets vs SSE vs long polling
- [ ] API gateway failure modes
- [ ] API security threat modeling
- [ ] Request/response size limits
- [ ] API quota management
- [ ] API idempotency beyond POST
- [ ] HTTP/1.1 vs HTTP/2 head-of-line blocking considerations
- [ ] gRPC connection/channel management

## 19. Advanced Database Engineering

- [ ] Database indexing internals
- [ ] B-tree vs Hash indexes
- [ ] Composite indexes and index selectivity
- [ ] `EXPLAIN` / `EXPLAIN ANALYZE`
- [ ] Query-plan analysis
- [ ] Transaction isolation levels
- [ ] MVCC
- [ ] Deadlocks and deadlock detection
- [ ] Optimistic vs pessimistic locking
- [ ] Database connection exhaustion
- [ ] Database failover behavior
- [ ] Read-after-write consistency
- [ ] Sharding / horizontal partitioning
- [ ] Partition pruning
- [ ] Database replication lag
- [ ] Hot partitions / hot keys
- [ ] Backup and restore strategy
- [ ] Point-in-time recovery
- [ ] Database disaster recovery

## 20. Advanced Messaging & Event Streaming

- [ ] Consumer rebalancing
- [ ] Consumer-group behavior
- [ ] Partition scaling
- [ ] Hot partitions
- [ ] Consumer-lag diagnosis
- [ ] Message retention strategy
- [ ] Event replay architecture
- [ ] Replay safety and idempotency
- [ ] Dead-letter topic operational strategy
- [ ] Transactional messaging
- [ ] Kafka ISR / replication concepts
- [ ] Kafka producer `acks`
- [ ] Kafka idempotent producer
- [ ] Pub/Sub flow control
- [ ] Pub/Sub lease management
- [ ] Subscriber concurrency tuning

## 21. Advanced Performance Engineering

- [ ] Node.js Event Loop Utilization (ELU) vs Event Loop Delay
- [ ] CPU profiling — CPU-bound vs I/O-bound diagnosis
- [ ] V8 JIT optimization / deoptimization and performance impact
- [ ] Memory leak vs memory fragmentation vs high allocation rate
- [ ] HTTP connection pooling / `http.Agent` tuning
- [ ] TCP connection exhaustion
- [ ] Ephemeral port exhaustion
- [ ] File descriptor exhaustion
- [ ] DNS latency and DNS caching
- [ ] Keep-alive connection exhaustion
- [ ] HTTP/1.1 vs HTTP/2 performance characteristics
- [ ] N+1 calls between microservices
- [ ] Fan-out/fan-in latency amplification
- [ ] Tail latency
- [ ] Coordinated omission in load testing
- [ ] Little's Law — concurrency = throughput × latency
- [ ] Capacity planning — RPS → concurrency → pods → DB connections
- [ ] Per-service latency budgets / performance budgets
- [ ] Benchmarking methodology — warm-up, steady state, percentile analysis
- [ ] Performance regression detection in CI/CD
- [ ] CPU throttling investigation
- [ ] CPU steal time
- [ ] Memory pressure vs memory leak
- [ ] Network latency decomposition
- [ ] TCP connection-state analysis
- [ ] TIME_WAIT exhaustion
- [ ] Kernel/network bottleneck diagnosis
- [ ] GC vs CPU vs I/O bottleneck identification
- [ ] Queueing theory basics

## 22. Advanced Security

### Application / API Security

- [ ] Threat modeling for microservices
- [ ] Zero Trust architecture
- [ ] Authentication vs authorization
- [ ] Service-to-service authorization
- [ ] JWT validation — issuer, audience, expiry and algorithm
- [ ] Token propagation across service chains
- [ ] OAuth2 — Authorization Code + PKCE
- [ ] OAuth2 — Client Credentials
- [ ] mTLS certificate rotation
- [ ] API replay attacks
- [ ] Idempotency and security implications
- [ ] SSRF against cloud metadata services
- [ ] API abuse / credential stuffing / bot attacks
- [ ] DDoS protection architecture

### Kubernetes / Container Security

- [ ] Kubernetes service-account token security
- [ ] Container escape / privilege-escalation concepts
- [ ] Linux capabilities
- [ ] Seccomp / AppArmor
- [ ] East-west vs north-south traffic security
- [ ] NetworkPolicy design and troubleshooting
- [ ] Runtime vulnerability detection
- [ ] Pod-to-pod security boundaries

### Supply Chain / Data Security

- [ ] Dependency confusion
- [ ] Typosquatting
- [ ] SBOM — Software Bill of Materials
- [ ] Image provenance / trusted artifacts
- [ ] Data encryption at rest vs in transit
- [ ] KMS and key rotation
- [ ] PII/data masking in logs
- [ ] Security incident response
- [ ] Auditability and forensic investigation

## 23. GCP Architecture & Networking

- [ ] VPC architecture
- [ ] Shared VPC
- [ ] VPC Peering
- [ ] Private Service Connect
- [ ] Cloud NAT
- [ ] Cloud DNS
- [ ] Cloud Router
- [ ] GCP firewall rules
- [ ] Internal vs external load balancers
- [ ] Global vs regional load balancing
- [ ] Service Accounts
- [ ] IAM Conditions
- [ ] Organization / Folder / Project hierarchy
- [ ] Resource hierarchy and policy inheritance
- [ ] GCP quotas and service limits
- [ ] GCP budgets and cost controls
- [ ] Cloud Logging architecture
- [ ] Cloud Monitoring architecture
- [ ] Secret Manager architecture
- [ ] Artifact Registry
- [ ] Cloud Storage integration
- [ ] Cloud SQL integration
- [ ] Pub/Sub integration
- [ ] Memorystore integration
- [ ] BigQuery integration patterns

## 24. Kubernetes Internals

- [ ] Kubernetes control-plane architecture
- [ ] API Server
- [ ] Scheduler
- [ ] Controller Manager
- [ ] etcd
- [ ] Kubernetes reconciliation loop
- [ ] Admission controllers
- [ ] CRDs / Operators
- [ ] Service types — ClusterIP / NodePort / LoadBalancer
- [ ] kube-proxy / service networking
- [ ] EndpointSlices
- [ ] NetworkPolicy troubleshooting
- [ ] Pod lifecycle states
- [ ] Termination grace period
- [ ] QoS classes — Guaranteed / Burstable / BestEffort
- [ ] ResourceQuota vs LimitRange
- [ ] Horizontal vs Vertical vs event-driven scaling
- [ ] KEDA
- [ ] Kubernetes scheduling mechanics
- [ ] Pod topology spread constraints

## 25. Production Debugging & Incident Response

- [ ] Production incident triage
- [ ] Establishing blast radius
- [ ] Mitigation vs root-cause fix
- [ ] Rollback vs roll-forward decision
- [ ] Debugging latency regression
- [ ] Debugging memory leaks
- [ ] Debugging CPU spikes
- [ ] Debugging event-loop blocking
- [ ] Debugging connection-pool exhaustion
- [ ] Debugging Pub/Sub backlog
- [ ] Debugging DNS failures
- [ ] Debugging intermittent 5xx errors
- [ ] Debugging cascading failures
- [ ] Debugging OOMKilled
- [ ] Debugging CrashLoopBackOff
- [ ] Debugging node-level failures
- [ ] Incident commander responsibilities
- [ ] Postmortem / RCA
- [ ] Preventing recurrence
- [ ] SLO-based incident prioritization

## 26. Architecture Trade-off Questions

- [ ] REST vs gRPC
- [ ] REST vs GraphQL
- [ ] Kafka vs Pub/Sub
- [ ] Redis vs database cache
- [ ] Cloud SQL vs Spanner
- [ ] Firestore vs Bigtable
- [ ] GKE vs Cloud Run
- [ ] GKE Autopilot vs Standard
- [ ] Monolith vs microservices
- [ ] Synchronous vs asynchronous communication
- [ ] Choreography vs orchestration
- [ ] Saga vs distributed transaction
- [ ] CQRS vs traditional architecture
- [ ] Multi-region vs single-region
- [ ] Active-active vs active-passive
- [ ] Sidecar vs library
- [ ] Service mesh vs direct service communication

## 27. Additional Senior+ System Design Scenarios

- [ ] Design an API Gateway for 100+ microservices
- [ ] Design a distributed job-processing platform
- [ ] Design a high-scale payment system
- [ ] Design a URL shortener at massive scale
- [ ] Design a WhatsApp-like messaging system
- [ ] Design a large-scale file upload/download system
- [ ] Design a distributed scheduler
- [ ] Design a real-time analytics platform
- [ ] Design a multi-region active-active system
- [ ] Design a global rate limiter
- [ ] Design a distributed cache
- [ ] Design an event replay platform
- [ ] Design a feature-flag platform
- [ ] Design a centralized configuration service
- [ ] Design a notification platform
- [ ] Design a large-scale audit/compliance system

---

## 🎯 Senior-Level Interview Answer Pattern

For major architecture, performance, security and production questions, prepare to answer in this order:

1. **Clarify requirements and constraints**
2. **State the proposed architecture**
3. **Explain the request/data flow**
4. **Identify bottlenecks and failure points**
5. **Explain scalability**
6. **Explain consistency and correctness**
7. **Explain security**
8. **Explain observability**
9. **Explain failure/recovery behavior**
10. **Explain cost implications**
11. **State alternatives and trade-offs**
12. **Give a real production example where possible**

For a 12+ year candidate, prioritize **trade-off reasoning, production incidents, debugging methodology, capacity planning and architectural decision-making** over memorized definitions.
