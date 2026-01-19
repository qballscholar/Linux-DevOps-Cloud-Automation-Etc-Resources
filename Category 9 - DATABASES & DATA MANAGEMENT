**\========================================**  
**CATEGORY 9: DATABASES & DATA MANAGEMENT**  
**\========================================**

**9.1 MYSQL/MARIADB ADMINISTRATION:**

**/\* COMMENT: MySQL is the world's most popular open-source relational database.**  
   **Understanding user management, backup/restore, and performance tuning**  
   **is essential for database administration. \*/**

**KEY CONCEPTS:**  
**• InnoDB: Default storage engine with ACID compliance**  
**• Replication: Master-slave for read scaling**  
**• Indexes: Improve query performance**  
**• Transactions: ACID-compliant data operations**  
**• Backup Strategies: Logical and physical backups**

**USER MANAGEMENT:**  
**\-- Create user**  
**CREATE USER 'appuser'@'localhost' IDENTIFIED BY 'password';**

**\-- Grant privileges**  
**GRANT ALL PRIVILEGES ON database.\* TO 'appuser'@'localhost';**  
**GRANT SELECT, INSERT, UPDATE ON database.table TO 'appuser'@'%';**

**\-- Revoke privileges**  
**REVOKE INSERT ON database.\* FROM 'appuser'@'localhost';**

**\-- Remove user**  
**DROP USER 'appuser'@'localhost';**

**\-- Flush privileges**  
**FLUSH PRIVILEGES;**

**BACKUP AND RESTORE:**  
**\# Logical backup (mysqldump)**  
**mysqldump \-u root \-p database \> backup.sql**  
**mysqldump \-u root \-p \--all-databases \> all\_databases.sql**  
**mysqldump \-u root \-p database table1 table2 \> tables\_backup.sql**

**\# Restore from backup**  
**mysql \-u root \-p database \< backup.sql**

**\# Physical backup (for InnoDB)**  
**mysql**  
**hotcopy \--all-databases /backup/location**

**PERFORMANCE TUNING:**  
**\# Check running queries**  
**SHOW FULL PROCESSLIST;**

**\# Kill long-running query**  
**KILL QUERY \[process\_id\];**

**\# Analyze table**  
**ANALYZE TABLE table\_name;**

**\# Optimize table**  
**OPTIMIZE TABLE table\_name;**

**\# Check table status**  
**SHOW TABLE STATUS LIKE 'table\_name';**

**INDEX MANAGEMENT:**  
**\-- Create index**  
**CREATE INDEX idx\_column ON table(column);**  
**CREATE UNIQUE INDEX idx\_unique ON table(column);**  
**CREATE INDEX idx\_composite ON table(col1, col2);**

**\-- Drop index**  
**DROP INDEX idx\_column ON table;**

**\-- Show indexes**  
**SHOW INDEX FROM table;**

**BEST PRACTICES:**  
**• Regular backups using mysqldump or physical backups**  
**• Implement replication for high availability**  
**• Use appropriate indexes for query optimization**  
**• Monitor slow query log**  
**• Implement connection pooling**  
**• Set appropriate buffer pool size (InnoDB)**

**9.2 POSTGRESQL ADMINISTRATION:**

**/\* COMMENT: PostgreSQL is an advanced open-source relational database with strong**  
   **ACID compliance and support for complex queries. It's known for extensibility,**  
   **JSON support, and advanced features like full-text search. \*/**

**KEY CONCEPTS:**  
**• MVCC: Multi-Version Concurrency Control**  
**• ACID Compliance: Strong transaction guarantees**  
**• Schemas: Logical database organization**  
**• Extensions: Add functionality (PostGIS, pg\_stat\_statements)**  
**• WAL: Write-Ahead Logging for durability**

**USER AND DATABASE MANAGEMENT:**  
**\-- Create user**  
**CREATE USER appuser WITH PASSWORD 'password';**

**\-- Create database**  
**CREATE DATABASE mydb OWNER appuser;**

**\-- Grant privileges**  
**GRANT ALL PRIVILEGES ON DATABASE mydb TO appuser;**  
**GRANT SELECT, INSERT, UPDATE ON ALL TABLES IN SCHEMA public TO appuser;**

**\-- Connect to database**  
**\\c mydb**

**\-- List databases**  
**\\l**

**\-- List tables**  
**\\dt**

**BACKUP AND RESTORE:**  
**\# Backup database**  
**pg\_dump dbname \> backup.sql**  
**pg\_dump \-Fc dbname \> backup.dump  \# Custom format**  
**pg\_dumpall \> all\_databases.sql     \# All databases**

**\# Restore database**  
**psql dbname \< backup.sql**  
**pg\_restore \-d dbname backup.dump**

**PERFORMANCE MONITORING:**  
**\-- Check active connections**  
**SELECT \* FROM pg\_stat\_activity;**

**\-- Terminate connection**  
**SELECT pg\_terminate\_backend(pid);**

**\-- Table sizes**  
**SELECT**  
  **schemaname,**  
  **tablename,**  
  **pg\_size\_pretty(pg\_total\_relation\_size(schemaname||'.'||tablename)) AS size**  
**FROM pg\_tables**  
**ORDER BY pg\_total\_relation\_size(schemaname||'.'||tablename) DESC;**

**\-- Index usage**  
**SELECT \* FROM pg\_stat\_user\_indexes;**

**VACUUM AND MAINTENANCE:**  
**\-- Vacuum to reclaim space**  
**VACUUM ANALYZE;**  
**VACUUM FULL table\_name;**

**\-- Auto vacuum settings (postgresql.conf)**  
**autovacuum \= on**  
**autovacuum\_max\_workers \= 3**

**BEST PRACTICES:**  
**• Regular VACUUM ANALYZE for performance**  
**• Use pg\_stat\_statements for query analysis**  
**• Implement streaming replication for HA**  
**• Configure appropriate shared\_buffers and work\_mem**  
**• Use connection pooling (PgBouncer)**

**9.3 MONGODB BASICS:**

**/\* COMMENT: MongoDB is a NoSQL document database storing data in JSON-like documents.**  
   **It provides flexibility, horizontal scaling, and is excellent for unstructured**  
   **or semi-structured data. \*/**

**KEY CONCEPTS:**  
**• Documents: JSON-like data structures (BSON)**  
**• Collections: Groups of documents**  
**• Replica Sets: High availability groups**  
**• Sharding: Horizontal data partitioning**  
**• Indexes: Improve query performance**

**BASIC COMMANDS:**  
**// Show databases**  
**show dbs**

**// Use/create database**  
**use mydb**

**// Show collections**  
**show collections**

**// Insert document**  
**db.users.insertOne({**  
  **name: "John Doe",**  
  **email: "john@example.com",**  
  **age: 30,**  
  **tags: \["developer", "devops"\]**  
**})**

**// Insert multiple documents**  
**db.users.insertMany(\[**  
  **{ name: "Jane", email: "jane@example.com" },**  
  **{ name: "Bob", email: "bob@example.com" }**  
**\])**

**// Find documents**  
**db.users.find()                          // All documents**  
**db.users.find({ age: { $gt: 25 } })     // Age greater than 25**  
**db.users.find({ tags: "developer" })     // Contains tag**  
**db.users.findOne({ name: "John Doe" })   // Single document**

**// Update documents**  
**db.users.updateOne(**  
  **{ name: "John Doe" },**  
  **{ $set: { age: 31 } }**  
**)**

**db.users.updateMany(**  
  **{ age: { $lt: 30 } },**  
  **{ $set: { status: "young" } }**  
**)**

**// Delete documents**  
**db.users.deleteOne({ name: "John Doe" })**  
**db.users.deleteMany({ age: { $lt: 18 } })**

**INDEXING:**  
**// Create index**  
**db.users.createIndex({ email: 1 })           // Ascending**  
**db.users.createIndex({ name: 1, age: \-1 })   // Compound**  
**db.users.createIndex({ email: 1 }, { unique: true })  // Unique**

**// List indexes**  
**db.users.getIndexes()**

**// Drop index**  
**db.users.dropIndex("email\_1")**

**BACKUP AND RESTORE:**  
**\# Backup**  
**mongodump \--db mydb \--out /backup/**  
**mongodump \--uri="mongodb://user:pass@host:27017/mydb"**

**\# Restore**  
**mongorestore /backup/**  
**mongorestore \--db mydb /backup/mydb/**

**BEST PRACTICES:**  
**• Design schemas for read/write patterns**  
**• Use indexes appropriately**  
**• Implement replica sets for HA**  
**• Use sharding for horizontal scaling**  
**• Monitor with MongoDB Atlas or Ops Manager**

**9.4 REDIS CACHE:**

**/\* COMMENT: Redis is an in-memory data structure store used as cache, message broker,**  
   **and database. Its speed and versatility make it ideal for caching, session storage,**  
   **and real-time analytics. \*/**

**KEY CONCEPTS:**  
**• In-Memory: Extremely fast data operations**  
**• Data Structures: Strings, lists, sets, hashes, sorted sets**  
**• Persistence: RDB snapshots and AOF logging**  
**• Pub/Sub: Message broadcasting**  
**• Replication: Master-slave for HA**

**BASIC COMMANDS:**  
**\# String operations**  
**SET key "value"**  
**GET key**  
**SETEX key 3600 "value"   \# Set with expiry (seconds)**  
**DEL key**  
**EXISTS key**  
**TTL key                   \# Time to live**

**\# Hash operations**  
**HSET user:1 name "John"**  
**HSET user:1 email "john@example.com"**  
**HGET user:1 name**  
**HGETALL user:1**  
**HDEL user:1 email**

**\# List operations**  
**LPUSH mylist "item1"**  
**RPUSH mylist "item2"**  
**LRANGE mylist 0 \-1**  
**LPOP mylist**

**\# Set operations**  
**SADD myset "member1"**  
**SADD myset "member2"**  
**SMEMBERS myset**  
**SISMEMBER myset "member1"**  
**SREM myset "member1"**

**\# Sorted set operations**  
**ZADD leaderboard 100 "player1"**  
**ZADD leaderboard 200 "player2"**  
**ZRANGE leaderboard 0 \-1 WITHSCORES**  
**ZREVRANGE leaderboard 0 9  \# Top 10**

**CACHING PATTERNS:**  
**\# Cache-aside pattern (lazy loading)**  
**value \= redis.get(key)**  
**if value is None:**  
    **value \= database.query()**  
    **redis.setex(key, 3600, value)**

**\# Write-through pattern**  
**redis.set(key, value)**  
**database.save(value)**

**\# Session storage**  
**SETEX session:abc123 1800 "{\\"user\_id\\": 1, \\"logged\_in\\": true}"**

**MONITORING:**  
**\# Server info**  
**INFO**  
**INFO memory**  
**INFO stats**

**\# Monitor commands in real-time**  
**MONITOR**

**\# Check memory usage**  
**MEMORY USAGE key**

**\# Slow log**  
**SLOWLOG GET 10**

**BEST PRACTICES:**  
**• Set appropriate maxmemory and eviction policy**  
**• Use connection pooling**  
**• Implement TTL for cache keys**  
**• Use Redis Sentinel for HA**  
**• Monitor memory usage and key patterns**
