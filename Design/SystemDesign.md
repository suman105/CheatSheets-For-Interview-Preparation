# **📌 System Design Cheatsheet**

## **1. Caching**
### **🔹 What is Caching?**
Caching stores frequently accessed data in memory to reduce retrieval time from the database or disk storage.

### **🔹 Types of Caching**
| Type                 | Description |
|----------------------|-------------|
| Client-Side Caching | Stored on the user's device (e.g., browser cache, CDN) |
| Server-Side Caching | Stored at the backend (e.g., Redis, Memcached) |

### **🔹 Cache Eviction Policies**
- **LRU (Least Recently Used)** – Removes least recently accessed items.
- **LFU (Least Frequently Used)** – Removes items accessed the least.
- **FIFO (First In First Out)** – Removes oldest items first.

### **🔹 Flowchart: Cache Lookup Process**
```plaintext
       +------------------+
       |  Client Request  |
       +------------------+
               |
               v
       +------------------+
       |   Check Cache    |
       +------------------+
          /       \
       Yes        No
       |           |
       v           v
   +-----------+   +------------------+
   | Return    |   | Fetch from DB    |
   | Cached    |   | Store in Cache   |
   | Response  |   +------------------+
   +-----------+
```

### **🔹 Tools:** Redis, Memcached, CDN (Cloudflare, Akamai)

---

## **2. Load Balancing**
### **🔹 What is Load Balancing?**
Distributes traffic across multiple servers to prevent overload and improve reliability.

### **🔹 Types of Load Balancers**
| Type                  | Description |
|----------------------|-------------|
| **DNS Load Balancing** | Uses DNS records to distribute requests across multiple IPs. |
| **Layer 4 Load Balancer** | Operates at TCP/UDP level (e.g., AWS NLB). |
| **Layer 7 Load Balancer** | Routes requests based on URL, cookies, headers (e.g., Nginx, HAProxy). |

### **🔹 Load Balancing Algorithm**
- **Round Robin** – Cyclically distributes requests.
- **Least Connections** – Sends requests to the least busy server.
- **Weighted Load Balancing** – Prioritizes servers based on capacity.

### **🔹 Flowchart: Load Balancing**
```plaintext
Client Request
       |
       v
+---------------------+
| Load Balancer      |
+---------------------+
       |
----------------------
|         |         |
v         v         v
Server 1  Server 2  Server 3
```

### **🔹 Tools:** Nginx, HAProxy, AWS ELB, Google Load Balancer

---

## **3. Database Sharding**
### **🔹 What is Database Sharding?**
Splitting large datasets into smaller, distributed parts (shards) to improve **scalability & performance**.

### **🔹 Types of Sharding**
| Type                  | Description |
|----------------------|-------------|
| **Horizontal Sharding** | Divides data across multiple databases (e.g., users ID 1-100 in DB1, 101-200 in DB2). |
| **Vertical Sharding** | Different tables stored in separate databases (e.g., orders in DB1, users in DB2). |
| **Hash-Based Sharding** | Distributes data using a **hash function** to spread data evenly. |

### **🔹 Flowchart: Hash-Based Sharding**
```plaintext
Incoming Query
       |
       v
+------------------+
| Hash Function    |
+------------------+
       |
----------------------------
|        |        |        |
v        v        v        v
DB1      DB2      DB3      DB4
```

### **🔹 Tools:** MySQL Partitioning, PostgreSQL, MongoDB Sharding

---

## **4. Microservices Architecture**
### **🔹 What are Microservices?**
A **modular approach** where an application is split into **small, independent services** that communicate via APIs.

### **🔹 Flowchart: Microservices**
```plaintext
Client Request
       |
       v
+------------------+
| API Gateway      |
+------------------+
       |
------------------------------
|         |         |         |
v         v         v         v
Auth     Users     Orders   Payments
Service  Service   Service  Service
```

### **🔹 Tools:** Docker, Kubernetes, API Gateway (Kong, Nginx), Kafka, RabbitMQ.

---

## **5. API Design**
### **🔹 Best Practices**
✔ **Versioning** (`/api/v1/users`).  
✔ **Authentication & Authorization** (OAuth, JWT, API keys).  
✔ **Rate Limiting** to prevent API abuse.  

---

## **6. Message Queues & Event-Driven Architecture**
### **🔹 Flowchart: Pub/Sub Messaging**
```plaintext
+----------+       +------------+       +-------------+
| Producer | ----> |  Message   | ----> | Subscriber  |
| (Service)|       |   Queue    |       | (Service)   |
+----------+       +------------+       +-------------+
```

### **🔹 Tools:** Apache Kafka, RabbitMQ, Amazon SQS.

---

## **7. Scaling Strategies**
| Scaling Strategy  | Description |
|-------------------|-------------|
| **Vertical Scaling** | Adding more CPU, RAM to a single server. |
| **Horizontal Scaling** | Adding more servers (distributed system). |
| **Read Replicas** | Creating copies of databases for read operations. |
| **Multi-Master Replication** | Multiple nodes handle both reads & writes. |

---

## **8. CAP Theorem**
| Type | Description |
|------|-------------|
| **Consistency (C)** | All nodes have the same data at the same time. |
| **Availability (A)** | Every request gets a response. |
| **Partition Tolerance (P)** | The system works even if some network connections fail. |

💡 **In a distributed system, you can only have two of the three.**
- **CP (Consistency + Partition Tolerance):** MongoDB, HBase.
- **AP (Availability + Partition Tolerance):** Cassandra, DynamoDB.

---

## **9. Security Best Practices**
✔ Use **HTTPS (TLS encryption)**.  
✔ Implement **OAuth, JWT for authentication**.  
✔ Prevent **SQL Injection** (Use ORM, prepared statements).  
✔ Secure **sensitive data** with encryption.

---

## **📌 Summary**
This cheatsheet provides a **high-level overview** of key **System Design concepts** including **Caching, Load Balancing, Database Sharding, Microservices, API Design, Messaging Queues, Scaling, CAP Theorem, and Security.** 🚀
