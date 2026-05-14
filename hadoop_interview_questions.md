# Hadoop Engineer Interview Questions & Answers

## 1. Basic Hadoop

### What is Hadoop?
Hadoop is an open-source framework used to store and process large datasets using distributed computing.

### Core Components
- HDFS: Storage
- MapReduce: Processing
- YARN: Resource management

### NameNode vs DataNode
- NameNode: Manages metadata
- DataNode: Stores actual data blocks

### Replication Factor
Default is 3. It ensures fault tolerance.

---

## 2. HDFS

### How HDFS Works
Files are split into blocks and distributed across nodes.

### FSImage & EditLog
- FSImage: Snapshot of file system
- EditLog: Recent changes

### Secondary NameNode
It performs checkpointing, not a backup.

---

## 3. MapReduce

### Phases
- Map
- Shuffle
- Sort
- Reduce

### Combiner
Acts as mini-reducer to optimize performance.

### Partitioner
Decides which reducer gets which data.

---

## 4. YARN

### Components
- ResourceManager
- NodeManager
- ApplicationMaster

### Containers
Unit of resource allocation (CPU + Memory).

---

## 5. Hive

### What is Hive?
Data warehouse tool on Hadoop for SQL-like queries.

### Partitioning vs Bucketing
- Partitioning: Divides data by column
- Bucketing: Hash-based distribution

---

## 6. Spark vs Hadoop

### Why Spark is Faster?
Uses in-memory processing.

### RDD
Resilient Distributed Dataset – immutable distributed collection.

---

## 7. Sqoop & Flume

### Sqoop
Transfers data between RDBMS and Hadoop.

### Flume
Used for log data ingestion.

---

## 8. Advanced

### Fault Tolerance
Achieved using replication.

### Small File Problem
Too many small files overload NameNode.

---

## 9. Scenarios

### Handling Small Files
Use HDFS archives or combine files.

### NameNode Failure
Use HA setup with standby NameNode.

---

## 10. Practical

### Word Count (Concept)
Map: Emit word,1
Reduce: Sum values

---

## 11. Real-Time

### Hadoop Real-Time?
No (batch processing). Use Spark/Kafka.

---

## 12. Behavioral

### Project Explanation
Explain architecture, tools, and optimizations clearly.
