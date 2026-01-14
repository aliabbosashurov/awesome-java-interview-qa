# Spring & Spring Boot

### 1. What are the disadvantages of Jakarta EE?

> Heavyweight, container-dependent, slower development cycle, and less flexible for modern microservices.

- Requires full application servers (WildFly, WebLogic, Payara), increasing operational complexity.
- Slow startup due to container bootstrapping (CDI, JTA, JMS, JPA), making it unsuitable for serverless or ephemeral
  workloads.
- Rigid specification process slows innovation compared to community-driven frameworks.
- Historically less modular and more bloated; APIs often interdependent.
- Limited ecosystem for microservices compared to Spring (cloud integrations, observability, tooling).

> Jakarta EE containers load most subsystems eagerly at startup. This causes heavy classpath scanning, JNDI registry
> initialization, and CDI container creation, which increases memory footprint and delays readiness. The spec also
> enforces abstraction layers that prevent aggressive optimizations used by frameworks like Spring Boot or Micronaut.

> Jakarta EE provides a solid, standardized enterprise stack but remains constrained by container heaviness, slow
> innovation cycles, and insufficient cloud-native alignment. Its full-server boot process, deep abstraction layers, and
> weaker microservice tooling make it less efficient for modern distributed systems compared to lighter, modular
> frameworks.

---

### 2. Why Spring?

> Spring offers flexibility, modularity, fast development, and strong ecosystem support for modern distributed systems.

- Removes container dependency; you run applications anywhere as plain Java processes.
- Highly modular: use only what you need (Spring MVC, Data, Security, Cloud, etc.).
- Strong ecosystem with integrations for messaging, observability, cloud platforms, testing, and DevOps.
- Supports both monoliths and microservices gracefully.
- Rich extension points and customizable dependency injection model.

> Spring’s container is lightweight and built around POJO philosophy. Bean creation, lifecycle, and dependency
> resolution are managed via a flexible IoC container that loads only necessary components, improving performance and
> enabling cloud-native patterns.

> Spring became the de-facto standard because it provides a flexible, container-less, modular programming model backed
> by a huge ecosystem and rapid adoption of modern architectural patterns. It fits small services, large systems, and
> cloud-native deployments much better than traditional Jakarta EE.

---

### 3. Why was the Spring Framework developed?

> To simplify and modernize enterprise Java development, which was over-complicated under early J2EE.

- J2EE (predecessor of Jakarta EE) required heavy containers and verbose programming models (EJBs).
- Spring introduced lightweight DI, AOP, and POJO-based programming to reduce complexity.
- Allowed developers to avoid vendor lock-in and write testable business logic.
- Aimed to bring flexibility and simplicity to enterprise Java.

> Spring provided an alternative inversion-of-control container based on reflection, bean factories, and runtime
> configuration, breaking away from rigid, precompiled EJB components. This allowed developers to wire components
> dynamically and test them outside application servers.

> Spring was created to eliminate the heavy, complex, container-driven programming model of early enterprise Java. It
> introduced lightweight DI, modular design, testability, and flexibility, enabling developers to build enterprise
> applications using plain Java without relying on restrictive EJB models.

---

### 4. What are the advantages of Spring?

> Lightweight, modular, non-container dependent, and backed by a massive ecosystem.

- Dependency Injection and AOP simplify business logic and cross-cutting concerns.
- Integration modules for web, data, messaging, security, cloud, and reactive programming.
- Highly testable due to POJO-based architecture.
- Works anywhere: standalone, servlet container, cloud, Docker, Kubernetes.

> Spring’s bean lifecycle is optimized using caching, lazy initialization, reflection metadata reuse, and scoped
> proxies. These patterns reduce overhead while allowing massive extensibility through BeanPostProcessors and factory
> hooks.

> Spring enables flexible, modular, testable development with unmatched ecosystem support. Its DI container and AOP
> model allow clean design, while its integration modules make it ideal for building scalable distributed systems.

---

### 5. What is Spring Boot and why was it created?

> A convention-over-configuration framework that eliminates manual setup and simplifies creating Spring applications.

- Reduces boilerplate configuration required in classic Spring apps.
- Provides embedded servers (Tomcat, Jetty, Netty) to eliminate WAR packaging.
- Offers production-ready features: metrics, health checks, logging, and error handling.
- Uses auto-configuration to guess and configure components based on classpath.

> Spring Boot introduced an opinionated autoconfiguration engine driven by classpath scanning, conditional bean
> creation, and metadata providers. This allows runtime determination of environment and dynamic provisioning of
> components.

> Spring Boot modernizes the Spring ecosystem with auto-configuration, embedded servers, and production-ready features,
> dramatically reducing setup time and enabling fast, cloud-native development.

---

### 5.1 What is the role of SpringApplication class?

> SpringApplication bootstraps a Spring Boot application and initializes the application context.

- Creates and refreshes ApplicationContext
- Performs classpath scanning and auto-configuration
- Loads environment properties and profiles
- Registers listeners and initializers
- Starts embedded web servers if present

> SpringApplication orchestrates the entire startup lifecycle using SpringFactoriesLoader and ApplicationContextFactory.
> SpringApplication acts as the entry point and coordinator of Spring Boot’s auto-configuration model, abstracting
> complex startup logic into a predictable, extensible bootstrap process aligned with modern cloud-native applications.

---

### 6. Advantages of Spring Boot over classic Spring?

> No XML, no manual configuration, quicker startup, embedded servers, and built-in production tooling.

- Automatic bean configuration using condition evaluators.
- Zero or minimal XML; everything is annotation or convention-driven.
- Embedded Tomcat/Jetty speeds up development and deployment.
- Opinionated defaults enforce best practices.
- Actuator provides metrics, observability, and health endpoints.

> Auto-configuration relies on conditional annotations (`@ConditionalOnClass`, `@ConditionalOnMissingBean`, etc.) to
> lazily provision beans. This dramatically reduces configuration complexity and improves startup and memory efficiency.

> Spring Boot turns Spring into a highly productive, convention-oriented platform with embedded servers, smart
> auto-configuration, and built-in observability — a major advancement over manual configuration in classic Spring.

---

### 7. What is Auto-configuration in Spring Boot?

> A mechanism that automatically configures Spring beans based on classpath contents, environment, and existing bean
> definitions.

- Uses `@Configuration` classes enabled by `@EnableAutoConfiguration`.
- Registers beans only when certain conditions match.
- Reduces boilerplate: e.g., creating `DataSource`, `EntityManagerFactory`, or `WebMvcConfigurer`.

> Auto-config classes are discovered via `spring.factories` (Spring Boot ≤ 2.x) or
`META-INF/spring/org.springframework.boot.autoconfigure.AutoConfiguration.imports` (Spring Boot 3.x) and loaded early
> during application context bootstrap. Conditional evaluation uses ASM-based metadata inspection to avoid loading
> classes
> prematurely.

> Auto-configuration dynamically provisions beans by evaluating runtime conditions and classpath metadata, eliminating
> the need for manual configuration for most common infrastructure components.

---

### 8. How does `@SpringBootApplication` work internally?

> It combines `@SpringBootConfiguration`, `@EnableAutoConfiguration`, and `@ComponentScan`.

- `@SpringBootConfiguration` → marks the class as a configuration source.
- `@ComponentScan` → scans the package for Spring-managed beans.
- `@EnableAutoConfiguration` → triggers Spring Boot’s auto-config engine.

> `@EnableAutoConfiguration` imports `AutoConfigurationImportSelector`, which loads metadata from
`AutoConfiguration.imports` files, filters them based on conditions, and adds valid configurations to the application
> context during startup.

> `@SpringBootApplication` bootstraps component scanning, configuration registration, and the entire auto-configuration
> mechanism, serving as the central entry point for Spring Boot applications.

---

### 9. Role of `spring-boot-starter-*` dependencies?

> They provide curated dependency sets for specific functionalities.

- Group common dependencies into a single coordinate (e.g., `spring-boot-starter-web`).
- Enforce consistent, compatible versions via dependency management.
- Reduce manual dependency management and version conflicts.

> Spring Boot's BOM (Bill of Materials) ensures all starter dependencies are version-aligned. Starters also implicitly
> trigger auto-configurations because adding libraries to the classpath activates related conditions (e.g.,
`DispatcherServlet` config when Spring MVC is present).

> Starters provide pre-assembled, version-managed dependency bundles that simplify project setup and automatically
> activate relevant auto-configurations.

---

### 10. What is `spring.factories` and how does auto-configuration use it?

> A metadata file used to discover auto-configuration classes.

- Located under `META-INF/spring.factories` (Boot 2.x and earlier).
- Maps `EnableAutoConfiguration` to a list of auto-config classes.
- Spring Boot loads these entries and evaluates them as part of startup.

> `AutoConfigurationImportSelector` reads `spring.factories` using Spring’s `SpringFactoriesLoader`. It then
> conditionally loads classes via bytecode metadata without initializing them, enabling fast and scalable conditional
> configuration.

> `spring.factories` provides the registry for Spring Boot’s auto-configuration mechanism, enabling discovery,
> conditional loading, and efficient bootstrapping of framework components.

---

### 11. List the modules of Spring

> Core, Beans, Context, AOP, JDBC, ORM, Web, Messaging, Test, and various integration modules.
> Key Spring modules:

- **Core & Beans** – IoC container, bean lifecycle, metadata parsing.
- **Context** – application context, resource loading, environment abstraction.
- **AOP** – aspects, proxies, cross-cutting concerns.
- **Expression Language (SpEL)** – runtime expression evaluation.
- **JDBC & Tx** – JDBC template, transaction abstraction.
- **ORM** – integrations with JPA, Hibernate, MyBatis.
- **Web MVC & WebFlux** – Servlet-based and reactive web stacks.
- **Messaging** – integration with STOMP, WebSocket, message channels.
- **Test** – Spring TestContext framework, test utilities.

> Spring’s architecture is built around layered containers and BeanFactory post-processing, making modules loosely
> coupled
> but highly integrable.

> Spring consists of modular components such as Core, Beans, Context, AOP, JDBC, ORM, Web MVC, WebFlux, Messaging, and
> Test, which together provide a full-stack enterprise application framework.

---

### 12. What is IoC?

> Inversion of Control is a principle where object creation and dependency management are delegated to a container, not
> done manually.


> IoC reverses the traditional flow: instead of components constructing their dependencies, the framework injects them.
> This improves decoupling, testability, and modularity.

> The IoC container parses metadata (annotations, XML), builds dependency graphs, resolves constructor-setter-field
> dependencies, and orchestrates initialization phases using BeanPostProcessors.

> IoC shifts control of object creation and wiring from application code to the container, enabling cleaner design,
> easier
> testing, and more flexible dependency management.

---

### 13. What is the purpose of IoC?

> To decouple components and centralize dependency management.

- Prevents hard-coded object creation (`new`).
- Encourages interface-driven design.
- Enables consistent lifecycle and configuration management.
- Simplifies mocking and testing.

> IoC facilitates dependency graphs managed by the container, allowing cross-cutting behaviors (AOP, scopes, proxying)
> to
> be applied transparently.

> The purpose of IoC is to reduce coupling, increase flexibility, and provide centralized, controllable object lifecycle
> and dependency management.

---

### 14. What is DI?

> Dependency Injection is the concrete implementation of IoC where dependencies are provided to an object externally.
> Types: constructor, setter, field.  
> The container analyzes dependencies and injects them into beans during initialization.

> DI execution involves constructor resolution, setter invocation, field reflection, circular dependency checks, and
> proxy
> creation if needed.

> DI implements IoC by supplying an object’s dependencies from the outside, improving modularity and allowing flexible
> configuration and testing.

---

### 15. What types of DI exist?

> Constructor Injection, Setter Injection, and Field Injection.

- **Constructor Injection (CI):** Dependencies are required and immutable.
- **Setter Injection (SI):** Optional or changeable dependencies.
- **Field Injection:** Direct field assignment via reflection (not recommended).

> Spring resolves constructor dependencies first, performs setter injections next, then applies BeanPostProcessors,
> followed by lifecycle callbacks.

> Constructor, setter, and field injection, each offering different levels of immutability, clarity, and
> testability.

---

### 16. What is SI?

> Setter Injection uses setter methods to provide dependencies.

- Marked with `@Autowired` on a setter method.
- Allows optional or late-bound dependencies.
- Supports reconfiguration after bean creation.

> Spring invokes setters after instantiating the bean but before post-processing and initialization callbacks.
> SI injects dependencies through setters and is useful for optional or mutable dependencies but provides weaker
> invariants than constructor injection.

---

### 17. What is CI?

> Constructor Injection provides dependencies through the constructor.

- Preferred because it ensures required dependencies are available at creation time.
- Supports immutability and makes objects more testable.
- Enforced automatically when only one constructor exists.

> Spring resolves constructor arguments using dependency graphs and will fail fast when dependencies are missing,
> preventing partially initialized beans.

> CI injects dependencies via constructors, making required dependencies explicit, immutable, and safely initialized.

---

### 17.1 Why is constructor injection preferred in Spring? Why does circular dependency fail with constructor injection but not setter injection?

> Constructor injection enforces immutability and explicit dependencies but makes circular dependencies unresolvable at
> creation time.

- Ensures all required dependencies are provided at object creation
- Makes beans immutable and easier to reason about and test
- Prevents partially initialized beans
- Encourages fail-fast behavior during context startup
- Setter injection allows bean instantiation first, then dependency wiring later

> With constructor injection, Spring must fully resolve all dependencies before instantiating a bean. Circular
> dependencies create an unsatisfiable graph, whereas setter injection allows early bean references to break the cycle.
> Constructor injection is preferred because it produces immutable, fully initialized beans and exposes design flaws
> early. Circular dependencies fail with constructor injection because Spring cannot create either bean without the
> other,
> while setter injection works due to Spring’s two-phase instantiation and early singleton exposure mechanism.


---

### 18. What is a Bean?

> A bean is an object managed by the Spring IoC container.

- Created, configured, initialized, and destroyed by the container.
- Registered via annotations (`@Component`, `@Bean`) or XML.
- Scoped (singleton, prototype, request, session, etc.).

> A bean passes through construction, dependency injection, post-processing, AOP proxying, initialization, and
> destruction
> phases inside the container.

> A bean is a fully lifecycle-managed object inside the Spring context, created and configured according to metadata
> supplied by the application.

---

### 18.1 Explain Bean Lifecycle in Spring

> The Spring bean lifecycle is the sequence of steps a bean undergoes from instantiation to destruction within the
> Spring IoC container.

<img src="/assets/spring-bean-lifecycle.jpg" alt="Spring bean scopes" height="550" width="700"/>

- **Instantiation:** The Spring container creates a new instance of the bean using constructor injection or default
  constructor.
- **Populate properties:** Spring sets the bean’s properties using dependency injection (DI).
- **Aware interfaces callback:** If the bean implements `BeanNameAware`, `BeanFactoryAware`, or
  `ApplicationContextAware`, the container injects the corresponding context information.
- **BeanPostProcessor (pre-initialization):** `postProcessBeforeInitialization` methods of registered
  `BeanPostProcessor` implementations are called.
- **Initialization:**
    - The bean’s `afterPropertiesSet()` method from `InitializingBean` is called.
    - Or a custom `init-method` is invoked if configured.
- **BeanPostProcessor (post-initialization):** `postProcessAfterInitialization` methods are called.
- **Bean is ready for use:** The bean is fully initialized and can be used by the application.
- **Destruction:**
    - For singleton beans, when the container shuts down, `DisposableBean.destroy()` or a configured `destroy-method` is
      called.
    - For prototype beans, destruction is the responsibility of the client code.

> Internally, Spring maintains a lifecycle context per bean, applying dependency injection first, then processing
> through `BeanPostProcessor` chains, allowing AOP proxies and other interceptors to wrap the bean before it is returned
> for use. Singleton beans are cached in the container, while prototype beans are created anew for each request.
> The Spring bean lifecycle ensures proper instantiation, dependency injection, initialization, optional proxying, and
> destruction hooks. Leveraging `Aware` interfaces, `BeanPostProcessor`s, and lifecycle callbacks enables advanced
> scenarios like custom initialization logic, resource management, and dynamic proxy wrapping in modern Spring
> applications.

---

### 19. What is an IoC Container?

> The component that manages beans and their dependencies.

- Reads configuration metadata.
- Instantiates and wires beans.
- Manages lifecycle hooks and scopes.
- Applies AOP proxies and post-processors.

> The container builds a dependency graph, handles circular dependency resolution, executes BeanFactoryPostProcessors,
> and
> applies proxies via CGLIB or JDK dynamic proxy.

> An IoC container orchestrates bean creation, wiring, lifecycle, scope handling, and cross-cutting functionality,
> acting
> as the core runtime engine of Spring.

---

### 19.1 When exactly does Spring choose JDK dynamic proxies vs CGLIB?

> Spring uses JDK proxies when a bean implements an interface; otherwise, it falls back to CGLIB.

- JDK dynamic proxy:
    - Requires at least one interface
    - Proxies only interface methods
    - Lower memory footprint
- CGLIB proxy:
    - Subclasses the target class
    - Required when no interface is present
    - Cannot proxy final classes or final methods
- Forced via `proxyTargetClass = true`

> Proxy choice is decided at runtime by ProxyFactory based on interfaces and configuration flags.
> By default, Spring prefers JDK proxies for simplicity and safety, switching to CGLIB only when necessary.
> Understanding this distinction is critical when dealing with class-based features like @Transactional, method
> visibility, and final methods.


---

### 20. What types of IoC Containers exist in Spring?

> BeanFactory and ApplicationContext.

- **BeanFactory:** Basic container with lazy initialization, no advanced features.
- **ApplicationContext:** Full-featured container with autowiring, AOP, events, i18n, and eager initialization.

> ApplicationContext extends BeanFactory and integrates environment abstraction, resource loading, event publishing, and
> post-processor auto-detection.

> Spring provides BeanFactory (minimal) and ApplicationContext (full-featured), with ApplicationContext being the
> standard
> for enterprise applications due to its extended capabilities.

---

### 21. How many ways are there to wire beans?

> Three main ways: annotation-based, Java-based, and XML-based wiring.

- **Annotation-based**: `@Component`, `@Autowired`, `@Qualifier`, stereotype annotations.
- **Java-based (Java Config)**: `@Configuration` + `@Bean` methods.
- **XML-based**: legacy bean definitions.  
  Internally all forms end up registering bean definitions into the same BeanFactory.

> Spring merges metadata from multiple sources (annotations, Java config, XML), normalizes them into BeanDefinition
> objects, and resolves dependencies during container startup.

> Spring supports bean wiring through annotations, Java configuration, and XML, each feeding metadata into a unified,
> centralized BeanFactory model.

---

### 21.1 How does Spring resolve circular dependencies internally?

> Spring resolves circular dependencies using early singleton exposure during the bean lifecycle.

- Bean instantiation happens before dependency injection
- Spring registers an ObjectFactory for early bean references
- Dependent beans receive a reference to an incompletely initialized bean
- Works only for singleton-scoped beans
- Not supported for constructor injection or prototype scope

> Internally, Spring uses three-level caching: singletonObjects, earlySingletonObjects, and singletonFactories to
> resolve circular references.

> Spring’s circular dependency resolution relies on exposing early references during setter-based dependency injection.
> This mechanism avoids deadlock at the cost of temporarily exposing partially constructed beans, which is why
> constructor
> injection deliberately disallows it.


---

### 22. What is the difference between @Component, @Service, @Repository, and @Controller?

> All are stereotypes of `@Component`, but serve semantic and functional roles.

- **@Component** – generic component.
- **@Service** – service-layer semantics; signals business logic.
- **@Repository** – DAO semantics; enables translation of persistence exceptions.
- **@Controller** – Spring MVC controller; enables request mapping and view handling.

> `@Repository` triggers `PersistenceExceptionTranslationPostProcessor`.  
`@Controller` is picked up by HandlerMapping infrastructure.

> All four are stereotypes of `@Component`, but `@Service`, `@Repository`, and `@Controller` convey intent and add
> layer-specific behaviors.

---

### 23. What is the difference between @Bean and @Component?

> `@Component` auto-discovers classes; `@Bean` defines methods that produce beans.

- `@Component` → classpath scanning, used for component classes.
- `@Bean` → used inside `@Configuration` classes to declare beans programmatically.
- `@Bean` allows full control over instantiation logic.

> `@Configuration` classes use CGLIB proxies so that calls to `@Bean` methods return the same singleton instance managed
> by the container.

> `@Component` marks classes for auto-detection, while `@Bean` explicitly defines bean creation logic inside
> configuration classes.

---

### 24. What is @Primary and when to use it?

> Marks a bean as the default candidate when multiple beans match a type.

- Applied when several beans implement the same interface.
- The container uses the `@Primary` bean unless a `@Qualifier` overrides it.

> During autowiring, Spring ranks candidates; `@Primary` increases priority while still allowing qualifiers to override.

> Use `@Primary` to set a default bean among multiple type-compatible beans.

---

### 25. What is the difference between @Autowired and @Qualifier annotations?

> `@Autowired` selects beans by type; `@Qualifier` refines selection by name.

- Autowiring resolves type; if multiple beans exist, ambiguity occurs.
- `@Qualifier("beanName")` specifies which bean to use.

> Resolution algorithm:

1. Match by type →
2. Filter by qualifiers →
3. Fallback to bean name if needed.

> `@Autowired` injects by type, while `@Qualifier` narrows the choice to a specific bean.

---

### 26. What is the difference between @Autowired with @Qualifier and @Inject with @Named?

> Functionally similar; `@Autowired/@Qualifier` are Spring-specific, `@Inject/@Named` come from JSR-330.

- `@Autowired` + `@Qualifier` = Spring-native DI.
- `@Inject` + `@Named` = JSR-330 standard DI.
- Behavior is almost identical in Spring.
- `@Autowired` supports required=false and constructor autowiring features.

> Spring internally supports both annotation sets by registering JSR-330 post-processors (
`AutowiredAnnotationBeanPostProcessor`).

> The difference is mostly semantic and standards-based: Spring-native vs. JSR-330. Behavior is equivalent inside
> Spring.

---

### 27. What is @Lookup annotation and how does it work?

> Injects a bean dynamically by overriding a method via runtime-generated proxy.

- Used when a singleton needs a fresh prototype instance.
- Spring creates a CGLIB subclass of your bean.
- Overrides the annotated method to return a newly fetched bean from the context.

> Spring intercepts calls to the `@Lookup` method, looks up the target bean in the BeanFactory at runtime, and injects
> it dynamically, even though the containing bean is a singleton.

> `@Lookup` enables runtime bean retrieval by creating a subclass proxy that overrides the method to fetch prototype or
> scoped beans on each call.

---

### 28. What happens if you inject a prototype bean into a singleton without @Lookup?

> The prototype is created once; the singleton always uses the same instance.

- Prototype scope only affects how many times the container creates instances.
- Singleton receives the prototype *once* during initialization.
- No new instances are created afterward.

> DI occurs at container startup; dependency resolution does not dynamically recreate prototypes unless explicitly
> requested (e.g., lookup method injection).

> The singleton will hold a single prototype instance forever, defeating the purpose of prototype scope.

---

### 29. When does init-method execute?

> After dependency injection and post-processing but before the bean is used.
> Execution order:

1. Instantiate bean
2. Inject dependencies
3. Apply BeanPostProcessors (before-init)
4. **Invoke init-method** (or `@PostConstruct`)
5. Apply BeanPostProcessors (after-init)

> The container ensures initialization happens only after full dependency graph resolution and proxy creation.

> Init methods run once the bean is fully constructed, wired, post-processed, and ready for use.

---

### 30. When does destroy-method execute?

> When the application context shuts down.

- Triggered on `context.close()` or JVM shutdown.
- Executes `@PreDestroy` or custom destroy methods.
- Applies only to singleton beans (prototypes are not managed post-initialization).

> Spring registers shutdown hooks and invokes destruction callbacks in reverse order of bean creation to avoid
> dependency issues.

> Destroy methods run during context shutdown to allow resource cleanup, connection closing, and graceful bean
> destruction.

---

### 31. What is @PostConstruct and @PreDestroy used for?

> They define lifecycle callbacks for initialization and destruction of beans.

- **@PostConstruct** runs after dependency injection and BeanPostProcessors.
- **@PreDestroy** runs during context shutdown.
- Used for resource initialization, validation, starting background tasks, releasing resources.

> Spring invokes these via `CommonAnnotationBeanPostProcessor`, integrating them into the bean lifecycle.

> @PostConstruct and @PreDestroy provide declarative lifecycle hooks for preparing and cleaning up beans managed by the
> IoC container.

---

### 32. What is a conditional bean and why is it needed?

> A bean created only if certain conditions are met.

- Uses `@Conditional` or specialized conditions (`@ConditionalOnClass`, etc.).
- Useful for environment-specific configuration, classpath-based activation, feature toggles.

> Conditions run before bean registration. They inspect environment, classpath, property values, and existing beans
> using metadata-based evaluation.

> Conditional beans allow dynamic, environment-aware bean creation, enabling flexible configuration and
> auto-configuration mechanisms.

---

### 32.1  What is @Conditional? Difference between @ConditionalOnBean and @ConditionalOnMissingBean?

> @Conditional enables conditional bean registration based on runtime state.

- @Conditional:
    - Base mechanism using Condition interface
    - Evaluated during configuration phase
- @ConditionalOnBean:
    - Registers bean only if another bean exists
- @ConditionalOnMissingBean:
    - Registers bean only if no matching bean exists
- Heavily used in Spring Boot auto-configuration

> Conditions are evaluated before bean instantiation, during configuration class parsing.
> @Conditional is the foundation of Spring Boot’s auto-configuration model. @ConditionalOnBean and
> @ConditionalOnMissingBean enable modular, override-friendly designs where user-defined beans can seamlessly replace
> framework defaults.

---

### 33. When is @PropertySource needed?

> When loading custom property files into the Spring Environment.

- Adds external `.properties` files to Spring's environment.
- Enables usage with `@Value` or configuration classes (`@ConfigurationProperties`).
- Useful for modular configs not already included by Spring Boot.

> `PropertySource` is processed by `PropertySourcesPlaceholderConfigurer`, which resolves placeholders at bean creation
> time.

> Use @PropertySource to load additional property files into Spring’s environment when they are not automatically
> handled by the framework.

---

### 34. What is BeanFactory in Spring?

> The basic IoC container responsible for creating and managing beans.

- Lazy initialization.
- Provides essential DI features.
- Does not automatically detect BeanPostProcessors or support advanced features.

> BeanFactory is the core interface implemented by DefaultListableBeanFactory, the internal engine behind all contexts.

> BeanFactory is the minimal, backbone container responsible for dependency creation and wiring.

---

### 35. What is ApplicationContext in Spring?

> A full-featured IoC container extending BeanFactory.

- Supports automatic BeanPostProcessor detection.
- Provides event publishing, i18n, environment abstraction.
- Eager initialization of singletons.
- Integrates AOP and resource loading.

> ApplicationContext wraps BeanFactory and layers multiple subsystems such as event multicaster, message source, and
> post-processor registries.

> ApplicationContext is the high-level container used in real applications, providing advanced services beyond
> dependency injection.

---

### 36. What is the difference between BeanFactory and ApplicationContext?

> BeanFactory is basic; ApplicationContext is advanced and feature-rich.

| Feature                  | BeanFactory | ApplicationContext |
|--------------------------|-------------|--------------------|
| Lazy init                | Yes         | No (eager)         |
| AOP auto-detection       | No          | Yes                |
| Event system             | No          | Yes                |
| i18n                     | No          | Yes                |
| Environment abstraction  | No          | Yes                |
| Post-processor discovery | Manual      | Automatic          |

> ApplicationContext pre-instantiates singletons and auto-registers BeanPostProcessors, enabling AOP proxies and
> lifecycle callbacks.

> BeanFactory provides minimal DI; ApplicationContext provides the complete Spring ecosystem.

---

### 37.What are all the bean scopes in Spring Boot?

> Spring Boot supports several bean scopes: Singleton, Prototype, Request, Session, Application, and WebSocket.

![Spring Bean Scopes](/assets/spring-bean-scopes.png)

- **Singleton**: Default scope. One instance per Spring container; reused everywhere.
- **Prototype**: New instance created each time it is requested from the container.
- **Request**: One instance per HTTP request; only valid in web-aware Spring contexts.
- **Session**: One instance per HTTP session; useful for session-scoped data.
- **Application**: One instance per ServletContext; shared across all requests and sessions in a web application.
- **WebSocket**: One instance per WebSocket session; used in WebSocket-based applications.

> Lifecycle differences: Singleton beans are fully managed by Spring, including initialization and destruction
> callbacks. Prototype beans are only initialized by Spring; destroy callbacks are not called. Request, Session, and
> Application scopes are managed per web context. WebSocket beans are managed per WebSocket session.
>
> Choosing scope depends on your use case: Singleton for shared stateless beans, Prototype for stateful beans,
> Request/Session/Application for web-specific scopes, and WebSocket for WebSocket session state.
---

### 38. What is lazy loading in Spring?

> A bean is created only when first requested, not at startup.

- Enabled with `@Lazy`.
- Reduces startup time.
- Useful for rarely used beans or expensive initializations.

L>azy proxies can be created so that the real bean initializes upon first method invocation.

> Lazy loading defers bean creation until needed, optimizing startup and resource usage.

---

### 39. What is circular dependency in Spring? How does Spring handle it? When does it fail?

> A cycle where Bean A depends on Bean B and Bean B depends on Bean A.

Spring resolves circular dependencies using **singleton early references**:

- Uses a three-level cache:
    - level 1: fully initialized singletons
    - level 2: early partially constructed instances
    - level 3: factory for singleton proxies
- Works only for setter/field injection.

Fails when:

- Constructor injection creates a cycle (cannot resolve).
- Proxies or scopes prevent early reference exposure.
- Circular dependency detection is disabled (Spring Boot 2.6+ default).

> Early-exposed objects allow wiring before initialization but after instantiation, which works only for non-constructor
> DI.

> Spring handles circular dependencies via early singleton references; setter-based cycles work, constructor-based
> cycles fail.

---

### 40. What is the difference between constructor injection and setter injection?

- **Constructor Injection**
    - Ensures all required dependencies are available.
    - Supports immutability.
    - Fails fast if dependencies are missing.
    - Avoids circular dependencies.

- **Setter Injection**
    - Optional or changeable dependencies.
    - Allows partial initialization.
    - Can cause circular dependency issues.

> Constructor injection integrates cleanly with modern DI patterns and is favored for thread-safe, immutable beans.

> Constructor injection gives strict, immutable dependency guarantees; setter injection is flexible but weaker and prone
> to misconfiguration.

---

### 41. What is proxying in Spring? (JDK Dynamic Proxy vs CGLIB)

> Proxying wraps a target bean with an intermediary object to apply cross-cutting behavior (AOP, transactions, security

- A proxy intercepts method calls and delegates to advice (before/after/around) or to the original implementation.
- **JDK Dynamic Proxy:** created via `java.lang.reflect.Proxy`, requires one or more interfaces; the proxy implements
  those interfaces and delegates to an `InvocationHandler`.
- **CGLIB Proxy:** generates a subclass of the concrete class at runtime and overrides methods to insert interception
  logic; does not need interfaces.
- Proxies are used for Spring AOP, `@Transactional`, `@Async`, security, and lazy-initialization scenarios.

> - JDK proxies only proxy interfaces; any call that bypasses the interface (direct class cast or self-invocation to a
    non-interface method) won’t be intercepted.

- CGLIB proxies require a default (non-final) method to override; final classes/methods cannot be proxied by
  subclassing.
- Spring decides proxy strategy based on available metadata and configuration; bytecode generation (CGLIB) is slightly
  heavier at creation time but allows richer interception semantics.

> Proxying in Spring is the runtime wrapping of beans to inject cross-cutting behavior. JDK dynamic proxies are
> interface-driven and lightweight; CGLIB proxies subclass concrete classes enabling method-level interception even when
> no interface exists. Understanding limitations (self-invocation, final methods, interface vs class calls) is essential
> when designing services that rely on AOP or transactional proxies.

---

### 42. When does Spring use CGLIB instead of JDK proxies?

> Spring uses CGLIB when there is no applicable interface to proxy or when explicitly configured to force class-based
> proxies.

- Default: if the bean implements at least one interface and proxyTargetClass is false, Spring prefers JDK proxies.
- Spring uses CGLIB when:
    - `proxyTargetClass=true` is set (`@EnableAspectJAutoProxy(proxyTargetClass=true)` or
      `spring.aop.proxy-target-class=true`).
    - The bean has no interfaces to proxy.
    - For `@Configuration` classes (Spring uses CGLIB to ensure `@Bean` methods return container-managed singletons).
- CGLIB is chosen to preserve method-level proxying when interface-based interpolation is not possible.

> Spring’s AOP infrastructure chooses proxies during `BeanPostProcessor` phase. For `@Configuration` classes, CGLIB
> proxies are mandatory because Spring must intercept method calls within the configuration class to enforce singleton
> semantics of `@Bean` methods.

> Use CGLIB when interface-based proxies are unavailable or when class-based proxies are explicitly requested. Spring
> selects strategy automatically but you can force class-based proxying where needed (e.g., configuration classes,
> no-interface beans, or when specific proxy semantics are required).

---

### 43. When and why should you use the @Value annotation in Spring?

> Use `@Value` to inject simple, often one-off values or expressions from properties, environment, or SpEL directly into
> fields or parameters.

- Typical uses: inject a single property (`@Value("${app.timeout}")`), inline SpEL expressions (
  `@Value("#{2 * T(java.lang.Integer).parseInt('${app.factor}')}")`), or bean references.
- Good for quick values or simple transformations where creating a configuration POJO would be overkill.
- Not ideal for large or hierarchical configuration groups — prefer `@ConfigurationProperties` for that.

> `@Value` is resolved by the property placeholder mechanism and can participate in refreshable contexts (with
> additional frameworks). It executes early in bean creation (placeholder resolution phase) and can combine environment
> properties with SpEL for computed defaults.

> `@Value` is a pragmatic tool for injecting single properties or computed values. For structured, validated, grouped
> configuration prefer `@ConfigurationProperties`; use `@Value` for concise, local injection of simple settings or
> expressions.

---

### 44. What is @ConfigurationProperties and how is it different from @Value?

> `@ConfigurationProperties` binds hierarchical groups of external properties into a strongly-typed POJO; `@Value`
> injects single values or expressions.

- `@ConfigurationProperties(prefix="app")` maps `app.*` properties to fields (including nested objects, lists, maps) and
  supports type conversion and validation (`@Validated`).
- `@Value` injects one-off primitives or expressions and offers no grouping, validation, or conversion beyond simple
  conversions.
- `@ConfigurationProperties` is preferable for domain-style config with many related settings and when you need
  testable, injectable config objects.

> `@ConfigurationProperties` binding happens through Spring’s `Binder` (Boot) or
`PropertySourcesPlaceholderConfigurer` (classic) allowing relaxed binding, complex types, and immutable
> constructor-based binding in modern Spring Boot. It aligns with 12-factor principles by making configuration explicit,
> typed, and testable.

> Choose `@ConfigurationProperties` for structured, validated, and testable configuration mapping. Use `@Value` for
> small, local, or computed values where a dedicated configuration class would be unnecessary overhead.

---

### 45. What is SpEL (Spring Expression Language)?

> SpEL is Spring’s expression language for evaluating expressions at runtime, enabling property access, method
> invocation, conditional logic, and bean references.

- Supports access to beans, properties, collections, operators, method calls, T(...) type references, and inline
  lists/maps.
- Used in annotation attributes, XML configuration, `Environment`-based expressions, security, and caching.
- Expressions are parsed and evaluated by `ExpressionParser` and executed in an `EvaluationContext`.

> SpEL integrates tightly with the Spring container, enabling expressions to reference beans by name, evaluate within
> the application context, and access property sources. It also supports compilation of frequently used expressions for
> better performance.
> SpEL is a powerful, integrated expression engine that allows dynamic resolution and computation of values inside
> Spring configuration and annotations, with runtime method invocation, bean access, and conditional logic.

---

### 46. In what ways can SpEL be used?

> In annotations (`@Value`, `@Cacheable`, security), XML config, programmatic evaluation, and conditional expressions.
> Common uses:

- `@Value("#{bean.method()}")` or `@Value("${prop}")` with SpEL combos.
- `@PreAuthorize("hasRole('ADMIN') and #id==principal.id")` security expressions.
- Cache keys: `@Cacheable(key="#user.id + '_' + #page")`.
- Conditional loading: `@ConditionalOnExpression("${feature.enabled:false}")`.
- Programmatically via `SpelExpressionParser` and `StandardEvaluationContext`.

> SpEL can be optimized by parsing and reusing expression instances and, when used heavily (e.g., large rule sets), can
> be compiled to improve throughput. In Spring Boot, SpEL evaluation participates in property resolution when needed.

> Use SpEL in annotations, security, cache keys, conditional configuration, and wherever runtime-evaluated expressions
> referencing the container or environment are required.

---

### 47. When is SpEL used?

> When configuration, annotations, or runtime decisions require computed values, bean references, or conditional logic
> that cannot be expressed as static properties.

- When a value depends on other beans, runtime state, or computed expressions.
- For declarative security rules, cache keys, or conditional bean creation requiring expression evaluation.
- In advanced configuration scenarios where property placeholders alone are insufficient.

> Prefer SpEL for concise inline logic; for complex rules or heavy computation, move logic to beans and call methods
> from SpEL (keeping expressions simple and maintainable).
> SpEL is appropriate when configuration needs lightweight runtime computation or context-aware decisioning; avoid
> overusing it for complex business logic.

---

### 48. What is the difference between #{...} and ${...} in SpEL?

> `${...}` resolves property placeholders from the environment; `#{...}` evaluates SpEL expressions (can call methods,
> access beans, do computations).

- `${...}` is handled by the property placeholder resolver and reads values from property sources (properties/YAML/env).
  It is not an expression language.
- `#{...}` is evaluated by the SpEL engine and can reference beans (`@beanName`), invoke methods, evaluate conditionals,
  and perform arithmetic.
- Spring typically resolves `${...}` first, then evaluates `#{...}` so you can use `${...}` inside `#{...}`.

> Using `${}` inside `#{}` allows combining static config with dynamic evaluation. Beware of evaluation ordering and
> null/absent property behavior — use defaults or conditional checks.

> Use `${}` for straightforward configuration values and `#{}` when you need computed or contextual logic in your
> configuration or annotations.

---

### 49. How does SpEL differ from OGNL and MVEL?

> SpEL is Spring-focused with tight container integration; OGNL is object-graph navigation oriented; MVEL prioritizes
> runtime performance and expression compilation.

- **SpEL:** Integrates with Spring Beans, lifecycle, and `EvaluationContext`. Supports type references, bean resolution,
  method invocation, and property access tailored for Spring.
- **OGNL:** Originally used in frameworks like Struts for object navigation; powerful for UI frameworks but not tightly
  integrated with Spring internals.
- **MVEL:** Designed for speed and embeddability; used in rule engines (Drools); supports compiling expressions to
  improve performance.
- Syntax and capabilities overlap, but SpEL’s strengths are Spring integration, security expression hooks, and
  configuration use-cases.

> SpEL is adequate for configuration and annotation-driven expressions; for ultra-high-performance or complex rule
> engines, MVEL (or compiled expression engines) may be preferable. OGNL is largely historical in modern Spring apps.

> SpEL is the natural choice inside Spring because of its integration and features; OGNL and MVEL are alternatives with
> different historical and performance trade-offs, but they are less suited for idiomatic Spring configuration.

---

### 50. For what purpose are @Configuration and @ComponentScan annotations used?

> `@Configuration` marks a class as a source of bean definitions; `@ComponentScan` instructs Spring where to discover
> component classes to register as beans.

- **@Configuration:** Declares a class that contains `@Bean` factory methods. Spring treats it specially (CGLIB proxies)
  so `@Bean` method calls return container-managed singletons. It’s a replacement for XML `<beans>` definitions.
- **@ComponentScan:** Scans the specified packages for stereotype annotations (`@Component`, `@Service`, `@Repository`,
  `@Controller`) and registers them as bean definitions. It supports include/exclude filters and base package
  configuration.

> When used together (commonly on the main application class), they bootstrap the application context: `@ComponentScan`
> populates bean definitions discovered via classpath scanning, and `@Configuration` supplies explicit programmatic
> beans.
> The interplay ensures consistent wiring and correct singleton semantics via proxying.

> `@Configuration` defines programmatic bean factories and lifecycle semantics; `@ComponentScan` automates the discovery
> of component classes. Together they form the foundation of modern Java-based Spring configuration, replacing verbose
> XML
> and enabling modular, testable application setup.

---

### 51. What is AOP?

> AOP (Aspect-Oriented Programming) modularizes cross-cutting concerns such as logging, transactions, caching, and
> security.

> AOP works by intercepting method executions using generated proxies and applying additional behavior (advice) before,
> after, or around the method call. This removes scattered boilerplate code from services and keeps business logic
> clean.
> Spring AOP is proxy-based (JDK or CGLIB); it only intercepts public methods on Spring-managed beans. Full bytecode
> weaving (AspectJ) offers deeper join point coverage.

> AOP enables isolating cross-cutting behavior in reusable components (aspects) and applying them declaratively to
> target
> methods, improving separation of concerns and maintainability.

---

### 52. In AOP terminology, what is an aspect?

> An aspect is a modular unit of cross-cutting logic.
> An aspect encapsulates pointcuts (where to intercept) and advice (what behavior to execute). Examples: logging aspect,
> transaction aspect, security aspect.

> Spring reads aspect definitions during bean post-processing and attaches advice through proxy creation using the AOP
> infrastructure.
> An aspect is the combination of interception rules and cross-cutting logic packaged as a reusable, declarative module.

---

### 53. What is a cross-cutting concern?

> A concern that affects multiple parts of the system and cannot be cleanly placed in a single module.

> Examples: logging, security, caching, transactions. These concerns would otherwise require repeated boilerplate code
> across multiple services and layers.

> AOP lets these concerns run orthogonally to business logic by weaving them at runtime.
> Cross-cutting concerns span many components; AOP centralizes them into aspects and applies them transparently to
> target methods.

---

### 54. What is the difference between AOP and OOP?

> OOP models core business logic; AOP models orthogonal behavior applied across many OOP components.

- **OOP:** organizes code via classes and inheritance.
- **AOP:** decorates OOP behavior using advice applied through proxies or weaving.
- OOP alone cannot cleanly modularize cross-cutting concerns; AOP complements OOP by injecting behavior at join points.

> AOP introduces an additional dimension of modularity beyond class hierarchies by weaving behavior into execution flow.
> OOP structures primary abstractions; AOP handles orthogonal system-wide behavior without polluting classes.

---

### 55. What is a join point?

> A join point is a specific point in program execution where AOP can intercept.

> In Spring AOP, join points are limited to **method executions** on Spring-managed beans.  
> In full AspectJ, join points include constructor calls, field access, exception handlers, etc.

> Spring uses proxying, so only external method calls on beans can be intercepted; internal self-invocations are not
> join points. A join point is the exact interception point—most commonly, a method execution in Spring.

---

### 56. What is the difference between pointcut and advice?

> Pointcut defines *where* to intervene; advice defines *what* to do.

- **Pointcut:** expression selecting join points (method patterns, annotations).
- **Advice:** logic executed at those join points (before, after, around).

> Spring combines them at runtime to configure proxies so that advice wraps target method calls.
> Pointcuts select interception targets; advice supplies the behavior executed there.

---

### 57. How many types of advice are there in Spring AOP?

> Five: Before, After Returning, After Throwing, After (finally), and Around.

- **@Before** — runs before method execution.
- **@AfterReturning** — runs when method completes successfully.
- **@AfterThrowing** — runs when method throws an exception.
- **@After** — runs regardless of outcome (finally).
- **@Around** — wraps the method; can control execution, arguments, and result.

> Around advice uses `ProceedingJoinPoint` allowing full control over invocation chain—most powerful but most invasive.
> Spring AOP provides five advice types, enabling interception at any stage of method execution.

---

### 58. How can AOP be configured using XML?

> Using `<aop:config>`, `<aop:aspect>`, `<aop:pointcut>`, and `<aop:advisor>` tags.
> XML AOP wiring typically looks like:

```xml

<aop:config>
    <aop:pointcut id="serviceOps" expression="execution(* com.app.service.*.*(..))"/>
    <aop:aspect ref="loggingAspect">
        <aop:before method="log" pointcut-ref="serviceOps"/>
    </aop:aspect>
</aop:config>
```

---

### 59. How can AOP be configured using Java?

> Annotate an @Aspect class and enable AOP with @EnableAspectJAutoProxy.

```java

@Configuration
@EnableAspectJAutoProxy
public class AppConfig {
}

@Aspect
@Component
public class LoggingAspect {
    @Before("execution(* com.app.service.*.*(..))")
    public void log() { ...}
}
// Spring scans for @Aspect classes and wires advice using the AOP infrastructure.

```

### 60. What is Spring MVC?

> A web framework based on the Model–View–Controller pattern.

> Spring MVC maps HTTP requests to controller methods, handles data binding, validation, view rendering, and REST APIs.
> It uses _DispatcherServlet_ as the front controller, routing requests through handler mappings, interceptors, argument
> resolvers, and returning responses via message converters.
> Spring MVC’s request-processing pipeline is highly extensible: custom resolvers, filters, interceptors, exception
> handlers (@ControllerAdvice), and message converters integrate seamlessly for REST and web apps.

<img src="/assets/spring-req-resp-lifecycle.JPG" height=600>
---

### 61. What are the advantages of Spring MVC over other web frameworks?

> Spring MVC offers modularity, flexibility, integration with Spring ecosystem, REST support, and testability.

- Tight integration with Spring IoC, AOP, transactions, and security.
- Supports annotation-based request mapping, flexible data binding, and validation.
- Built-in REST and content negotiation support.
- Extensible via interceptors, argument resolvers, message converters.
- Promotes testable controllers with mock frameworks.

> Unlike older frameworks (Struts, JSF), Spring MVC separates concerns cleanly, leverages dependency injection, and
> provides fine-grained control over request-processing flow.
> Spring MVC is highly modular, flexible, IoC-aware, REST-friendly, and testable, making it superior to many legacy web
> frameworks for enterprise applications.

---

### 62. What is Spring MVC built on?

> Spring MVC is built on the Servlet API and the Spring Framework core.

- Uses `javax.servlet` or `jakarta.servlet` as a base.
- Relies on Spring IoC container for bean management.
- Integrates AOP, validation, and message conversion via Spring core modules.

> DispatcherServlet acts as the front controller; Spring MVC layers such as handler mappings, controllers, and view
> resolvers operate within the servlet lifecycle.
> Spring MVC leverages the Servlet API and Spring core features to provide a flexible, IoC-aware web framework.

---

### 63. What is the Central Servlet?

> The central servlet is the core controller in Spring MVC that delegates requests to controllers and views.

- Known as `DispatcherServlet`.
- Receives all requests for a web application (via URL mapping).
- Coordinates handler mapping, execution, view resolution, and response rendering.

> Central servlet acts as the orchestration hub, enabling layered request processing, interceptors, and flexible
> controller integration.
> The central servlet is DispatcherServlet, coordinating request handling, controller invocation, and view rendering in
> Spring MVC.

---

### 64. What is DispatcherServlet?

> DispatcherServlet is the front controller of Spring MVC.

- Extends `HttpServlet`.
- Receives all incoming requests configured via `web.xml` or `ServletRegistrationBean`.
- Delegates processing to controllers, resolves views, and renders responses.
- Integrates seamlessly with Spring’s IoC container.

> DispatcherServlet uses handler mappings, handler adapters, and view resolvers to decouple request mapping from
> controller logic, enabling a flexible pipeline.
> DispatcherServlet is the central front controller orchestrating the request-processing lifecycle in Spring MVC
> applications.

---

### 65. What is the responsibility of DispatcherServlet?

> To route requests, invoke appropriate controllers, and render views.
> Responsibilities include:

- Receive HTTP requests.
- Consult handler mappings to identify the right controller.
- Invoke handler via adapter.
- Apply interceptors.
- Resolve the logical view name to a concrete view.
- Render response via view resolvers.
- Handle exceptions via configured handlers.

> DispatcherServlet centralizes cross-cutting responsibilities and decouples web-layer logic from the business layer,
> following the Front Controller pattern.

> DispatcherServlet orchestrates request routing, controller execution, view resolution, and response rendering, forming
> the core of Spring MVC’s request lifecycle.

---

### 66. What is the difference between @RestController and @Controller?

> `@RestController` combines `@Controller` and `@ResponseBody`, returning data directly; `@Controller` typically returns
> a view.

- `@Controller`: used for web pages, returns view names resolved by view resolvers.
- `@RestController`: returns JSON/XML directly, suitable for REST APIs.
- `@RestController` eliminates the need to annotate each method with `@ResponseBody`.

> Using `@RestController` simplifies REST API development, avoiding view resolution and serialization boilerplate.
> `@Controller` is for web page MVC, `@RestController` is for RESTful endpoints returning response bodies directly.

---

### 67. What is @ResponseEntity and when should you use it?

> `@ResponseEntity` represents the entire HTTP response, including status, headers, and body.

- Allows fine-grained control over HTTP responses.
- Useful for setting custom status codes, headers, or returning non-standard response formats.
- Often used in REST APIs to handle errors, content negotiation, and response metadata.

> Spring uses `HttpMessageConverters` to serialize the body of `ResponseEntity` into JSON, XML, or other formats
> depending on request headers.
> Use `ResponseEntity` when you need full control of the HTTP response, including status, headers, and body, typically
> in RESTful APIs.

---

### 68. What is the difference between @PathVariable and @RequestParam?

> `@PathVariable` extracts values from URI path segments; `@RequestParam` extracts values from query parameters.

- `@PathVariable`: `/users/{id}` → maps `id`.
- `@RequestParam`: `/users?id=123` → maps query parameter `id`.
- Both support type conversion, optional parameters, and default values.

> Path variables are used for RESTful resource identification; request parameters are for filtering, sorting, or
> optional inputs.
> `@PathVariable` binds URI template variables; `@RequestParam` binds query string or form parameters.

---

### 69. What is View Resolver?

> A View Resolver maps logical view names to actual view implementations.

- Converts controller-returned strings to JSP, Thymeleaf, or other template files.
- Common implementations: `InternalResourceViewResolver`, `ThymeleafViewResolver`.
- Supports prefix, suffix, and caching.

> View resolvers decouple controllers from concrete view technologies and allow pluggable templating engines.
> A View Resolver transforms logical view names returned by controllers into concrete views for rendering.

---

### 70. What is a Template Engine?

> A template engine generates dynamic content by merging data with templates.

- Examples: Thymeleaf, FreeMarker, Velocity.
- Supports variables, conditionals, loops, and expressions.
- Integrates with Spring MVC to render dynamic HTML pages or emails.

> Template engines separate presentation from logic, enabling maintainable and reusable views.
> A template engine dynamically renders content by processing templates with injected model data, enabling flexible and
> maintainable view rendering.

---

### 71. Describe the process of a request coming to the server and returning a web page to the client — what stages does it go through?

> The request passes through DispatcherServlet, handler mapping, controller, view resolution, and response rendering.

1. **Request received** by `DispatcherServlet`.
2. **Handler Mapping** identifies the appropriate controller based on URL.
3. **Controller** processes request, interacts with service/DAO, populates model.
4. **Handler Adapter** invokes the controller method.
5. **View Resolver** maps logical view name to template.
6. **View Rendering** merges model data into the template (Thymeleaf/JSP).
7. **Response returned** to client.

> Spring MVC decouples routing, business logic, and view rendering. Interceptors, exception resolvers, and filters can
> intervene at multiple points. DispatcherServlet orchestrates the pipeline.
> Incoming HTTP requests are handled by DispatcherServlet, routed via handler mappings to controllers, processed to
> generate models, resolved through view resolvers, rendered by templates, and returned as HTTP responses.

---

### 72. What is Thymeleaf?

> Thymeleaf is a modern server-side Java template engine for rendering HTML, XML, and text-based views.

- Supports natural templates (can be opened in browsers as static HTML).
- Fully integrated with Spring MVC.
- Provides expressions, conditional rendering, loops, internationalization, and URL resolution.

> Thymeleaf processes templates in two modes: **server mode** (dynamic rendering) and **natural mode** (templates
> readable as static HTML).
> Thymeleaf is a flexible, natural, and Spring-friendly template engine for dynamic view rendering.

---

### 73. Why is Thymeleaf used?

> For clean, maintainable HTML templates, natural templates, and seamless Spring integration.

- Eliminates mixing Java code in views.
- Supports advanced templating features: iteration, conditionals, i18n.
- Works with Spring MVC for model binding and form handling.
- Enables static prototyping for designers.

> Natural templates allow frontend developers to work with static HTML before backend integration, improving
> productivity and collaboration.
> Thymeleaf is used to create readable, maintainable, and dynamic templates, fully compatible with Spring MVC and
> natural HTML.

---

### 74. What makes Thymeleaf different from other template engines?

> It supports natural templates that render as valid HTML, enabling static preview and dynamic server-side processing.

- Can display correctly in browsers without backend rendering.
- Syntax integrates seamlessly with HTML attributes (`th:text`, `th:if`).
- Offers advanced features like URL rewriting, internationalization, fragment inclusion.
- Unlike JSP or FreeMarker, templates are designer-friendly and maintainable.

> Natural templating ensures frontend/back-end decoupling and allows static and dynamic rendering modes without altering
> template markup.
> Thymeleaf’s natural templating and HTML-friendly syntax differentiate it from other engines, facilitating maintainable
> and designer-friendly dynamic content.

---

### 75. How to integrate Thymeleaf with Spring?

> Add Thymeleaf starter dependency and configure template resolver, engine, and view resolver.

- Spring Boot: add `spring-boot-starter-thymeleaf` dependency; auto-configures resolver.
- Classic Spring MVC: define `SpringResourceTemplateResolver`, `SpringTemplateEngine`, and `ThymeleafViewResolver`
  beans.
- Map controllers to return logical view names.

> Integration allows Thymeleaf to access Spring MVC model attributes and handle form binding and URL rewriting.
> Integrate Thymeleaf via Spring Boot starter or configure template engine, resolver, and view resolver in classic
> Spring; controllers return logical view names populated with model attributes.

---

### 76. How to work with MessageSource in Thymeleaf?

> Use `MessageSource` for internationalization; access messages in templates with `#{...}` expressions.

- Configure `ReloadableResourceBundleMessageSource` bean.
- Reference messages in Thymeleaf: `<p th:text="#{welcome.message}"></p>`.
- Supports locale resolution via `LocaleResolver`.

> Thymeleaf automatically integrates with Spring’s `MessageSource`, providing context-aware i18n rendering.
> Configure a MessageSource bean and reference messages in Thymeleaf templates using `#{message.code}` for
> internationalization.

---

### 77. What are Variable Expressions (${...})?

> Used to access model attributes or context variables in Thymeleaf templates.

- Syntax: `${variable}`
- Example: `<p th:text="${user.name}"></p>`
- Evaluates values from model, request, session, or application scope.

> Variable expressions resolve via `IContext` provided by Thymeleaf, supporting null-safe navigation and collection
> access.
> `${...}` expressions bind template elements to model or context variables in Thymeleaf.

---

### 78. What are Selection Variable Expressions (*{...})?

> Short-hand expressions used within `th:object` context to access form-bound properties.

- Syntax: `*{property}` within a form tag: `<form th:object="${user}"> <input th:field="*{name}"/> </form>`
- Resolves relative to the current selection object, avoiding repeated `${user.property}`.

> Selection expressions improve readability in forms by scoping property access to the bound object.
> `*{...}` accesses properties of the current selection object in form binding, making templates concise and
> maintainable.

---

### 79. What are Message Expressions (#{...})?

> Used to access messages from MessageSource (i18n) in Thymeleaf.

- Syntax: `#{message.code}`
- Example: `<p th:text="#{welcome.message}"></p>`
- Resolves messages according to the current locale.

> Message expressions integrate Spring i18n support seamlessly, enabling multi-language templates.
> `#{...}` expressions access localized messages from Spring MessageSource in Thymeleaf templates.

---

### 80. What are Link URL Expressions (@{...})?

> Used to generate URLs dynamically in Thymeleaf templates.

- Syntax: `@{/path}` or `@{/path(param=${value})}`
- Resolves context-relative URLs, handles query parameters and URI variables.
- Example: `<a th:href="@{/users/{id}(id=${user.id})}">Profile</a>`

> Link expressions integrate with Spring MVC URL mapping and context paths, providing safe and maintainable link
> generation.
> `@{...}` expressions generate context-aware, dynamic URLs in Thymeleaf, including path variables and query parameters.

---

### 81. What are Fragment Expressions (~{...})?

> Fragment expressions reference reusable template fragments in Thymeleaf.

- Syntax: `~{templateName :: fragmentName}`
- Example: `<div th:insert="~{fragments/header :: header}"></div>`
- Can include parameters: `<div th:insert="~{fragments/header :: header(param=${value})}"></div>`
- Supports insertion, replacement, or inclusion in multiple templates.

> Fragment expressions allow modular template design and DRY principle, enabling reuse of headers, footers, and other UI
> components.
> `~{...}` expressions import and include reusable fragments from other templates, optionally passing parameters for
> dynamic rendering.

---

### 82. What are Literals?

> Literal expressions are fixed values written directly in Thymeleaf expressions.

- Examples: strings `'Hello'`, numbers `42`, booleans `true/false`
- Can be used in variable expressions or inlined in templates.
- Helps combine static and dynamic content: `th:text="'Hello ' + ${user.name}"`

> Thymeleaf evaluates literals during template processing alongside variables and message expressions.
> Literals are static, hard-coded values used in expressions or concatenations with dynamic data in Thymeleaf templates.

---

### 83. What is the syntax of the No-Operation token and why is it used?

> The No-Operation token is `th:attr="~{}"` (or `th:*`) and prevents attribute processing, leaving the HTML element
> unmodified.

- Example: `<div th:attr="~{}">Content</div>`
- Used to neutralize attribute evaluation or prevent default Thymeleaf processing.
- Useful in templates intended to render as static HTML without Thymeleaf evaluation.

> No-op allows templates to serve both static preview and dynamic content without changing markup.
> The No-Operation token disables Thymeleaf evaluation for an attribute, preserving the element as-is for static
> rendering.

---

### 84. How to add an attribute to an HTML element?

> Use `th:attr` or specific attribute processors like `th:href`, `th:src`, `th:id`.

- Example: `<a th:href="@{/users}" th:title="${user.name}">Link</a>`
- `th:attr` allows setting multiple attributes: `<div th:attr="data-id=${user.id}, data-role='admin'"></div>`

> Attribute processors dynamically compute attribute values at template rendering, allowing safe and maintainable HTML
> manipulation.
> Add attributes using `th:*` processors or `th:attr` for multiple dynamic attributes in Thymeleaf templates.

---

### 85. What are Attribute Appending and Prepending?

> Techniques to modify an existing HTML attribute by appending or prepending new values dynamically.

- `th:attrappend="class=' new-class'"` → appends to existing `class`.
- `th:attrprepend="class='prefix-'"` → prepends to existing `class`.
- Avoids overwriting existing attributes while dynamically enhancing them.

> Useful for dynamic class manipulation, data attributes, or incremental changes in templates.
> Attribute appending/prepending dynamically modifies existing HTML attributes without overwriting, supporting flexible
> template behavior.

---

### 86. What are template fragments?

> Reusables parts of a template, like headers, footers, or menu blocks, that can be included in multiple templates.

- Defined using `th:fragment`.
- Can accept parameters to make fragments dynamic.
- Can be inserted or replaced using `th:insert`, `th:replace`, or `th:include`.

> Fragments enable modularity, DRY design, and maintainable templates across large applications.
> Template fragments are modular reusable template sections that can be parameterized and reused in multiple templates.

---

### 87. What is the syntax for creating a fragment?

> Use `th:fragment="fragmentName"` on an element.

- Example: `<div th:fragment="header">Header Content</div>`
- Can accept parameters: `<div th:fragment="header(title)">Header: [[${title}]]</div>`
- The fragment can later be inserted or replaced in other templates.

> Fragments support parameterization, making them versatile for dynamic templates.
> Define fragments with `th:fragment="name(parameters)"` to create reusable template sections.

---

### 88. What is Attribute Precedence?

> The order in which Thymeleaf evaluates and applies attribute processors when multiple attributes are present on the
> same element.

- Example: `th:href` overrides `href` attribute.
- `th:attr` can override individual attributes dynamically.
- Thymeleaf defines a fixed precedence to resolve conflicts between multiple attribute processors.

> Understanding precedence prevents unexpected template behavior and ensures dynamic attributes render correctly.
> Attribute precedence determines which Thymeleaf attribute processors take priority when multiple attributes modify the
> same HTML property.

---

### 89. What is Expression inlining?

> Expression inlining allows expressions to be evaluated directly within text or attributes using special delimiters.

- Enables embedding `${...}`, `#{...}`, or `*{...}` inside textual content.
- Example: `<p th:text="|Hello, ${user.name}|"></p>`
- The pipe (`|`) marks the start and end of inlined expression text.

> Expression inlining simplifies template readability and avoids concatenation with multiple `th:text` or `th:utext`
> attributes.
> Expression inlining evaluates expressions directly in text content, enabling concise and readable template
> expressions.

---

### 90. What is the syntax of Expression inlining?

> Use vertical bars `|...|` to enclose text with embedded expressions.

- Example: `<p th:text="|Hello, ${user.name}! Today is ${#dates.format(today,'dd MMM')}|"></p>`
- Multiple expressions can coexist inside a single inline block.
- Supports `${}`, `#{}`, and `*{}` expressions.

> Inlining allows dynamic text rendering while preserving template readability, natural HTML, and static preview
> compatibility.
> Wrap text containing expressions with `|...|` to enable Thymeleaf expression inlining in attributes or text nodes.

---

### 91. What is Spring JDBC?

> A Spring module that simplifies JDBC by removing boilerplate and providing template-based database operations.

- Uses `JdbcTemplate` to manage connections, statements, result sets, and exceptions automatically.
- Converts SQLExceptions into Spring’s unified `DataAccessException`.
- Keeps full SQL control while reducing repetitive DAO logic.
- Supports clean, testable data-access layers.

> Internally, Spring JDBC executes raw SQL using the standard JDBC API but abstracts repetitive resource management and
> exception translation, ensuring safer and more consistent behavior across databases.
> Spring JDBC is a lightweight, SQL-centric abstraction that eliminates boilerplate while maintaining full control over
> SQL execution, improving maintainability and readability.

---

### 92. What is the difference between Spring JDBC and the JDBC API?

> JDBC API is low-level and requires manual resource management; Spring JDBC abstracts this with templates and helper
> classes.

- JDBC requires explicitly opening and closing `Connection`, `Statement`, and `ResultSet`.
- SQLExceptions must be handled manually in try/catch/finally blocks.
- Spring JDBC automates cleanup and translates exceptions into runtime `DataAccessException`.
- Simplifies query execution to single method calls.

> Spring JDBC still relies on the JDBC API underneath but provides higher-level abstractions that reduce boilerplate and
> improve code safety and readability.
> Spring JDBC offers concise, maintainable, and safer database access while retaining the flexibility and performance of
> raw JDBC.

---

### 93. Why use Spring JDBC instead of plain JDBC API?

> To eliminate boilerplate, improve safety, and simplify repetitive SQL operations.

- Prevents resource leaks by handling connections, statements, and result sets automatically.
- Offers easy row mapping via `RowMapper` and helper methods.
- Provides consistent exception handling across databases.
- Reduces code size and improves readability for CRUD operations.

> Spring JDBC reduces common pitfalls of JDBC, like forgetting to close resources, and provides a unified,
> exception-safe approach without adding ORM complexity.
> Using Spring JDBC results in cleaner, safer, and more maintainable data-access code compared to plain JDBC.

---

### 94. What is NamedParameterJdbcTemplate?

> A JdbcTemplate variant that allows using named parameters instead of positional `?` placeholders.

- Supports descriptive parameters like `:id` or `:username`.
- Useful for queries with multiple or repeated parameters.
- Accepts parameter maps or `MapSqlParameterSource`.
- Internally converts named parameters to positional parameters for execution.

> NamedParameterJdbcTemplate improves readability and reduces errors in SQL statements with many parameters.
> It provides the same performance as JdbcTemplate but with clearer, more maintainable SQL using named parameters.

---

### 95. What is the difference between NamedParameterJdbcTemplate and JdbcTemplate?

> JdbcTemplate uses positional parameters (`?`), while NamedParameterJdbcTemplate uses named parameters (`:paramName`).

- Positional parameters require correct ordering and duplication handling.
- Named parameters improve query readability and maintainability.
- NamedParameterJdbcTemplate delegates actual execution to JdbcTemplate.
- Both share the same JDBC execution logic internally.

> NamedParameterJdbcTemplate adds a layer for parsing and mapping names to positions but does not change execution
> performance.
> NamedParameterJdbcTemplate enhances clarity for complex SQL while retaining all core JdbcTemplate features.

---

### 96. What is the purpose of SimpleJdbcInsert?

> A helper class that simplifies INSERT operations without writing SQL manually.

- Automatically generates insert SQL based on table and column metadata.
- Supports retrieving auto-generated keys.
- Reduces boilerplate for simple CRUD operations.
- Ideal for metadata-driven or repetitive inserts.

> Internally, it queries the database metadata to construct the appropriate INSERT statement dynamically.
> SimpleJdbcInsert allows developers to perform inserts cleanly and safely without manually constructing SQL statements.

---

### 97. How to call stored procedures using Spring JDBC?

> Use `SimpleJdbcCall` to execute stored procedures declaratively and safely.

- Configures procedure name, parameters, and return values.
- Eliminates manual `CallableStatement` handling.
- Supports IN, OUT, INOUT parameters and result sets.
- Can introspect procedure metadata to simplify setup.

> Spring internally wraps JDBC CallableStatements and manages parameter binding, execution, and exception translation
> automatically.
> SimpleJdbcCall provides a clean, type-safe abstraction for invoking stored procedures without boilerplate code.

---

### 98. What is Spring Data JPA? What is JpaRepository?

> Spring Data JPA simplifies JPA-based data access; JpaRepository is its core interface providing CRUD, pagination,
> sorting, and query methods.

- Generates queries from method names (e.g., `findByEmail`).
- Supports pagination, sorting, and transactional behavior.
- Integrates with JPA providers like Hibernate.
- JpaRepository extends `CrudRepository` and `PagingAndSortingRepository`.

> Spring Data JPA generates implementations at runtime using proxy objects and query derivation while leveraging JPA
> features like caching, lazy loading, and entity state management.
> Spring Data JPA automates repository patterns and reduces boilerplate while fully leveraging ORM capabilities.

---

### 99. What is the difference between findById() and getOne()/getReference() in Spring Data JPA?

> `findById()` fetches the entity immediately; `getOne()`/`getReference()` returns a lazy proxy.

- `findById()` executes a database query and returns an `Optional`.
- `getReference()` returns a reference proxy without hitting the database initially.
- Accessing uninitialized proxies outside a transaction triggers `LazyInitializationException`.
- Useful for associations or foreign keys where only the ID is needed initially.

> `getReference()` leverages JPA’s lazy-loading proxies, delaying database access until required fields are accessed.
> Use `getReference()` for lightweight entity references and `findById()` when actual entity data is needed immediately.

---

### 100. What is Spring Security?

> A framework providing authentication, authorization, and security mechanisms for Spring applications.

- Supports form login, OAuth2, JWT, and method-level security.
- Provides a filter chain for request interception and access control.
- Includes CSRF protection, password hashing, session management, and CORS handling.
- Highly extensible with custom authentication and authorization logic.

> Built on a flexible filter-chain architecture, Spring Security enforces authentication and authorization before
> controller invocation, providing consistent and centralized security enforcement.
> Spring Security centralizes and standardizes authentication and authorization with strong defaults, extensible
> filters, and modern security practices suitable for enterprise applications.
---

### 101. What is the architecture of Spring Security?

> Spring Security follows a **filter-chain-based architecture** to secure web applications at multiple levels.

- Core components include:
    - **Filter Chain**: Intercepts requests and applies security logic before reaching controllers.
    - **AuthenticationManager**: Validates credentials and returns an `Authentication` object.
    - **AuthenticationProvider**: Contains the logic to authenticate a user (e.g., JDBC, LDAP, JWT).
    - **SecurityContext**: Holds authentication details for the current thread, typically via `SecurityContextHolder`.
    - **AccessDecisionManager & Voter**: Decide whether a user has access to a resource.
    - **UserDetailsService**: Loads user-specific data.
- Spring Security integrates seamlessly with Spring MVC, Servlet filters, and modern reactive applications.

> Internally, Spring Security uses a **chain-of-responsibility pattern**. Each filter processes the request and passes
> it down, allowing modular security features like authentication, authorization, CSRF protection, and session
> management.
> The architecture ensures **centralized, flexible, and extensible security** where filters, providers, and decision
> managers are configurable for modern enterprise-grade Java applications.

---

### 102. What is Authentication?

> Authentication is the process of verifying a user’s identity.

- Confirms that a user is who they claim to be using credentials (username/password, token, OAuth, etc.).
- Typically involves `AuthenticationManager` and `AuthenticationProvider` in Spring Security.
- Returns an `Authentication` object containing user details and authorities upon successful verification.

> In Spring Security, authentication stores the verified `Authentication` in `SecurityContextHolder`. This context is
> thread-local, ensuring secure access for the current request and avoiding cross-thread contamination.
> Authentication is the **first step in security**, forming the foundation for subsequent authorization decisions.

---

### 103. What is Authorization?

> Authorization is the process of determining whether an authenticated user has permission to access a resource.

- Checks user roles, permissions, or attributes against access rules.
- Enforced via annotations (`@PreAuthorize`, `@RolesAllowed`) or URL-based rules in `SecurityFilterChain`.
- Can leverage `AccessDecisionManager` and voters to implement fine-grained access control.

> Authorization occurs **after authentication** and ensures users can only perform actions or access resources they are
> permitted to, maintaining principle of least privilege.
> Properly implemented authorization prevents privilege escalation and enforces security policies at the application
> layer.

---

### 104. What is the difference between authentication and authorization?

> Authentication verifies identity; authorization determines access rights.

- Authentication: Who are you? (login, token verification)
- Authorization: What are you allowed to do? (role checks, permission checks)
- Authentication always precedes authorization in the request lifecycle.

> Spring Security tightly couples these processes: filters handle authentication first, populate `SecurityContext`, then
> authorization checks occur via `AccessDecisionManager` or annotations.
> Understanding this distinction is crucial for designing secure applications: authentication protects identity,
> authorization protects resources.

---

### 105. What is RBAC?

> RBAC (Role-Based Access Control) is a model where **permissions are assigned to roles, and users inherit permissions
via roles**.

- Simplifies access management in large systems by decoupling users and permissions.
- Roles can represent business functions (e.g., ADMIN, USER, MANAGER).
- Often used in conjunction with Spring Security’s authorities.

> RBAC reduces complexity and errors by avoiding direct user-permission assignments, and aligns well with enterprise
> security policies.
> In Spring Security, roles map to `GrantedAuthority` objects used in authorization decisions.

---

### 106. What is Role and Permission?

> A role is a collection of permissions; a permission is a specific action or access right.

- **Role**: High-level abstraction of responsibilities (e.g., `ADMIN`, `EDITOR`).
- **Permission**: Fine-grained operation allowed (e.g., `READ_REPORTS`, `WRITE_USER`).
- Users gain effective permissions through assigned roles.

> Roles and permissions are the building blocks of RBAC, allowing scalable and maintainable security models.
> Best practice: Keep roles broad and permissions specific to minimize complexity and improve auditability.

---

### 107. What is DelegatingFilterProxy and what is its purpose?

> `DelegatingFilterProxy` is a Servlet Filter that delegates requests to a Spring-managed bean.

- Integrates Spring Security filters into the standard Servlet filter chain.
- Allows configuration of filters in `web.xml` or `ServletRegistration` while leveraging Spring’s DI.
- Commonly delegates to `springSecurityFilterChain`.

> It bridges **Servlet API and Spring context**, enabling Spring-managed security beans to participate in request
> processing.
> DelegatingFilterProxy ensures modularity, testability, and seamless Spring integration in web security.

---

### 108. What is SecurityFilterChain and what is its purpose?

> `SecurityFilterChain` is a collection of security filters defining the security policies for HTTP requests.

- Filters are executed in order for authentication, authorization, CSRF, CORS, etc.
- Configured via `HttpSecurity` in Spring Security 5+.
- Supports multiple chains with different matchers for URL-based segregation.

> Internally, it implements a **chain-of-responsibility** pattern, ensuring modular, ordered execution of security
> concerns.
> SecurityFilterChain is the **core of Spring Security’s HTTP request protection**, enabling flexible, declarative, and
> programmatically configurable security.

---

### 109. What is CSRF?

> CSRF (Cross-Site Request Forgery) is an attack where a malicious site triggers unintended actions on behalf of an
> authenticated user.

- Spring Security provides CSRF protection via tokens stored in the session and validated on state-changing requests (
  POST, PUT, DELETE).
- Tokens are embedded in forms or HTTP headers.
- Stateless APIs often disable CSRF and rely on tokens or JWT instead.

> CSRF prevention ensures **actions are intentional**, not triggered by external attackers exploiting an authenticated
> session.
> Enabling CSRF protection is critical for web applications with session-based authentication.

---

### 110. How does Spring Security store passwords by default? (BCrypt)

> Spring Security uses **BCryptPasswordEncoder** by default for password hashing.

- Applies a **salted, adaptive hashing algorithm** to protect passwords.
- Configurable strength factor (work factor) controls computational cost.
- Ensures hashed passwords are safe against rainbow table attacks and brute-force attempts.

> BCrypt is deliberately slow and includes per-password salts, making it resistant to modern cracking techniques. Spring
> Security encourages storing only hashes, never plaintext passwords.
> Using BCryptPasswordEncoder is considered **best practice** for modern secure applications, balancing security,
> performance, and interoperability.

---

### 111.What is PasswordEncoder? How do you configure it?

> `PasswordEncoder` is an interface for encoding and verifying passwords securely in Spring Security.

- Provides methods like `encode(CharSequence rawPassword)` and
  `matches(CharSequence rawPassword, String encodedPassword)`.
- Common implementations include `BCryptPasswordEncoder`, `Pbkdf2PasswordEncoder`, and `Argon2PasswordEncoder`.
- Configured as a Spring Bean and injected into authentication providers or services.

```java

@Bean
public PasswordEncoder passwordEncoder() {
    return new BCryptPasswordEncoder(12); // strength factor = 12
    // 29dae230941ljnljafe...
}

// better one
@Bean
public PasswordEncoder passwordEncoder() {
    return PasswordEncoderFactories.createDelegatingPasswordEncoder();
    // {bcrypt}29dae230941ljnljafe...
}
```

---

### 112. What kind of class is SecurityContextHolder?

> _SecurityContextHolder_ is a utility class that stores the SecurityContext for the current execution thread.
> Internally, SecurityContextHolder abstracts context storage, enabling per-thread security information and supporting
> asynchronous execution with proper propagation.
> Essential for programmatic security access and building custom authentication/authorization logic in Spring Security.

- Holds authentication and principal information.
- Default strategy: ThreadLocal storage; other strategies include InheritableThreadLocal or MODE_GLOBAL

```java
Authentication auth = SecurityContextHolder.getContext().getAuthentication();
```

---

### 113. What is the purpose of the @AuthenticationPrincipal annotation?

> @AuthenticationPrincipal injects the currently authenticated principal directly into controller methods.
> Works with custom user details and OAuth2 principal objects, providing type-safe and declarative access to
> authentication data.

```java

@GetMapping("/profile")
public String profile(@AuthenticationPrincipal UserDetails user) {
    return "Hello, " + user.getUsername();
}
```

---

### 114. How do you implement JWT authentication in Spring Boot?

> JWT authentication secures APIs by validating signed tokens instead of session-based authentication.
> JWT avoids server-side sessions, is stateless, scalable, and supports microservices, but requires careful token
> expiration and revocation handling.

- User logs in → AuthenticationManager validates credentials.
- Generate JWT using secret/private key.
- Client includes JWT in Authorization: Bearer <token› header.
- Custom OncePerRequestFilter validates JWT, sets authentication in SecurityContextHolder .

---

### 115. How do you configure method-level security using @PreAuthorize and @Secured?

> Enable annotation-based method security with @EnableMethodSecurity and use @PreAuthorize or @Secured on service
> methods.
> Method-level security ensures business logic protection beyond HTTP endpoints, preventing unauthorized access even if
> a URL is exposed.

- @PreAuthorize supports SpEL for complex conditions (#user.id == principal.id).
- @Secured is simpler, role-based only.

```java

@Service
public class ReportService {
    @PreAuthorize("hasRole('ADMIN')")
    public void deleteReport(Long id) { ...}

    @Secured("ROLE_USER")
    public List<Report> listReports() { ...}
}

```

---

### 116. What kind of class is MessageSource?

> MessageSource is an interface in Spring for resolving internationalized messages.

- Retrieves localized messages from properties files or databases.
- Methods: getMessage (String code, Object] args, Locale locale) •
- Common implementation: ResourceBundleMessageSource.

---

### 117. What is the purpose of the LocaleResolver interface?

> LocaleResolver determines the current locale for a request in Spring MVC.

- SessionLocaleResolver (stores locale in session)
- CookieLocaleResolver (stores locale in cookies)
- AcceptHeaderLocaleResolver (reads Accept-Language header)

---

### 118. What kind of class is LocaleChangeInterceptor?

> LocaleChangeInterceptor is a Spring MVC interceptor that switches the locale dynamically based on a request parameter.
> Interceptor automatically updates the locale before controller execution, enabling runtime internationalization.

- Common usage: URL parameter ?lang=en .
- Works with a configured LocaleResolver.

```java

@Bean
public LocaleChangeInterceptor localeChangeInterceptor() {
    LocaleChangeInterceptor interceptor = new LocaleChangeInterceptor();
    interceptor.setParamName("lang");
    return interceptor;
}

```

---

### 119. How many ways are there in Spring to handle exceptions?

> Spring provides **three main ways** to handle exceptions in web applications.

- **@ExceptionHandler**: Handle exceptions locally within a controller.
- **@ControllerAdvice / @RestControllerAdvice**: Global exception handling across multiple controllers.
- **HandlerExceptionResolver**: Low-level strategy interface allowing custom resolution of exceptions.

> Internally, Spring maintains a list of `HandlerExceptionResolver`s. When an exception occurs, it iterates through
> resolvers (including `ExceptionHandlerExceptionResolver`) to find a matching handler.
> Proper exception handling improves maintainability and ensures consistent HTTP responses and logging in
> enterprise-grade applications.

---

### 120. What is the purpose of the @ResponseStatus annotation?

> `@ResponseStatus` maps an exception or method to a specific HTTP status code.
> Ensures the client receives the correct HTTP status without manual response manipulation.

- Can be applied to custom exceptions or controller methods.
- Example:

```java

@ResponseStatus(HttpStatus.NOT_FOUND)
public class ResourceNotFoundException extends RuntimeException {
}
```

---

### 121. What is the purpose of the @ControllerAdvice annotation?

> @ControllerAdvice allows global exception handling and cross-cutting controller logic.
> Internally, Spring registers ControllerAdviceBeans and checks controller mappings to apply advice methods across
> multiple controllers.
> Using @ControllerAdvice ensures consistent exception handling, reduces duplication, and centralizes cross-cutting
> logic in enterprise apps.

```java

@ControllerAdvice
public class GlobalExceptionHandler {
    @ExceptionHandler(ResourceNotFoundException.class)
    public ResponseEntity<String> handleNotFound(ResourceNotFoundException ex) {
        return ResponseEntity.status(HttpStatus.NOT_FOUND).body(ex.getMessage());
    }
}

```

---

### 122.What is the purpose of the @ExceptionHandler annotation?

> @ExceptionHandler marks a method to handle specific exceptions thrown by a controller or globally via
> @ControllerAdvice.
> Spring matches the exception type at runtime and invokes the annotated method, bypassing default error pages.

- Can handle one or multiple exception types.
- Returns a view, ResponseEntity, or custom response object.

```java

@ExceptionHandler(IllegalArgumentException.class)
public ResponseEntity<String> handleBadRequest(IllegalArgumentException ex) {
    return ResponseEntity.badRequest().body(ex.getMessage());
}

```

---

### 123. What is the difference between @ControllerAdvice and @RestControllerAdvice?

> @RestControllerAdvice is a specialization of @ControllerAdvice that adds @ResponseBody semantics by default.

- @ControllerAdvice : Returns view names by default; suitable for MVC web apps.
- @RestControllerAdvice : Returns JSON/XML responses directly; ideal for REST APIs.
- Both support global exception handling, @InitBinder, and @ModelAttribute .

---

### 124. What is a Filter?

> A Filter is a Servlet API component that intercepts requests and responses for pre- or post-processing.

- Defined in javax. servlet. Filter interface.
- Common uses: authentication, logging, CORS, compression.
- Executed before controllers and can modify request/response objects.
- Configurable via @Component, web. xmI, or FilterRegistrationBean.

---

### 125. What is an Interceptor?

> An Interceptor is a Spring MVC component that intercepts requests handled by controllers.
> Interceptors operate at the Spring MVC layer, allowing access to controller models and view rendering, unlike servlet
> filters which work lower in the request chain.

- preHandle() : Before controller execution.
- postHandle () : After controller execution, before view rendering.
- afterCompletion() : After request completion.

---

### 126.What is @Transactional? On which layer should it be placed?

> `@Transactional` declaratively defines a transaction boundary for a method or class.
> Internally, Spring uses AOP proxies to wrap the method, interacting with the configured PlatformTransactionManager to
> begin, commit, or rollback transactions as needed.

- Ensures that all database operations within the annotated scope are executed atomically.
- Automatically commits the transaction on successful completion or rolls back on runtime exceptions (unchecked
  exceptions by default).
- Should be placed on the **service layer**, not on controllers or repositories, to maintain **separation of concerns**.
- Example:

```java

@Service
public class OrderService {

    @Transactional
    public void placeOrder(Order order) {
        orderRepository.save(order);
        paymentService.charge(order);
    }
}
```

---

### 127. What are the propagation behaviors in @Transactional? Explain REQUIRED, REQUIRES_NEW, and other propagation levels. Also, what are isolation levels and their purpose?

> Transaction propagation defines **how a transactional method behaves when called within an existing transaction**,
> while isolation levels define **how transactions interact with each other to ensure data consistency**.

- **Propagation Behaviors**:  
  Spring supports several propagation behaviors:
    - **REQUIRED (default)**: Joins the current transaction if one exists; otherwise, starts a new transaction. Common
      for standard service layer methods.
    - **REQUIRES_NEW**: Always creates a new, independent transaction, suspending any existing transaction. Useful for
      operations that must commit independently, such as audit logging.
    - **SUPPORTS**: Executes within a transaction if one exists; otherwise, executes non-transactionally. Typically used
      for read-only operations.
    - **NOT_SUPPORTED**: Executes non-transactionally, suspending any existing transaction. Useful for operations that
      must not run within a transaction.
    - **MANDATORY**: Requires an existing transaction; throws an exception if none exists. Ensures that the method is
      only executed as part of a transaction.
    - **NEVER**: Executes non-transactionally and throws an exception if a transaction exists.
    - **NESTED**: Executes within a nested transaction if a current transaction exists; otherwise, behaves like
      REQUIRED. Nested transactions allow partial rollback within a larger transaction using savepoints.

- **Isolation Levels**:  
  Isolation levels control the visibility of transactional changes and prevent phenomena like dirty reads,
  non-repeatable reads, and phantom reads:
    - **DEFAULT**: Uses the database’s default isolation level.
    - **READ_UNCOMMITTED**: Allows dirty reads; a transaction may see uncommitted changes from other transactions.
    - **READ_COMMITTED**: Prevents dirty reads; only committed changes from other transactions are visible.
    - **REPEATABLE_READ**: Ensures that repeated reads of the same row in the same transaction return consistent
      results, preventing non-repeatable reads.
    - **SERIALIZABLE**: The strictest isolation; ensures full transaction isolation, effectively serializing concurrent
      transactions to avoid conflicts, at the cost of performance.

- **Example: Combining Propagation and Isolation**

```java

@Transactional(propagation = Propagation.REQUIRES_NEW, isolation = Isolation.REPEATABLE_READ)
public void transferFunds(Account from, Account to, BigDecimal amount) {
    debit(from, amount);
    credit(to, amount);
}
// Here, the method runs in a new transaction (REQUIRES_NEW), ensuring that even if the caller's
// transaction fails, the fund transfer is isolated. REPEATABLE_READ ensures consistent reads for
// account balances.
```

> Propagation behaviors are implemented via Spring AOP proxies, which intercept method calls to
> manage transaction boundaries according to the defined propagation. Isolation levels are enforced at
> the database level through Connection. setTransactionIsolation() .
> Understanding both propagation and isolation is critical for ensuring atomicity, consistency, and
> correctness in complex enterprise systems. Correctly combining propagation and isolation prevents
> issues like lost updates, dirty reads, or inconsistent data in nested service calls, making applications
> reliable under high concurrency.
---

### 128.How do you externalize configuration in Spring Boot?

> Externalizing configuration allows Spring Boot applications to separate code from environment-specific settings.

- Spring Boot supports multiple configuration sources:
    - **application.properties** or **application.yml** files.
    - **Environment variables** (e.g., `SPRING_DATASOURCE_URL`).
    - **Command-line arguments** (`--server.port=8081`).
    - **Java system properties** (`-Dspring.profiles.active=dev`).
    - **External configuration files** outside the JAR (`spring.config.location`).
    - **Config servers** (Spring Cloud Config) for centralized configuration.
- Properties are automatically bound to `@ConfigurationProperties` or `@Value` fields in beans.

> Internally, Spring Boot uses a **property sources hierarchy** with the following priority (highest to lowest):
> command-line args → environment variables → application properties/yaml → default values. This ensures flexible,
> environment-specific configuration without modifying code.
> Externalizing configuration is a best practice for **12-factor apps**, supporting multiple environments, DevOps
> pipelines, and containerized deployments.

---

### 129.What are Spring Boot profiles? How do you activate a profile?

> Spring Boot profiles provide a way to **load environment-specific configuration selectively**.

- Example use cases: `dev`, `test`, `prod`.
- Profiles can be declared in property files:

```properties
# application-dev.properties
spring.datasource.url = jdbc:h2:mem:devdb
```

- Command-line argument: --spring profiles.active=dev
- Environment variable: SPRING_PROFILES_ACTIVE=dev
- Programmatically via SpringApplication.setAdditionalProfiles("dev").

---

### 130.What is Spring Boot Actuator? Name some important endpoints.

> Spring Boot Actuator provides production-ready monitoring, metrics, and operational endpoints for Spring Boot
> applications. Actuator uses Micrometer under the hood for metrics and integrates with monitoring systems like
> Prometheus, Grafana, or CloudWatch.
> Important endpoints:

- /actuator/health - Shows application health status.
- /actuator/metrics - Exposes key metrics like JVM memory, CPU, and database usage.
- /actuator/env - Shows active configuration properties and environment variables.
- /actuator/loggers - Dynamically view and configure logging levels.
- /actuator/beans - Lists all Spring beans and their dependencies.
- /actuator/httptrace - Shows recent HTTP requests and responses (debugging).

---

### 131.What is the difference between /actuator/env and /actuator/configprops?

> `/actuator/env` shows the **environment properties**, while `/actuator/configprops` exposes the **configuration beans
and their bound properties**.

- **/actuator/env**:
    - Displays all property sources and environment variables.
    - Shows the values of `application.properties`, `application.yml`, system environment variables, and command-line
      arguments.
    - Useful for debugging which properties are active and their sources.
- **/actuator/configprops**:
    - Shows all beans annotated with `@ConfigurationProperties` and their current bound values.
    - Provides a hierarchical view of configuration objects rather than flat key-value pairs.
    - Useful for inspecting complex nested configurations and custom properties.

> Internally, Spring Boot uses `EnvironmentEndpoint` to aggregate environment properties, while
`ConfigurationPropertiesReportEndpoint` inspects all `@ConfigurationProperties` beans in the application context.
> Understanding the difference is critical for **debugging configuration issues** and ensuring that externalized
> properties are bound correctly to beans.

---

### 132. What is Spring Boot DevTools? What features does it provide?

> Spring Boot DevTools is a **development-time utility** that improves productivity by providing automatic reloads and
> additional debugging features.

- Key features:
    - **Automatic restart**: Detects classpath changes and reloads the application context.
    - **LiveReload support**: Automatically refreshes the browser when resources change.
    - **Property defaults for development**: e.g., disables template caching, enables debug logging.
    - **Remote development support**: Allows remote applications to trigger restarts and live reloads.
    - **Conditional restart**: Excludes certain files from triggering restarts (e.g., static resources).

> Internally, DevTools uses a **two-classloader strategy** to reload changed classes without restarting the JVM,
> significantly improving turnaround time.
> DevTools is strictly for **development environments**; it should not be included in production artifacts.

---

### 133. How do you change the embedded server in Spring Boot (Tomcat → Jetty → Undertow)?

> Spring Boot uses **Tomcat by default**, but it can be swapped with Jetty or Undertow by replacing the starter
> dependency.

1. **Exclude the default Tomcat**:

```xml

<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
    <exclusions>
        <exclusion>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-tomcat</artifactId>
        </exclusion>
    </exclusions>
</dependency>
```

2. **Add the desired server starter**:

```xml

<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-jetty</artifactId>
</dependency>

```

> Spring Boot automatically detects the server dependency and configures it as the embedded server.
> No additional code changes are required.
---

### 134.What is WebClient vs RestTemplate? When to use which?

> `RestTemplate` is a synchronous, blocking HTTP client, whereas `WebClient` is a reactive, non-blocking HTTP client.

- **RestTemplate**:
    - Uses a thread-per-request model.
    - Easier for traditional, blocking REST APIs.
    - Deprecated in Spring 5 in favor of `WebClient`.
- **WebClient**:
    - Part of Spring WebFlux.
    - Non-blocking, supports reactive streams (`Mono` and `Flux`).
    - Better for high-concurrency, streaming, or asynchronous scenarios.
- **When to use**:
    - Use `RestTemplate` for legacy or simple blocking calls.
    - Use `WebClient` for scalable, reactive, or asynchronous HTTP calls.

> Internally, `WebClient` uses `Reactor Netty` or other reactive connectors, allowing efficient resource usage under
> high load, while `RestTemplate` uses `HttpURLConnection` or Apache HTTP client synchronously.
> Modern applications targeting scalability should favor `WebClient` while `RestTemplate` remains for backward
> compatibility.

---

### 135.What is the purpose of @EntityListeners and @PrePersist/@PreUpdate?

> `@EntityListeners` allows attaching lifecycle callback logic to JPA entities, while `@PrePersist` and `@PreUpdate`
> define methods executed before insert or update.

- Example:

```java

@Entity
@EntityListeners(AuditListener.class)
public class User {
    @Id
    @GeneratedValue
    private Long id;
    private LocalDateTime createdAt;
    private LocalDateTime updatedAt;

    @PrePersist
    public void onCreate() {
        createdAt = LocalDateTime.now();
    }

    @PreUpdate
    public void onUpdate() {
        updatedAt = LocalDateTime.now();
    }
}
```

---

### 136. How do you write unit and integration tests in Spring Boot?

> Unit tests focus on isolated components, while integration tests verify the interaction between Spring Boot layers.

```java

@SpringBootTest
class UserServiceTest {
    @MockBean
    private UserRepository repo;

    @Test
    void createUserTest() {
        when(repo.save(any())).thenReturn(new User());
        assertNotNull(userService.createUser("test"));
    }
}
```

---

### 137.What is the difference between @MockBean and @Mock?

> @Mock is a plain Mockito mock, @MockBean(MockitoBean in newer spring boot versions) is a Spring Boot managed mock
> injected into the application context.

- @Mock:
    - Used for unit testing isolated classes.
    - Not registered in Spring context.
- @MockBean: (MockitoBean in newer spring boot versions)
    - Replaces a bean in the Spring context with a mock.
    - Useful in integration or slice tests to mock dependencies.

---

### 138. What is TestRestTemplate and WebTestClient?

- TestRestTemplate:
    - Synchronous, blocking REST client.
    - Ideal for testing REST endpoints with @SpringBootTest (webEnvironment = WebEnvironment. RANDOM_PORT) .
- WebTestClient:
    - Reactive, non-blocking client.
    - Works with WebFlux and Spring MVC applications.
    - Supports reactive streams and functional endpoint testing.

---

### 139. What is Graceful Shutdown in Spring Boot?

> Graceful shutdown ensures that the application stops accepting new requests while completing in-flight requests before
> termination.

```properties
server.shutdown = graceful
spring.lifecycle.timeout-per-shutdown-phase = 30s
```

- Ensures database connections, threads, and resources are properly released.
- Useful in Kubernetes, Docker, or cloud deployments to avoid request loss.

> Internally, Spring Boot hooks into ApplicationContext lifecycle and the embedded server to delay shutdown until
> requests are completed or timeout occurs.
---

### 140.What are Spring Boot test slices? Explain @SpringBootTest, @WebMvcTest, @DataJpaTest, and their purposes.

> Spring Boot test slices allow **loading only the relevant parts of the application context** for faster, focused
> testing instead of initializing the full context.

- **@SpringBootTest**:
    - Loads the **full application context**.
    - Used for **end-to-end integration tests**, including controllers, services, repositories, and external
      configurations.
    - Can start the application on a random or defined port for real HTTP testing.
- **@WebMvcTest**:
    - Loads **only web layer components** (controllers, filters, advice, converters).
    - Excludes service and repository beans unless explicitly mocked.
    - Ideal for **unit-testing controllers** with `MockMvc`.
- **@DataJpaTest**:
    - Loads **JPA repositories, entity mappings, and database configuration**.
    - Automatically configures an **in-memory database** (H2) for testing.
    - Used for **testing persistence logic** without starting the web layer.
- **Other slices**:
    - `@JsonTest` – test JSON serialization/deserialization.
    - `@RestClientTest` – test REST clients with `WebClient` or `RestTemplate`.
    - `@JdbcTest` – test JDBC components.

> Internally, each test slice is implemented using **Spring Boot’s auto-configuration exclusions**, creating a
> lightweight `ApplicationContext` with only the necessary beans. This improves test speed, reduces memory usage, and
> isolates the component under test.
> Test slices allow developers to write **focused, fast, and maintainable tests**, ensuring correctness of specific
> layers (web, persistence, messaging) without the overhead of full integration tests.
---

### 141. What is Spring Boot?

> Spring Boot is a framework that simplifies the creation of stand-alone, production-ready Spring applications with
> minimal configuration.

- Provides auto-configuration to reduce boilerplate setup.
- Includes embedded servers (Tomcat, Jetty) for quick deployment without external server setup.
- Offers opinionated defaults for Spring applications, enabling faster development cycles.
- Integrates seamlessly with Spring modules like Spring Data, Security, and MVC.

> Spring Boot internally leverages Spring’s dependency injection and context management, automatically scanning and
> configuring beans based on the classpath and application properties. Auto-configuration uses conditional annotations (
> e.g., `@ConditionalOnClass`) to enable or disable features dynamically.
> Spring Boot streamlines Spring application development by combining convention-over-configuration, embedded runtime,
> and auto-configuration, allowing engineers to focus on business logic while maintaining Spring’s flexibility and
> scalability.

---

### 142. What is the difference between Spring and Spring Boot?

> Spring is a general-purpose framework for dependency injection and enterprise applications, while Spring Boot is a
> rapid application development framework built on top of Spring with auto-configuration and embedded servers.

- Spring requires explicit configuration of beans, contexts, and deployment settings.
- Spring Boot reduces manual setup via auto-configuration, starter dependencies, and embedded servers.
- Spring Boot follows opinionated defaults, while Spring provides full flexibility at the cost of verbosity.

> Spring Boot builds on Spring Core and MVC, using annotations and conditional configuration to simplify typical
> patterns. It avoids boilerplate XML or Java config while leveraging Spring’s underlying container and bean lifecycle.
> Spring is the foundation, providing core IoC, AOP, and modularity, while Spring Boot accelerates application
> development with embedded servers, auto-configuration, and production-ready features.

---

### 143. What is the purpose of the Jackson library?

> Jackson is a Java library for converting Java objects to JSON and vice versa (serialization and deserialization).

- Supports flexible mapping between Java classes and JSON structures.
- Handles complex nested objects, collections, and polymorphism.
- Integrates with REST frameworks like Spring MVC to automatically parse request bodies and produce JSON responses.

> Jackson uses reflection and annotations at runtime to inspect classes and fields, dynamically generating JSON
> structures without requiring manual parsing.
> Jackson is the de facto standard for JSON processing in Java applications, offering high performance, configurability,
> and seamless integration with Spring for RESTful APIs.

---

### 144. What is the purpose of the ObjectMapper class?

> ObjectMapper is the main Jackson class responsible for reading and writing JSON data from/to Java objects.

- Provides methods like `readValue()` for deserialization and `writeValueAsString()` for serialization.
- Supports configuration for custom naming strategies, date formats, inclusion policies, and modules.
- Can handle both simple and complex object graphs.

> ObjectMapper maintains an internal `JsonFactory` and `SerializerProvider` to efficiently parse and generate JSON while
> respecting annotations and registered modules.
> ObjectMapper is the core of Jackson operations, enabling precise and high-performance JSON mapping while supporting
> advanced customizations and integration with frameworks like Spring Boot.

---

### 145. Where in the Spring Framework is the Jackson library used?

> Jackson is used primarily in Spring MVC and Spring WebFlux for HTTP message conversion between JSON and Java objects.

- `MappingJackson2HttpMessageConverter` uses Jackson to serialize responses and deserialize request bodies.
- Spring Boot automatically configures Jackson if `spring-boot-starter-web` is included.
- Supports integration with `@RequestBody`, `@ResponseBody`, and `RestTemplate` or `WebClient`.

> Spring relies on Jackson’s annotations and ObjectMapper configuration to dynamically map HTTP JSON payloads to Java
> objects during request handling, respecting field visibility, naming strategies, and type information.
> Jackson is the standard JSON processor in Spring for REST APIs, providing transparent serialization and
> deserialization with minimal boilerplate and full customization capabilities.

---

### 146. List the most important Jackson annotations with their purposes.

> Key Jackson annotations control JSON serialization and deserialization behavior for Java objects.

- `@JsonProperty` → Customizes the JSON property name for a field.
- `@JsonIgnore` → Excludes a field from JSON serialization/deserialization.
- `@JsonInclude` → Controls inclusion criteria (e.g., non-null, non-empty) for JSON output.
- `@JsonFormat` → Specifies date/time format or pattern.
- `@JsonCreator` → Marks a constructor or factory method for deserialization.
- `@JsonValue` → Indicates a method whose return value should be used as the JSON representation.
- `@JsonAnyGetter` / `@JsonAnySetter` → Dynamically map extra JSON properties to a Map.

> These annotations are processed at runtime by Jackson’s ObjectMapper, influencing how fields are mapped, ignored, or
> formatted, enabling precise control over JSON structure.
> Jackson annotations are essential tools for defining how Java objects map to JSON, providing both global configuration
> through ObjectMapper and per-class customization for API consistency.

---

### 147. What is Spring Data JPA?

> Spring Data JPA is a Spring abstraction that simplifies working with JPA-based data persistence by providing
> repositories and reducing boilerplate.

- Provides `CrudRepository`, `JpaRepository`, and custom query support.
- Handles entity lifecycle, transactions, and standard CRUD operations automatically.
- Integrates seamlessly with Hibernate or other JPA providers.

> Internally, Spring Data JPA dynamically generates repository implementations using proxy classes and reflection,
> translating method names into JPQL or SQL queries.
> Spring Data JPA accelerates database development by combining JPA’s ORM capabilities with repository abstractions,
> enabling clean, declarative, and testable data access layers.

---

### 148. What is the difference between Spring Data JPA and Hibernate?

> Hibernate is a JPA implementation and ORM tool, while Spring Data JPA is an abstraction layer that simplifies using
> Hibernate or any JPA provider.

- Hibernate manages entity mapping, persistence, caching, and query execution.
- Spring Data JPA provides repository interfaces, query derivation, and reduces boilerplate on top of Hibernate.
- Hibernate can be used standalone, whereas Spring Data JPA depends on Spring infrastructure.

> Spring Data JPA dynamically creates proxies and method-level query implementations, leveraging Hibernate for actual
> SQL execution, transaction management, and caching.
> Hibernate is the engine; Spring Data JPA is the productivity layer that reduces manual coding and standardizes
> repository patterns while still using Hibernate’s full ORM power.

---

### 149. What kind of interfaces are JpaRepository and CrudRepository? What's the difference?

> Both are Spring Data repository interfaces; CrudRepository provides basic CRUD, while JpaRepository extends it with
> JPA-specific features and batch operations.

- `CrudRepository<T, ID>` → Provides `save()`, `findById()`, `findAll()`, `deleteById()`.
- `JpaRepository<T, ID>` → Extends `CrudRepository` with methods like `flush()`, `saveAll()`, `findAll(Pageable)`, and
  JPA-specific operations.
- Both are implemented at runtime by Spring Data proxies.

> The repository interfaces use dynamic proxy generation and reflection to implement methods based on JPA or query
> derivation, avoiding manual DAO implementations.
> CrudRepository covers minimal persistence needs, while JpaRepository provides richer JPA-centric operations and
> pagination support, enabling cleaner and more expressive repository code in modern Spring applications.

---

### 150. What is the purpose of the @Entity annotation?

> `@Entity` marks a Java class as a JPA entity to be mapped to a database table.

- Signals the JPA provider to manage the class lifecycle and persistence.
- Fields are mapped to table columns, with primary key typically annotated using `@Id`.
- Works with `@Table` to define custom table names or schema.

> At runtime, the JPA provider reads `@Entity` metadata and generates SQL statements, caches entity definitions, and
> integrates with the persistence context for transactions and caching.
> `@Entity` is fundamental for ORM mapping in Spring Data JPA and Hibernate, turning plain Java objects into managed
> database entities with minimal boilerplate.

---

### 151. What is the purpose of the @Transactional annotation? Where should it be placed?

> `@Transactional` manages transaction boundaries, ensuring atomicity, consistency, isolation, and durability (ACID) in
> database operations.

- Can be applied at **class level** (all public methods) or **method level** (specific method transaction).
- Ensures that all operations within a transaction either **commit** or **rollback** on exceptions.
- Supports attributes like `propagation`, `isolation`, `readOnly`, and `timeout`.

> Spring AOP proxies intercept method calls on `@Transactional` beans. Depending on the proxy type (JDK or CGLIB),
> transactions are started before method execution and committed/rolled back after execution.
> Use `@Transactional` on service-layer methods rather than repositories for business-level transaction control.
> Method-level placement allows fine-grained control, while class-level placement provides consistent transactional
> behavior for all methods.

---

### 151.1 Why does @Transactional not work on private methods?

> @Transactional does not work on private methods because Spring applies transactions via proxies, and private methods
> cannot be intercepted.

- Spring AOP is proxy-based, not bytecode-weaving by default
- Proxies intercept only external method calls
- Private methods are not visible to subclasses or proxies
- Self-invocation bypasses the proxy entirely

> The transaction interceptor is applied at the proxy boundary, not within the target class itself.
> @Transactional works only on public (and sometimes protected/package-private) methods invoked through the Spring
> proxy. Private methods are excluded by design, reinforcing the principle that transactional boundaries should be part
> of
> the public service contract.

---

### 152. What is the purpose of the @Modifying annotation?

> `@Modifying` marks a repository query method as a **write operation** (INSERT, UPDATE, DELETE) in Spring Data JPA.

- Must be used with `@Query` for custom update/delete statements.
- Allows the execution of non-select queries via JPA.
- Often combined with `@Transactional` to ensure atomicity.

> Without `@Modifying`, Spring treats `@Query` as a read operation and throws exceptions for updates/deletes.
> `@Modifying` signals Spring Data JPA to execute a modifying statement and adjust the EntityManager accordingly,
> ensuring correct transaction handling and automatic flush behavior.

---

### 153.What is Query Creation in Spring Data JPA? Give examples.

> Query Creation automatically generates queries based on repository method names.

- Method names like `findByFirstNameAndLastName(String first, String last)` are parsed into JPQL queries.
- Supports operators: `And`, `Or`, `Between`, `Like`, `GreaterThan`, `OrderBy`.
- Example:

```java
  List<User> findByAgeGreaterThanOrderByLastNameDesc(int age);
```

---

### 154.What is Projection? How many types are there? (Interface-based, DTO, Closed vs Open)

> Projection defines a way to retrieve specific parts of an entity rather than the full object.

- Interface-based Projection: Defines getters in an interface for selected fields.
- DTO Projection: Uses constructor expressions or custom DTOs.
- Closed Projection: Only exposes defined fields; cannot access nested properties.
- Open Projection: Can compute additional fields or navigate nested properties.

```java
interface UserNameOnly {
    String getFirstName();

    String getLastName();
}

List<UserNameOnly> findByActiveTrue();

```

> Spring Data JPA dynamically maps results to the interface or DTO using constructor expressions or reflection,
> optimizing fetch strategies and reducing unnecessary data retrieval.
> Projections improve performance and encapsulation by fetching only necessary data while supporting both
> interface-based
> and DTO-based patterns for flexible and type-safe queries.

---

### 155.What is Auditing in Spring Data JPA? How to enable it?

> Auditing automatically tracks entity creation, modification, and the user responsible for changes.
> Spring Data JPA intercepts entity lifecycle events using EntityListeners, populating auditing fields before persist or
> update operations.
> Auditing ensures consistent tracking of changes for compliance and debugging without manual timestamp or user
> handling,
> integrating seamlessly with Spring Data JPA.

- Annotate a configuration class with @EnableJpaAuditing .
- Use @CreatedDate, @LastModifiedDate, @CreatedBy, @LastModifiedBy in entities.
- Ensure a bean implements AuditorAware<T> for current user resolution.

---

### 156.What is the purpose of @CreatedDate, @LastModifiedDate, @CreatedBy etc.?

> These annotations mark entity fields for automatic population by Spring Data JPA auditing.

- @CreatedDate → Timestamp when the entity is first persisted.
- @LastModifiedDate → Timestamp when the entity is updated.
- @CreatedBy → User who created the entity.

---

### 157.What is the difference between save() and saveAndFlush()?

> save() persists an entity but may delay execution until the transaction is committed, while saveAndFlush() persists
> and immediately flushes changes to the database.

- save () → Entity is persisted in the persistence context; database insert/update may be deferred.
- saveAndFlush() → Forces immediate SQL execution, useful when subsequent operations depend
  on the database state.

---

### 158.What is the difference between findById() and getReferenceById()?

> findById() fetches the entity immediately, while getReferenceById() returns a lazy proxy.

- findById() → Executes a SQL query immediately; returns Optional<T> .
- getReferenceById() → Returns a proxy; database access occurs when a property is accessed.
  Useful for associating entities without fetching full data eagerly.

> getReferenceById() leverages JPA lazy loading, avoiding unnecessary database hits, but accessing non-existent entities
> can throw EntityNotFoundException.
> Choosing between them affects performance and lazy-loading behavior; getReferenceById() is ideal for linking entities
> without fetching data upfront.

---

### 159.What is the N+1 problem and how to solve it in Spring Data JPA?

> The N+1 problem occurs when fetching a collection of entities causes one query for the parent plus N queries for child
> entities.

Example: Fetch 10 orders → 1 query for orders + 10 queries for order items.

- Eager fetching using @EntityGraph.
- Join fetch in JPQL: SELECT o FROM Order o JOIN FETCH o.items.
- Batch fetching with Hibernate @BatchSize.

> The issue arises due to lazy-loading proxies triggering queries per child entity, impacting performance significantly
> in large datasets.
> Proper fetch strategy planning, batch size tuning, and join fetching are key to avoiding N+1 issues, ensuring
> high-performance data access.

---

### 160.What is HATEOAS?

> HATEOAS (Hypermedia as the Engine of Application State) is a REST design principle where responses include hypermedia
> links for client navigation.

- Provides links to related resources or actions dynamically in API responses.
- Spring supports HATEOAS via spring-boot-starter-hateoas and RepresentationModel.

```java
class Main {
    static void main() {
        EntityModel<User> model = EntityModel.of(user);
        model.add(linkTo(methodOn(UserController.class).getUser(user.getId())).withSelfRel());
    }
}

```

> HATEOAS decouples client logic from fixed URLs, allowing APIs to evolve without breaking clients, by exposing
> actionable links based on current resource state.
> Implementing HATEOAS improves API discoverability, reduces hard-coded endpoints in clients, and aligns RESTful
> services
> with mature hypermedia-driven architectures.

---

### 161. What is EntityModel, CollectionModel, and PagedModel?

> They are Spring HATEOAS classes for representing resources and collections with hypermedia links.

- **EntityModel<T>** → Wraps a single domain object and allows adding links (e.g., `self`, `related`).
- **CollectionModel<T>** → Wraps a collection of resources (e.g., a list of `EntityModel`) and supports links for the
  entire collection.
- **PagedModel<T>** → Extends `CollectionModel` for paginated resources; includes metadata like page number, size, total
  elements, and links for next/previous pages.

> These classes enable standardized hypermedia representation, automatically integrating links, metadata, and content
> for REST APIs while keeping the domain model clean.
> EntityModel, CollectionModel, and PagedModel facilitate HATEOAS-driven REST APIs by decoupling hypermedia concerns
> from domain entities, enabling self-descriptive, navigable API responses with clear structure and pagination support.

---

### 162. What are the advantages and disadvantages of HATEOAS?

> HATEOAS improves API discoverability and client decoupling but adds complexity and payload overhead.

- **Advantages:**
    - Clients dynamically navigate resources using links instead of hard-coded endpoints.
    - API evolves without breaking clients.
    - Encourages self-descriptive, REST-compliant responses.
- **Disadvantages:**
    - Increased response size due to embedded links.
    - Higher implementation complexity.
    - Clients must understand hypermedia format, adding learning curve.

> Spring HATEOAS efficiently manages links and resource models, but the added abstraction may impact performance and
> complexity for small/simple APIs.
> Use HATEOAS when building complex, evolving APIs with rich client navigation; avoid it for lightweight, internal APIs
> or performance-critical endpoints where link overhead outweighs benefits.

---

### 163. When should HATEOAS be used and when should it be avoided?

> Use HATEOAS for discoverable, self-descriptive, evolving APIs; avoid for simple or high-performance APIs.

- **Use cases:**
    - Public APIs with multiple resources and relationships.
    - APIs requiring dynamic navigation by clients.
    - Systems where endpoints may change over time.
- **Avoid:**
    - Internal microservices with tightly coupled clients.
    - High-throughput, performance-critical endpoints.
    - Simple CRUD APIs where links provide minimal added value.

> HATEOAS adds runtime metadata and requires client understanding, so it should be selectively applied based on API
> complexity and maintainability requirements.
> Strategic HATEOAS adoption improves client flexibility and API longevity without unnecessary overhead for simple or
> internal systems.

---

### 164. What is Spring Data REST? When would you use it?

> Spring Data REST automatically exposes Spring Data repositories as RESTful endpoints.

- Eliminates manual controller creation for CRUD operations.
- Supports pagination, sorting, filtering, and HATEOAS out of the box.
- Integrates with Spring Data JPA repositories seamlessly.

> Internally, Spring Data REST uses repository metadata, Jackson, and Spring HATEOAS to dynamically generate REST
> endpoints, hypermedia responses, and entity serialization.
> Use Spring Data REST for **rapid prototyping** or simple CRUD APIs without custom business logic. Avoid it when
> fine-grained control, custom workflows, or complex security is required.

---

### 165. How to provide Authentication and Authorization in a Spring Boot REST API?

> Use Spring Security to enforce authentication (who you are) and authorization (what you can do) in REST APIs.

- **Authentication options:**
    - JWT (stateless, token-based)
    - OAuth2 / OpenID Connect
    - Basic authentication (for simple cases)
- **Authorization options:**
    - Role-based access control (RBAC) using `@PreAuthorize` or `@RolesAllowed`
    - Method-level security with annotations like `@Secured`
    - URL-based access rules in `SecurityFilterChain` configuration

- Example (JWT-based security):

```java

@Bean
public SecurityFilterChain filterChain(HttpSecurity http) throws Exception {
    http.csrf().disable()
            .authorizeHttpRequests(auth -> auth
                    .requestMatchers("/api/admin/**").hasRole("ADMIN")
                    .anyRequest().authenticated()
            )
            .oauth2ResourceServer(OAuth2ResourceServerConfigurer::jwt);
    return http.build();
}
````

---

### 166. What is JWT? What are its three parts?

> JWT (JSON Web Token) is a compact, URL-safe token format used for securely transmitting claims between parties.

- **Three parts of JWT:**
    1. **Header** → Contains token type (`JWT`) and signing algorithm (`HS256`, `RS256`).
    2. **Payload** → Contains claims (standard: `sub`, `exp`, `iat`; custom: user roles, permissions).
    3. **Signature** → Cryptographic signature of header + payload to ensure integrity and authenticity.

> The token is Base64URL-encoded and structured as `header.payload.signature`. The signature prevents tampering and
> ensures the token was issued by a trusted authority.
> JWT is widely used for stateless authentication in microservices and REST APIs because it carries all necessary claims
> in a compact, verifiable form, eliminating the need for server-side session storage.

---

### 167. How does JWT authentication work in Spring Boot?

> JWT authentication in Spring Boot validates requests by checking the token instead of traditional session-based
> authentication.

- **Workflow:**
    1. Client logs in with credentials → server generates JWT and returns it.
    2. Client includes JWT in `Authorization: Bearer <token>` header for subsequent requests.
    3. Spring Security intercepts requests, extracts and validates JWT.
    4. If valid, authentication is set in `SecurityContext` for method-level or URL-based authorization.

- Tokens typically include claims like username, roles, and expiration time.

> Spring Security processes JWT using filters (e.g., `OncePerRequestFilter`), parsing the token, validating the
> signature, and populating the security context with an authenticated principal.
> JWT authentication enables **stateless, scalable, and decoupled** security suitable for REST APIs and distributed
> systems without maintaining server sessions.

---

### 168. How to configure JWT with Spring Security (SecurityFilterChain + JwtAuthenticationFilter)?

> JWT integration in Spring Boot involves a custom filter for token validation and a `SecurityFilterChain`
> configuration.

- **Steps:**
    1. Create `JwtAuthenticationFilter` extending `OncePerRequestFilter`:
       ```java
       @Component
       public class JwtAuthenticationFilter extends OncePerRequestFilter {
           @Override
           protected void doFilterInternal(HttpServletRequest request,
                                           HttpServletResponse response,
                                           FilterChain filterChain) throws ServletException, IOException {
               String token = extractToken(request);
               if (token != null && validateToken(token)) {
                   UsernamePasswordAuthenticationToken auth =
                       getAuthentication(token);
                   SecurityContextHolder.getContext().setAuthentication(auth);
               }
               filterChain.doFilter(request, response);
           }
       }
       ```
    2. Configure `SecurityFilterChain`:
       ```java
       @Bean
       public SecurityFilterChain securityFilterChain(HttpSecurity http,
                                                      JwtAuthenticationFilter jwtFilter) throws Exception {
           http.csrf().disable()
               .authorizeHttpRequests(auth -> auth
                   .requestMatchers("/api/auth/**").permitAll()
                   .anyRequest().authenticated()
               )
               .addFilterBefore(jwtFilter, UsernamePasswordAuthenticationFilter.class);
           return http.build();
       }
       ```

> The filter intercepts every request, extracts the JWT, validates it, and sets the authentication in the
`SecurityContext`. The `SecurityFilterChain` defines which endpoints are protected and how filters are applied.
> This configuration creates a **stateless, token-driven security mechanism**, ensuring only requests with valid JWTs
> can access protected endpoints.

---

### 169. What is the difference between OAuth2 Resource Server (JWT) and OAuth2 Client?

> OAuth2 Resource Server validates access tokens to protect resources, while OAuth2 Client obtains tokens to access
> protected resources on behalf of a user.

- **Resource Server:**
    - Protects APIs.
    - Validates JWT or opaque tokens from an authorization server.
    - Configured with `spring-boot-starter-oauth2-resource-server`.
- **Client:**
    - Requests tokens from an authorization server (e.g., via authorization code flow).
    - Calls external APIs using the obtained access token.
    - Configured with `spring-boot-starter-oauth2-client`.

> Resource Server focuses on **token validation** for incoming requests, whereas Client focuses on **token acquisition
and outbound API calls** on behalf of a user.
> Understanding the distinction ensures proper architecture for microservices: servers validate tokens, clients request
> them securely without storing user credentials.

---

### 170. What is CORS? How to configure it properly in Spring Boot?

> CORS (Cross-Origin Resource Sharing) is a security mechanism that allows browsers to access resources from a different
> origin than the requesting page.

- **Problem:** Browsers block requests from different origins by default (Same-Origin Policy).
- **Configuration in Spring Boot:**
    1. **Global configuration via `WebMvcConfigurer`:**
       ```java
       @Configuration
       public class CorsConfig implements WebMvcConfigurer {
           @Override
           public void addCorsMappings(CorsRegistry registry) {
               registry.addMapping("/api/**")
                       .allowedOrigins("http://example.com")
                       .allowedMethods("GET","POST","PUT","DELETE")
                       .allowCredentials(true);
           }
       }
       ```
    2. **Controller-level using `@CrossOrigin`:**
       ```java
       @CrossOrigin(origins = "http://example.com")
       @RestController
       public class MyController { ... }
       ```

> Proper CORS configuration ensures that only trusted origins can access API resources, preventing cross-origin attacks
> while allowing legitimate cross-domain interactions.
> Correct CORS setup is essential for REST APIs consumed by web clients in different domains, balancing security and
> usability.

---

What is OpenAPI/Swagger and why is it used in Spring Boot?

> OpenAPI (formerly Swagger) is a specification for describing REST APIs, enabling automatic documentation, client
> generation, and API testing.

- Provides a machine-readable description of endpoints, request/response models, and HTTP methods.
- Allows auto-generation of interactive API documentation (Swagger UI).
- Facilitates contract-first development and API client code generation in multiple languages.

> In Spring Boot, OpenAPI definitions are generated from controllers and model classes using annotations (`@Operation`,
`@Schema`, etc.) or automatically scanned by libraries like springdoc-openapi.
> OpenAPI simplifies API documentation, reduces manual maintenance, and provides standardized, interactive, and
> consumable REST API descriptions for developers and clients.

---

### 172. What is springdoc-openapi? Why is it preferred over springfox now?

> `springdoc-openapi` is a Spring Boot library that automatically generates OpenAPI 3 documentation from Spring
> MVC/WebFlux controllers.

- Supports Spring Boot 3+ natively, unlike Springfox which struggles with modern Spring versions.
- Automatically scans `@RestController`, `@RequestMapping`, and `@Schema` annotations.
- Provides integration with Swagger UI for interactive API exploration.

> Internally, springdoc leverages Spring’s `HandlerMethod` introspection and model scanning to generate
> OpenAPI-compliant JSON dynamically.
> It is preferred over Springfox because it is actively maintained, compatible with the latest Spring Boot and Java
> versions, supports OpenAPI 3, and provides easier customization for grouping and tagging APIs.

---

### 173. In springdoc, how can APIs be grouped?

> APIs can be grouped using **groups** or **tags** in springdoc.

- **Tags**: Annotate controllers or operations with `@Tag(name="users", description="User operations")`.
- **Groups**: Define multiple `GroupedOpenApi` beans to generate separate API docs for different modules or packages:
  ```java
  @Bean
  public GroupedOpenApi userApi() {
      return GroupedOpenApi.builder()
              .group("users")
              .pathsToMatch("/api/users/**")
              .build();
  }
  ```

---

### 174. What is the purpose of the @Async annotation?

> @Async allows methods to execute asynchronously in a separate thread, enabling non-blocking operations.

- Can be applied at method or class level.
- Returns CompletableFuture, Future, or void.
- Useful for long-running tasks like email sending, batch jobs, or remote service calls.

> Spring uses proxies and TaskExecutor to execute the annotated method in a thread separate from the caller, freeing the
> main thread.
> @Async improves responsiveness and throughput by delegating work to background threads, decoupling task execution from
> request handling in Spring applications.
---

### 175.How does @Async work internally (proxy, TaskExecutor)?

> @Async works by creating a Spring proxy around the bean and delegating method calls to a configured TaskExecutor.

- A proxy intercepts method calls and submits them to an executor (default: SimpleAsyncTaskExecutor ).
- The actual method executes in a separate thread managed by the executor.
- Returns immediately if the method returns void or a Future / CompletableFuture wraps the
  result.

---

### 176.How to handle exceptions in @Async methods?

> Exceptions in @Async methods do not propagate to the caller thread by default.

```java

@Async
public CompletableFuture<String> asyncTask() {
    return CompletableFuture.supplyAsync(() -> {
        if (someError) throw new RuntimeException("Error");
        return "Done";
    }).exceptionally(ex -> "Fallback");
}

```

---

### 177.What is the purpose of @EnableAsync and TaskExecutor?

> @EnableAsync enables Spring’s asynchronous method execution, and TaskExecutor defines the thread pool and execution
> behavior.

- @EnableAsync registers the AsyncAnnotationBeanPostProcessor to detect @Async annotations.
- TaskExecutor controls:
    - Thread pool size
    - Queue capacity
    - Thread naming
    - Rejection policies

```java

@Bean(name = "asyncExecutor")
public Executor asyncExecutor() {
    ThreadPoolTaskExecutor executor = new ThreadPoolTaskExecutor();
    executor.setCorePoolSize(5);
    executor.setMaxPoolSize(20);
    executor.setQueueCapacity(100);
    executor.initialize();
    return executor;
}

```

---

### 178.What happens if you call an @Async method from the same class?

> Calling an @Async method from within the same class bypasses the Spring proxy, so the method executes synchronously in
> the caller thread.

- Internal calls do not go through the proxy, so no new thread is spawned.
- Only external calls via the Spring-managed bean trigger asynchronous execution.

---

### 179.What is the @Profile annotation? How do you activate profiles?

> @Profile allows conditional bean registration based on the active Spring profile.

- application.properties/yaml: spring.profiles.active=dev
- Command-line: —spring.profiles.active=dev
- Programmatically: ConfigurableEnvironment.setActiveProfiles("dev")

---

### 180.What is the order of precedence for properties in Spring Boot?

> Spring Boot resolves properties using a well-defined precedence hierarchy, where higher sources override lower ones.

Precedence order (high → low):

1. Devtools global properties
2. SPRING_APPLICATION_JSON (environment variable or system property)
3. Command-line arguments
4. Java system properties ( System.getProperties () )
5. OS environment variables
6. RandomValuePropertySource
7. application. properties or application. yml outside JAR
8. application properties or application.yml inside JAR
9. @PropertySource annotations
10. Default properties ( SpringApplication.setDefaultProperties())

---

### 181. What is @ConfigurationProperties? Difference from @Value?

> `@ConfigurationProperties` binds a group of external configuration properties to a POJO, while `@Value` injects
> individual property values.

- **@ConfigurationProperties**:
    - Maps nested properties using a prefix (e.g., `app.datasource.url` → `AppProperties.datasource.url`).
    - Supports type-safe binding and complex structures (lists, maps, nested classes).
    - Example:
      ```java
      @ConfigurationProperties(prefix = "app.datasource")
      public class DataSourceProperties {
          private String url;
          private String username;
          private String password;
          // getters/setters
      }
      ```
- **@Value**:
    - Injects a single property value (`@Value("${app.datasource.url}")`).
    - Limited type conversion; harder for nested structures.

> Internally, Spring binds properties to beans using the `Binder` mechanism for `@ConfigurationProperties`, whereas
`@Value` relies on SpEL expression evaluation.
> Use `@ConfigurationProperties` for structured, type-safe configuration binding and `@Value` for simple, individual
> property injection.

---

### 182. What is the difference between @Controller and @RestController?

> `@Controller` handles HTTP requests and returns views, while `@RestController` returns JSON/XML responses directly.

- **@Controller**:
    - Typically used with templates (Thymeleaf, JSP).
    - Methods return view names.
    - Must use `@ResponseBody` to return raw data.
- **@RestController**:
    - Combines `@Controller` + `@ResponseBody`.
    - Automatically serializes return objects to JSON/XML using Jackson.

> Spring uses `HttpMessageConverters` to serialize responses from `@RestController` methods.
> `@RestController` simplifies REST API development by removing the need for `@ResponseBody` annotations, making
> controllers concise and focused on data responses.

---

### 183. What is @ResponseEntity? When to return it?

> `ResponseEntity` represents an HTTP response, including status, headers, and body.

- Enables full control over HTTP response:
    - Status codes (`200 OK`, `404 Not Found`, `500 Internal Server Error`)
    - Headers (`Location`, `Cache-Control`, `Content-Type`)
    - Body content (JSON, XML, or custom objects)
- Example:
  ```java
  @GetMapping("/user/{id}")
  public ResponseEntity<User> getUser(@PathVariable Long id) {
      return userService.findById(id)
              .map(ResponseEntity::ok)
              .orElse(ResponseEntity.notFound().build());
  }
  ```

---

### 184. What is the difference between @Validated and @Valid?

> @Valid is a JSR-380 standard annotation for bean validation, while @Validated is a Spring-specific variant with
> support for validation groups.

- @Valid:
    - Triggers validation on method parameters or bean fields.
    - No group support.
- @Validated:
    - Supports validation groups (`@Validated(OnCreate.class)` ).
    - Can be applied at class or method level in Spring components.

---

### 185.What is the difference between @Component, @Service, @Repository?

> All are Spring stereotypes for bean registration; their distinction is semantic and functional.
> Use @Component for generic beans, @Service for business logic, and @Repository for DAO layers to improve code clarity
> and enable exception translation where needed.

- @Component:
    - Generic stereotype for any Spring-managed bean.
- @Service:
    - Indicates a service layer bean (business logic).
    - Primarily for readability and documentation; no functional difference.
- @Repository:
    - Marks a persistence/DAO layer bean.
    - Adds exception translation (converts persistence exceptions into DataAccessException).

---

### 186. How do we publish and listen to custom events in Spring Boot?

> Custom events in Spring Boot allow decoupled communication between components using the **ApplicationEventPublisher**
> mechanism.

- **Steps to publish and listen:**
    1. **Define a custom event:**
       ```java
       public class UserCreatedEvent {
           private final Long userId;
           public UserCreatedEvent(Long userId) { this.userId = userId; }
           public Long getUserId() { return userId; }
       }
       ```
    2. **Publish the event:**
       ```java
       @Service
       public class UserService {
           private final ApplicationEventPublisher publisher;
           public UserService(ApplicationEventPublisher publisher) { this.publisher = publisher; }
           public void createUser(User user) {
               // save user
               publisher.publishEvent(new UserCreatedEvent(user.getId()));
           }
       }
       ```
    3. **Listen to the event:**
       ```java
       @Component
       public class UserEventListener {
           @EventListener
           public void handleUserCreated(UserCreatedEvent event) {
               // handle event
           }
       }
       ```

> Spring’s event mechanism is synchronous by default and leverages the `ApplicationEventMulticaster` internally to
> notify all listeners.
> Custom events enable **loosely coupled design**, allowing services to react to domain events without direct
> dependencies, improving maintainability and testability.

---

### 187.What is the purpose of ApplicationEventPublisher?

> `ApplicationEventPublisher` is used to **publish events to the Spring application context** so that all registered
> listeners can react.

- Allows decoupled communication between components.
- Works with any type of event, not necessarily extending `ApplicationEvent`.
- Can be injected into services, controllers, or other Spring-managed beans.

> Internally, the publisher delegates to `ApplicationEventMulticaster`, which iterates over listeners and invokes them
> based on event type.
> It provides a **standard mechanism to broadcast events** in Spring applications, supporting both synchronous and
> asynchronous handling depending on the configuration.

---

### 188.What is the purpose of the @EventListener annotation?

> `@EventListener` marks a method as a **listener for a specific event type**, automatically invoked when the event is
> published.

- Can listen to any object type as an event.
- Supports conditional execution with `condition` attribute.
- Can specify `classes` or `fallbackExecution` to fine-tune behavior.

> Spring detects `@EventListener` via post-processing and registers the method with the `ApplicationEventMulticaster`,
> invoking it when an event of the matching type is published.
> `@EventListener` simplifies event handling without implementing interfaces like `ApplicationListener`, enabling
> declarative, readable, and maintainable event-driven code.

---

### 189.What is @TransactionalEventListener and when should you use it (with phases)?

> `@TransactionalEventListener` triggers event listeners **in coordination with Spring transactions**, executing only if
> a transaction reaches a specified phase.

- **Phases:**
    - `AFTER_COMMIT` (default) → execute after transaction commits successfully.
    - `BEFORE_COMMIT` → execute just before commit.
    - `AFTER_ROLLBACK` → execute only if transaction rolls back.
    - `AFTER_COMPLETION` → always execute after transaction completes.

- Example:
  ```java
  @TransactionalEventListener(phase = TransactionPhase.AFTER_COMMIT)
  public void handleUserCreated(UserCreatedEvent event) {
      // execute only if transaction succeeds
  }
  ```

---

### 190.Can @EventListener methods be made asynchronous? How?

> Yes, by combining @EventListener with @Async to execute the listener in a separate thread.

```java

@Configuration
@EnableAsync
public class AsyncConfig {
}

```

```java

@Component
public class UserEventListener {
    @Async
    @EventListener
    public void handleUserCreated(UserCreatedEvent event) {
        // executes asynchronously
    }
}

```

---

### 191. Why is database migration important?

> Database migration ensures consistent, version-controlled updates to the database schema, aligned with application
> code.

- Keeps schema in sync across environments (development, staging, production).
- Prevents runtime errors caused by missing tables, columns, or constraints.
- Enables automated, repeatable deployments and safe rollbacks.
- Facilitates team collaboration and CI/CD integration.

> In modern applications, unmanaged schema changes lead to drift between environments, causing bugs or downtime.
> Migrations formalize schema evolution.
> Database migration is critical for reliable, predictable, and maintainable application deployments, ensuring both data
> integrity and operational consistency.

---

### 192. What is Flyway and how does Spring Boot auto-configure it?

> Flyway is a version-controlled database migration tool that applies SQL or Java-based migrations to maintain schema
> consistency.

- Spring Boot auto-configures Flyway when `flyway-core` is on the classpath.
- Default configuration:
    - Scans `classpath:db/migration` for migration scripts.
    - Applies pending migrations at application startup.
- Can be customized via `spring.flyway.*` properties (locations, baseline version, placeholders).

> Internally, Spring Boot creates a `Flyway` bean using `FlywayAutoConfiguration`, binds it to the configured
`DataSource`, and calls `migrate()` automatically during context initialization.
> Flyway simplifies schema evolution, reduces manual DBA work, and ensures repeatable, consistent migrations across
> environments.

---

### 193. What are Versioned migrations in Flyway?

> Versioned migrations are sequential, incrementally applied scripts identified by a **version number**.

- Naming convention: `V1__init.sql`, `V2__add_users_table.sql`, `V3__alter_column.sql`.
- Each migration is executed **once** in order based on version.
- Supports both SQL and Java-based migration classes.

> Flyway tracks applied versions in the `flyway_schema_history` table to prevent re-execution.

> Versioned migrations provide a clear, auditable history of schema changes, ensuring deterministic and reliable
> database evolution.

---

### 194. Where should Flyway migration scripts be placed?

> By default, Flyway expects migration scripts in `classpath:db/migration`.

- Location can be customized with:
  ```properties
  spring.flyway.locations=classpath:db/migration,filesystem:/sql/migrations
  ```

---

### 195.What happens if two Flyway migrations have the same version?

> Flyway will fail the migration process due to a version conflict.

- Duplicate version numbers in migration filenames are not allowed.
- Flyway relies on version numbers to determine execution order.
- Conflicts are detected at startup, preventing partial or inconsistent migrations.

---

### 196. What is Liquibase and how does it differ from Flyway?

> Liquibase is a database schema change management tool that uses XML, YAML, JSON, or SQL “changesets” to track,
> version, and apply migrations.

- Supports both **declarative and imperative** migrations.
- Tracks applied changesets in a database table (`DATABASECHANGELOG`).
- Supports rollback scripts, complex conditional logic, and database-independent changes.
- Flyway focuses on **sequential SQL/Java scripts**, whereas Liquibase emphasizes **flexible, structured changesets with
  rollback support**.

> Liquibase provides advanced features like cross-database compatibility and rollback capabilities, making it suitable
> for enterprise systems with heterogeneous databases, while Flyway is simpler and relies on versioned scripts.

---

### 197. What are the main differences between Flyway and Liquibase?

> Both are migration tools but differ in approach, flexibility, and feature set.

| Feature               | Flyway                     | Liquibase                                 |
|-----------------------|----------------------------|-------------------------------------------|
| Migration format      | SQL or Java scripts        | XML, YAML, JSON, SQL                      |
| Rollback support      | Limited                    | Full rollback support                     |
| Database independence | Low (script-based)         | High (abstract changesets)                |
| Tracking table        | `flyway_schema_history`    | `DATABASECHANGELOG`                       |
| Complexity            | Simple, lightweight        | More powerful, enterprise-friendly        |
| Community adoption    | Widely used, simpler CI/CD | Preferred in complex enterprise scenarios |

> Flyway emphasizes simplicity and deterministic versioned execution; Liquibase provides richer features, including
> change tracking, rollbacks, and cross-database support.

---

### 198. How to run migrations differently in test vs production profiles?

> Spring Boot allows profile-specific migration configuration using properties or YAML.

- **Flyway example:**
  ```properties
  spring.profiles.active=test
  spring.flyway.locations[0]=classpath:db/migration/test
  spring.flyway.locations[1]=classpath:db/migration/common
  ```
- **Liquibase example:**
  ```yaml
  spring:
   profiles: test
   liquibase:
     change-log: classpath:/db/changelog/db.changelog-test.yaml

  ```

> Spring automatically loads the profile-specific configuration at startup, enabling different migration sets or
> behaviors for test, dev, and production environments.
> Profile-specific migrations ensure testing databases can have seed or mock data, while production migrations remain
> clean and safe.
---

### 199.What is the difference between MongoRepository and MongoTemplate?

> MongoRepository is a Spring Data interface-based abstraction for CRUD operations, whereas MongoTemplate is a
> low-level, template-based API for more complex queries.

- MongoRepository:
    - Provides auto-generated CRUD and query methods.
    - Supports Query Creation, @Query , projections, pagination.
    - Simple and declarative.
- MongoTemplate:
    - Supports complex queries, aggregation, map-reduce, bulk operations.
    - Fully programmatic and flexible.
    - Lower-level access compared to repository abstraction.

---

### 200.How to create and publish a custom ApplicationEvent?

> Custom ApplicationEvents allow decoupled components to communicate in Spring Boot.

- **Steps:**
    1. **Define the event class**:
       ```java
       public class UserRegisteredEvent {
           private final Long userId;
           public UserRegisteredEvent(Long userId) { this.userId = userId; }
           public Long getUserId() { return userId; }
       }
       ```
    2. **Publish the event**:
       ```java
       @Service
       public class UserService {
           private final ApplicationEventPublisher publisher;
           public UserService(ApplicationEventPublisher publisher) { this.publisher = publisher; }
           public void registerUser(User user) {
               // save user
               publisher.publishEvent(new UserRegisteredEvent(user.getId()));
           }
       }
       ```
    3. **Listen to the event**:
       ```java
       @Component
       public class UserEventListener {
           @EventListener
           public void handleUserRegistered(UserRegisteredEvent event) {
               // handle event
           }
       }
       ```

> Spring uses `ApplicationEventMulticaster` internally to notify all listeners, by default **synchronously** in the
> publisher thread.
> Custom events promote **loose coupling** and clean separation of concerns, enabling scalable, event-driven designs.

---

### 201.What is the default transaction phase for @TransactionalEventListener? Why AFTER_COMMIT is safest?

> The default phase is **AFTER_COMMIT**.

- `AFTER_COMMIT` ensures the listener executes **only if the enclosing transaction successfully commits**.
- Other phases:
    - `BEFORE_COMMIT` → before commit, may run even if commit fails later.
    - `AFTER_ROLLBACK` → runs only on rollback.
    - `AFTER_COMPLETION` → always runs after transaction finishes (commit or rollback).

> Using `AFTER_COMMIT` is safest because it prevents side effects from executing if the transaction rolls back, ensuring
> consistency and avoiding actions based on uncommitted or aborted changes.
> It is especially important for sending notifications, triggering external systems, or creating audit logs tied to
> transactional data.

---

### 202.How to execute a MongoDB transaction in Spring Boot?

> MongoDB transactions provide atomic operations across multiple documents or collections in replica sets or sharded
> clusters.

```java

@Service
public class UserService {
    private final MongoTemplate mongoTemplate;

    public UserService(MongoTemplate mongoTemplate) {
        this.mongoTemplate = mongoTemplate;
    }

    public void performTransaction() {
        ClientSession session = mongoTemplate.getMongoDbFactory().getSession();
        session.startTransaction();
        try {
            mongoTemplate.insert(new User("Alice"), session);
            mongoTemplate.insert(new Order("Order1"), session);
            session.commitTransaction();
        } catch (Exception e) {
            session.abortTransaction();
            throw e;
        } finally {
            session.close();
        }
    }
}
// Can also use @Transactional on methods when using Spring Data MongoDB 4+ with transaction-aware MongoTransactionManager.

```

> MongoDB transactions ensure atomicity across multiple operations, similar to relational database transactions, but are
> only supported in replica sets or sharded clusters.
> Proper use of transactions prevents partial updates and maintains data consistency in complex operations.
---

### 203. When would you choose MongoDB over a relational database in a Spring Boot project?

> MongoDB is preferred when the application requires flexible schemas, horizontal scalability, or document-oriented
> modeling.

- Use cases:
    - Dynamic, evolving data structures (JSON documents).
    - Large-scale, high-throughput applications requiring horizontal scaling.
    - Applications that benefit from rich embedded documents or hierarchical data.
    - Event sourcing, logging, analytics, or content management systems.
- Avoid MongoDB when:
    - Strong relational integrity and complex joins are required.
    - ACID transactions across multiple entities are critical (though limited multi-document
      transactions are possible).
    - Mature reporting or BI tools rely on relational queries.

---

### 204.What is Cache?

> Cache is a temporary storage layer that stores frequently accessed data to reduce latency and improve system
> performance.

- Caching stores results of expensive operations (like DB queries or computations) in memory or fast-access storage.
- It reduces response time for repeated requests and decreases load on backend systems.
- Common caching mechanisms include in-memory caches (e.g., `ConcurrentHashMap`), distributed caches (e.g., Redis,
  Memcached), and HTTP caches.

> At the JVM level, caching often uses fast heap memory or off-heap memory, leveraging data locality and avoiding
> repeated I/O operations.
> Cache improves system throughput and response time by keeping frequently used data close to the application, reducing
> redundant processing and I/O bottlenecks.

---

### 205.Why is caching considered an important concept in REST architecture?

> Caching in REST reduces server load and improves client-side performance by storing responses of idempotent requests.

- REST APIs often deal with repeated requests for the same resource.
- HTTP caching headers (`Cache-Control`, `ETag`, `Last-Modified`) allow clients and intermediaries to cache responses
  efficiently.
- Reduces latency and network bandwidth usage.
- Improves scalability by minimizing repeated backend computations.

> Proper caching aligns with REST principles like statelessness and idempotency. ETag and conditional GETs ensure
> freshness while maintaining consistency across distributed clients.
> Caching is essential in REST to enhance performance, scalability, and user experience without compromising the
> stateless nature of the service.

---

### 206. What kind of interface is CacheManager?

> `CacheManager` is a Spring interface that provides access to one or more `Cache` instances.

- It is part of `org.springframework.cache` and abstracts the caching implementation.
- Supports retrieving caches by name and managing multiple cache regions.
- Can be implemented by in-memory caches, EhCache, Redis, or other third-party cache providers.

> In Spring, `CacheManager` decouples business logic from caching implementation, allowing seamless switching of cache
> backends without changing application code.
> `CacheManager` provides a uniform, implementation-agnostic way to manage caches in Spring, enabling consistent caching
> practices across the application.

---

### 207.Which requests (GET, POST, DELETE, etc.) should be cached?

> Only safe and idempotent requests, primarily GET, should be cached.

- GET requests are read-only and repeatable without side effects, making them ideal for caching.
- POST, PUT, DELETE modify server state and should generally not be cached.
- Conditional caching (ETag, Last-Modified) can sometimes optimize POST/PUT responses but is less common.

> Caching non-idempotent requests can lead to stale or inconsistent data, violating REST semantics and introducing
> potential bugs.
> Cache GET responses to maximize performance and maintain correctness, while avoiding caching state-changing operations
> to ensure data integrity.

---

### 208. When should caching not be used?

> Caching should be avoided for rapidly changing, highly dynamic, or sensitive data where freshness and consistency are
> critical.

- Highly volatile data (e.g., stock prices, real-time feeds) may render caches stale quickly.
- Sensitive or personal data might violate security or privacy if cached improperly.
- Operations with small computational cost or low access frequency might not benefit from caching.
- Cache invalidation complexity outweighs performance gain.

> Misused caching can cause stale data, memory pressure, and consistency problems in distributed systems.
> Avoid caching when data freshness, security, or low re-use frequency outweighs the performance benefit.

---

### 209.What is Redis?

> Redis is an in-memory, distributed key-value store commonly used as a cache and message broker.

- Supports strings, hashes, lists, sets, sorted sets, and more complex data structures.
- Provides extremely low latency and high throughput.
- Can persist data to disk and replicate across nodes for fault tolerance.
- Supports pub/sub messaging and Lua scripting.

> Redis uses an in-memory data structure optimized for fast access, with optional persistence, making it ideal for
> caching, session storage, and high-speed analytics.
> Redis is a versatile, high-performance caching solution widely used in modern Java applications for reducing DB load,
> speeding up responses, and supporting distributed caching strategies.

---

### 210.How can caching be used in Spring?

> Spring provides annotation-based and programmatic caching support via `@Cacheable`, `@CachePut`, `@CacheEvict`, and
`CacheManager`.

- `@Cacheable` stores method results in the cache automatically.
- `@CachePut` updates cache without affecting method execution.
- `@CacheEvict` removes stale data from cache.
- `CacheManager` allows centralized management of multiple caches.
- Supports integration with Redis, EhCache, Caffeine, and other providers.

```java

@Service
public class UserService {
    @Cacheable(value = "users", key = "#id")
    public User getUserById(Long id) {
        simulateSlowService();
        return userRepository.findById(id).orElseThrow();
    }

    private void simulateSlowService() {
        try {
            Thread.sleep(2000);
        } catch (InterruptedException e) {
            Thread.currentThread().interrupt();
        }
    }
}
```

> Spring’s caching abstraction decouples business logic from caching implementation, ensuring consistent, maintainable,
> and high-performance caching strategies in modern applications.
> By leveraging Spring caching annotations and CacheManager, developers can transparently improve performance, reduce
> backend load, and maintain clean separation of concerns.

---

### 211.What is the difference between RestTemplate, RestClient, WebClient, and others?

> RestTemplate is a synchronous, blocking HTTP client; WebClient is a modern reactive, non-blocking HTTP client;
> RestClient is a newer declarative HTTP client in Spring.

- **RestTemplate**
    - Synchronous/blocking HTTP calls.
    - Legacy Spring client, still widely used.
    - Good for simple, imperative-style REST calls.
    - Uses `HttpMessageConverter` to marshal/unmarshal request and response bodies.
    - Deprecated in Spring 5+ in favor of `WebClient`.

- **WebClient**
    - Part of Spring WebFlux, supports reactive, non-blocking calls.
    - Can handle streaming data and backpressure efficiently.
    - Supports both synchronous (`block()`) and asynchronous/reactive (`Mono`/`Flux`) operations.
    - More suitable for high-throughput, scalable microservices.

- **RestClient**
    - Introduced in Spring 6 (Spring Boot 3), declarative and type-safe.
    - Uses interface-based approach for REST calls, similar to Feign clients.
    - Simplifies REST API consumption with compile-time validation and easier integration.
    - Supports both synchronous and reactive operations under the hood.

- **Other clients**
    - **Feign Client**: Declarative REST client, integrates with Spring Cloud; can be reactive with WebClient adapter.
    - **Apache HttpClient / OkHttp**: Low-level, general-purpose HTTP clients, often used for advanced configuration or
      performance tuning.

> RestTemplate uses traditional `HttpURLConnection` or Apache HttpClient internally, performing blocking I/O. WebClient
> leverages reactive Netty or other async connectors to avoid blocking threads. RestClient adds compile-time safety and
> declarative abstraction on top of modern HTTP APIs.
> In modern Spring applications:

- Prefer **WebClient** for non-blocking, scalable APIs.
- Use **RestClient** for type-safe, declarative REST consumption.
- Avoid **RestTemplate** for new projects but maintain it for legacy codebases.
- Choose **Feign** or **low-level clients** for specialized requirements.

---

### 212. What is ApplicationRunner vs CommandLineRunner?

> Both are startup hooks, but ApplicationRunner provides structured access to application arguments.

- CommandLineRunner:
    - Receives raw String[] arguments
    - Simpler, less structured
- ApplicationRunner:
    - Receives ApplicationArguments
    - Supports option and non-option arguments
- Both run after ApplicationContext is fully initialized
- Execution order can be controlled with @Order

> ApplicationRunner is better suited for complex startup logic requiring parsed arguments.
> Both interfaces enable post-startup execution, but ApplicationRunner is preferred in modern applications due to its
> richer argument model and cleaner separation of concerns.

---

### 213.

>
---

### 214.

>
---

### 215.

>
---

### 216.

>
---

### 217.

>
---

### 218.

>
---

### 219.

>
---

### 220.

>
---

### 221.

>
---

### 222.

>
---

### 223.

>
---

### 224.

>
---

### 225.

>
---

### 226.

>
---

### 227.

>
---

### 228.

>
---

### 229.

>
---

### 230.

>
---

### 231.

>
---

### 232.

>
---

### 233.

>
---

### 234.

>
---

### 235.

>
---

### 236.

>
---

### 237.

>
---

### 238.

>
---

### 239.

>
---

### 240.

>
---

### 241.

>
---

### 242.

>
---

### 243.

>
---

### 244.

>
---

### 245.

>
---

### 246.

>
---

### 247.

>
---

### 248.

>
---

### 249.

>
---

### 250.

>
---

### 251.

>
---

### 252.

>
---

### 253.

>
---

### 254.

>
---

### 255.

>
---

### 256.

>
---

### 257.

>
---

### 258.

>
---

### 259.

>
---

### 260.

>
---

### 261.

>
---

### 262.

>
---

### 263.

>
---

### 264.

>
---

### 265.

>
---

### 266.

>
---

### 267.

>
---

### 268.

>
---

### 269.

>
---

### 270.

>
---

### 271.

>
---

### 272.

>
---

### 273.

>
---

### 274.

>
---

### 275.

>
---

### 276.

>
---

### 277.

>
---

### 278.

>
---

### 279.

>
---

### 280.

>
---

### 281.

>
---

### 282.

>
---

### 283.

>
---

### 284.

>
---

### 285.

>
---

### 286.

>
---

### 287.

>
---

### 288.

>
---

### 289.

>
---

### 290.

>
---

### 291.

>
---

### 292.

>
---

### 293.

>
---

### 294.

>
---

### 295.

>
---

### 296.

>
---

### 297.

>
---

### 298.

>
---

### 299.

>
---

### 300.

>
---