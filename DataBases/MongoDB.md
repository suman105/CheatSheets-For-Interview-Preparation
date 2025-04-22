# MongoDB Cheatsheet

## Databases
```sh
use myDatabase  // Switches to or creates a database
show dbs       // Lists all databases
db.dropDatabase()  // Drops the current database
```

## Collections
```sh
db.createCollection("users")  // Creates a collection
db.getCollectionNames()       // Lists all collections in the current database
db.users.drop()               // Drops the users collection
```

## Documents
```sh
db.users.insertOne({ name: "John Doe", age: 30, department: "HR" })  // Inserts a single document
```

## BSON & _id
- MongoDB uses BSON (Binary JSON) for data storage.
- Every document has a unique `_id` field, automatically generated as an `ObjectId` if not provided.
```sh
db.users.find({ _id: ObjectId("507f1f77bcf86cd799439011") })  // Query by _id
```

---

## CRUD Operations
### Create
```sh
db.users.insertOne({ name: "Jane Doe", age: 28, department: "Finance" })  // Inserts one document
db.users.insertMany([  // Inserts multiple documents
  { name: "Alice", age: 25, department: "IT" },
  { name: "Bob", age: 35, department: "HR" }
])
```

### Read
```sh
db.users.find()                          // Retrieves all documents
db.users.find({ department: "HR" })      // Filters by department
db.users.findOne({ name: "John Doe" })   // Retrieves one document
db.users.find().pretty()                 // Formats output for readability
```

### Update
```sh
db.users.updateOne({ name: "John Doe" }, { $set: { age: 31 } })  // Updates one document
db.users.updateMany({ department: "HR" }, { $set: { salary: 50000 } })  // Updates multiple documents
db.users.replaceOne({ name: "John Doe" }, { name: "John Doe", age: 31, department: "HR", salary: 50000 })  // Replaces one document
```

### Delete
```sh
db.users.deleteOne({ name: "John Doe" })       // Deletes one document
db.users.deleteMany({ department: "HR" })      // Deletes multiple documents
db.users.deleteMany({})                        // Deletes all documents in collection
```

---

## Querying Data
### Basic Queries
```sh
db.users.find({ department: "HR" })                     // Exact match
db.users.find({ age: { $gt: 25 } })                    // Greater than
db.users.find({ $and: [{ department: "HR" }, { age: { $gt: 25 } }] })  // Logical AND
db.users.find({ department: { $in: ["HR", "Finance"] } })  // In array
```

### Array Queries
```sh
db.users.find({ skills: { $elemMatch: { name: "MongoDB", level: "Advanced" } } })  // Matches array element
db.users.find({ skills: { $size: 3 } })                // Matches array length
```

### Projection
```sh
db.users.find({ department: "HR" }, { name: 1, age: 1, _id: 0 })  // Include name and age, exclude _id
```

### Sorting & Pagination
```sh
db.users.find().sort({ age: 1 })           // Sort ascending (1), descending (-1)
db.users.find().limit(10).skip(20)         // Paginate: skip 20, limit to 10
```

### Count & Distinct
```sh
db.users.countDocuments({ department: "HR" })  // Count documents matching query
db.users.distinct("department")               // Unique values of a field
```

---

## Indexing
### Types
```sh
db.users.createIndex({ name: 1 })                      // Single-field index
db.users.createIndex({ name: 1, age: -1 })             // Compound index
db.users.createIndex({ skills: 1 })                    // Array index
db.users.createIndex({ name: "text", department: "text" })  // Text index
db.places.createIndex({ location: "2dsphere" })        // Geospatial index
```

### Management
```sh
db.users.getIndexes()                 // List all indexes
db.users.dropIndex("name_1")          // Drop specific index
db.users.dropIndexes()                // Drop all indexes (except _id)
```

### Properties
```sh
db.users.createIndex({ email: 1 }, { unique: true })  // Unique index
db.logs.createIndex({ createdAt: 1 }, { expireAfterSeconds: 3600 })  // TTL index
db.users.createIndex({ name: 1 }, { partialFilterExpression: { age: { $gt: 25 } } })  // Partial index
```

---

## Aggregation Framework
### Basic Example
```sh
db.users.aggregate([
  { $match: { department: "HR" } },          // Filter documents
  { $group: { _id: "$department", count: { $sum: 1 } } }  // Group and count
])
```

### Pipeline Stages
```sh
{ $match: { age: { $gt: 25 } } }           // Filter documents
{ $group: { _id: "$department", total: { $sum: "$salary" } } }  // Group and sum
{ $sort: { age: 1 } }                      // Sort results
{ $project: { name: 1, age: 1, _id: 0 } }  // Select fields
{ $limit: 10 }                             // Limit results
{ $skip: 5 }                               // Skip results
{ $unwind: "$skills" }                     // Unwind array
```

### Join with $lookup
```sh
{
  $lookup: {
    from: "departments",
    localField: "department_id",
    foreignField: "_id",
    as: "department_info"
  }
}
```

### Operators
- **Arithmetic**: `$add`, `$subtract`, `$multiply`, `$divide`
- **Comparison**: `$eq`, `$ne`, `$gt`, `$gte`, `$lt`, `$lte`
- **Logical**: `$and`, `$or`, `$not`, `$nor`
- **String**: `$concat`, `$toLower`, `$toUpper`
- **Date**: `$year`, `$month`, `$dayOfMonth`
- **Array**: `$size`, `$slice`, `$map`, `$filter`

### Map-Reduce
```sh
db.users.mapReduce(
  function() { emit(this.department, 1); },  // Map function
  function(key, values) { return Array.sum(values); },  // Reduce function
  { out: "department_counts" }  // Output collection
)
```

---

## Data Modeling
### Embedded Documents
```sh
db.users.insertOne({
  name: "John Doe",
  address: { street: "123 Main St", city: "New York", zip: "10001" }
})
```

### References
```sh
db.users.insertOne({ name: "John Doe", department_id: ObjectId("507f1f77bcf86cd799439011") })
```

### Schema Validation
```sh
db.createCollection("users", {
  validator: {
    $jsonSchema: {
      bsonType: "object",
      required: ["name", "age"],
      properties: {
        name: { bsonType: "string" },
        age: { bsonType: "int", minimum: 18 }
      }
    }
  }
})
```

---

## Transactions
### Multi-Document Transactions
```js
const session = db.getMongo().startSession();
session.startTransaction();
try {
  const users = session.getDatabase("myDatabase").users;
  const accounts = session.getDatabase("myDatabase").accounts;
  users.insertOne({ name: "John Doe" }, { session });
  accounts.insertOne({ user_id: ObjectId("507f1f77bcf86cd799439011"), balance: 1000 }, { session });
  session.commitTransaction();
} catch (error) {
  session.abortTransaction();
  console.error("Transaction aborted:", error);
} finally {
  session.endSession();
}
```

### Read/Write Concerns
```sh
db.users.find().readConcern("majority")  // Read committed data
db.users.insertOne({ name: "John Doe" }, { writeConcern: { w: "majority" } })  // Write to majority
```

---

## Replication
### Replica Set
```sh
rs.initiate()  // Initialize replica set
rs.add("mongodb1.example.com")  // Add member
rs.add("mongodb2.example.com")
rs.status()  // Check replica set status
```

### Read Preferences & Write Concerns
```sh
db.users.find().readPref("secondary")  // Read from secondary
db.users.insertOne({ name: "John Doe" }, { writeConcern: { w: 2 } })  // Write to 2 nodes
```

---

## Sharding
```sh
sh.addShard("shard1.example.com")  // Add shard
sh.shardCollection("myDatabase.users", { name: 1 })  // Shard collection by name
sh.status()  // Check sharding status
```
- **Shard Key**: Defines how data is distributed across shards.
- **Chunks**: Logical data splits, automatically balanced.
- **Balancer**: Ensures even distribution of chunks across shards.

---

## Security
### Authentication & Authorization
```sh
use admin
db.createUser({ user: "admin", pwd: "password", roles: ["root"] })  // Create admin user
db.grantRolesToUser("admin", ["readWriteAnyDatabase"])  // Grant roles
db.auth("admin", "password")  // Authenticate
```

### Encryption
```sh
mongod --enableEncryption --encryptionKeyFile /path/to/keyfile  // Enable encryption at rest
```

### Auditing
```sh
mongod --auditDestination file --auditFormat JSON --auditPath /var/log/mongodb/audit.json  // Enable auditing
```

---

## Performance Optimization
```sh
db.users.find({ name: "John Doe" }).explain("executionStats")  // Analyze query performance
db.users.find({ name: "John Doe" }).hint({ name: 1 })  // Force index usage
db.setProfilingLevel(2)  // Log all operations for profiling
```
- MongoDB uses memory-mapped files for caching.
- Connection pooling is built-in for efficient connections.

---

## Advanced Features
### Change Streams
```js
const changeStream = db.users.watch();
changeStream.on("change", (change) => console.log(change));  // Monitor collection changes
```

### Graph Lookup
```sh
db.users.aggregate([
  {
    $graphLookup: {
      from: "users",
      startWith: "$manager_id",
      connectFromField: "manager_id",
      connectToField: "_id",
      as: "managementChain"
    }
  }
])
```

### Full-Text Search
```sh
db.articles.createIndex({ content: "text" })  // Create text index
db.articles.find({ $text: { $search: "MongoDB" } })  // Perform text search
```

### Time Series Collections
```sh
db.createCollection("weather", {
  timeseries: {
    timeField: "timestamp",
    metaField: "sensor_id",
    granularity: "hours"
  }
})
```
