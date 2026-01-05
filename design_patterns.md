# Design Patterns

---

### 1. What is a Design Pattern?

> A design pattern is a reusable solution to a common problem in software design.

- It is a proven idea, not ready-made code.
- It describes how classes and objects should interact.
- It helps teams communicate and build better systems.
- Patterns come from real-world experience.

> Design patterns make code clearer and more flexible.
> In Java projects, they support good practices like SOLID and help create maintainable, scalable applications.

---

### 2. Why are Design Patterns important?

> They help write code that is easier to read, maintain, and extend.

- Reduce code duplication.
- Make changes safer and faster.
- Improve teamwork with shared terms.
- Lower bugs in large systems.

> Patterns keep components loosely coupled.
> In modern Java (Spring, microservices), patterns lead to clean, testable production code.

---

### 3. What are the three main categories of Design Patterns?

> Creational, Structural, and Behavioral.

- **Creational**: How objects are created (Singleton, Factory Method, Builder).
- **Structural**: How classes and objects are composed (Adapter, Proxy, Decorator).
- **Behavioral**: How objects communicate (Strategy, Observer, Command).

> These categories come from the Gang of Four (GoF) book.
> Knowing them helps you quickly find the right pattern for a problem.

---

### 4. What problems do Creational patterns solve?

> They control and simplify object creation.

- Hide complex construction logic.
- Let clients use interfaces, not concrete classes.
- Support different creation based on configuration.
- Help manage object lifecycle.

> Creational patterns are useful when constructors get too complicated.
> In Java, they work well with Spring dependency injection.

---

### 5. Why is Singleton often considered risky?

> It creates global shared state that can cause issues.

- Hidden dependencies.
- Harder to test (difficult to mock).
- Thread-safety problems if not careful.
- Limits future flexibility.

> Modern Java prefers Spring @Bean with singleton scope instead of manual Singleton.
> Use Singleton only when really needed and implement it safely (enum or static holder).

---

### 6. What problem does the Factory Method pattern solve?

> It lets subclasses decide which object to create.

- Clients depend on interfaces only.
- Easy to add new types later.
- Follows open/closed principle.
- Creation logic in one place.

> Factory Method is great when the exact type is decided at runtime.
> Common in Java frameworks for extensible designs.

---

### 7. Why is the Builder pattern useful?

> It makes building complex objects clear and safe.

- Avoids long constructor parameter lists.
- Supports optional parameters.
- Step-by-step construction.
- Works well with immutable objects.

> Java has no named parameters, so Builder improves readability.
> Popular for DTOs and configuration objects; Lombok @Builder makes it even easier.

---

### 8. What problems do Structural patterns solve?

> They help combine classes and objects flexibly.

- Prefer composition over inheritance.
- Connect incompatible interfaces.
- Add behavior without changing classes.
- Simplify complex subsystems.

> Structural patterns use wrapping and delegation.
> They fit perfectly with Java interfaces and default methods.

---

### 9. Why is the Proxy pattern common in Spring?

> It adds extra behavior without touching business code.

- Transactions (@Transactional).
- Security checks.
- Lazy loading.
- Logging and caching.

> Spring creates proxies (JDK or CGLIB) to intercept calls.
> Proxy is the base of Aspect-Oriented Programming (AOP) in Spring.

---

### 10. What problem does the Strategy pattern solve?

> It allows changing behavior at runtime.

- Replaces large if-else blocks.
- Each algorithm in its own class.
- Easy to test and extend.
- Can inject different strategies.

> In Java 8+, simple strategies can use lambdas.
> Strategy keeps code clean and follows single responsibility.

---

### 11. Why is the Observer pattern popular?

> It supports loose coupling in event-driven systems.

- One subject notifies many observers.
- Observers can subscribe/unsubscribe dynamically.
- Good for reactive designs.
- Used in UI and messaging.

> In Java: event listeners, Spring ApplicationEvents, reactive streams.
> Observer helps build scalable, modular applications.

---

### 12. When should you not use Design Patterns?

> When they add unnecessary complexity.

- Small or simple projects.
- Problems that will not change.
- When a direct solution is clearer.
- Too early abstraction (YAGNI).

> Patterns should solve real problems.
> Good Java code starts simple and adds patterns only when needed.

---

### 13. What problem does the Adapter pattern solve?

> It makes incompatible interfaces work together.

- Wraps existing class with new interface.
- Reuses legacy or third-party code.
- No need to change original classes.
- Common with external libraries.

> Adapter translates calls between different APIs.
> Helps integrate old code with new systems.

---

### 14. What problem does the Decorator pattern solve?

> It adds behavior dynamically without inheritance.

- Avoids many subclasses.
- Mix and match features.
- Follows open/closed principle.
- Uses composition.

> Classic Java example: InputStream wrappers (BufferedInputStream).
> Decorator offers flexible enhancement.

---

### 15. What problem does the Command pattern solve?

> It turns a request into an object.

- Encapsulates actions.
- Supports undo/redo.
- Enables queuing and scheduling.
- Decouples sender from receiver.

> Used in Java thread pools (Runnable), UI actions, job queues.
> With lambdas, simple commands are easier.

---

### 16. Why is the Template Method pattern useful?

> It defines algorithm steps while allowing customization.

- Common flow in base class.
- Subclasses override specific steps.
- Avoids duplication.
- Keeps process consistent.

> Relies on inheritance.
> Sometimes replaced by Strategy for more flexibility.

---

### 17. What problem does the Facade pattern solve?

> It provides a simple interface to a complex subsystem.

- Hides internal details.
- Reduces client coupling.
- Makes API easier to use.
- Single entry point.

> Common in service layers and libraries.
> In microservices, often used as client or gateway.

---

### 18. What problem does the Chain of Responsibility pattern solve?

> It passes requests along a chain of handlers.

- No hard-coded handler.
- Dynamic order and easy to extend.
- Good for filters and authentication.
- Each handler has one responsibility.

> Used in Servlet filters, Spring Security.
> Creates clean processing pipelines.

---

### 19. What is the difference between Strategy and State?

> Strategy changes behavior from outside; State changes based on internal state.

- Strategy is injected and rarely changes.
- State manages its own transitions.
- Both use composition.

> State is useful for objects with complex lifecycle.
> Choose Strategy for algorithms, State for lifecycle behavior.

---

### 20. What problem does the Abstract Factory pattern solve?

> It creates families of related objects.

- Consistent object groups (e.g., UI themes).
- Switch entire families easily.
- Hides concrete classes.
- Works with DI.

> Useful for multi-platform or configurable systems.
> Enables pluggable architectures in Java.

---

### 21. How does Dependency Injection relate to Design Patterns?

> DI implements Inversion of Control using patterns.

- Reduces coupling.
- Easier testing with mocks.
- Central creation (container).
- Combines Factory and Singleton ideas.

> Spring makes DI standard for bean management.
> Preferred way for creational needs in modern Java.

---

### 22. What is the difference between Proxy and Decorator?

> Both wrap objects, but intent is different.

- Proxy controls access (security, lazy load).
- Decorator adds new behavior.
- Proxy usually same interface.
- Decorator enhances functionality.

> Spring proxies are mostly for access control.
> Intent decides which pattern to use.

---

### 23. Why prefer composition over inheritance?

> Composition is more flexible and safe.

- Runtime changes possible.
- Mix multiple behaviors.
- Avoids fragile base class issues.
- No deep hierarchies.

> Many patterns (Decorator, Strategy) use composition.
> Modern Java favors interfaces over class inheritance.

---

### 24. How are Design Patterns used in Spring?

> Spring builds on many classic patterns.

- Proxy → AOP and transactions.
- Singleton → default bean scope.
- Factory → BeanFactory.
- Template Method → JdbcTemplate.
- Observer → ApplicationEvents.

> Knowing patterns helps understand Spring better.
> Spring hides pattern details so you focus on business logic.

---

### 25. Which Design Patterns are most asked in Java interviews?

> Singleton, Factory Method, Builder, Adapter, Proxy, Strategy, Observer, Decorator, Template Method, Command.

- They appear in real projects and frameworks.
- Questions focus on intent and trade-offs.
- Spring examples are valuable.

> Explain why and when to use them, plus modern alternatives (lambdas, DI).