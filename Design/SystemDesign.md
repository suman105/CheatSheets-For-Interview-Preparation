# 📌 System Design Cheatsheet

This cheatsheet provides a comprehensive overview of key **System Design concepts** for building scalable, reliable, and secure systems. It covers **Caching, Load Balancing, Database Sharding, Microservices, API Design, Message Queues, Scaling Strategies, CAP Theorem, Security, and more**. Each section includes explanations, flowcharts, tools, and best practices.

---

## 1. Caching
### 🔹 What is Caching?
Caching stores frequently accessed data in memory to reduce latency and load on databases or disk storage, improving system performance.

### 🔹 Types of Caching
| Type                 | Description                                                                 | Examples                     |
|----------------------|-----------------------------------------------------------------------------|------------------------------|
| **Client-Side Caching** | Data stored on the user's device to reduce server requests.                 | Browser cache, CDN (Content Delivery Network) |
| **Server-Side Caching** | Data stored at the backend to speed up server responses.                    | Redis, Memcached             |
| **Database Caching**    | Query results cached to reduce database load.                               | MySQL Query Cache, Redis     |
| **Application Caching** | Caches application-level objects or computations.                          | Application memory, Guava Cache |

### 🔹 Cache Eviction Policies
- **LRU (Least Recently Used)**: Removes least recently accessed items.
- **LFU (Least Frequently Used)**: Removes least frequently accessed items.
- **FIFO (First In, First Out)**: Removes oldest items first.
- **TTL (Time-To-Live)**: Removes items after a specified expiration time.

### 🔹 Flowchart: Cache Lookup Process
```plaintext
       +------------------+
       |  Client Request  |
       +------------------+
               |
               v
       +------------------+
       |   Check Cache    |<-- Cache Hit
       +------------------+
          /       \
       Yes        No
       |           |
       v           v
   +-----------+   +------------------+
   | Return    |   | Fetch from DB    |
   | Cached    |   | Store in Cache   |
   | Response  |   +------------------+
   +-----------+         |
                         v
                   +------------------+
                   | Return Response  |
                   +------------------+
```

### 🔹 Best Practices
- **Cache Invalidation**: Use strategies like write-through, write-back, or TTL to keep cache consistent with the source.
- **Cache Warming**: Preload cache with frequently accessed data during system startup.
- **Monitoring**: Track cache hit/miss ratios to optimize performance.
- **Consistency**: Handle cache staleness in distributed systems using eventual consistency or invalidation.

### 🔹 Tools
- **Redis**: In-memory key-value store with persistence and advanced data structures.
- **Memcached**: High-performance, distributed memory caching system.
- **CDN**: Cloudflare, Akamai, AWS CloudFront for edge caching.
- **Varnish**: HTTP accelerator for caching web content.

---

## 2. Load Balancing
### 🔹 What is Load Balancing?
Load balancing distributes incoming traffic across multiple servers to prevent overload, improve reliability, and ensure high availability.

### 🔹 Types of Load Balancers
| Type                  | Description                                                                 | Examples                     |
|-----------------------|-----------------------------------------------------------------------------|------------------------------|
| **DNS Load Balancing** | Uses DNS to distribute requests across multiple server IPs.                  | Route 53, Cloudflare DNS     |
| **Layer 4 Load Balancer** | Operates at the transport layer (TCP/UDP), routing based on IP and port.  | AWS NLB, HAProxy (TCP mode)  |
| **Layer 7 Load Balancer** | Operates at the application layer, routing based on URL, headers, or cookies. | Nginx, HAProxy, AWS ALB     |

### 🔹 Load Balancing Algorithms
- **Round Robin**: Distributes requests sequentially across servers.
- **Least Connections**: Routes to the server with the fewest active connections.
- **Weighted Load Balancing**: Assigns weights to servers based on capacity.
- **IP Hash**: Routes based on a hash of the client's IP for session persistence.
- **Least Response Time**: Routes to the server with the fastest response time.

### 🔹 Flowchart: Load Balancing
```plaintext
       +------------------+
       | Client Request   |
       +------------------+
               |
               v
       +------------------+
       | Load Balancer    |
       +------------------+
               |
    -------------------------------
   |            |            |
   v            v            v
Server 1     Server 2     Server 3
```

### 🔹 Best Practices
- **Health Checks**: Monitor server health and route traffic only to healthy servers.
- **Session Persistence**: Use sticky sessions for stateful applications.
- **SSL Termination**: Offload SSL decryption to the load balancer for performance.
- **Geo-Based Routing**: Route traffic based on geographic location for low latency.

### 🔹 Tools
- **Nginx**: Open-source web server and load balancer.
- **HAProxy**: High-performance TCP and HTTP load balancer.
- **AWS ELB**: Elastic Load Balancer (ALB, NLB, CLB).
- **Google Cloud Load Balancer**: Global and regional load balancing.

---

## 3. Database Sharding
### 🔹 What is Database Sharding?
Sharding splits large datasets into smaller, distributed parts (shards) across multiple databases to improve scalability, performance, and manageability.

### 🔹 Types of Sharding
| Type                  | Description                                                                 | Use Case                     |
|-----------------------|-----------------------------------------------------------------------------|------------------------------|
| **Horizontal Sharding** | Splits rows of a table across multiple databases based on a shard key.     | User data by ID range        |
| **Vertical Sharding**   | Splits different tables or columns across databases.                       | Separate user and order data |
| **Hash-Based Sharding** | Uses a hash function on the shard key to distribute data evenly.           | Even data distribution       |
| **Range-Based Sharding** | Divides data based on ranges of the shard key (e.g., A-M, N-Z).           | Ordered data like timestamps |

### 🔹 Flowchart: Hash-Based Sharding
```plaintext
       +------------------+
       | Incoming Query   |
       +------------------+
               |
               v
       +------------------+
       | Hash Function    |
       +------------------+
               |
    -------------------------------
   |        |        |        |
   v        v        v        v
  DB1      DB2      DB3      DB4
```

### 🔹 Best Practices
- **Shard Key Selection**: Choose a key with high cardinality and even distribution (e.g., user_id).
- **Rebalancing**: Plan for shard rebalancing as data grows or shrinks.
- **Cross-Shard Queries**: Minimize queries that span multiple shards for performance.
- **Monitoring**: Track shard size and query performance to avoid hotspots.

### 🔹 Tools
- **MongoDB Sharding**: Built-in sharding with range and hash-based options.
- **MySQL Partitioning**: Supports range, list, and hash partitioning.
- **PostgreSQL**: Citus for distributed sharding.
- **Vitess**: Sharding solution for MySQL.

---

## 4. Microservices Architecture
### 🔹 What are Microservices?
Microservices split an application into small, independent services that communicate via APIs, enabling scalability, flexibility, and independent deployment.

### 🔹 Key Components
- **Service**: A single, focused function (e.g., User Service, Order Service).
- **API Gateway**: Central entry point for routing and cross-cutting concerns (e.g., authentication).
- **Service Discovery**: Dynamic discovery of services (e.g., Consul, Eureka).
- **Circuit Breaker**: Prevents cascading failures by isolating faulty services.

### 🔹 Flowchart: Microservices
```plaintext
       +------------------+
       | Client Request   |
       +------------------+
               |
               v
       +------------------+
       | API Gateway      |
       +------------------+
               |
    -------------------------------
   |        |        |        |
   v        v        v        v
Auth     Users    Orders   Payments
Service  Service  Service  Service
```

### 🔹 Best Practices
- **Single Responsibility**: Each service should have one primary function.
- **Decentralized Data**: Each service owns its database to avoid tight coupling.
- **Event-Driven Communication**: Use message queues for asynchronous communication.
- **Resilience**: Implement circuit breakers, retries, and timeouts.
- **Monitoring**: Use distributed tracing (e.g., Jaeger, Zipkin) to track requests.

### 🔹 Tools
- **Docker**: Containerization for microservices.
- **Kubernetes**: Orchestration for deployment and scaling.
- **API Gateway**: Kong, Nginx, AWS API Gateway.
- **Service Mesh**: Istio, Linkerd for service-to-service communication.
- **Message Brokers**: Kafka, RabbitMQ for event-driven systems.

---

## 5. API Design
### 🔹 What is API Design?
API design involves creating standardized interfaces for services to communicate, ensuring usability, scalability, and security.

### 🔹 Best Practices
- **Versioning**: Use URL versioning (`/api/v1/users`) or headers to manage changes.
- **RESTful Principles**: Use HTTP methods (GET, POST, PUT, DELETE) and resources (e.g., `/users/{id}`).
- **Authentication/Authorization**: Implement OAuth 2.0, JWT, or API keys.
- **Rate Limiting**: Prevent abuse by limiting requests per user (e.g., 1000/hour).
- **Error Handling**: Return standard error codes (e.g., 400, 404, 500) with meaningful messages.
- **Pagination**: Use limit and offset for large datasets (e.g., `/users?limit=10&offset=20`).

### 🔹 Example: REST API
```json
GET /api/v1/users/123
{
  "id": 123,
  "name": "John Doe",
  "email": "john@example.com"
}

POST /api/v1/users
{
  "name": "Jane Doe",
  "email": "jane@example.com"
}
Response: 201 Created
```

### 🔹 Tools
- **Swagger/OpenAPI**: For API documentation and testing.
- **Postman**: For API development and testing.
- **AWS API Gateway**: Managed API platform.
- **GraphQL**: Alternative to REST for flexible queries.

---

## 6. Message Queues & Event-Driven Architecture
### 🔹 What are Message Queues?
Message queues enable asynchronous communication between services by buffering messages, decoupling producers and consumers.

### 🔹 Key Patterns
- **Publish/Subscribe (Pub/Sub)**: Producers publish messages to topics; subscribers receive them.
- **Point-to-Point**: Messages are sent to a specific consumer via a queue.
- **Dead Letter Queue**: Stores failed messages for later processing.

### 🔹 Flowchart: Pub/Sub Messaging
```plaintext
+----------+       +------------+       +-------------+
| Producer | ----> | Message    | ----> | Subscriber  |
| (Service)|       | Queue/Topic|       | (Service)   |
+----------+       +------------+       +-------------+
                           |
                           v
                     +-------------+
                     | Dead Letter |
                     | Queue       |
                     +-------------+
```

### 🔹 Best Practices
- **Idempotency**: Ensure consumers can handle duplicate messages.
- **Message Prioritization**: Prioritize critical messages in high-traffic systems.
- **Monitoring**: Track queue depth and processing latency.
- **Retry Mechanisms**: Implement exponential backoff for failed messages.

### 🔹 Tools
- **Apache Kafka**: Distributed streaming platform for high-throughput.
- **RabbitMQ**: Message broker for reliable queueing.
- **Amazon SQS**: Managed message queue service.
- **Redis Pub/Sub**: Lightweight pub/sub for real-time messaging.

---

## 7. Scaling Strategies
### 🔹 What is Scaling?
Scaling increases a system's capacity to handle more load by adding resources or optimizing performance.

### 🔹 Types of Scaling
| Strategy              | Description                                                                 | Pros/Cons                     |
|-----------------------|-----------------------------------------------------------------------------|-------------------------------|
| **Vertical Scaling**   | Adds more CPU, RAM, or storage to a single server.                         | Simple, but limited by hardware |
| **Horizontal Scaling** | Adds more servers to distribute load.                                      | Complex, but highly scalable   |
| **Read Replicas**      | Creates database copies for read operations.                               | Reduces read load, eventual consistency |
| **Multi-Master Replication** | Multiple database nodes handle reads and writes.                    | High availability, complex sync |

### 🔹 Best Practices
- **Stateless Services**: Design services to be stateless for easy horizontal scaling.
- **Database Optimization**: Use indexing, partitioning, and caching to reduce load.
- **Auto-Scaling**: Use cloud tools (e.g., AWS Auto Scaling) to dynamically adjust resources.
- **Load Testing**: Simulate traffic to identify bottlenecks before scaling.

### 🔹 Tools
- **AWS Auto Scaling**: Automatically scales EC2 instances.
- **Kubernetes**: Autoscaling for containerized applications.
- **MySQL/PostgreSQL**: Read replicas and partitioning.
- **MongoDB**: Sharding and replication.

---

## 8. CAP Theorem
### 🔹 What is the CAP Theorem?
In distributed systems, you can only guarantee two of the following three properties at the same time:
- **Consistency (C)**: All nodes have the same data at the same time.
- **Availability (A)**: Every request receives a response, even if some nodes fail.
- **Partition Tolerance (P)**: The system continues to operate despite network failures.

### 🔹 CAP Trade-Offs
| Type | Description                                      | Examples                     |
|------|--------------------------------------------------|------------------------------|
| **CP** | Prioritizes consistency and partition tolerance. | MongoDB, HBase, Redis        |
| **AP** | Prioritizes availability and partition tolerance.| Cassandra, DynamoDB, CouchDB  |
| **CA** | Prioritizes consistency and availability (rare). | Traditional RDBMS (non-distributed) |

### 🔹 Best Practices
- **Understand Requirements**: Choose CP for financial systems, AP for user-facing apps.
- **Eventual Consistency**: Use for AP systems to handle high availability.
- **Compensating Transactions**: Handle inconsistencies in AP systems with retries or rollbacks.

---

## 9. Security Best Practices
### 🔹 Key Principles
- **Confidentiality**: Protect sensitive data with encryption.
- **Integrity**: Ensure data is not tampered with (e.g., checksums, signatures).
- **Availability**: Prevent denial-of-service (DoS) attacks.

### 🔹 Best Practices
- **Use HTTPS**: Encrypt all network traffic with TLS.
- **Authentication/Authorization**: Use OAuth 2.0, JWT, or API keys; implement RBAC (Role-Based Access Control).
- **Prevent SQL Injection**: Use ORMs (e.g., Sequelize, Hibernate) or prepared statements.
- **Data Encryption**: Encrypt sensitive data at rest (e.g., AES-256) and in transit.
- **Rate Limiting**: Limit requests to prevent abuse (e.g., 1000/hour per user).
- **Secure Dependencies**: Regularly update libraries and scan for vulnerabilities (e.g., Snyk).
- **Logging and Monitoring**: Log security events and monitor for anomalies (e.g., Splunk, ELK Stack).

### 🔹 Tools
- **Keycloak**: Identity and access management.
- **Vault**: Secrets management for credentials.
- **OWASP ZAP**: Security testing for APIs.
- **AWS KMS**: Key management for encryption.

---

## 10. Monitoring and Logging
### 🔹 What is Monitoring and Logging?
Monitoring tracks system performance and health, while logging records events for debugging and auditing.

### 🔹 Key Metrics
- **Latency**: Time taken to process requests.
- **Error Rate**: Frequency of failed requests.
- **Throughput**: Number of requests handled per second.
- **Resource Usage**: CPU, memory, disk, and network utilization.

### 🔹 Best Practices
- **Distributed Tracing**: Track requests across microservices (e.g., Jaeger, Zipkin).
- **Alerting**: Set up alerts for critical thresholds (e.g., PagerDuty, Opsgenie).
- **Log Aggregation**: Centralize logs for analysis (e.g., ELK Stack, Loki).
- **Dashboards**: Visualize metrics with tools like Grafana or Prometheus.

### 🔹 Tools
- **Prometheus**: Time-series monitoring for metrics.
- **Grafana**: Visualization for metrics and logs.
- **ELK Stack**: Elasticsearch, Logstash, Kibana for logging.
- **New Relic**: Application performance monitoring.

---

## 📌 Summary Table
| Concept                  | Key Points                                                                 | Tools                              |
|--------------------------|---------------------------------------------------------------------------|------------------------------------|
| **Caching**              | Reduces latency with in-memory data storage.                              | Redis, Memcached, Cloudflare       |
| **Load Balancing**       | Distributes traffic for reliability and scalability.                      | Nginx, HAProxy, AWS ELB            |
| **Database Sharding**    | Splits data for scalability and performance.                             | MongoDB, MySQL, Citus              |
| **Microservices**        | Modular, independent services with API communication.                    | Docker, Kubernetes, Kafka          |
| **API Design**           | Standardized, secure, and scalable interfaces.                           | Swagger, Postman, AWS API Gateway  |
| **Message Queues**       | Asynchronous communication for decoupling.                               | Kafka, RabbitMQ, Amazon SQS        |
| **Scaling Strategies**   | Vertical, horizontal, and database scaling.                              | AWS Auto Scaling, Kubernetes       |
| **CAP Theorem**          | Trade-offs in distributed systems (C, A, P).                             | MongoDB (CP), Cassandra (AP)       |
| **Security**             | Encryption, authentication, and secure practices.                        | Keycloak, Vault, OWASP ZAP         |
| **Monitoring/Logging**   | Tracks performance and records events.                                   | Prometheus, Grafana, ELK Stack     |

This cheatsheet is a **high-level guide** to designing scalable, reliable, and secure systems. 🚀