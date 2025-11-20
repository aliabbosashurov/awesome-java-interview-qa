# Mongo / NoSQL

### 1. What is NoSQL in one sentence?

> NoSQL is a class of databases designed for flexible schema, horizontal scalability, and high-performance operations on
> large volumes of structured, semi-structured, or unstructured data.

- Unlike relational databases, NoSQL databases do not require fixed schemas or SQL for queries.
- They are optimized for distributed storage, high throughput, and low-latency access.
- Often used in big data, real-time analytics, and microservices architectures.

> NoSQL databases trade off strict ACID guarantees for scalability, schema flexibility, and performance, leveraging
> eventual consistency or other distributed consistency models.
> NoSQL enables modern applications to efficiently store and query heterogeneous and large-scale datasets without rigid
> relational constraints, making it ideal for cloud-native and high-throughput systems.

---

### 2. What are the main types of NoSQL databases?

> NoSQL databases are categorized into **document, key-value, column-family, and graph** databases based on data model
> and access patterns.

- **Document:** Stores JSON-like documents (e.g., MongoDB, Couchbase). Flexible schema; good for hierarchical or
  semi-structured data.
- **Key-Value:** Stores data as key-value pairs (e.g., Redis, DynamoDB). Extremely fast lookups.
- **Column-Family:** Stores data in column families, optimized for analytics and sparse datasets (e.g., Cassandra,
  HBase).
- **Graph:** Stores entities as nodes and relationships as edges (e.g., Neo4j, Amazon Neptune). Optimized for connected
  data and relationship queries.

> These types reflect trade-offs in query flexibility, performance, storage layout, and consistency models, allowing
> architects to choose based on use case.
> Understanding NoSQL types helps engineers design scalable, performant, and appropriate storage for modern
> applications, from caching and messaging to analytics and graph traversals.

---

### 3. What is MongoDB and what type of NoSQL is it?

> MongoDB is a high-performance, open-source **document-oriented NoSQL database**.

- Stores data as flexible, JSON-like documents with dynamic schema.
- Supports secondary indexes, aggregation pipelines, and replication for high availability.
- Horizontally scalable via sharding.

> MongoDB internally uses BSON (binary JSON) for efficient storage and retrieval, providing type support and optimized
> memory layout.
> MongoDB is ideal for applications needing flexible schemas, hierarchical data, and rapid development, providing a
> modern alternative to relational databases in many microservices and cloud-native architectures.

---

### 4. What is a Document in MongoDB?

> A document in MongoDB is a JSON-like data structure that represents a single record or object.

- Stored in BSON format for efficiency.
- Can contain nested documents, arrays, and complex types.
- Analogous to a “row” in relational databases but schema-free.

> Documents allow flexible modeling of hierarchical and semi-structured data without enforcing rigid schemas, reducing
> object-relational impedance mismatch.
> MongoDB documents provide self-contained, expressive data units, supporting rapid iteration and nested data structures
> naturally.

---

### 5. What is a Collection in MongoDB?

> A collection in MongoDB is a grouping of documents, analogous to a table in relational databases.

- Does not enforce schema—different documents in the same collection can have different structures.
- Supports indexes, validation rules, and sharding.
- Named logically to represent entity types (e.g., `users`, `orders`).

> Collections provide logical organization, efficient queries, and scalable storage while retaining the schema
> flexibility of individual documents.
> In practice, collections are the fundamental unit for CRUD operations, aggregation, and indexing in MongoDB.

---

### 6. What is BSON? Why does MongoDB use it instead of plain JSON?

> BSON (Binary JSON) is a binary-encoded serialization format used by MongoDB for documents.

- Stores data types not supported by JSON, such as `Date`, `Binary`, `ObjectId`, and `Decimal128`.
- Optimized for fast traversal, indexing, and storage efficiency.
- Enables efficient memory layout and network transport.

> Unlike JSON, which is text-based and lacks certain type fidelity, BSON provides a compact, type-rich, and performant
> representation of documents for internal processing.
> MongoDB uses BSON to combine human-readable document structure with high-performance binary storage, enabling rich
> types, efficient querying, and indexing without sacrificing flexibility.

---

### 7. What is the primary key called in MongoDB? (ObjectId vs custom _id)

> The primary key in MongoDB is `_id`, which uniquely identifies each document within a collection.

- **ObjectId:** Default 12-byte identifier generated automatically; encodes timestamp, machine ID, process ID, and
  counter for uniqueness.
- **Custom _id:** Developers can assign a custom value (string, number, UUID, etc.) as the `_id` field.
- `_id` is automatically indexed to ensure fast lookups and uniqueness.

> The `_id` field guarantees each document’s identity within a collection, serving as the basis for efficient indexing,
> replication, and sharding in distributed MongoDB clusters.
> MongoDB uses `_id` as a flexible and mandatory primary key to ensure data integrity and performance, while allowing
> developers to choose auto-generated `ObjectId` or application-defined identifiers based on business requirements.

---

### 8.When would you choose MongoDB over PostgreSQL/MySQL in a Spring Boot project? When would you never choose it?

> Choose MongoDB when schema flexibility, hierarchical data, or high write scalability matters; avoid it when strict
> ACID relational constraints or complex joins are required.

- **Use MongoDB when:**
    - Data schema is evolving or heterogeneous (JSON-like documents).
    - Application requires horizontal scaling (sharding) and high throughput.
    - Working with hierarchical, nested, or semi-structured data.
    - Rapid prototyping or agile development where schema changes are frequent.

- **Avoid MongoDB when:**
    - Strict ACID transactions across multiple entities are required (complex multi-table operations).
    - Extensive relational queries with joins are core to business logic.
    - Reporting or analytics rely heavily on normalized relational structures.

> MongoDB provides flexibility, scalability, and fast reads/writes for dynamic, document-oriented workloads, whereas
> relational databases ensure strict consistency and structured relationships.
> In Spring Boot, MongoDB is ideal for microservices, caching, logging, and JSON-heavy APIs, while PostgreSQL/MySQL is
> preferred for banking, ERP, and other relationally-intensive systems.

---

### 9.How does Spring Data MongoDB map Java objects to MongoDB documents?

> Spring Data MongoDB maps Java objects to BSON documents using **mapping metadata and converters**.

- Uses `@Document` on classes to denote a collection.
- Uses `@Id` to map the primary key (`_id`).
- Field names are automatically mapped; custom names via `@Field`.
- Nested objects are recursively mapped as embedded documents.
- Supports type conversions via `MongoConverter` (SimpleMongoConverter, MappingMongoConverter).

> Internally, Spring Data MongoDB converts Java objects to `Document` objects, serializes them to BSON, and performs
> CRUD operations via `MongoTemplate` or repository abstractions.
> This abstraction allows developers to work with plain Java objects while maintaining flexibility and type safety,
> without manually serializing or parsing BSON.

---

### 10.What is the difference between `@Entity` (JPA) and `@Document` (MongoDB)?

> `@Entity` marks a class as a relational database entity, while `@Document` marks a class as a MongoDB document stored
> in a collection.

- **@Entity**: Requires a relational table, primary key, and schema mapping. Supports JPA features like `@OneToMany`,
  lazy loading, and JPQL.
- **@Document**: Maps to a MongoDB collection, supports flexible, nested structures, and does not enforce a schema.

> While `@Entity` relies on ORM and SQL, `@Document` relies on BSON serialization, allowing schema-less storage and
> hierarchical data representation.
> Choosing between them reflects the underlying database choice: relational vs document-oriented.

---

### 11.What is the difference between `MongoRepository` and `MongoTemplate`? When do you use which?

> `MongoRepository` is a declarative repository interface for CRUD and query methods; `MongoTemplate` is a lower-level,
> imperative API for complex queries and operations.

- **MongoRepository**
    - Extends `PagingAndSortingRepository` and `CrudRepository`.
    - Automatically provides CRUD, pagination, and query derivation (`findByName`, `findByAgeGreaterThan`).
    - Declarative, easy-to-use, good for standard operations.

- **MongoTemplate**
    - Low-level API for fine-grained control.
    - Supports complex queries, aggregations, transactions, and index management.
    - Required for custom operations that cannot be expressed via repository method names or annotations.

---

### 12.How do you implement pagination with Spring Data MongoDB? Explain `Page` vs `Slice` vs `Pageable`.

> Pagination in Spring Data MongoDB is implemented via `Pageable` for request parameters, returning `Page` or `Slice`.

- **Pageable**: Interface for page request info (page number, size, sort).
- **Page**: Contains content + total elements + total pages + metadata.
- **Slice**: Contains content + `hasNext()` flag; does not require total count query (more efficient for large
  datasets).

```java
Page<User> page = userRepository.findByStatus("ACTIVE", PageRequest.of(0, 10));
Slice<User> slice = userRepository.findByStatus("ACTIVE", PageRequest.of(0, 10));
```

> Slice is preferred for infinite scroll or streaming scenarios, Page is used when total count is needed.

---

### 13.How do you write custom queries using @Query and @Aggregation in Spring Data MongoDB?

> @Query defines JSON-style MongoDB queries; @Aggregation defines pipeline-based aggregations.

```java

@Query("{ 'age' : { $gte: ?0 } }")
List<User> findUsersOlderThan(int age);

@Aggregation(pipeline = {
        "{ $match: { status: 'ACTIVE' } }",
        "{ $group: { _id: '$role', count: { $sum: 1 } } }"
})
List<RoleCount> countActiveUsersByRole();

```

---

### 14. What are common performance pitfalls when using Spring Data MongoDB?

> Common performance pitfalls include unindexed queries, excessive data fetching, and misuse of schema modeling leading
> to high latency and memory pressure.

- **Unindexed queries:** Queries without appropriate indexes cause full collection scans.
- **Large documents or embedded arrays:** Fetching unnecessarily large or deeply nested documents increases memory and
  network overhead.
- **Excessive `findAll()` usage:** Loading entire collections instead of paginated or filtered queries.
- **Improper schema modeling:** Over-embedding large arrays or frequent references causing multiple round trips.
- **Ignoring projection:** Fetching all fields instead of only required fields increases payload and processing.
- **Blocking operations on reactive contexts:** Using blocking `MongoTemplate` calls in reactive pipelines can reduce
  throughput.

> At the MongoDB engine level, slow queries trigger collection scans, increasing CPU, I/O, and lock contention;
> unsharded large collections may exacerbate performance issues.
> Avoiding these pitfalls requires careful indexing, projection, pagination, embedding vs referencing decisions, and
> using reactive or streaming APIs for large datasets.

---

### 15. How do you use the Aggregation framework with Spring Data MongoDB?

> The Aggregation framework allows complex data processing pipelines using stages like `$match`, `$group`, `$sort`,
`$project`, etc., directly mapped via Spring Data.

- Use `Aggregation` and `AggregationOperations` classes in `MongoTemplate`:

```java
Aggregation agg = Aggregation.newAggregation(
        Aggregation.match(Criteria.where("status").is("ACTIVE")),
        Aggregation.group("role").count().as("count"),
        Aggregation.sort(Sort.Direction.DESC, "count")
);

AggregationResults<RoleCount> results = mongoTemplate.aggregate(agg, "users", RoleCount.class);
```

---

### 16.How do you handle large or streaming results from MongoDB in Spring Boot?

> For large datasets, use streaming with MongoTemplate.stream() or reactive Flux from ReactiveMongoTemplate to process
> data efficiently without loading everything into memory.

```java
try(CloseableIterator<User> cursor = mongoTemplate.stream(
        query(where("status").is("ACTIVE")), User.class)){
        cursor.

forEachRemaining(user ->

process(user));
        } // or with reactive approach
```

---

### 17.How do you configure multiple MongoDB databases in one Spring Boot app?

> Multiple MongoDB databases can be configured by defining separate `MongoTemplate` and `MongoDatabaseFactory` beans for
> each database.

- Define `MongoProperties` for each database in `application.yml` or `application.properties`.
- Create `MongoClient`/`MongoDatabaseFactory` beans for each database:

```java

@Configuration
public class MultiMongoConfig {

    @Bean
    @Primary
    public MongoTemplate primaryMongoTemplate(@Qualifier("primaryFactory") MongoDatabaseFactory factory) {
        return new MongoTemplate(factory);
    }

    @Bean
    @Primary
    public MongoDatabaseFactory primaryFactory() {
        return new SimpleMongoClientDatabaseFactory("mongodb://user:pass@host:27017/primaryDB");
    }

    @Bean
    public MongoTemplate secondaryMongoTemplate(@Qualifier("secondaryFactory") MongoDatabaseFactory factory) {
        return new MongoTemplate(factory);
    }

    @Bean
    public MongoDatabaseFactory secondaryFactory() {
        return new SimpleMongoClientDatabaseFactory("mongodb://user:pass@host:27017/secondaryDB");
    }
}
```

- Use @Qualifier to inject the correct template in repositories or services.

> Each MongoTemplate is tied to a specific database and allows independent operations, enabling multi-database Spring
> Boot
> applications.
> This approach allows isolation, transactional boundaries, and independent configuration for each MongoDB database in
> the
> same application context.
---

### 18.How do you define compound indexes and TTL indexes with Spring Data MongoDB?

> Spring Data MongoDB supports index creation via annotations or programmatically using MongoTemplate.

- **Compound index**: Combines multiple fields.

```java

@Document
@CompoundIndexes({
        @CompoundIndex(name = "email_status_idx", def = "{'email' : 1, 'status': -1}")
})
public class User { ...
}

```

- **TTL index**: Automatically expires documents after a certain duration.
```java
@Document
public class Session {
    @Id private String id;

    @Indexed(name = "expireAtIndex", expireAfterSeconds = 3600)
    private Instant createdAt = Instant.now();
}

```

---

### 19.

>
---

### 20.

>
---

### 21.

>
---

### 22.

>
---

### 23.

>
---

### 24.

>
---

### 25.

>
---

### 26.

>
---

### 27.

>
---

### 28.

>
---

### 29.

>
---

### 30.

>
---

### 31.

>
---

### 32.

>
---

### 33.

>
---

### 34.

>
---

### 35.

>
---

### 36.

>
---

### 37.

>
---

### 38.

>
---

### 39.

>
---

### 40.

>
---

### 41.

>
---

### 42.

>
---

### 43.

>
---

### 44.

>
---

### 45.

>
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