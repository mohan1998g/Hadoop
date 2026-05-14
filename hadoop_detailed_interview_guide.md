# 📘 Hadoop Engineer Interview – Complete Guide (Detailed Q&A)

---

# 1. What is Hadoop?
Hadoop is an open-source distributed computing framework designed to store and process large volumes of data across clusters of commodity hardware.

### Key Features
- Distributed storage (HDFS)
- Parallel processing (MapReduce)
- Fault tolerance (replication)
- Scalability (add more nodes)

### Example
A company storing petabytes of log data uses Hadoop to distribute files across multiple nodes instead of a single server.

---

# 2. Hadoop Architecture (High-Level)

```
        +-------------------+
        |   Client Request  |
        +-------------------+
                 |
        +-------------------+
        |   NameNode        |
        +-------------------+
          /        |           +--------+ +--------+ +--------+
   |DataNode| |DataNode| |DataNode|
   +--------+ +--------+ +--------+
```

---

# 3. HDFS Deep Dive

## How Write Works
1. Client sends request to NameNode
2. NameNode returns block locations
3. Data written to DataNodes (pipeline)

## How Read Works
1. Client asks NameNode
2. NameNode gives block locations
3. Client reads from nearest DataNode

---

## FSImage & EditLog
- FSImage: snapshot of metadata
- EditLog: transaction log

## Secondary NameNode
- Merges FSImage + EditLog
- Performs checkpointing

⚠️ Interview Tip: Not a backup node.

---

# 4. MapReduce Detailed

## Flow Diagram
```
Input -> Map -> Shuffle -> Sort -> Reduce -> Output
```

## Example: Word Count

### Mapper
```
Hello World Hello
→ (Hello,1), (World,1), (Hello,1)
```

### Reducer
```
Hello → 2
World → 1
```

## Key Concepts
- Combiner: Local aggregation
- Partitioner: decides reducer
- Shuffle: data transfer between map and reduce

---

# 5. YARN Architecture

```
        ResourceManager
           /        NodeManager  NodeManager
         |             |
   Containers     Containers
```

## Components
- ResourceManager: Scheduler
- NodeManager: Worker
- ApplicationMaster: Job coordinator

---

# 6. Hive Detailed

## Architecture
```
User -> HiveQL -> Driver -> Execution Engine -> HDFS
```

## Managed vs External Table
| Feature | Managed | External |
|--------|--------|----------|
|Data control|Hive|User|
|Drop table|Deletes data|Keeps data|

## Partitioning Example
```
CREATE TABLE sales(year INT, amount INT)
PARTITIONED BY (country STRING);
```

---

# 7. Spark vs Hadoop

| Feature | Hadoop | Spark |
|--------|--------|--------|
|Processing|Disk-based|In-memory|
|Speed|Slow|Fast|
|Use case|Batch|Batch + Stream|

## Why Spark Faster?
- In-memory computation
- DAG execution

---

# 8. Sqoop & Flume

## Sqoop
Used for structured data transfer.

Example:
```
sqoop import --connect jdbc:mysql://db --table emp
```

## Flume
Used for log ingestion.

Architecture:
```
Source -> Channel -> Sink
```

---

# 9. Advanced Topics

## Small File Problem
- Too many small files overload NameNode memory

### Solution
- HAR files
- Sequence files
- HBase

## Compression
- Gzip
- Snappy
- LZO

---

# 10. Scenario-Based Answers

## Q: NameNode Crash?
Answer:
- Use HA setup (Active + Standby)
- Metadata recovered via JournalNodes

## Q: Large Small Files?
Answer:
- Combine files
- Use HBase

## Q: Slow Hive Query?
Answer:
- Use partitioning
- Use ORC format
- Enable Tez execution

---

# 11. Real-Time Processing

## Hadoop Limitation
- Batch only

## Alternative
- Spark Streaming
- Kafka
- Flink

---

# 12. Real Interview Question Answer

## Question: Explain full data pipeline

### Sample Answer
- Data ingestion using Flume/Kafka
- Store in HDFS
- Process using Spark/Hive
- Export using Sqoop

---

# ✅ Final Interview Tips
- Always explain with diagrams
- Use real examples
- Show optimization techniques
- Highlight project experience

---

✅ This document can be used for:
- Quick revision
- Interview preparation
- Mock interviews
