# Microservices

### 1. What is a microservice architecture, and how does it differ from monolithic architecture?

> Microservices split an application into many small, independent services. A monolith is one large application deployed
> as a single unit.

- Microservices focus on small business functions with independent deployment and scaling.
- Monoliths combine all modules into one process, sharing the same memory and release cycle.
- Microservices communicate over the network (HTTP/gRPC), while monoliths use in-process calls.
- Microservices support team autonomy and faster releases but increase operational complexity.

> Microservices replace direct method calls with network communication, which adds latency and failure risks but
> improves isolation and resilience.
> Microservices bring flexibility, independent scaling, and better failure isolation. Monoliths are simpler and faster
> to build but harder to scale and evolve over time.

---

### 2. What are the core principles of microservices (as per domain-driven design)?

> Microservices should match business domains, remain loosely coupled, and be independently deployable.

- Services follow clear domain boundaries.
- Each service owns its data and logic.
- Teams are fully responsible for their service lifecycle.
- Communication is explicit and well-defined through APIs.
- Services prefer asynchronous messaging when suitable.

> DDD helps define clear domain boundaries (bounded contexts) so microservices can grow and change independently without
> creating tight coupling.
> Microservices follow DDD by focusing on domain clarity, strong boundaries, and autonomous teams, which allows faster
> development and safer evolution.

---

### 3. Explain the advantages and disadvantages of microservices.

> Microservices improve agility and scaling but add complexity in deployment, monitoring, and communication.

- **Advantages**
    - Independent releases and faster iterations.
    - Scalable per service, not for the whole system.
    - Better fault isolation: one failing service does not crash everything.
    - Allows different technologies per service when needed.

- **Disadvantages**
    - Harder to debug and trace because the system is distributed.
    - Requires strong DevOps, CI/CD, and automation.
    - Network calls add latency and new failure modes.
    - Data consistency is harder; often uses eventual consistency.

> Because services communicate over the network, engineers must handle partial failures, backpressure, and retries,
> which do not exist inside a monolith.
> Microservices bring great flexibility and scaling options, but only when the organization can handle the extra
> complexity of distributed systems.

---

### 4. What is bounded context in Domain-Driven Design (DDD) and its relation to microservices?

> A bounded context defines a clear domain area with its own rules and models. Microservices usually match these
> boundaries.

- Each bounded context has its own domain language and data model.
- It prevents mixing unrelated concepts across domains.
- A typical microservice represents one bounded context.
- Communication between contexts happens through stable APIs and translations.

> Bounded contexts avoid model pollution and force teams to treat domain boundaries seriously, while microservices
> enforce these boundaries at runtime.
> Bounded contexts define the domain structure, and microservices turn those structures into independent, deployable
> units with clear ownership.

---

### 5. How do you decide the boundaries/seams when splitting a monolith into microservices?

> Choose boundaries based on domain meaning, cohesion, and business needs—not technical layers.

- Identify subdomains and bounded contexts using DDD.
- Look for areas where teams struggle to release changes.
- Separate features that scale differently.
- Find modules with unstable or changing requirements.
- Avoid splitting by layers (controllers/services/repos), which creates weak boundaries.

> When splitting a monolith, the separation of data, transactions, and domain rules often reveals natural seams for new
> services.
> The best boundaries follow the domain structure, allow independent releases, and avoid creating high network traffic
> between services.

---

### 6. What is the difference between decomposition by business capability vs subdomain?

> Capabilities describe what the business does; subdomains describe how the domain is structured.

- **Business capability**
    - High-level business function (e.g., Payments, Shipping).
    - Often too large for a single microservice.
    - Useful for organizing teams.

- **Subdomain**
    - More detailed domain part, defined through DDD.
    - Better match for service boundaries.
    - Has its own domain rules and language.

> Business capabilities guide organizational planning, while subdomains guide technical design and service boundaries.
> Microservices should follow subdomains because they create cleaner models, clearer ownership, and better long-term
> maintainability.

---

### 7. What is the API Gateway pattern and why is it needed?

> An API Gateway is a single entry point that routes, secures, and aggregates requests to backend services.

- Hides internal service structure from clients.
- Offers rate limiting, authentication, and caching.
- Helps clients avoid calling many services directly.
- Enables protocol translation (e.g., REST to gRPC).

> API Gateways remove complexity from clients and allow backend services to evolve without breaking client applications.
> The API Gateway improves client simplicity, centralizes cross-cutting concerns, and protects internal microservices
> behind a controlled access layer.

---

### 8. What is service discovery and how does it work (e.g., Eureka, Consul, Kubernetes DNS)?

> Service discovery lets services find each other dynamically without hardcoded addresses.

- **Eureka/Consul**: services register themselves and clients query the registry.
- **Kubernetes DNS**: Kubernetes manages service names and IPs automatically.
- Helps with autoscaling—new instances appear automatically.
- Allows load balancing using instance lists or virtual IPs.

> Dynamic discovery avoids outdated network addresses and supports environments where pods/containers restart
> frequently.
> Service discovery ensures reliable communication in a system where services constantly scale, move, or restart.

---

### 9. Explain client-side vs server-side load balancing in microservices.

> Client-side load balancing chooses the instance on the client; server-side uses a proxy or load balancer to choose the
> instance.

- **Client-side**
    - Client retrieves instance list from the registry.
    - Reduces extra network hops.
    - Clients must integrate with the registry.

- **Server-side**
    - Proxy (Nginx, Envoy, ALB) picks the instance.
    - Clients remain simple.
    - Adds one extra hop but centralizes routing.

> Client-side is common for internal service-to-service calls; server-side suits external traffic and public APIs.
> Use client-side when services need direct control and low latency; use server-side for centralized routing and simpler
> clients.

---

### 10. What is the Circuit Breaker pattern and why is it important?

> A Circuit Breaker stops calls to a failing service to protect the system from cascading failures.

- Tracks errors or slow responses.
- Opens the circuit when failures exceed a threshold.
- Prevents blocking threads and wasting resources.
- Moves to half-open mode to test if the service has recovered.

> Circuit Breakers protect thread pools, prevent timeouts from spreading, and improve system stability under heavy load.
> A Circuit Breaker is essential for microservices because it stops failures from spreading, supports graceful recovery,
> and keeps the system responsive even when dependencies are unstable.
---

### 11. How do you implement resilience in microservices (Retry, Timeout, Bulkhead, Fallback)?

> Use a combination of timeouts, retries with backoff, isolation (bulkheads), and fallbacks to prevent failures from
> cascading and to provide graceful degradation.

- **Timeouts**
    - Set per-call deadlines to avoid waiting forever (HTTP client, gRPC deadlines).
    - Prefer short, realistic timeouts and propagate them end-to-end.
- **Retries**
    - Use idempotent or safe retry logic (exponential backoff + jitter).
    - Avoid retrying non-idempotent operations without coordination.
- **Bulkhead**
    - Isolate resources (thread pools, connection pools) per dependency to avoid resource exhaustion.
    - Use thread-pool or semaphore bulkheads for blocking vs non-blocking calls.
- **Fallback**
    - Provide a degraded response (cached value, default, or read-only mode).
    - Keep fallbacks lightweight and well-tested to avoid hiding faults.

> At the JVM level, blocking threads are a scarce resource — bulkheads and timeouts protect thread pools and event
> loops. Retries increase load; use circuit breakers to stop retry storms. Implement resilience using libraries like
> Resilience4j (non-blocking-friendly) or platform features (Envoy retries, gRPC deadlines).
>
> Implement resilience holistically: add client-side timeouts, safe retries with backoff, isolate resources with
> bulkheads, and provide meaningful fallbacks. Use circuit breakers to stop retry storms and ensure observability (
> metrics/traces) for tuning.

---

### 12. What is eventual consistency and when does it apply in microservices?

> Eventual consistency means data replicas will converge to the same state over time; it applies when immediate strong
> consistency is impractical across separate services/databases.

- Use when services own independent datastores and synchronous distributed transactions are too costly or unavailable.
- Typical patterns: asynchronous replication, event propagation, and compensating actions.
- Client must accept stale reads for a short window or use read-after-write strategies when needed.
- Useful for high-throughput systems, scalability, and availability (CAP trade-offs).

> On the JVM, eventual consistency commonly arises after publishing domain events (Kafka) and applying them
> asynchronously. Developers must reason about causality, idempotence, and ordering to ensure correct convergence.
>
> Use eventual consistency where availability and partition tolerance matter more than immediate strong consistency.
> Design APIs, UX, and error handling around the convergence window, and provide strategies (read-your-writes,
> versioning, conflict resolution) when necessary.

---

### 13. How do you handle distributed transactions across microservices?

> Prefer avoiding two-phase commit; instead use compensating transactions (Sagas) or design for eventual consistency.

- **Two-Phase Commit (2PC)**
    - Strong consistency but blocks resources and reduces availability — rarely recommended in microservices.
- **Sagas**
    - Sequence of local transactions with compensating actions if one step fails.
    - Can be orchestrated (central coordinator) or choreographed (events).
- **Idempotence**
    - Ensure actions can be retried safely.
- **Design alternatives**
    - Use event-driven flows, outbox pattern, and state machine-based retries rather than distributed locks.

> 2PC requires a coordinator and distributed locks; it introduces blocking and single points of failure. Sagas move
> consistency responsibility to application logic and are more compatible with microservice autonomy.
>
> For microservices, design to avoid global ACID where possible: use local transactions, publish events (outbox), and
> implement sagas/compensation for business-level consistency. Instrument and test failure paths thoroughly.

---

### 14. Explain the Saga pattern (orchestration vs choreography).

> A Saga is a sequence of local transactions where failures are handled by compensating transactions; orchestration uses
> a central coordinator, choreography uses events.

- **Orchestration**
    - Central Saga orchestrator tells services what to do next.
    - Easier to reason and observe (single place for workflow logic).
- **Choreography**
    - Services publish and subscribe to events to advance the workflow.
    - Decentralized and more loosely coupled, but can be harder to trace and reason about.
- **Compensation**
    - Each local transaction has an undo/compensating action if the saga fails.
- **Reliability**
    - Use durable messaging, idempotent handlers, and persistent saga state.

> Orchestration centralizes flow control (state machine, retry/backoff), reducing accidental coupling. Choreography
> leverages event-driven flow and is more resilient to coordinator failure but requires well-defined event contracts and
> observability.
> Use sagas to manage long-running multi-service business processes: choose orchestration when you need explicit control
> and observability; choose choreography for high looser-coupled, scalable flows. Always design compensations,
> idempotence, and durable state for reliability.

---

### 15. What is CQRS and Event Sourcing? When should you use them?

> CQRS separates reads from writes; Event Sourcing stores state changes as events instead of mutating snapshots. Use
> them when domain complexity, performance, or auditability benefits outweigh added complexity.

- **CQRS**
    - Read model optimized for queries; write model handles commands and validation.
    - Useful when read and write workloads differ or when complex read shapes are required.
- **Event Sourcing**
    - System state is the replay of ordered events; great for auditing, debugging, and temporal queries.
    - Requires event schemas, migration strategy, and snapshotting for performance.
- **When to use**
    - High-complexity domains, audit/tracing requirements, or where rebuilding state from events is valuable.
    - Avoid for simple CRUD systems due to operational overhead.

> Event sourcing changes how you reason about state: debugging and replay are powerful but require careful event
> versioning, tooling, and storage design. JVM systems must tune serialization (Avro/Protobuf) and snapshot frequency to
> avoid long replays.
> Use CQRS + Event Sourcing for complex domains needing auditability, temporal queries, or optimized read models. For
> most CRUD services, traditional models are simpler and more maintainable.

---

### 16. How do you handle inter-service communication (REST vs gRPC vs asynchronous messaging)?

> Choose based on latency, payload, schema needs, and coupling: REST/gRPC for synchronous calls, async messaging for
> loose coupling and eventual consistency.

- **REST (HTTP/JSON)**
    - Human-readable, universal, easy for browsers and third parties.
    - Higher serialization cost and less strict schema.
- **gRPC**
    - Binary, strongly-typed (Protobuf), low latency, streaming support.
    - Good for internal high-performance service-to-service calls.
- **Asynchronous messaging**
    - Kafka/RabbitMQ/Pulsar for events/commands, decouples producers and consumers.
    - Good for durability, buffering, and scaling; enables eventual consistency.
- **Hybrid**
    - Use synchronous calls for simple request/response; async for long-running or high-throughput flows.
- **Contracts**
    - Use schema/IDL (OpenAPI, Protobuf) and strict versioning for compatibility.

> gRPC provides built-in flow control and deadlines; REST is ubiquitous and easier to cache. Messaging introduces
> at-least-once semantics; developers must handle idempotence and ordering on the JVM.
>
> Match the communication style to the problem: use REST or gRPC for direct queries/commands with low fan-out; use
> messaging for events, decoupling, and resilience. Always define schemas, retries, timeouts, and idempotent handlers.

---

### 17. What are the trade-offs between synchronous and asynchronous communication?

> Synchronous offers immediate response and simpler control flow; asynchronous gives resilience, scalability, and
> decoupling at the cost of increased complexity and eventual consistency.

- **Synchronous**
    - Simpler to reason about (request → response).
    - Tighter coupling and increased latency across call chains.
    - Risk of cascading failures and blocking resources.
- **Asynchronous**
    - Improves availability and decouples components.
    - Supports buffering and better throughput under load.
    - Requires handling eventual consistency, ordering, and retries.
- **Operational**
    - Async requires durable infrastructure, monitoring, and replay strategies.
    - Synchronous needs strict timeout and circuit-breaker configuration.

> Synchronous calls are simpler but fragile at scale; asynchronous flows shift complexity to messaging and eventual
> consistency management, which is safer for high-scale, fault-tolerant systems.
>
> Choose sync for immediate user interactions and simple flows; choose async for high-throughput, long-running, or
> decoupled workflows, and design compensations and observability accordingly.

---

### 18. What is event-driven architecture and how does Kafka/RabbitMQ/Pulsar fit in?

> Event-driven architecture uses events to communicate state changes; Kafka/RabbitMQ/Pulsar are messaging platforms that
> enable reliable event distribution.

- **Event-driven principles**
    - Services emit events when state changes; other services react asynchronously.
    - Enables loose coupling, scalability, and temporal decoupling.
- **Kafka**
    - High-throughput, partitioned commit-log; great for event streams, replay, and durable storage.
    - Strong ordering per partition and consumer group model.
- **RabbitMQ**
    - Message broker with flexible routing (exchanges/queues); good for task queues and complex routing.
    - Focused on at-most-once/at-least-once delivery depending on configuration.
- **Pulsar**
    - Combines messaging and streaming with multi-tenancy and tiered storage; supports event streaming semantics and
      topic-based models.
- **Design**
    - Use schema registries (Avro/Protobuf), idempotence, consumer offsets, and monitoring.

> Kafka is optimized for streaming and replay, RabbitMQ for flexible routing and low-latency queueing, and Pulsar for
> hybrid streaming+queueing with built-in multi-tenancy. JVM services must handle consumer groups, offset commits, and
> message serialization.
> Use an event-driven approach when you need decoupling, scalability, or auditability: pick Kafka for stream processing
> and replayability, RabbitMQ for task/work queues and flexible routing, or Pulsar for multi-tenant streaming at scale.

---

### 19. How do you version APIs in microservices?

> Version APIs explicitly and evolve with backward-compatible changes first; use semantic versioning, contract-first
> design, and deprecation policies.

- **Versioning strategies**
    - URL versioning (`/v1/orders`) — simple and explicit.
    - Header versioning (custom or `Accept` media type) — more flexible for clients.
    - Content negotiation — uses MIME types to signal versions.
    - Schema evolution (Protobuf/gRPC) — keep backward/forward-compatible field rules.
- **Compatibility rules**
    - Additive changes (new optional fields) are safe.
    - Non-additive changes (remove/rename required fields) need new versions.
- **Practical practices**
    - Prefer backward-compatible changes and blue-green or canary deployments.
    - Maintain clear deprecation timelines and automated tests for contract compatibility.
    - Use API Gateway to route versions and transform requests when necessary.
- **Testing & tooling**
    - Use contract tests (PACT), CI checks, and API docs (OpenAPI) to ensure compatibility.

> For gRPC/Protobuf, follow field numbering and reserved ranges to maintain schema compatibility. For REST, design
> resources and payloads conservatively and validate backward compatibility via contract tests.
>
> Version deliberately: prefer schema evolution and consumer-driven contract testing to minimize breaking changes. When
> breaking changes are unavoidable, publish a new version, route via API Gateway, and communicate a clear deprecation
> schedule.

---

### 20. How do you perform end-to-end testing in a microservices environment?

> End-to-end (E2E) testing verifies that multiple services work together correctly under realistic conditions.

- Use a stable test environment with real or containerized services (Docker Compose, Testcontainers).
- Test full flows: REST APIs, messaging, database, cache, and external integrations.
- Prefer contract tests to reduce the need for heavy E2E tests.
- Use synthetic test data and reset environments using tools like Testcontainers or ephemeral Kubernetes namespaces.
- Integrate distributed tracing (Sleuth/Zipkin/OpenTelemetry) to follow requests across services.

> Because microservices include asynchronous events, queues, and distributed transactions, E2E tests must handle delays,
> retries, and eventual consistency — often requiring polling or waiting for message consumption.
>
> Use E2E tests sparingly: rely on unit tests and contract tests for speed, but run E2E tests to confirm cross-service
> workflows, event processing, and real data flows in a near-production environment.

---

### 21. What is the strangler fig pattern for migrating from monolith to microservices?

> The strangler fig pattern gradually replaces parts of a monolith by routing specific features to new microservices.

- Introduce an API Gateway or reverse proxy.
- Route certain endpoints/features to the new microservices instead of the monolith.
- Move functionality piece-by-piece until the old logic is “strangled” and removed.
- Minimize risk by avoiding big-bang rewrites.

> This pattern allows independent rollout, rollback, and monitoring of new microservices without touching the rest of
> the monolith.
>
> The strangler fig pattern reduces migration risk by slowly replacing monolith functionality, using controlled routing
> to shift traffic and validating new microservices step by step.

---

### 22. How do you manage shared databases vs database per service?

> Each microservice should own its own database to avoid tight coupling and shared schema constraints.

- **Database per service**
    - Strong independence, faster releases.
    - Allows schema changes without affecting others.
    - Encourages clear domain boundaries and bounded contexts.
- **Shared database**
    - Creates strong coupling; schema changes risk breaking multiple services.
    - Harder to enforce domain boundaries.
    - Sometimes used temporarily during migration.
- Best practices:
    - Use asynchronous events instead of cross-service joins.
    - Use API calls instead of reading another service’s tables.
    - Use the Outbox Pattern to publish domain events reliably.

> JVM-based services using shared DBs often become “distributed monoliths” — tight couplings remain though services are
> split. Database per service avoids this but requires event-driven integration.
>
> Prefer database per service for true autonomy. If a shared DB is needed temporarily, treat it as a transitional step
> and plan to move toward independent data ownership.

---

### 23. What is polyglot persistence and its implications?

> Polyglot persistence means using different types of databases for different services based on their needs.

- Allows choosing the best storage type (SQL, NoSQL, key/value, document, graph).
- Supports specialized use cases (e.g., Elasticsearch for search, Redis for caching).
- Offers better performance and flexibility.
- Adds complexity: more operational overhead, monitoring, backups, and expertise.
- Requires strong data governance and schema evolution strategy.

> Java microservices often combine PostgreSQL for OLTP, MongoDB for documents, Redis for caching, and Kafka for event
> logs — but each adds operational and cognitive load.
>
> Polyglot persistence gives each service optimal storage but increases operational complexity, requiring disciplined
> DevOps, strong observability, and clear ownership.

---

### 24. Explain the role of Spring Boot and Spring Cloud in Java microservices.

> Spring Boot simplifies building standalone microservices; Spring Cloud adds tools for distributed systems (config,
> discovery, resilience).

- **Spring Boot**
    - Auto-configures web servers, data access, metrics, and security.
    - Easy to package as light microservices with minimal boilerplate.
- **Spring Cloud**
    - Adds distributed system features: config management, discovery, routing, tracing, and resilience.
    - Works well with cloud platforms (Kubernetes, AWS, GCP).
- **Benefits**
    - Fast development, strong ecosystem, production-ready features.
    - Integrates with Resilience4j, Sleuth, Zipkin, OpenFeign, and Spring Cloud Gateway.

> Spring Boot handles local concerns (web, data, metrics), while Spring Cloud handles cross-service concerns (discovery,
> config, tracing). Together they provide a complete microservice stack for JVM teams.
>
> Spring Boot builds the microservice itself, while Spring Cloud provides essential cloud-native patterns — making them
> the default choice for Java microservice development.

---

### 25. What are the key Spring Cloud components (Config Server, Sleuth, Zipkin, Gateway, OpenFeign, Resilience4j)?

> Spring Cloud offers core components for configuration, routing, tracing, client calls, and resilience.

- **Config Server**
    - Centralized external configuration (Git-based).
    - Allows dynamic refresh and environment separation.
- **Spring Cloud Sleuth**
    - Adds trace IDs, span IDs, and propagation for distributed tracing.
    - Integrates with Zipkin/OpenTelemetry.
- **Zipkin (Deprecated)**
    - Distributed tracing UI for visualizing latency and service calls.
    - Helps debug slow or failing service interactions.
- **Spring Cloud Gateway**
    - API Gateway with routing, filters, rate limiting, and auth integration.
    - Lightweight and reactive.
- **OpenFeign**
    - Declarative HTTP client with interface-based REST calls.
    - Integrates with discovery, load balancing, and resilience.
- **Resilience4j**
    - Circuit breakers, retries, timeouts, bulkheads, rate limiters.
    - Works with reactive and blocking code.

> These Spring Cloud components solve the main challenges of distributed systems: configuration, communication, routing,
> tracing, and resilience — all integrated with Spring Boot.
>
> Spring Cloud provides the essential building blocks for stable, observable, and resilient microservices, including
> configuration, discovery, routing, client abstraction, and fault tolerance.

---

### 26. How does Spring Cloud Config work for centralized configuration?

> Spring Cloud Config provides one central place for storing and delivering configuration to all microservices.

- Configuration is stored in a Git repo (preferred), filesystem, or Vault.
- A **Config Server** reads the configuration and exposes it through REST endpoints.
- Microservices (Config Clients) load configuration during startup or via `/actuator/refresh`.
- Supports profiles (dev/test/prod), versioning, encryption of secrets, and rollback.
- Reduces duplication, keeps services lightweight, and makes configuration changes safer.

> Spring Cloud Config removes the need to rebuild or redeploy services when configuration changes — only the config repo
> needs updates.
>
> The Config Server pulls configuration from a central source and each microservice fetches the values on startup or
> refresh, ensuring consistency across environments.

---

### 27. What is distributed tracing and how do you implement it (Zipkin, Jaeger, OpenTelemetry)?

> Distributed tracing helps track a single request as it flows through many microservices.

- Each request gets a **trace ID** and each step is a **span**.
- The trace ID moves across services via HTTP headers or message metadata.
- Helps find slow services, errors, bottlenecks, and latency issues.

**Tools:**

- **Zipkin** — lightweight, easy integration with Spring Cloud Sleuth.
- **Jaeger** — CNCF project, high-performance, works well with Kubernetes.
- **OpenTelemetry** — open standard for instrumentation; exporters can send data to Zipkin/Jaeger.

**Implementation steps (Spring Boot):**

1. Add Spring Cloud Sleuth or OpenTelemetry instrumentation libraries.
2. Services automatically generate trace IDs and spans.
3. Deploy Zipkin/Jaeger collector + UI.
4. View traces to understand delays, failures, and dependencies.

> Distributed tracing gives you observability across microservices, showing the whole request path and making debugging
> much easier.
>
> Use instrumentation (Sleuth or OpenTelemetry) to generate trace IDs and forward them to Zipkin or Jaeger, where you
> can analyze latency and service interactions.

---

### 28. How do you secure microservices (OAuth2, JWT, mTLS)?

> Microservice security protects communication, identities, and access between clients and services.

**Key techniques:**

- **OAuth2**
    - Provides delegated authorization.
    - Often used with an Authorization Server (Keycloak, Auth0, AWS Cognito).
    - Microservices validate access tokens from clients.

- **JWT (JSON Web Token)**
    - Self-contained token containing user identity and roles.
    - Services verify the signature without calling a central auth service.
    - Works well for stateless microservices.

- **mTLS (Mutual TLS)**
    - Both client and server present certificates.
    - Ensures strong service-to-service authentication.
    - Often used inside a service mesh for zero-trust networks.

**Best practices:**

- Put auth at the Gateway.
- Validate tokens inside each service.
- Use short-lived tokens and refresh tokens.
- Protect internal traffic using mTLS.

> OAuth2 handles user authorization, JWT enables stateless validation, and mTLS secures service-to-service
> communication — together forming a robust security model.
>
> Combine OAuth2 + JWT for user access and mTLS for internal service identity to create a zero-trust microservice
> environment.

---

### 29. What is the difference between authentication and authorization in microservices?

> Authentication verifies **who** a user or service is; authorization controls **what** they can access.

- **Authentication**
    - Confirms identity.
    - Uses credentials, tokens, certificates.
    - Example: Logging in or validating a JWT.

- **Authorization**
    - Determines permissions.
    - Defines allowed actions or resources.
    - Example: Admin can delete a user, normal user cannot.

In microservices:

- Authentication often happens at the API Gateway or Authorization Server.
- Authorization checks happen inside each microservice.

> Authentication identifies the caller; authorization determines their rights within the system.
>
> AuthN proves identity, AuthZ controls permissions — both are critical in distributed architectures.

---

### 30. Explain service mesh (Istio, Linkerd) and its benefits.

> A service mesh manages communication between microservices using sidecar proxies instead of application code.

**Key features:**

- mTLS for secure service-to-service communication.
- Traffic control (routing, retries, timeouts).
- Observability: metrics, logs, tracing.
- Circuit breakers and rate limiting.
- Blue/green and canary deployments.

**Popular meshes:**

- **Istio** — very powerful, rich features, works well with Kubernetes.
- **Linkerd** — lighter, simpler, built for reliability.

> A service mesh moves complex networking concerns out of your application code and into an infrastructure layer.
>
> With a mesh, you get security, traffic control, and observability “for free” without changing your Java microservice
> code.

---

### 31. What problems does a service mesh solve that Spring Cloud doesn’t?

> Spring Cloud solves app-level concerns; a service mesh solves infrastructure-level concerns.

**Service Mesh Capabilities (not handled well by Spring Cloud):**

- mTLS enforcement between all services automatically.
- Zero-trust networking without modifying application code.
- Traffic shadowing, fault injection, and advanced routing.
- Global, centralized policies across all services (e.g., retries, timeouts).
- Sidecar proxies handle cross-language communication (polyglot support).
- Infrastructure-powered observability (Envoy proxies collect metrics & traces).

**Spring Cloud Limitations:**

- Only works well for JVM services.
- Requires code changes for resilience, tracing, routing.
- Does not provide built-in mTLS.
- Struggles with polyglot microservice environments.

> Spring Cloud is powerful for Java-based applications, but a service mesh gives consistent security, traffic control,
> and observability for **any** language with **no code changes**.
>
> A service mesh covers infrastructure-level networking features (mTLS, traffic control, advanced policies), while
> Spring Cloud covers application-level patterns — together they complement each other.

---

### 32. How do you handle logging in a distributed microservices system?

> Use structured, correlated, and centralized logging with trace IDs and contextual fields to enable cross-service
> diagnostics.

- Emit structured logs (JSON) with stable fields: timestamp, level, service, instance-id, trace-id, span-id, user-id,
  request-id, and relevant domain fields.
- Propagate correlation IDs (trace-id / span-id) from the entry point (API Gateway) through all calls; use MDC (Mapped
  Diagnostic Context) in Java to attach these to every log line.
- Centralize logs with a log shipper (Filebeat/Fluentd) into a storage/analysis system (ELK/Opensearch, Loki, or cloud
  logging).
- Enrich logs with relevant domain/contextual values, avoid logging secrets, and set consistent retention and indexing
  strategies.
- Use sampling for high-volume traces/logs to control cost; keep full logs for errors and important transactions.
- Implement log-level strategies (info for normal ops, debug for development only) and have runtime toggles for
  increased verbosity.

> Correlated structured logs plus distributed trace IDs are essential: on the JVM use MDC to store trace/request IDs,
> ensure async frameworks preserve MDC (or use instrumentation that propagates context), and ship logs to a centralized
> store where queries can join logs with traces.
>
> Centralized, structured logging with propagated trace/request IDs and contextual fields is the backbone of
> diagnosability in microservices. Use MDC for per-request context, ship logs to a central store, and link logs to
> traces
> and metrics for fast root-cause analysis.

---

### 33. What are common anti-patterns in microservices (distributed monolith, too fine-grained services)?

> Common anti-patterns include splitting services incorrectly (too fine-grained) and keeping strong runtime coupling (
> distributed monolith).

- **Distributed monolith**
    - Services are deployed separately but remain tightly coupled (shared DB, synchronous chatty calls, coordinated
      deployments).
    - Results: fragility, slow deployments, and poor resilience.
- **Too fine-grained services**
    - Excessive network hops, high operational cost, and orchestration complexity.
    - Leads to high latencies and debugging difficulty.
- **Shared database across services**
    - Creates schema coupling and blocks independent evolution.
- **Anemic services**
    - Services that are only thin RPC wrappers with domain logic still centralized—leads to duplication and coupling.
- **Lack of ownership**
    - No clear service/team ownership causes slow changes and poor responsibility for operability.
- **Ignoring observability/security**
    - No tracing, metrics, or auth by default leads to unmanageable systems.

> These anti-patterns often stem from incorrect decomposition, lack of DDD, or immature DevOps. The JVM ecosystem
> amplifies issues when blocking threads and shared pools are exhausted by chatty sync calls across services.
>
> Avoid anti-patterns by designing service boundaries around bounded contexts, owning data per service, reducing
> synchronous chatty calls, and creating clear team ownership. Balance the number of services against operational
> capacity — prefer slightly coarser-grained services that are cohesive and independently deployable.

---

### 34. How do you monitor microservices (metrics, health checks, dashboards - Prometheus + Grafana)?

> Monitor via application metrics, health checks, logs, and dashboards; use Prometheus to collect metrics and Grafana to
> visualize them.

- Expose application metrics (latency, error rates, throughput, resource usage) using Micrometer for Spring Boot (
  Micrometer bridges to Prometheus).
- Provide health endpoints (`/actuator/health`) with readiness/liveness probes for orchestrators (Kubernetes).
- Use Prometheus to scrape metrics, set alerting rules for SLO breaches, and store time-series data.
- Build Grafana dashboards for service-level, business-level, and system-level views (SLO-based dashboards).
- Configure alerting on error rates, latency P95/P99, saturations (CPU, heap, thread pools), and queue lengths.
- Use synthetic and real traffic tests, and correlate metrics with logs and traces for deeper analysis.

> Micrometer standardizes metric names and tags for JVM apps; Prometheus scrape model fits well with ephemeral
> containers. Instrument thread pools, connection pools, and JVM internals (GC, memory) to catch resource issues early.
>
> Combine metrics (Prometheus), dashboards (Grafana), health checks (Kubernetes Actuator), and alerts to detect and act
> on problems quickly. Correlate metrics with logs and traces to move from detection to diagnosis and resolution.

---

### 35. What is observability and the three pillars (logs, metrics, traces)?

> Observability is the ability to understand system behavior from external outputs; its three pillars are logs, metrics,
> and traces.

- **Metrics**
    - Aggregated numeric data points over time (latency percentiles, QPS, error rates).
    - Good for alerting and SLO monitoring.
- **Logs**
    - Detailed event records for specific events, errors, and context.
    - Useful for forensic analysis and debugging.
- **Traces**
    - Distributed traces show request flow across services, timings per span, and where time is spent.
    - Useful for performance debugging and dependency analysis.
- Observability requires instrumentation, correlation (trace-id), good metadata, and tooling to query across pillars.

> The three pillars complement each other: metrics show that something is wrong, traces show where in the call path the
> problem occurs, and logs provide detailed context to diagnose the root cause.
>
> Instrument services to emit high-quality metrics, structured logs, and trace spans with shared identifiers. Use
> tools (Prometheus, Grafana, Zipkin/Jaeger/OpenTelemetry, ELK/Loki) to link the pillars and enable fast detection and
> triage.

---

### 36. How do you handle schema evolution in event-driven systems?

> Manage schema changes with backward/forward compatibility rules, schema registry, and versioning strategies (additive
> changes only when possible).

- Use a schema registry (Avro/Confluent Schema Registry, Protobuf with tooling) to store, validate, and evolve event
  schemas.
- Prefer additive changes: add optional fields with defaults, avoid removing or renaming fields without a migration
  plan.
- Use explicit versioning when incompatible changes are required (topic per version or version field in payload).
- Implement consumers that are resilient: tolerate unknown fields and missing fields with defaults.
- For breaking changes, apply staged migration: write side-by-side producers, dual-write, or use the strangler-like
  approach for event schemas.
- Employ the Outbox pattern to guarantee consistency when writing events and DB updates.

> Schema registries help enforce compatibility checks at producer time; producers should refuse incompatible schema
> updates. On the JVM, use generated classes (Avro/Protobuf) carefully and include transformers to handle old/new event
> shapes.
>
> Use schema registries, follow compatibility rules, prefer additive changes, and plan migrations for incompatible
> changes. Consumers should be tolerant and producers should validate schemas to prevent runtime failures.

---

### 37. What is the difference between idempotency and exactly-once semantics?

> Idempotency ensures repeated operations have the same effect as one execution; exactly-once guarantees a single effect
> even with retries — which is hard to achieve in distributed systems.

- **Idempotency**
    - Designed at the application level: use idempotency keys, unique request IDs, or deduplication stores.
    - Common pattern for REST/command endpoints and message consumers (store processed message IDs).
    - Guarantees no duplicate side-effects if the same request is applied multiple times.
- **Exactly-once**
    - Stronger: end-to-end single effect even with retries and failures.
    - Requires coordinated support from messaging system and storage (transactional producers/consumers, idempotent
      writes).
    - Often approximated in practice (e.g., Kafka's exactly-once semantics with transactions), but still requires
      careful app design.
- **Trade-offs**
    - Exactly-once is expensive and complex; idempotency + at-least-once delivery is pragmatic and common.

> On the JVM, implement idempotency via unique keys in DB transactions or dedup tables. For messaging, use transactional
> outbox + idempotent consumer logic or Kafka transactions to approach exactly-once.
>
> Prefer idempotent operations as a design principle — it is simpler and robust. Use system-level features (e.g., Kafka
> transactions) to get closer to exactly-once when business needs and cost justify the complexity.

---

### 38. How do you implement rate limiting and throttling in microservices?

> Use token-bucket or leaky-bucket algorithms enforced at the gateway or at service edge to protect resources; apply
> quotas and per-caller limits.

- Implement rate limiting at the API Gateway or edge proxy (Envoy, API Gateway) to stop abusive or excessive traffic
  early.
- Use distributed algorithms (Redis-backed token bucket, Bucket4j, or Envoy rate limiting service) for horizontal
  scalability.
- Distinguish between global limits, per-client/user limits, per-API limits, and dynamic quotas tied to subscriptions or
  SLOs.
- Apply throttling (gradual slowing) and hard limits (reject with 429). Return standard headers (Retry-After,
  X-RateLimit-*) to inform clients.
- Integrate with auth to provide per-user or per-tenant limits and use circuit breakers and backpressure downstream.

> Implement rate limiting near the edge for best effect; for critical internal paths, add service-level limits to avoid
> noisy neighbors. Use Redis or token-bucket libraries for distributed state and resilience.
>
> Protect services by applying rate limits at the gateway and service edge, using distributed token buckets for
> horizontal scale, and exposing clear rate-limit headers and policies. Combine with throttling and circuit breakers for
> graceful degradation.

---

### 39. What is backpressure and how do you handle it (especially with reactive streams)?

> Backpressure is the mechanism to control the flow of data so consumers are not overwhelmed by producers; reactive
> streams provide built-in backpressure support.

- Reactive libraries (Project Reactor, RxJava) implement the Reactive Streams protocol with `Publisher`, `Subscriber`,
  and demand signals (`request(n)`).
- Use bounded buffers, windowing, and rate-limiting operators (`onBackpressureBuffer`, `onBackpressureDrop`,
  `limitRate`) to control memory and latency.
- Prefer non-blocking approaches: avoid blocking thread pools that can be exhausted; use asynchronous processing with
  bounded concurrency.
- Apply end-to-end flow-control: when downstream is slow, propagate backpressure signals upstream (or apply buffering
  with limits and fallbacks).
- Combine with circuit breakers and bulkheads: when backpressure indicates overload, degrade gracefully (e.g., return
  503, serve cached responses).

> Reactive streams give a formal way to signal demand; on the JVM, use Reactor/Netty/gRPC with backpressure-aware
> operators and avoid unbounded buffering which causes OOM and latency spikes.
>
> Handle backpressure by designing flow-control from source to sink: use reactive streams’ demand signals, bounded
> buffers, drop/overflow strategies, and graceful degradation. This keeps systems responsive and prevents resource
> exhaustion under load.

---

### 40. What is blue-green deployment and canary release in microservices context?

> Blue-green deploys two identical environments and switches traffic between them; canary releases roll out changes to a
> small subset of users before full rollout.

- **Blue-green**
    - Maintain two environments (blue = current, green = new).
    - Deploy the new version to green, run smoke tests, then switch router/load balancer to green.
    - Easy rollback by switching back to blue if issues appear.
    - Good for zero-downtime and quick rollback, but needs double capacity.
- **Canary**
    - Deploy new version to a small percentage of traffic or a subset of instances.
    - Monitor metrics (errors, latency, business KPIs) during the canary window.
    - Gradually increase exposure if healthy; roll back if problems surface.
    - Safer for incremental risk and real-user validation, but needs careful automation and monitoring.

> At runtime, JVM-related concerns include warm-up (JIT), classloading, and JVM heap sizing — canaries reveal
> performance differences from JIT and GC behavior that don’t appear in unit tests. Use health checks and JVM metrics (GC
> pause, CPU, thread counts) as part of canary gating.
> 
> Use blue-green when you want an immediate full switch and fast rollback; use canaries for gradual validation and safer
> risk management. In both cases automate traffic switching, monitoring, and rollback, and include JVM-level signals (GC,
> CPU, internal metrics) in your acceptance criteria.

---

### 41. How do you manage secrets in microservices (Vault, Kubernetes secrets, AWS Secrets Manager)?

> Store secrets in a secure secret store and avoid hardcoding them; use short-lived credentials and principle of least
> privilege.

- Options:
    - **HashiCorp Vault** — dynamic secrets, lease/renewal, secret rotation, policies.
    - **Kubernetes Secrets** — native to k8s; use encryption at rest and RBAC; better used with a secrets provider for
      production.
    - **Cloud secret managers** (AWS Secrets Manager, GCP Secret Manager, Azure Key Vault) — managed rotation, IAM
      integration, audit logs.
- Best practices:
    - Do not store secrets in code or config repos.
    - Use short-lived credentials and automatic rotation when possible.
    - Provide services with least-privilege access via IAM or Vault policies.
    - Audit access and enable encryption in transit and at rest.
    - Inject secrets at runtime (environment variables, mounted volumes, or sidecar fetchers), and avoid logging them.
- Operational notes:
    - Provide fallback and bootstrapping options (e.g., initial bootstrap token).
    - Use cache with TTL to reduce secret-store load but honor rotation.

> JVM apps commonly use credential providers (Spring Cloud Vault, AWS SDK) to fetch secrets at startup or on-demand.
> Watch out for secret exposure in heap dumps, logs, or stack traces — clear secrets from memory after use if necessary.
> 
> Centralize secret management in a purpose-built store (Vault or cloud provider), use short-lived credentials and
> strict access policies, inject secrets at runtime, and audit usage. Combine platform-native features with
> application-layer best practices to reduce risk.

---

### 42. What is the role of container orchestration in microservices?

> Container orchestration (Kubernetes, ECS) automates deployment, scaling, service discovery, and lifecycle management
> of microservices.

- Core responsibilities:
    - Scheduling containers on cluster nodes and handling node failures.
    - Service discovery and internal DNS for inter-service communication.
    - Horizontal pod/instance autoscaling based on CPU, custom metrics, or events.
    - Rolling updates, rollbacks, and pod restarts to support zero-downtime deploys.
    - Resource isolation (CPU, memory limits), quotas, and affinity rules.
    - Health checks, readiness/liveness probes, and lifecycle hooks.
- Additional features:
    - Persistent volumes and storage orchestration.
    - Network policies and integration with service meshes.
    - Secrets and config injection and RBAC for operational control.
- Operational benefits:
    - Standardized deployment model, improved utilization, and self-healing.
    - Facilitates GitOps, declarative infrastructure, and CI/CD pipelines.

> For JVM apps, orchestration must consider startup/shutdown hooks, graceful termination (SIGTERM handling), heap/stack
> sizing, JMX/metrics exposure, and probe tuning to avoid premature restarts due to GC pauses.
> 
> Use container orchestration as the runtime control plane for microservices: it provides scheduling, scaling,
> discovery, and lifecycle tools that operationalize microservice patterns and enable resilient, observable, and
> automatable deployments.

---

### 43. How do you handle data consistency during microservice failures?

> Design for eventual consistency and use compensations, retries with idempotence, outbox patterns, and durable
> messaging to recover from partial failures.

- Techniques:
    - **Local transactions + Outbox pattern**: write DB changes and outgoing events in the same local transaction; a
      background process publishes the outbox reliably.
    - **Sagas/Compensating transactions**: implement business-level rollback steps when a multi-step process fails.
    - **Idempotent consumers & deduplication**: ensure retries do not cause duplicate side effects.
    - **Durable messaging**: use persistent brokers and retry queues to ensure messages aren’t lost during failures.
    - **Transaction boundaries & isolation**: keep transactions small and local to reduce failure blast radius.
    - **Monitoring & Alerts**: alert on outbox backlog, retry failures, or broken compensations.
- UX and API strategies:
    - Provide eventual-consistency indicators to users (processing state).
    - Offer read-after-write workarounds (read your writes from the authoritative service) when strict consistency is
      required.

> JVM processes must ensure ACID for local DB operations and make event publication reliable (outbox) because
> distributed two-phase commit is usually impractical. Also monitor JVM-level failures (OOM, long GC) that can leave local
> queues or outbox in inconsistent states and design restart-safe processors.
> 
> Expect and code for partial failure: use outbox to guarantee event publication, sagas/compensation to restore business
> invariants, idempotency to handle retries, and clear user-facing states for eventual consistency. Combine durable
> messaging and good observability to detect and recover from inconsistencies.

---

### 44. What is the 12-factor app methodology and its relevance to microservices?

> The 12-factor app is a set of best practices for building cloud-native, portable, and maintainable apps; it fits
> microservices by promoting stateless processes, config separation, and declarative operations.

- Key factors relevant to microservices:
    - **Config**: store config in the environment, not code (factor III).
    - **Dependencies**: declare and isolate dependencies (factor II).
    - **Backing services**: treat databases and services as attached resources (factor IV).
    - **Stateless processes**: processes are ephemeral and share-nothing (factor VI).
    - **Port binding**: apps expose services via port, enabling containerized deployment (factor VII).
    - **Concurrency & scaling**: scale via process model (factor VIII).
    - **Logs**: treat logs as event streams (factor XI).
    - **Dev/prod parity**: keep environments similar to reduce surprises (factor X).
- Benefits:
    - Predictable deployments, easy scaling, and compatibility with orchestration and CI/CD.
    - Encourages 12-factor apps to be composable and cloud-ready microservices.

> JVM microservices should follow 12-factor principles: externalize config, avoid in-process state, and stream logs to
> central systems. Pay attention to JVM-specific needs (heap tuning and JVM args) passed via environment/config injection.
> 
> Use the 12-factor methodology as a practical checklist for building microservices that are portable, scalable, and
> operable in cloud environments — it aligns well with containers, orchestration, and CI/CD practices.

---

### 45. How do you handle cross-cutting concerns (logging, security, validation) without code duplication?

> Centralize cross-cutting concerns with shared libraries, middleware (filters/interceptors), and platform features (API
> Gateway, service mesh) to avoid duplication.

- Patterns:
    - **Shared libraries**: provide reusable client libraries for auth, logging helpers, validation utilities, and
      metrics instrumentation (keep minimal to avoid tight coupling).
    - **Framework features**: use Spring Boot filters, interceptors, AOP, or WebFlux filters for common logic.
    - **API Gateway**: enforce authentication, rate limiting, and request validation at the edge.
    - **Service mesh**: offload mTLS, retries, and observability to sidecars without application changes.
    - **Contract & schema validation**: use OpenAPI/JSON Schema or Protobuf to auto-generate validation code and keep
      contracts authoritative.
    - **Platform policies and CI checks**: enforce static checks, security scans, and policies via CI and platform
      admission controllers.
- Trade-offs:
    - Shared libs can create coupling; keep them lightweight and stable.
    - Use infra solutions (gateway/mesh) when you need language-agnostic enforcement.

> For JVM apps, use Spring Boot auto-configuration to apply defaults and reduce per-service boilerplate. Preserve loose
> coupling by pushing non-business logic to infra layers or small, well-versioned libraries.
> 
> Implement cross-cutting concerns through a mix of small shared libraries, framework interceptors, API Gateway, and
> service mesh capabilities — choose the balance that reduces duplication while keeping services autonomous and easy to
> evolve.

---

### 46. How do you measure the success/maturity of a microservices adoption in an organization?

> Measure maturity by technical, organizational, and operational indicators: delivery speed, reliability, ownership, and
> observable metrics.

- Key indicators:
    - **Delivery metrics**: lead time for changes, deployment frequency, mean time to restore (MTTR).
    - **Operational metrics**: service-level indicators (SLI/SLA), error rates, latency P95/P99, and availability.
    - **Ownership & team structure**: teams own services end-to-end and can deploy independently.
    - **Observability & automation**: comprehensive metrics, tracing, automated tests, and CI/CD pipelines.
    - **Operational burden**: manageable number of services per team, low toil due to automation.
    - **Governance & standards**: consistent API contracts, security posture, and lifecycle policies.
    - **Business outcomes**: improved time-to-market, reduced outages, and measurable cost/efficiency gains.
- Maturity stages:
    - **Initial**: monolith + experiments, limited automation.
    - **Adopting**: multiple services, basic CI/CD, partial ownership.
    - **Mature**: autonomous teams, full automation, robust observability, and documented patterns.
    - **Optimized**: cost-aware, proactive SRE practices, and continuous improvement cycles.

> Combine qualitative signals (team autonomy, developer experience) with quantitative metrics (DORA metrics, SLOs) to
> assess maturity. Watch for anti-patterns (too many tiny services, lack of ownership) as indicators of immaturity.
> 
> Evaluate microservices success by measuring delivery speed, reliability, ownership, automation, and business impact.
> Use DORA metrics and SLO-driven monitoring plus organizational signals (clear ownership and low operational toil) to
> determine maturity and guide further improvements.
---

### 47.

>
---

### 48.

>
---

### 49.

>
---

### 50.

>
---

### 51.

>
---

### 52.

>
---

### 53.

>
---

### 54.

>
---

### 55.

>
---

### 56.

>
---

### 57.

>
---

### 58.

>
---

### 59.

>
---

### 60.

>
---

### 61.

>
---

### 62.

>
---

### 63.

>
---

### 64.

>
---

### 65.

>
---

### 66.

>
---

### 67.

>
---

### 68.

>
---

### 69.

>
---

### 70.

>
---

### 71.

>
---

### 72.

>
---

### 73.

>
---

### 74.

>
---

### 75.

>
---

### 76.

>
---

### 77.

>
---

### 78.

>
---

### 79.

>
---

### 80.

>
---

### 81.

>
---

### 82.

>
---

### 83.

>
---

### 84.

>
---

### 85.

>
---

### 86.

>
---

### 87.

>
---

### 88.

>
---

### 89.

>
---

### 90.

>
---

### 91.

>
---

### 92.

>
---

### 93.

>
---

### 94.

>
---

### 95.

>
---

### 96.

>
---

### 97.

>
---

### 98.

>
---

### 99.

>
---

### 100.

>
---