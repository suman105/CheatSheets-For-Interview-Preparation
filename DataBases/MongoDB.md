# MongoDB Cheatsheet

## Databases
```sh
use myDatabase // Switches to or creates a database
```

## Collections
```sh
db.createCollection("users") // Creates a collection
```

## Documents
```sh
db.users.insertOne({ name: "John Doe", age: 30, department: "HR" })
```

## BSON & _id
- MongoDB uses BSON (Binary JSON)
- Every document has a unique `_id` field
```sh
db.users.find({ _id: ObjectId("507f1f77bcf86cd799439011") })
```

---

##  CRUD Operations
### Create
```sh
db.users.insertOne({ name: "Jane Doe", age: 28, department: "Finance" })
db.users.insertMany([
  { name: "Alice", age: 25, department: "IT" },
  { name: "Bob", age: 35, department: "HR" }
])
```
### Read
```sh
db.users.find()
db.users.find({ department: "HR" })
db.users.findOne({ name: "John Doe" })
```
### Update
```sh
db.users.updateOne({ name: "John Doe" }, { $set: { age: 31 } })
db.users.updateMany({ department: "HR" }, { $set: { salary: 50000 } })
db.users.replaceOne({ name: "John Doe" }, { name: "John Doe", age: 31, department: "HR", salary: 50000 })
```
### Delete
```sh
db.users.deleteOne({ name: "John Doe" })
db.users.deleteMany({ department: "HR" })
```

---

## Querying Data
### Basic
```sh
db.users.find({ department: "HR" })
db.users.find({ age: { $gt: 25 } })
db.users.find({ $and: [{ department: "HR" }, { age: { $gt: 25 } }] })
db.users.find({ department: { $in: ["HR", "Finance"] } })
```
### Array Queries
```sh
db.users.find({ skills: { $elemMatch: { name: "MongoDB", level: "Advanced" } } })
db.users.find({ skills: { $size: 3 } })
```
### Projection
```sh
db.users.find({ department: "HR" }, { name: 1, age: 1 })
```
### Sorting & Pagination
```sh
db.users.find().sort({ age: 1 })
db.users.find().limit(10).skip(20)
```
### Count & Distinct
```sh
db.users.countDocuments({ department: "HR" })
db.users.distinct("department")
```

---

## Indexing
### Types
```sh
db.users.createIndex({ name: 1 })
db.users.createIndex({ name: 1, age: -1 })
db.users.createIndex({ skills: 1 })
db.users.createIndex({ name: "text", department: "text" })
db.places.createIndex({ location: "2dsphere" })
```
### Management
```sh
db.users.getIndexes()
db.users.dropIndex("name_1")
```
### Properties
```sh
db.users.createIndex({ email: 1 }, { unique: true })
db.logs.createIndex({ createdAt: 1 }, { expireAfterSeconds: 3600 })
db.users.createIndex({ name: 1 }, { partialFilterExpression: { age: { $gt: 25 } } })
```

---

## Aggregation Framework
### Basic Example
```sh
db.users.aggregate([
  { $match: { department: "HR" } },
  { $group: { _id: "$department", count: { $sum: 1 } } }
])
```
### Pipeline Stages
```sh
{ $match: { age: { $gt: 25 } } }
{ $group: { _id: "$department", total: { $sum: "$salary" } } }
{ $sort: { age: 1 } }
{ $project: { name: 1, age: 1 } }
{ $limit: 10 }
{ $skip: 5 }
{ $unwind: "$skills" }
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
- Arithmetic: `$add`, `$subtract`, `$multiply`, `$divide`
- Comparison: `$eq`, `$ne`, `$gt`, `$gte`, `$lt`, `$lte`
- Logical: `$and`, `$or`, `$not`, `$nor`
- String: `$concat`, `$toLower`, `$toUpper`
- Date: `$year`, `$month`, `$dayOfMonth`
- Array: `$size`, `$slice`, `$map`, `$filter`

### Map-Reduce
```sh
db.users.mapReduce(
  function() { emit(this.department, 1) },
  function(key, values) { return Array.sum(values) },
  { out: "department_counts" }
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
  users.insertOne({ name: "John Doe" });
  accounts.insertOne({ user_id: ObjectId("..."), balance: 1000 });
  session.commitTransaction();
} catch (error) {
  session.abortTransaction();
} finally {
  session.endSession();
}
```
### Read/Write Concerns
```sh
db.users.find().readConcern("majority")
db.users.insertOne({ name: "John Doe" }, { writeConcern: { w: "majority" } })
```

---

## Replication
### Replica Set
```sh
rs.initiate()
rs.add("mongodb1.example.com")
rs.add("mongodb2.example.com")
```
### Read Preferences & Write Concerns
```sh
db.users.find().readPref("secondary")
db.users.insertOne({ name: "John Doe" }, { writeConcern: { w: 2 } })
```

---

## Sharding
```sh
sh.addShard("shard1.example.com")
sh.shardCollection("myDatabase.users", { name: 1 })
```
- Shard Key: Defines data distribution
- Chunks: Logical data splits
- Balancer: Equalizes chunks across shards

---

## Security
### Authentication & Authorization
```sh
use admin
db.createUser({ user: "admin", pwd: "password", roles: ["root"] })
db.grantRolesToUser("admin", ["readWriteAnyDatabase"])
```
### Encryption
```sh
mongod --enableEncryption --encryptionKeyFile /path/to/keyfile
```
### Auditing
```sh
mongod --auditDestination file --auditFormat JSON --auditPath /var/log/mongodb/audit.json
```

---

## Performance Optimization
```sh
db.users.find({ name: "John Doe" }).explain("executionStats")
db.users.find({ name: "John Doe" }).hint({ name: 1 })
db.setProfilingLevel(2) // Log all operations
```
- MongoDB uses memory-mapped files for caching
- Connection pooling is built-in

---

## Advanced Features
### Change Streams
```js
const changeStream = db.users.watch();
changeStream.on("change", (change) => console.log(change));
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
db.articles.createIndex({ content: "text" })
db.articles.find({ $text: { $search: "MongoDB" } })
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
### Atlas Search *(MongoDB Atlas)*
Advanced full-text capabilities with MongoDB Atlas.

---

