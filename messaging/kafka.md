# Kafka

### 1. What is Apache Kafka?

> Apache Kafka is a distributed, high-throughput, fault-tolerant event streaming platform designed for real-time data
> pipelines and messaging.

- Kafka allows applications to **publish and subscribe to streams of records** in a durable, scalable, and low-latency
  manner.
- It is optimized for **high-throughput, horizontal scalability, and durability**, making it suitable for event-driven
  architectures, log aggregation, and stream processing.
- Kafka decouples producers and consumers, enabling **real-time data integration across distributed systems**.

> Internally, Kafka uses a **distributed commit log architecture**, allowing sequential writes to disk for fast
> persistence and linear scalability across clusters.
>
> Kafka is the backbone for modern streaming systems, enabling real-time analytics, event-driven microservices, and
> large-scale data pipelines with guaranteed delivery and fault tolerance.

---

### 2. What are the main components of Kafka?

> Kafka consists of **Producers, Consumers, Brokers, Topics, Partitions, and a metadata service (ZooKeeper or KRaft)**
> that manage cluster coordination.

- **Producer:** Publishes records to Kafka topics.
- **Consumer:** Subscribes to topics and processes records.
- **Broker:** Kafka server that stores data and serves client requests.
- **Topic:** Logical stream of messages categorized by name.
- **Partition:** Ordered, immutable sequence of messages within a topic, providing parallelism.
- **ZooKeeper/KRaft:** Manages cluster metadata, leader election, and configuration (KRaft mode removes the ZooKeeper
  dependency).

> Kafka’s architecture separates **data storage, processing, and metadata management**, enabling massive scalability and
> reliability.
>
> These components allow Kafka to **decouple producers and consumers**, achieve fault tolerance via replication, and
> maintain strong consistency guarantees in distributed deployments.

---

### 3. What is a Topic in Kafka?

> A topic is a named stream of records to which producers write and from which consumers read.

- Topics provide **logical organization** for messages.
- Kafka topics are **multi-subscriber**, allowing multiple consumers to independently read the same stream.
- Each topic can be divided into **partitions** for parallelism and scalability.

> Topics abstract the underlying **distributed commit log**, making it easy to reason about data streams and retention
> policies.
>
> Topics are the fundamental unit of Kafka messaging, enabling efficient **data decoupling, partitioned scaling, and
configurable retention**.

---

### 4. What is a Partition in Kafka and why does Kafka use partitions?

> A partition is an **ordered, immutable sequence of messages** within a topic, providing parallelism, scalability, and
> ordering guarantees.

- Each partition has a **unique offset** for each message.
- Partitions allow Kafka to **scale horizontally** by distributing messages across multiple brokers.
- They provide **parallel consumption**, enabling high throughput for large data streams.
- Partitions are the unit of **replication** for fault tolerance.

> Kafka’s partitions ensure **message ordering within a partition** while allowing distributed, scalable storage across
> brokers.
>
> Partitions are key to Kafka’s **high throughput and fault tolerance**, enabling linear scalability and fine-grained
> parallel processing in modern streaming applications.

---

### 5. What is a Producer in Kafka? How does it work?

> A producer is a client that **publishes messages to Kafka topics**, deciding which partition each message should go
> to.

- Producers can use **key-based partitioning** to maintain order within a partition.
- Messages can be sent **synchronously or asynchronously**.
- Kafka producer clients **batch messages** for high throughput and use compression to optimize network and storage
  usage.
- Acks configuration (`acks=0,1,all`) controls durability guarantees.

> Kafka producers interact directly with **brokers and partition leaders**, using efficient binary protocols to minimize
> latency while ensuring reliability.
>
> Producers are responsible for **efficient, ordered, and reliable data ingestion** into Kafka, balancing throughput,
> latency, and durability according to the application’s needs.

---

### 6. What is a Consumer in Kafka? How does it work?

> A consumer is a client that **subscribes to topics and processes messages**, tracking offsets for reliable
> consumption.

- Consumers read messages from **specific partitions** and can start from **earliest, latest, or specific offsets**.
- Kafka supports **manual or automatic offset commits** for flexible delivery semantics.
- Consumers typically operate within **consumer groups** to share workload and ensure scalability.
- Each consumer in a group is assigned **exclusive partitions**, enabling parallel processing.

> Consumers interact with brokers and track offsets via **Kafka’s internal __consumer_offsets topic**, allowing
> fault-tolerant, replayable consumption.
>
> Consumers enable **scalable and reliable processing** of Kafka streams, supporting both real-time and batch processing
> scenarios while maintaining partition ordering guarantees.

---

### 7. What is a Consumer Group? Why is it important?

> A consumer group is a **set of consumers that jointly consume messages from a topic**, ensuring each message is
> processed exactly once by the group.

- Each partition is consumed by **only one consumer** in a group at a time.
- Consumer groups enable **horizontal scalability**: more consumers can handle more partitions.
- They allow **fault tolerance**: if a consumer fails, another takes over its partitions.

> Consumer groups implement **dynamic partition assignment and rebalance** via the group coordinator in the broker.
>
> Consumer groups are critical for **load distribution, scalability, and reliable processing** in distributed streaming
> applications.

---

### 8. How does Kafka guarantee message ordering?

> Kafka guarantees **message ordering within a partition**, but not across partitions.

- Messages are written sequentially to **partition logs** and assigned a **monotonic offset**.
- Consumers read partitions **in offset order**, preserving order.
- To maintain order, producers can **use a key** to ensure related messages go to the same partition.

> Kafka relies on **partition-level sequential logs**, avoiding global locking and enabling high throughput while still
> preserving ordering guarantees.
>
> By combining **partitioning and offset tracking**, Kafka allows applications to maintain **deterministic processing
order** for related messages, which is sufficient for most real-time streaming use cases.

---

### 9. How does Kafka achieve fault tolerance and high availability?

> Kafka achieves fault tolerance via **replication, ISR (In-Sync Replicas), and leader election** for partitions.

- Each partition has **replicas** on multiple brokers; one replica is the **leader**, others are followers.
- Followers replicate data from the leader and maintain **synchronized state**.
- If a leader fails, a follower from the **ISR** is promoted automatically.
- This ensures **no data loss** (depending on producer acks) and continuous availability.

> Kafka uses **quorum-based replication**: only replicas fully caught up in the ISR are eligible to become leaders,
> preventing split-brain or stale reads.
>
> Fault tolerance in Kafka is designed for **high availability, minimal downtime, and strong consistency guarantees**,
> making it suitable for mission-critical streaming applications.

---

### 10. What is the role of replication factor and ISR (In-Sync Replicas)?

> The replication factor defines **how many copies of each partition exist**, while the ISR tracks which replicas are
> fully synchronized with the leader.

- **Replication Factor:** Determines durability and fault tolerance; higher values mean more resilience.
- **ISR:** Subset of replicas that are fully caught up; only these can become leaders on failure.
- Replicas outside ISR are temporarily **lagging** and not eligible for leader promotion.

> Kafka’s replication mechanism ensures **strong consistency, durability, and automated failover**, balancing
> performance and reliability.
>
> Replication factor and ISR collectively ensure that Kafka partitions remain **highly available and durable**, even in
> the presence of broker failures, while providing predictable recovery behavior.

---

### 11. What are offsets in Kafka? How are they managed?

> Offsets are **unique sequential identifiers for messages within a partition**, tracking consumption progress.

- Each message in a partition has a **monotonically increasing offset**.
- Consumers track offsets to know which messages have been read.
- Offsets can be **committed automatically or manually** to Kafka’s `__consumer_offsets` topic.
- Enables **replay, fault tolerance, and exactly-once or at-least-once delivery semantics**.

> Offsets are not stored in brokers per se for consumers; the **Kafka internal topic** manages committed offsets, and
> consumers can restart reading from any offset, enabling flexible replay and recovery.
>
> Offsets are fundamental to Kafka’s **reliable, replayable consumption model**, allowing consumers to track progress
> independently while maintaining ordering guarantees within partitions.

---

### 12. What happens when a broker fails? How does Kafka handle it?

> Kafka handles broker failures through **partition leader election and replication**.

- Each partition has a **leader** and multiple followers (replicas).
- If a broker hosting a leader fails, a follower from the **ISR (in-sync replicas)** is promoted as the new leader.
- Producers and consumers automatically **redirect requests to the new leader**.
- Unavailable brokers eventually **resynchronize replicas** when they come back online.

> Kafka’s fault tolerance relies on **quorum-based ISR replication**, ensuring high availability and minimal downtime
> while avoiding stale reads.
>
> Broker failure handling ensures **continuous data availability, durability, and minimal disruption** in distributed
> streaming workloads.

---

### 13. What is the difference between acks=0, acks=1, and acks=all?

> `acks` controls **producer durability guarantees** by specifying how many broker acknowledgments are required for a
> write.

- `acks=0`: Producer does not wait for a broker response → **highest throughput, potential data loss**.
- `acks=1`: Waits for **leader acknowledgment** → moderate durability, risk if leader fails before replication.
- `acks=all` (or `-1`): Waits for **all ISR replicas** → strongest durability guarantee, slight latency tradeoff.

> Kafka uses **replication and ISR coordination** to implement `acks=all`, ensuring no messages are lost as long as at
> least one ISR replica survives.
>
> Configuring `acks` balances **latency, throughput, and data durability**, making it critical for production-grade
> systems depending on reliability requirements.

---

### 14. What is consumer rebalancing? When does it happen and what triggers it?

> Consumer rebalancing is the process of **redistributing partitions among consumers in a group**.

- Occurs when:
    - A consumer **joins or leaves** a group.
    - A **subscription changes** (e.g., new topics).
    - Broker or partition **metadata changes**.
- During rebalance, **consumers stop reading**, partitions are reassigned, then consumption resumes.

> Kafka’s group coordinator triggers rebalances to maintain **exclusive partition ownership** per consumer while
> ensuring workload distribution and fault tolerance.
>
> Rebalancing ensures **scalable, reliable, and consistent consumption** across dynamic consumer groups, but may
> temporarily pause processing, so careful tuning of session timeouts is important.

---

### 15. What is consumer lag? How do you monitor it?

> Consumer lag is the **difference between the latest offset in a partition and the offset a consumer has processed**.

- High lag indicates the consumer is **behind the producer**.
- Monitored via:
    - Kafka metrics (`records-lag-max`, `records-lag`).
    - Tools like **Kafka Consumer Group CLI, Prometheus, or Confluent Control Center**.
- Helps detect **slow consumers or bottlenecks** in processing pipelines.

> Lag is a **key operational metric**, reflecting throughput mismatches and potential performance issues in real-time
> streaming.
>
> Monitoring consumer lag ensures **streaming applications meet SLAs**, avoid backlogs, and maintain predictable
> real-time behavior.

---

### 16. Explain the producer configuration: linger.ms and batch.size

> `linger.ms` and `batch.size` control **message batching for throughput optimization**.

- `batch.size`: Maximum bytes of messages to accumulate before sending to a partition.
- `linger.ms`: Maximum time to wait for additional messages before sending a batch.
- Together, they **increase network and disk efficiency** by reducing small, frequent requests.

> Proper tuning balances **latency vs throughput**, e.g., higher linger.ms and batch.size improve throughput but may
> increase latency slightly.
>
> These configurations help **maximize producer efficiency**, particularly in high-volume pipelines, while preserving
> reliability guarantees.

---

### 17. What is log compaction? When would you use it?

> Log compaction retains **only the latest value for each key** in a topic, removing older duplicates.

- Maintains **key-based state**, unlike retention-based deletion.
- Useful for **change-data-capture (CDC) streams**, **materialized views**, or **stateful applications**.
- Compacted logs guarantee **latest update per key is always available**, even after failures.

> Compaction allows Kafka to **store evolving datasets efficiently**, providing durable state snapshots for downstream
> consumers without requiring full deletion-based retention.
>
> Log compaction is essential for **stateful, replayable event streams**, enabling efficient storage and reliable state
> reconstruction.

---

### 18. What is the difference between Kafka and traditional message queues (like RabbitMQ)?

> Kafka is a **distributed log-based streaming platform**, whereas RabbitMQ is a **message broker with queue-based
delivery**.

- Kafka:
    - Stores messages **durably and in order** with offsets.
    - Consumers can **replay messages**.
    - Scales horizontally via **partitions**.
- RabbitMQ:
    - Messages are **pushed to queues**; once consumed, they are removed.
    - Focuses on **complex routing and low-latency delivery**.
    - Scaling requires clustering or federation.

> Kafka is optimized for **high-throughput, fault-tolerant streaming**, while traditional queues excel in **low-latency,
transactional messaging**.
>
> The choice depends on **use case**: Kafka for event streaming and large-scale pipelines; RabbitMQ for task queues,
> RPC, or low-latency messaging.

---

### 19. What is Kafka Streams? How is it different from writing a normal consumer?

> Kafka Streams is a **library for building stateful stream processing applications** on top of Kafka.

- Provides **high-level abstractions**: KStream, KTable, aggregations, joins, windowing.
- Automatically handles **state management, fault tolerance, and scaling**.
- Normal consumers require **manual offset management, state handling, and aggregation logic**.

> Kafka Streams leverages **local state stores and changelog topics**, making stream processing **fault-tolerant,
exactly-once, and scalable**.
>
> Kafka Streams simplifies **building real-time analytics and transformations** while eliminating boilerplate and
> ensuring robust distributed state handling compared to raw consumers.

---

### 20. What is Kafka Connect? What are source and sink connectors?

> Kafka Connect is a **framework to integrate Kafka with external systems** via pluggable connectors.

- **Source connectors:** Pull data from external systems into Kafka topics (e.g., databases, logs).
- **Sink connectors:** Push data from Kafka topics to external systems (e.g., data warehouses, Elasticsearch).
- Supports **scaling, fault tolerance, and configuration-driven pipelines**.

> Kafka Connect abstracts **integration complexity**, offering a declarative, scalable approach for ingesting and
> exporting data without writing custom consumers or producers.
>
> Kafka Connect enables **streamlined, production-ready data pipelines**, bridging Kafka with diverse external systems
> efficiently and reliably.

---

### 21. How does Kafka handle message delivery guarantees?

> Kafka supports **at-most-once, at-least-once, and exactly-once delivery semantics**, controlled via producer acks,
> retries, and transactional APIs.

- **At-most-once:** Messages may be lost, but never duplicated.
- **At-least-once:** Messages are never lost, but duplicates can occur.
- **Exactly-once:** Messages are delivered once and only once using **idempotent producers and transactions**.
- Delivery guarantees depend on **producer configuration (`acks`, retries, idempotence) and consumer offset management
  **.

> Kafka achieves delivery guarantees through a combination of **partition logs, ISR replication, offset tracking, and
transactional APIs**, ensuring reliability in distributed streaming environments.
>
> By carefully configuring producers and consumers, Kafka enables **robust, predictable delivery semantics** suitable
> for real-time pipelines and stateful stream processing.

---

### 22. What is the purpose of the Kafka Schema Registry?

> The Schema Registry enforces **structured data formats and compatibility** for messages in Kafka topics.

- Stores **Avro, JSON, or Protobuf schemas** centrally.
- Validates **producer and consumer schema compatibility** to prevent breaking changes.
- Enables **evolution of schemas** (backward, forward, or full compatibility).

> Schema Registry integrates with Kafka to **enforce type safety and structured messaging**, reducing runtime errors and
> supporting data governance.
>
> Using Schema Registry ensures **reliable, evolvable, and self-describing event streams**, which is critical for
> large-scale enterprise pipelines.

---

### 23. What is Kafka’s retention policy? How does it manage disk usage?

> Kafka retention policy defines **how long messages are retained in topics** before being deleted or compacted.

- Two main retention strategies:
    - **Time-based retention (`retention.ms`)**: Messages older than the configured time are deleted.
    - **Size-based retention (`retention.bytes`)**: Oldest messages are deleted when topic size exceeds the limit.
- Topics can also be configured for **log compaction**, retaining only the latest value per key.
- Kafka periodically **trims logs**, freeing disk space while ensuring durability based on the configured policy.

> Retention policies allow Kafka to **control disk usage efficiently** while maintaining reliable storage for both
> streaming and replay use cases.
>
> Properly configured retention ensures **durable, predictable storage**, supports replay and auditing, and prevents
> disk exhaustion in production clusters.

---

### 24. What is KRaft? Why did Kafka remove ZooKeeper?

> KRaft (Kafka Raft Metadata mode) is **Kafka’s internal metadata management system**, replacing ZooKeeper.

- KRaft **manages cluster metadata, controller election, and topic configurations** using the Raft consensus algorithm.
- Kafka removed ZooKeeper to **simplify deployment, reduce operational complexity, and improve scalability**.

> KRaft allows Kafka to **control replication, leader election, and cluster membership natively**, removing an external
> dependency and streamlining operations.
>
> KRaft is the **modern architecture for Kafka metadata management**, enabling self-contained clusters with better fault
> tolerance and maintainability.

---

### 25. commitSync() vs commitAsync() – when to use which?

> `commitSync()` blocks until offsets are committed, while `commitAsync()` commits offsets asynchronously without
> blocking.

- **commitSync():** Guarantees offset is saved before proceeding → use when **strong consistency is required**.
- **commitAsync():** Non-blocking, higher throughput → use for **performance-sensitive applications**, optionally with a
  callback to handle failures.

> Synchronous commits **ensure predictable failure semantics**, while asynchronous commits **maximize throughput** but
> require careful error handling.
>
> Choosing between the two depends on **trade-offs between reliability and performance** in your consumer design.

---

### 26. How do you increase replication factor or number of partitions safely?

> Replication factor and partitions can be increased using **Kafka admin APIs or command-line tools**, but must consider
> data movement and ordering guarantees.

- **Increasing partitions:** Use `kafka-topics --alter --partitions`. Note: new partitions **do not preserve ordering**
  for existing messages.
- **Increasing replication factor:** Use `kafka-reassign-partitions` with a **reassignment JSON plan**. Avoid data loss
  by ensuring **all replicas are in-sync (ISR)** during migration.

> Partition and replication management involve **careful coordination of reassignments** to maintain high availability
> and minimal downtime.
>
> Safe scaling ensures **performance improvements and fault tolerance** without violating ordering or delivery
> guarantees.

---

### 27. What is the default partitioner? How does key hashing work?

> Kafka uses the **DefaultPartitioner**, which maps messages with a key to a partition using **hash(key) % numPartitions
**.

- Messages with the **same key always go to the same partition**, ensuring order.
- Messages without a key are **round-robin distributed** across partitions.

> Key hashing ensures **deterministic partition assignment**, enabling ordered processing per key while balancing load
> across partitions.
>
> Proper key selection is critical for **even load distribution and maintaining message ordering** in production topics.

---

### 28. What are the trade-offs of having too many partitions? How do you manually reassign partitions?

> Having too many partitions increases **parallelism** but can hurt **throughput, metadata overhead, and GC pressure**.

- Trade-offs:
    - Higher **memory and network load** on brokers.
    - Longer **leader election and recovery times**.
    - Increased **consumer metadata tracking overhead**.
- Manual reassignment: use `kafka-reassign-partitions` with a **JSON plan specifying partition-to-broker mapping**.

> Partition management is a balance between **scalability, parallelism, and broker resource utilization**.
>
> Proper planning avoids **performance bottlenecks** while enabling fine-grained scaling and balanced cluster load.

---

### 29. What is the difference between auto.offset.reset = earliest vs latest?

> This config determines **where a consumer starts reading when no committed offset exists**.

- `earliest`: Start from the **beginning of the partition**.
- `latest`: Start from the **end of the partition** (new messages only).

> Choice depends on whether you need **historical data replay** or only **real-time processing**.
>
> Correct configuration ensures **expected consumption behavior**, especially for new consumers joining existing topics.

---

### 30. When would you disable auto-commit and manage offsets manually?

> Manual offset management is used when **exactly-once or at-least-once delivery semantics** are required.

- Auto-commit may **commit offsets before processing completes**, risking data loss on failure.
- Manual commit allows **control after successful processing**, enabling retries and failure recovery.

> Manual offset control is essential for **fault-tolerant, idempotent, or transactional stream processing**.
>
> Disabling auto-commit ensures **reliable, predictable consumption**, especially in critical pipelines.

---

### 31. What is the difference between a Kafka consumer's poll() and subscribe() methods?

> `subscribe()` registers the consumer to topics or patterns, while `poll()` fetches messages from the broker.

- `subscribe()`: Sets up **topic subscription and triggers partition assignment**.
- `poll()`: Retrieves **records from assigned partitions**, triggers **heartbeat**, and updates offsets.
- `poll()` must be called **regularly** to avoid consumer group rebalancing due to timeout.

> `subscribe()` defines **what to consume**, `poll()` defines **when and how to consume**, reflecting Kafka’s *
*pull-based consumption model**.
>
> Understanding this difference is key for **managing consumer liveness, partition assignment, and offset control** in
> distributed streaming applications.

---

### 32.How does Kafka handle large messages?

> Kafka handles large messages via **segmenting, batching, and configurable message size limits**.
> Properly tuning message size ensures **efficient disk usage and network throughput** without destabilizing the broker.
> Handling large messages carefully prevents **performance bottlenecks** and maintains **cluster stability**.

- Default max message size: `message.max.bytes` per broker/producer/consumer.
- Large messages can **impact throughput, memory, and GC**, so they should be **split or compressed**.
- Kafka uses **segment-based storage**, so oversized messages can trigger rejections if limits are exceeded.

---

### 33.How does Kafka ensure message durability?

> Kafka ensures durability by **writing messages to disk and replicating across multiple brokers**.

- Messages are appended to **partition logs on the leader**.
- Followers replicate data according to the **replication factor and ISR**.
- Configurable `acks=all` ensures **all ISR replicas have received the message** before acknowledging the producer.

> Kafka’s design separates **fast sequential disk writes and replication**, maximizing throughput without compromising
> durability.
>
> This makes Kafka suitable for **mission-critical, durable streaming pipelines** with predictable delivery guarantees.

---

### 34. How does Kafka Streams handle stateful operations?

> Kafka Streams supports **stateful transformations like aggregations, joins, and windowing** using local state stores.
> Internal changelog topics and standby replicas ensure **exactly-once processing and fast recovery**.
>
> This design allows **real-time analytics and materialized views** while maintaining high throughput and fault
> tolerance.

- Each instance maintains a **rocksdb-backed local state store**.
- Changelog topics **persist state for recovery**.
- Allows **fault-tolerant, scalable stateful processing** without external databases.

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