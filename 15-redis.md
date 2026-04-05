# 🧪 Redis - Remote Dictionary Server

## Summary

This document covers Redis, an open-source, in-memory data structure store used as a database, cache, and message broker. Topics include Redis architecture, common data types (Strings, Lists, Sets, Hashes, Sorted Sets), key-based operations, persistence models (RDB and AOF), eviction policies, transactions, Pub/Sub, and advanced features like Redis Streams and Sentinel for high availability.

## Sommaire

- [1. Introduction to Redis](#1-introduction-to-redis)
  - [Definition](#definition)
  - [Why Use Redis?](#why-use-redis)
  - [Memory Architecture](#memory-architecture)
- [2. Data Types & Commands](#2-data-types-&-commands)
  - [Strings](#strings)
  - [Lists](#lists)
  - [Sets](#sets)
  - [Hashes](#hashes)
  - [Sorted Sets (ZSets)](#sorted-sets-zsets)
- [3. Key Management](#3-key-management)
  - [Expiration (TTL)](#expiration-ttl)
  - [Key Eviction Policies](#key-eviction-policies)
- [4. Persistence Models](#4-persistence-models)
  - [RDB (Snapshotting)](#rdb-snapshotting)
  - [AOF (Append Only File)](#aof-append-only-file)
- [5. Advanced Features](#5-advanced-features)
  - [Transactions (MULTI/EXEC)](#transactions)
  - [Pub/Sub (Messaging)](#pubsub)
  - [Lua Scripting](#lua-scripting)
- [6. High Availability & Scalability](#6-high-availability-&-scalability)
  - [Redis Sentinel](#redis-sentinel)
  - [Redis Cluster (Sharding)](#redis-cluster)
- [7. Caching Strategies](#7-caching-strategies)
  - [Cache Aside](#cache-aside)
  - [Read Through / Write Through](#read-through-write-through)
- [🔑 Key Takeaways](#key-takeaways)

---

## 1. Introduction to Redis

### Definition
Redis is an open-source (BSD licensed), in-memory data structure store. It is extremely fast because it keeps all data in RAM, making it ideal for caching, real-time analytics, and session management.

### Why Use Redis?
- **Speed:** Sub-millisecond latency.
- **Data Structures:** Supports strings, hashes, lists, sets, and more.
- **Persistence:** Can save data to disk optionally.
- **Atomic Operations:** Ensures data consistency even with concurrent access.

---

## 2. Data Types & Commands

### Strings
The most basic Redis data type. Can store text or binary data (up to 512MB).

```bash
SET name "Tariq"
GET name               # "Tariq"
INCR counter           # Increments a numeric string safely
SETEX session 60 "id"  # Set key with 60s expiration
```

### Lists
Collections of strings sorted by insertion order. Great for queues.

```bash
LPUSH tasks "Emailing" # Add to start
RPUSH tasks "Billing"  # Add to end
LPOP tasks             # Remove from start
LRANGE tasks 0 -1      # Get all elements
```

### Sets
Unordered collections of unique strings. Perfect for tracking unique visitors.

```bash
SADD tags "web" "dev"
SMEMBERS tags          # List all tags
SISMEMBER tags "web"   # Check existence (1 for true, 0 for false)
```

### Hashes
Maps between string fields and string values. Best for storing objects like user profiles.

```bash
HSET user:100 name "Alice" age "30"
HGET user:100 name     # "Alice"
HGETALL user:100       # Get all fields and values
```

### Sorted Sets (ZSets)
Similar to sets but every element is associated with a score. Useful for leaderboards.

```bash
ZADD leaderboard 100 "UserA" 250 "UserB" 50 "UserC"
ZRANGE leaderboard 0 -1 WITHSCORES # List all by score
```

---

## 3. Key Management

### Expiration (TTL)
You can set a Time-To-Live (TTL) for any key. Once the time expires, Redis automatically deletes the key.

```bash
EXPIRE mykey 3600  # Sets TTL to 1 hour
TTL mykey          # returns remaining time in seconds
```

### Key Eviction Policies
When Redis runs out of memory, it uses a policy to decide which keys to delete:
- **noeviction:** Returns error.
- **allkeys-lru:** Least Recently Used keys across all keys.
- **volatile-lru:** LRU only for keys with an expiration set.

---

## 4. Persistence Models

### RDB (Snapshotting)
Takes a snapshot of the dataset at specified intervals.
- **Pros:** Fast to reload, compact file.
- **Cons:** Risk of data loss between snapshots.

### AOF (Append Only File)
Logs every write operation received by the server.
- **Pros:** More durable, human-readable log.
- **Cons:** Larger files, slower to reload than RDB.

---

## 5. Advanced Features

### Transactions
Redis transactions allow the execution of a group of commands in a single step.

```bash
MULTI
SET account:1:balance 100
SET account:2:balance 200
EXEC
```

### Pub/Sub
A messaging paradigm where senders (publishers) do not program the messages to be sent directly to specific receivers (subscribers).

```bash
SUBSCRIBE news_channel
PUBLISH news_channel "Breaking news!"
```

---

## 6. High Availability & Scalability

### Redis Sentinel
Provides high availability. It monitors Redis instances and performs automatic failover if the master fails.

### Redis Cluster
Automatically splits your dataset among multiple Redis nodes. It provides horizontal scalability and some level of availability during failures.

---

## 7. Caching Strategies

### Cache Aside
1. Application checks the cache.
2. If hit: use data from cache.
3. If miss: query database, update cache, and return data.

---

## 🔑 Key Takeaways
- Redis is an **in-memory** store, prioritizing speed.
- It supports multiple **Data Structures** (Hashes, Sets, Lists, etc.).
- Use **TTL** for temporary data like sessions or rate limiting.
- Combine **RDB and AOF** for the best balance of speed and durability.
