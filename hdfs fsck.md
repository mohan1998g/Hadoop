### `hdfs fsck` — What is it?

`hdfs fsck` stands for **HDFS File System Check**. It is primarily a **diagnostic command** used to check the health and integrity of files in HDFS.

It can identify problems such as:

* Missing blocks
* Corrupt blocks
* Under-replicated blocks
* Over-replicated blocks
* Files with insufficient replication
* Filesystem inconsistencies

### Basic syntax

```bash
hdfs fsck <path>
```

Example:

```bash
hdfs fsck /data
```

You might see output such as:

```text
Status: HEALTHY
 Total size: 10 GB
 Total dirs: 20
 Total files: 100
 Total blocks (validated): 150
 Minimally replicated blocks: 150
 Over-replicated blocks: 0
 Under-replicated blocks: 0
```

---

## Is `hdfs fsck` used to repair HDFS?

**No, this is an important interview point.**

`hdfs fsck` is primarily a **check/reporting tool**, not a general repair command.

For example:

```bash
hdfs fsck /data
```

can tell you:

```text
Under-replicated blocks: 5
Missing blocks: 1
Corrupt blocks: 2
```

But `fsck` itself doesn't simply "repair everything."

### Common misconception

❌ Incorrect:

> `hdfs fsck` repairs corrupted HDFS files.

✅ Better:

> `hdfs fsck` checks HDFS filesystem health and reports missing, corrupt, under-replicated, or over-replicated blocks. HDFS mechanisms such as replication and DataNode recovery generally handle block recovery, while administrators use the diagnostic output to investigate problems.

---

# Important `fsck` options

### 1. Check a directory

```bash
hdfs fsck /data
```

Checks the files under `/data`.

---

### 2. Find under-replicated blocks

```bash
hdfs fsck /data -underReplicated
```

Useful for identifying blocks whose replication factor is below the configured requirement.

For example:

```text
Replication factor = 3

Expected:
Block A → DN1 DN2 DN3

Actual:
Block A → DN1 DN2
```

That block is **under-replicated**.

HDFS can normally detect this and schedule another replica.

---

### 3. Find missing blocks

```bash
hdfs fsck /data -list-corruptfileblocks
```

This helps identify files containing corrupt/missing blocks.

---

### 4. Show block information

```bash
hdfs fsck /data -files -blocks -locations
```

This is particularly useful for troubleshooting.

You can get information such as:

```text
File: /data/customers.csv
Blocks:
Block 1 → DataNode1, DataNode2, DataNode3
Block 2 → DataNode2, DataNode3, DataNode4
```

---

# What happens when a block is lost?

Suppose a file has replication factor **3**:

```text
customers.csv

Block 1 → DN1 DN2 DN3
Block 2 → DN1 DN2 DN3
Block 3 → DN1 DN2 DN3
```

Now DN3 fails:

```text
Block 1 → DN1 DN2
Block 2 → DN1 DN2
Block 3 → DN1 DN2
```

These blocks become **under-replicated**.

The NameNode detects this and schedules replication:

```text
Block 1 → DN1 DN2 DN4
Block 2 → DN1 DN2 DN5
Block 3 → DN1 DN2 DN6
```

So the cluster can recover the desired replication **without `fsck` directly repairing the blocks**.

---

# `fsck` vs repair

| Command/Mechanism                       | Purpose                                                  |
| --------------------------------------- | -------------------------------------------------------- |
| `hdfs fsck /data`                       | Check filesystem health                                  |
| `hdfs fsck ... -blocks`                 | Show block information                                   |
| `hdfs fsck ... -locations`              | Show DataNode locations                                  |
| `hdfs fsck ... -list-corruptfileblocks` | Identify corrupt files/blocks                            |
| HDFS replication                        | Recovers under-replicated blocks                         |
| DataNode                                | Stores/serves block replicas                             |
| NameNode                                | Tracks block metadata and replication                    |
| Administrator                           | Investigates serious corruption/missing-block situations |

### Interview answer

> **`hdfs fsck` is a diagnostic tool used to check the health and integrity of HDFS. It reports issues such as missing, corrupt, under-replicated, and over-replicated blocks. It does not act as a general repair command; HDFS's replication and recovery mechanisms handle many block-replication problems automatically.**
