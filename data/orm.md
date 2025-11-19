# ORM & Hibernate

### 1.What is ORM?

> ORM (Object-Relational Mapping) is a technique that maps Java objects to relational database tables, allowing
> developers to interact with the database using object-oriented paradigms instead of SQL.

> ORM frameworks abstract the persistence layer by converting database rows into Java objects and vice versa. This
> reduces boilerplate code for CRUD operations and enforces type safety. It allows developers to work with objects,
> relationships, and queries in Java rather than writing raw SQL statements manually.

> ORM frameworks maintain a **persistence context** that tracks entity states (transient, managed, detached, removed)
> and uses mechanisms like **dirty checking** to synchronize object changes with the database efficiently. Lazy vs eager
> fetching strategies, caching layers (first-level and second-level), and SQL generation optimization are key internal
> behaviors of ORM.

---

### 2. Which ORM frameworks do you know?

> Popular Java ORM frameworks include Hibernate, EclipseLink, Spring Data JPA, MyBatis (semi-ORM), and OpenJPA.

- **Hibernate:** Most widely used, full-featured ORM, supports JPA specification, caching, advanced fetching strategies.
- **EclipseLink:** Reference implementation of JPA, supports additional features like NoSQL, advanced mappings.
- **Spring Data JPA:** Builds on JPA, provides repository abstraction, query derivation from method names, and
  integrates seamlessly with Spring ecosystem.
- **MyBatis:** Semi-ORM; focuses on SQL mapping rather than full object management; gives fine-grained control over
  queries.
- **OpenJPA:** Apache project, JPA implementation, used in some legacy and enterprise apps.

---

### 3.Why should we use ORM?

> ORM simplifies database access, reduces boilerplate code, and allows developers to work with objects instead of SQL.

> Without ORM, developers manually write SQL and map results to objects, which is error-prone and repetitive. ORM
> automates CRUD operations, relationship management, and schema mapping. It ensures type safety, integrates with
> transaction management, and supports caching and lazy loading for performance optimization.

> ORM frameworks manage the **persistence context**, performing **dirty checking** to only update changed fields. This
> reduces unnecessary database operations. They also abstract database dialects, allowing applications to switch DB
> vendors with minimal code changes.

---

### 4.What are the advantages and disadvantages of ORM compared to plain JDBC?

> Advantages: Less boilerplate, object-oriented access, caching, database-agnostic, relationship management.  
> Disadvantages: Performance overhead, less fine-grained SQL control, learning curve, potential for N+1 query problems.

**Advantages:**

- Reduces boilerplate code for CRUD and object mapping.
- Supports object relationships (OneToOne, OneToMany, ManyToMany).
- First-level and second-level caching improve performance.
- Database-agnostic query generation via JPQL or Criteria API.

**Disadvantages:**

- Abstracted SQL can be less optimized than hand-tuned queries.
- Lazy-loading can cause N+1 query problems if not handled carefully.
- Complex joins and batch operations may require tuning or raw SQL.
- Learning curve for entity mappings, caching, and session management.

---

### 5.What is Jakarta Persistence API (JPA)?

> JPA is a Java specification for ORM that defines how Java objects are persisted to relational databases.

> JPA provides a standard set of annotations (`@Entity`, `@Table`, `@Id`, `@OneToMany`, etc.) and APIs (EntityManager,
> Criteria API, JPQL) for defining entity models and performing CRUD operations. It separates the specification from the
> implementation, allowing frameworks like Hibernate or EclipseLink to provide the runtime behavior.

> JPA defines the **persistence context**, entity life cycles (transient, managed, detached, removed), caching
> strategies, and query mechanisms. It allows vendor-agnostic ORM, while implementations handle SQL generation, lazy
> loading, and caching. Modern JPA (Jakarta EE 10+) supports modularity, criteria queries, and integration with Jakarta
> EE
> and Spring.

---

### 6.Why do we need JPA and how does it work?

> JPA provides a standard, vendor-agnostic way to map Java objects to relational databases, simplifying persistence and
> reducing boilerplate code.

> JPA abstracts low-level JDBC operations, handling object-to-table mapping, relationship management, and CRUD
> operations. Developers interact with entities through the **EntityManager**, which manages a **persistence context**.
> JPA tracks entity states (transient, managed, detached, removed) and synchronizes changes to the database
> automatically
> via **dirty checking** and transaction management.

> Under the hood, JPA implementations generate SQL dynamically based on the entity mappings and query definitions. They
> optimize database operations by batching writes, caching entities, and using lazy or eager fetching strategies. The
> persistence context ensures that each managed entity instance is unique within a transaction, preventing redundant
> database calls.

---

### 7. What is JPQL and how does it differ from SQL?

> JPQL (Java Persistence Query Language) is an object-oriented query language for JPA that operates on entity objects
> rather than database tables.

> JPQL allows querying entities and their relationships using Java class and field names instead of table and column
> names. It supports `SELECT`, `UPDATE`, and `DELETE` operations with object-oriented syntax. Unlike SQL, JPQL abstracts
> the underlying database schema, enabling portability across different database vendors.

> JPQL queries are translated by the JPA provider into native SQL at runtime. This allows features like **automatic
joins** on relationships, type-safe parameter binding, and integration with the persistence context. JPQL also supports
> entity-specific operations such as fetching associations, using aggregate functions, and navigating object graphs.

---

### 8.What is the Criteria API and when should it be used?

> The Criteria API is a type-safe, programmatic way to construct JPA queries using Java objects rather than strings.

> Criteria API allows developers to build queries dynamically with compile-time type safety, avoiding JPQL string
> errors. Queries are constructed using `CriteriaBuilder`, `CriteriaQuery`, and `Root` objects, which represent the
> query
> structure. It is especially useful when queries must be dynamic, conditional, or complex.

> Since queries are represented as Java objects, IDEs can validate types, auto-complete fields, and reduce runtime
> errors. The Criteria API integrates fully with the persistence context, ensuring that lazy loading, caching, and
> entity
> relationships are correctly managed.

---

### 9. What is the difference between Native Query and Named Query?

> A Native Query executes raw SQL directly on the database, while a Named Query is a statically defined JPQL or SQL
> query identified by a name.

- **Native Query:** Uses database-specific SQL, providing full control over query optimization and advanced SQL
  features. Less portable because it depends on the database dialect.
- **Named Query:** Defined using `@NamedQuery` (JPQL) or `@NamedNativeQuery` (SQL) annotations, precompiled at startup,
  and reusable throughout the application. Improves maintainability and readability.

> Named Queries are parsed and validated at application startup, catching errors early and allowing caching of query
> plans. Native Queries bypass JPA abstraction, which may be necessary for performance-critical queries or
> database-specific features but sacrifices portability and integration with entity state management.

---

### 10.What is the purpose of the @Entity annotation?

> `@Entity` marks a Java class as a JPA entity, making it persistable to a database table.

> When a class is annotated with `@Entity`, JPA recognizes it as a managed entity. Each instance corresponds to a row in
> a database table. The annotation allows JPA to track entity states, generate SQL for CRUD operations, and manage
> relationships and caching. An entity must have a primary key annotated with `@Id`.

> Entities are stored in the **persistence context**, where JPA ensures uniqueness, tracks changes (dirty checking), and
> synchronizes them with the database. `@Entity` triggers mapping metadata processing, enabling lazy/eager fetching and
> integration with JPQL and Criteria API queries.

---

### 11.How do @Table, @Column, and @Id annotations work?

> `@Table` maps an entity to a database table, `@Column` maps a field to a table column, and `@Id` marks a field as the
> primary key of the entity.

- `@Table(name = "table_name")` specifies the database table for the entity; if omitted, the table name defaults to the
  entity class name.
- `@Column(name = "column_name", nullable = false, unique = true, length = 255)` maps a field to a column and allows
  constraints, column length, nullability, and uniqueness to be defined.
- `@Id` identifies the primary key of the entity, which is required for JPA to uniquely identify each row. Fields
  annotated with `@Id` are often paired with `@GeneratedValue` for automatic key generation.

---

### 12.What are the differences between @GeneratedValue strategies (IDENTITY, SEQUENCE, UUID, TABLE, AUTO)?

> `@GeneratedValue` defines how primary keys are generated. Strategies differ in how the database generates or the JVM
> manages IDs.

- **IDENTITY:** Relies on the database auto-increment column; ID is generated at insert time. Limits batch inserts
  because ID is unknown before flush.
- **SEQUENCE:** Uses a database sequence object; allows preallocation of IDs and efficient batch inserts. Supports
  `@SequenceGenerator`.
- **UUID:** Generates a universally unique identifier in Java or via database function; useful for distributed systems.
- **TABLE:** Uses a dedicated table to store sequence-like values; portable but slower than native sequences.
- **AUTO:** JPA chooses the strategy based on the database dialect (often SEQUENCE for PostgreSQL, IDENTITY for MySQL).

---

### 13.How do you configure a SEQUENCE generator and @SequenceGenerator?

> `@SequenceGenerator` defines a sequence for primary key generation when using the SEQUENCE strategy.

```java

@Entity
public class Order {
    @Id
    @GeneratedValue(strategy = GenerationType.SEQUENCE, generator = "order_seq")
    @SequenceGenerator(name = "order_seq", sequenceName = "order_sequence", allocationSize = 50)
    private Long id;
}
```

- **name** : Reference name for the generator in @GeneratedValue .
- **sequence**Name : Name of the database sequence.
- **allocationsize**: Number of IDs preallocated for efficiency.

---

### 14. How does @OneToOne association work?

> @OneToOne maps a single entity to another single entity, representing a one-to-one relationship.

```java

@Entity
public class User {
    @OneToOne(cascade = CascadeType.ALL, fetch = FetchType.LAZY)
    @JoinColumn(name = "profile_id")
    private Profile profile;
}
```

- Each User has exactly one Profile.
- @JoinColumn specifies the foreign key in the owner entity table.
- Cascade types determine how operations propagate (e.g., persist, remove).
- Fetch type controls eager or lazy loading.

---

### 15. How do @OneToMany and @ManyToOne annotations work?

> @OneToMany maps a single entity to multiple related entities, and @ManyToOne maps multiple entities to a single parent
> entity. They represent bidirectional or unidirectional relationships.

```java

@Entity
public class Department {
    @OneToMany(mappedBy = "department", cascade = CascadeType.ALL, fetch = FetchType.LAZY)
    private List<Employee> employees;
}

@Entity
public class Employee {
    @ManyToOne
    @JoinColumn(name = "department_id")
    private Department department;
}

```

- mappedBy indicates the non-owning side.
- @JoinColumn defines the foreign key in the child table.
- Cascade and fetch strategies control operations and loading behavior.

---

### 16.How does @ManyToMany association work and how is JoinTable used?

> `@ManyToMany` defines a many-to-many relationship between two entities, typically managed via a join table that holds
> foreign keys to both entities.

```java

@Entity
public class Student {
    @ManyToMany(cascade = CascadeType.ALL, fetch = FetchType.LAZY)
    @JoinTable(
            name = "student_course",
            joinColumns = @JoinColumn(name = "student_id"),
            inverseJoinColumns = @JoinColumn(name = "course_id")
    )
    private Set<Course> courses;
}

@Entity
public class Course {
    @ManyToMany(mappedBy = "courses")
    private Set<Student> students;
}
```

- @JoinTable defines the linking table and the join columns.
- joincolumns references the current entity's foreign key; inverseJoincolumns references the
  other entity's foreign key.
- Bidirectional mapping is achieved using mappedBy on one side.

---

### 17.What is the difference between bidirectional and unidirectional relationships?

> Bidirectional relationships allow navigation from both entities, while unidirectional relationships allow navigation
> from only one entity.

- **Unidirectional:** Only one entity references the other; the non-owning entity has no awareness of the relationship.
- **Bidirectional:** Both entities reference each other; one side is the owner (maintains the foreign key) and the other
  is mapped with `mappedBy`.

---

### 18.What do the CascadeType values do (PERSIST, MERGE, REMOVE, DETACH, REFRESH, ALL)?

> CascadeType values determine which operations on a parent entity propagate automatically to associated child entities.

- **PERSIST:** Persists associated entities when parent is persisted.
- **MERGE:** Merges associated entities with the current persistence context.
- **REMOVE:** Deletes associated entities when parent is removed.
- **DETACH:** Detaches associated entities from the persistence context.
- **REFRESH:** Reloads associated entities from the database.
- **ALL:** Applies all cascade operations.

---

### 19. What is the difference between FetchType.LAZY and FetchType.EAGER?

> LAZY fetch delays loading of the association until accessed; EAGER fetch loads it immediately with the parent entity.

- **LAZY:** Association is proxied and loaded on access, saving memory and DB calls.
- **EAGER:** Association is loaded immediately with the parent, potentially loading unnecessary data.
-

---

### 20. What causes LazyInitializationException and how can it be solved?

> Occurs when a LAZY-loaded association is accessed outside an active persistence context.

- Happens after a session/transaction is closed.
- Solutions:
    1. Use **Open Session in View** pattern.
    2. Use **fetch joins** in JPQL (`JOIN FETCH`).
    3. Access the association within the transaction.
    4. Switch to **EAGER** fetch (careful for large collections).

---

### 21.What are @Embedded and @Embeddable annotations used for?

> `@Embeddable` marks a class as a reusable value object, and `@Embedded` embeds it into an entity.

```java

@Embeddable
public class Address {
    private String street;
    private String city;
}

@Entity
public class User {
    @Embedded
    private Address address;
}
```

---

### 22. How are @ElementCollection and @CollectionTable used?

> @ElementCollection maps a collection of basic or embeddable types, and @CollectionTable defines the table storing the
> collection.

```java

@Entity
public class User {
    @ElementCollection
    @CollectionTable(name = "user_emails", joinColumns = @JoinColumn(name = "user_id"))
    @Column(name = "email")
    private Set<String> emails;
}

```

---

### 23. What are Attribute Converters (@Convert) and when should they be used?

> Attribute converters transform entity attributes to and from database column representations.

```java

@Converter(autoApply = true)
public class BooleanToYNConverter implements AttributeConverter<Boolean, String> {
    @Override
    public String convertToDatabaseColumn(Boolean attribute) {
        return (attribute != null && attribute) ? "Y" : "N";
    }

    @Override
    public Boolean convertToEntityAttribute(String dbData) {
        return "Y".equals(dbData);
    }
}

```

---

### 24. What are EntityManagerFactory and EntityManager, and what are their responsibilities?

> `EntityManagerFactory` is a thread-safe factory that creates `EntityManager` instances, while `EntityManager` is a
> lightweight, non-thread-safe interface for managing entities and persistence operations.

- **EntityManagerFactory (EMF):**
    - Created once per application or persistence unit.
    - Reads persistence configuration (`persistence.xml` or Spring Data JPA config).
    - Manages connection pools, metadata, and provider initialization.
    - Thread-safe; can be shared across threads.
- **EntityManager (EM):**
    - Created from EMF.
    - Manages the **persistence context**, which tracks entity states (transient, managed, detached, removed).
    - Handles CRUD operations, queries, and transactional interactions.
    - Not thread-safe; typically used per transaction, request, or thread.

> The persistence context of an `EntityManager` maintains a first-level cache, ensuring each managed entity instance is
> unique in a transaction. EMF is heavyweight and expensive to create, while EM is lightweight and short-lived. Proper
> separation ensures efficient resource management and thread safety.

> `EntityManagerFactory` is the thread-safe, heavyweight factory responsible for creating and configuring
`EntityManager` instances. `EntityManager` is the lightweight interface that manages entity lifecycles, CRUD operations,
> transactions, and the persistence context. EMF provides global setup and connection management, while EM ensures
> per-transaction consistency and efficient entity state tracking.

---

### 25.How do the main EntityManager methods work (persist, merge, remove, find, refresh)?

- **persist:** Inserts a new entity and makes it managed.
- **merge:** Updates or attaches a detached entity to the persistence context.
- **remove:** Deletes a managed entity.
- **find:** Retrieves an entity by primary key.
- **refresh:** Reloads the entity state from the database.

```java
class Main {
    static void main() {
        EntityManager em = emf.createEntityManager();
        em.getTransaction().begin();

        em.persist(newEntity);   // Makes a transient entity managed and inserts it
        em.merge(detachedEntity); // Copies changes from a detached entity into a managed instance
        em.remove(managedEntity); // Deletes the entity from the database
        Entity e = em.find(Entity.class, id); // Retrieves by primary key
        em.refresh(managedEntity); // Reloads state from DB, overwriting unsaved changes

        em.getTransaction().commit();
    }
}
```

- **persist**: Throws exception if the entity already exists; entity becomes managed.
- **merge**: Returns a managed instance; the original detached entity remains detached.
- **remove**: Only works on managed entities; cascades if configured.
- **find**: First checks the persistence context, then queries the database.
- **refresh**: Forces synchronization with the database, discarding in-memory changes.

---

### 26.What is Persistence Context and Persistence Unit?

- **Persistence Context:** A set of managed entity instances tracked by an `EntityManager`.
- **Persistence Unit:** A configuration unit defining entities, data source, and JPA provider settings, typically in
  `persistence.xml`.

- **Persistence Context:**
    - Maintains the state of entities (transient, managed, detached, removed).
    - Ensures **identity guarantee**: one managed instance per entity per persistence context.
    - Supports **dirty checking** for automatic synchronization with the database.
- **Persistence Unit:**
    - Logical grouping of entities for JPA.
    - Defines connection properties, JPA provider, and caching strategies.
    - Each `EntityManagerFactory` is created for a persistence unit.

---

### 27. How is the Entity Lifecycle managed (New, Managed, Detached, Removed)?

> An entity can be in one of four states: **New (Transient), Managed, Detached, or Removed**.

- **New (Transient):** Not associated with a persistence context; not yet persisted.
- **Managed:** Associated with a persistence context; changes are tracked and flushed automatically.
- **Detached:** Previously managed but no longer associated with a persistence context; changes are not tracked.
- **Removed:** Marked for deletion; will be deleted upon transaction commit.

---

### 28.How do you create and use @NamedQuery and @NamedNativeQuery?

> `@NamedQuery` defines a reusable JPQL query, and `@NamedNativeQuery` defines a reusable native SQL query, both
> associated with an entity.

```java

@Entity
@NamedQuery(name = "User.findByEmail", query = "SELECT u FROM User u WHERE u.email = :email")
@NamedNativeQuery(name = "User.findByEmailNative", query = "SELECT * FROM users WHERE email = :email", resultClass = User.class)
public class User { ...
}

// Usage
User u = em.createNamedQuery("User.findByEmail", User.class)
        .setParameter("email", "abc@example.com")
        .getSingleResult();
```

---

### 29. What is Spring Data JPA and how does it differ from plain JPA?

> Spring Data JPA is a Spring framework module that extends JPA, providing repository abstractions, automatic query
> derivation, and integration with Spring, reducing boilerplate code compared to plain JPA.

- **Plain JPA:** Requires manual `EntityManager` operations for CRUD, queries, and transaction management. Developers
  write boilerplate code for persistence operations.
- **Spring Data JPA:** Allows defining repository interfaces (e.g., `JpaRepository`) with automatically implemented CRUD
  methods, query derivation from method names, and `@Query` annotations for custom JPQL or native SQL. Integrates
  seamlessly with Spring's dependency injection and transaction management.

> Spring Data JPA abstracts the persistence layer, allowing developers to focus on business logic rather than manual
> entity management. It works on top of any JPA provider (Hibernate, EclipseLink), automatically handling transactions,
> query execution, and paging/sorting.

---

### 30. What are the differences between Repository, CrudRepository, JpaRepository, and PagingAndSortingRepository?

- **Repository:** Marker interface for Spring Data repositories; provides typing only.
- **CrudRepository:** Adds basic CRUD operations (`save`, `findById`, `delete`).
- **PagingAndSortingRepository:** Extends `CrudRepository` with pagination and sorting capabilities.
- **JpaRepository:** Extends `PagingAndSortingRepository` with JPA-specific features like batch operations, flushing,
  and enhanced query support.

| Interface                  | Purpose                   | Key Methods/Features                                      |
|----------------------------|---------------------------|-----------------------------------------------------------|
| Repository                 | Marker interface          | Typing for Spring Data; no methods                        |
| CrudRepository             | CRUD support              | save, findById, delete, existsById, count                 |
| PagingAndSortingRepository | CRUD + pagination/sorting | findAll(Pageable), findAll(Sort)                          |
| JpaRepository              | Full JPA support          | saveAll, flush, saveAndFlush, deleteInBatch, JPQL queries |

---

### 31.How do you write custom JPQL and Native queries using @Query annotation?

> `@Query` allows defining custom JPQL or native SQL queries directly in Spring Data JPA repository methods.

```java
public interface UserRepository extends JpaRepository<User, Long> {

    // JPQL query
    @Query("SELECT u FROM User u WHERE u.email = :email")
    User findByEmail(@Param("email") String email);

    // Native SQL query
    @Query(value = "SELECT * FROM users WHERE email = :email", nativeQuery = true)
    User findByEmailNative(@Param("email") String email);
}
```

---

### 32. When are @Modifying and @Transactional required in Spring Data JPA?

> @Modifying is required for repository methods that perform INSERT, UPDATE, or DELETE; @Transactional ensures the
> operation occurs within a transaction.

```java

@Modifying
@Transactional
@Query("UPDATE User u SET u.active = false WHERE u.lastLogin < :date")
int deactivateInactiveUsers(@Param("date") LocalDate date);

```

- **@Modifying:** Indicates the query changes data, not a SELECT .
- **@Transactional:** Required to commit changes; Spring rolls back on exceptions.
- **Read-only** queries don't require @Modifying.

---

### 33. What are Specification and Querydsl, and when should they be used?

- **Specification**: JPA criteria-based query abstraction for dynamic, type-safe queries.
- **Querydsl**: Fluent API for type-safe queries in JPA or SQL.

> Specifications and Querydsl provide type-safe, dynamic query construction for JPA. Specifications use JPA Criteria
> API, while Querydsl provides a fluent, expressive DSL. Both are ideal for complex filtering, reusable predicates, and
> maintainable code in dynamic query scenarios.

```java
Specification<User> activeUsers = (root, query, cb) -> cb.equal(root.get("active"), true);
```

```java
QUser user = QUser.user;
List<User> users = new JPAQuery<>(em)
        .from(user)
        .where(user.active.isTrue())
        .fetch();

```

---

### 34. How do Hibernate 2nd Level Cache and Query Cache work?

- **2nd Level Cache**: Stores entities across sessions to reduce repeated database access. Entity-level cache shared by
  all sessions; configured via provider (Ehcache,
  Infinispan, etc.). Entities must be marked as @Cacheable .
- **Query Cache:** Stores query result sets, often referencing 2nd-level cached entities. Caches IDs returned by
  queries; requires 2nd-level cache for entity data. Must enable
  hibernate.cache.use query cache = true.

---

### 35.How do you integrate cache providers like Ehcache, Caffeine, or Infinispan?

> Configure the cache provider in Hibernate/Spring and annotate entities or queries to use caching.

```xml

<cache alias="users">
    <key-type>java.lang.Long</key-type>
    <value-type>com.example.User</value-type>
    <heap unit="entries">1000</heap>
</cache>

```

```java

@Entity
@Cacheable
@org.hibernate.annotations.Cache(usage = CacheConcurrencyStrategy.READ_WRITE)
public class User { ...
}

```

- Spring Boot: Configure spring. jpa.properties. hibernate.cache.region. factory_class and
  include provider dependency.
- Caffeine or Infinispan follow similar setup with provider-specific configuration.
- Query caching requires @QueryHints or hibernate.cache.use_query_cache = true.

---

### 36.What is @NaturalId and mutable natural ID?

> `@NaturalId` marks a domain-specific unique key in an entity, separate from the surrogate primary key. A **mutable
natural ID** allows changes to this unique field after the entity is persisted.

- **@NaturalId:** Used for alternate keys, e.g., email, username. Hibernate can optimize lookups using
  `session.byNaturalId(Entity.class).using("field", value).load()`.
- **Mutable natural ID:** Annotated with `@NaturalId(mutable = true)`. Hibernate tracks changes and ensures the natural
  ID cache is updated if modified.
- Useful when business rules require a unique identifier that may change, while maintaining surrogate primary key
  stability.

---

### 37.How is soft delete implemented in Hibernate (@SQLDelete, @Where, @Filter)?

> Soft delete marks an entity as inactive rather than removing it physically from the database. Hibernate provides
> annotations to automate this behavior.

```java

@Entity
@SQLDelete(sql = "UPDATE user SET deleted = true WHERE id = ?")
@Where(clause = "deleted = false")
public class User {
    private boolean deleted = false;
}
```

- **@SQLDelete**: Overrides the DELETE operation with an UPDATE.
- **@Where:** Filters entities automatically in queries (e.g., deleted = false ).
- **@Filter:** Allows dynamic, parameterized filtering for soft delete or multi-tenancy.

---

### 38. What new features were added in Jakarta EE 10+ and JPA 3.1/3.2?

- **Jakarta EE 10**: Complete namespace migration to jakarta.*, alignment with modern Java (17+),
  enhanced CDI, JSON Binding, REST support.
- **JPA 3.1/3.2**:
    - Support for Java Records as entities.
    - Enhanced criteria API features.
    - Improved integration with Jakarta EE 10 modules.
    - Support for optional type converters and additional JPQL functions.

---

### 39. Can JPA entities be Java Records or Sealed Classes? (Java 21+)

> Yes, JPA entities can be Java Records or Sealed Classes, with some constraints for mutability and persistence context
> compatibility.
---

### 40. What changes or benefits come with Virtual Threads (Project Loom) and JPA/Hibernate?

> Virtual Threads drastically reduce resource overhead for concurrent operations, improving scalability for
> JPA/Hibernate applications in I/O-bound scenarios.

- Virtual Threads (Java 21+) are lightweight threads managed by the JVM instead of OS threads.
- Hibernate queries blocking on DB connections can use virtual threads, allowing thousands of
  concurrent requests without exhausting OS threads.
- Integrates with JDBC drivers supporting StructuredTaskScope and reactive connection pooling.
- Minimal changes required for existing JPA code; mainly thread-per-request models benefit.

---

### 41.What is the difference between Reactive JPA (R2DBC) and traditional imperative JPA in Spring Boot 3.3+?

> Reactive JPA (R2DBC) provides non-blocking, asynchronous database access for reactive applications, whereas
> traditional JPA uses blocking, synchronous operations with `EntityManager`.

- **Imperative JPA:** Uses JDBC; each database call blocks the thread until completion. Suitable for classic,
  thread-per-request models.
- **Reactive JPA (R2DBC):** Non-blocking, reactive streams-based API; uses `Mono`/`Flux` for results, enabling high
  concurrency with fewer threads.
- Spring Data R2DBC replaces `CrudRepository`/`JpaRepository` with reactive repositories (`ReactiveCrudRepository`).
- Reactive model requires R2DBC-compatible drivers and reactive transaction management.

---

### 42.How do you configure auditing (@CreatedDate, @LastModifiedDate, @CreatedBy, @LastModifiedBy)?

**Short answer:**  
Auditing annotations automatically populate metadata fields for entity creation, modification, and user tracking.

**Detailed explanation:**

```java

@Entity
@EntityListeners(AuditingEntityListener.class)
public class User {
    @CreatedDate
    private LocalDateTime createdDate;

    @LastModifiedDate
    private LocalDateTime modifiedDate;

    @CreatedBy
    private String createdBy;

    @LastModifiedBy
    private String modifiedBy;
}

// Enable auditing in Spring Boot
@EnableJpaAuditing
@Configuration
public class JpaConfig {
}
```

- Requires @EntityListeners(AuditingEntityListener.class) on entities.
- Spring Security or a custom auditor aware bean can provide the current user.

---

### 43. How does @EntityGraph help solve the N+1 select problem?

> @EntityGraph allows defining fetch plans to eagerly load associations, reducing multiple queries that cause N+1
> problems.

```java

@EntityGraph(attributePaths = { "orders", "profile" })
List<User> findAll();
```

- Fetches User and related orders and profile in a single query or minimal joins.
- Overrides default FetchType. LAZY when executing the query.
- Prevents multiple separate SQL queries for each association.

---

### 44. What is the N+1 select problem and how can it be prevented?

> N+1 occurs when fetching N parent entities triggers additional queries for each child entity due to lazy loading.
> N+1 reduces performance dramatically in large datasets. Tools like Hibernate statistics or logs can detect excessive
> queries. Proper fetch planning and batching is essential in high-throughput applications.

**Prevention strategies**:

1. Use **JOIN FETC** in JPQL.
2. Use **@EntityGraph**.
3. Use batch fetching (**hibernate. default_batch_fetch_size** ).
4. Consider **DTO projections** to fetch only required fields.

---

### 45. How do Optimistic Locking (@Version) and Pessimistic Locking work?

- **Optimistic Locking** ( @Version): Detects concurrent updates using a version field; suitable for low
  contention.
- **Pessimistic Locking**: Locks rows in the database during a transaction; prevents concurrent updates.

Optimistic Locking*

```java

@Version
private Integer version;
```

- Hibernate increments the version on update.
- Concurrent updates on the same entity throw OptimisticLockException .

Pessimistic Locking:

```java
em.find(User .class, id, LockModeType.PESSIMISTIC_WRITE);
```

- Database locks the row until the transaction commits.
- Prevents concurrent modifications but can reduce throughput.

> Optimistic locking is ideal for high-read, low-write scenarios, minimizing database locks and deadlocks. Pessimistic
> locking is safer for high-contention situations but can cause thread blocking and decreased scalability.
---

### 46.

>
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