# 🍃 MongoDB - The NoSQL Database

## Summary

This document covers MongoDB, a leading NoSQL, document-oriented database. Topics include the NoSQL vs. SQL comparison, MongoDB architecture (Collections, Documents, BSON), CRUD operations using the Mongo Shell and drivers, indexing for performance, the powerful Aggregation Framework, data modeling patterns, and administration and security basics.

## Sommaire

- [1. Introduction to NoSQL & MongoDB](#1-introduction-to-nosql-&-mongodb)
  - [Definition](#definition)
  - [SQL vs. NoSQL Comparison](#sql-vs-nosql-comparison)
  - [When to Choose MongoDB](#when-to-choose-mongodb)
- [2. MongoDB Core Concepts](#2-mongodb-core-concepts)
  - [Documents (BSON)](#documents-bson)
  - [Collections](#collections)
  - [Databases](#databases)
  - [Dynamic Schema](#dynamic-schema)
- [3. CRUD Operations](#3-crud-operations)
  - [Create (Insert)](#create-insert)
  - [Read (Find)](#read-find)
  - [Update](#update)
  - [Delete](#delete)
- [4. Query Operators](#4-query-operators)
  - [Comparison Operators](#comparison-operators)
  - [Logical Operators](#logical-operators)
  - [Element Operators](#element-operators)
  - [Array Operators](#array-operators)
- [5. Indexing](#5-indexing)
  - [Definition](#definition-1)
  - [Types of Indexes](#types-of-indexes)
  - [Performance Optimization](#performance-optimization)
- [6. Aggregation Framework](#6-aggregation-framework)
  - [The Pipeline Concept](#the-pipeline-concept)
  - [Common Stages ($match, $group, $project)](#common-stages)
  - [Accumulators](#accumulators)
- [7. Data Modeling](#7-data-modeling)
  - [Embedding vs. Referencing](#embedding-vs-referencing)
  - [Schema Design Patterns](#schema-design-patterns)
- [8. Replication & Sharding](#8-replication-&-sharding)
  - [High Availability (Replica Sets)](#high-availability)
  - [Scalability (Sharding)](#scalability)
- [🔑 Key Takeaways](#key-takeaways)

---

## 1. Introduction to NoSQL & MongoDB

### Definition
MongoDB is an open-source, document-oriented NoSQL database designed for high volume data storage. Instead of using tables and rows as in traditional relational databases, MongoDB makes use of collections and documents.

### SQL vs. NoSQL Comparison

| Feature | SQL (Relational) | NoSQL (MongoDB) |
|---------|------------------|-----------------|
| **Data Model** | Tables / Rows | Documents (JSON/BSON) |
| **Schema** | Fixed / Predefined | Dynamic / Flexible |
| **Scaling** | Vertical (Scale Up) | Horizontal (Scale Out) |
| **Relationships** | Joins | Embedding / Linking |
| **Transactions** | ACID Compliant | High Performance / BASE |

### When to Choose MongoDB
- **Unstructured Data:** When your data structure is evolving or unpredictable.
- **Big Data:** When you need to scale horizontally across multiple servers.
- **Content Management:** Perfect for blogs, product catalogs, and user profiles.
- **Real-time Analytics:** High insertion rates and flexible querying.

---

## 2. MongoDB Core Concepts

### Documents (BSON)
Documents are the basic unit of data in MongoDB, similar to rows in SQL. They are stored in **BSON** (Binary JSON) format, which supports more data types than standard JSON (like Date and Binary data).

```json
{
  "_id": ObjectId("507f1f77bcf86cd799439011"),
  "name": "Jane Doe",
  "age": 28,
  "email": "jane@example.com",
  "interests": ["coding", "hiking"],
  "address": {
    "city": "Paris",
    "country": "France"
  }
}
```

### Collections
A collection is a group of MongoDB documents. It is the equivalent of an RDBMS table. Collections do not enforce a strict schema, meaning documents within a collection can have different fields.

---

## 3. CRUD Operations

### Create (Insert)
```javascript
// Insert a single document
db.users.insertOne({
  name: "John Smith",
  age: 30,
  status: "active"
});

// Insert multiple documents
db.users.insertMany([
  { name: "Alice", age: 25 },
  { name: "Bob", age: 35 }
]);
```

### Read (Find)
```javascript
// Find all documents
db.users.find();

// Find with filter
db.users.find({ age: { $gt: 25 } });

// Find one document
db.users.findOne({ name: "Alice" });

// Projection (select specific fields)
db.users.find({ status: "active" }, { name: 1, _id: 0 });
```

### Update
```javascript
// Update one
db.users.updateOne(
  { name: "John Smith" },
  { $set: { age: 31 } }
);

// Update many
db.users.updateMany(
  { age: { $lt: 30 } },
  { $set: { status: "young" } }
);
```

### Delete
```javascript
// Delete one
db.users.deleteOne({ name: "Bob" });

// Delete many
db.users.deleteMany({ status: "inactive" });
```

---

## 4. Query Operators

### Comparison Operators
- `$eq`: Matches values that are equal to a specified value.
- `$ne`: Matches all values that are not equal to a specified value.
- `$gt` / `$gte`: Greater than / Greater than or equal.
- `$lt` / `$lte`: Less than / Less than or equal.
- `$in`: Matches any of the values specified in an array.

### Logical Operators
- `$and`: Joins query clauses with a logical AND.
- `$or`: Joins query clauses with a logical OR.
- `$not`: Inverts the effect of a query expression.

---

## 5. Indexing

### Definition
Indexes support the efficient execution of queries in MongoDB. Without indexes, MongoDB must perform a *collection scan*, i.e. scan every document in a collection, to select those documents that match the query statement.

### Types of Indexes
- **Single Field:** Index on a single field of a document.
- **Compound Index:** Index on multiple fields.
- **Multikey Index:** Index on array fields.
- **Text Index:** Supports text search queries on string content.

```javascript
// Create an index
db.users.createIndex({ email: 1 }); // 1 for ascending, -1 for descending

// Create a compound index
db.users.createIndex({ name: 1, age: -1 });
```

---

## 6. Aggregation Framework

### The Pipeline Concept
The aggregation framework is a powerful tool for data analysis. It uses a "pipeline" approach where documents pass through stages that transform them into combined results.

```mermaid
graph LR
    A[Collection] --> B[$match]
    B --> C[$group]
    C --> D[$sort]
    D --> E[Result]
```

### Example
```javascript
db.orders.aggregate([
  // Phase 1: Filter orders by status
  { $match: { status: "completed" } },
  // Phase 2: Group by customer and sum total
  { $group: { _id: "$customerId", totalSpent: { $sum: "$amount" } } },
  // Phase 3: Sort by total spent descending
  { $sort: { totalSpent: -1 } }
]);
```

---

## 7. Data Modeling

### Embedding vs. Referencing
- **Embedding:** Storing related data in a single document. Best for "one-to-few" relationships and improving read performance.
- **Referencing:** Storing the ID of a related document. Best for "one-to-many" or "many-to-many" relationships to avoid data duplication.

---

## 8. Replication & Sharding

### High Availability
**Replica Sets** provide redundancy and high availability by keeping multiple copies of data on different servers. If the primary node fails, a secondary node is elected as the new primary.

### Scalability
**Sharding** is the process of storing data records across multiple machines. It is MongoDB's approach to meeting the demands of data growth (horizontal scaling).

---

## 🔑 Key Takeaways
- MongoDB uses **BSON** documents to store data flexibly.
- It is highly scalable through **Sharding**.
- The **Aggregation Framework** is essential for complex data processing.
- Choose **Embedding** for performance and **Referencing** for data integrity.
