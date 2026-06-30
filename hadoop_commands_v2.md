# 🔹 1. HDFS File System Commands (`hdfs dfs` / `hadoop fs`)

These are the most frequently used commands.

## ✅ Basic File Operations

```bash
hdfs dfs -ls /path
hdfs dfs -mkdir /path
hdfs dfs -mkdir -p /path/subdir
hdfs dfs -put localfile /hdfs/path
hdfs dfs -get /hdfs/file localpath
hdfs dfs -copyFromLocal file /hdfs/path
hdfs dfs -copyToLocal /hdfs/file localpath
```

## ✅ View & Read Files

```bash
hdfs dfs -cat /file
hdfs dfs -head /file
hdfs dfs -tail /file
hdfs dfs -text /file
```

## ✅ File/Directory Management

```bash
hdfs dfs -rm /file
hdfs dfs -rm -r /dir
hdfs dfs -rmdir /dir        # only if empty
hdfs dfs -mv /src /dest
hdfs dfs -cp /src /dest
```

## ✅ Disk Usage & Info

```bash
hdfs dfs -du /path
hdfs dfs -df -h
hdfs dfs -count /path
hdfs dfs -stat /file
```

## ✅ Permissions

```bash
hdfs dfs -chmod 755 /file
hdfs dfs -chown user:group /file
hdfs dfs -chgrp group /file
```

## ✅ File Operations (Advanced)

```bash
hdfs dfs -appendToFile localfile /hdfs/file
hdfs dfs -getmerge /dir mergedfile
hdfs dfs -touchz /file
```

***

# 🔹 2. HDFS Admin Commands (`hdfs dfsadmin`)

Used by admins.

```bash
hdfs dfsadmin -report
hdfs dfsadmin -safemode enter
hdfs dfsadmin -safemode leave
hdfs dfsadmin -refreshNodes
hdfs dfsadmin -finalizeUpgrade
```

***

# 🔹 3. NameNode & Cluster Commands

```bash
hdfs namenode -format
start-dfs.sh
stop-dfs.sh
```

***

# 🔹 4. YARN Commands (`yarn`)

Used for resource management.

## ✅ Application Management

```bash
yarn application -list
yarn application -status <app_id>
yarn application -kill <app_id>
```

## ✅ Node & Queue Info

```bash
yarn node -list
yarn node -status <node_id>
yarn queue -list
```

## ✅ Logs

```bash
yarn logs -applicationId <app_id>
```

***

# 🔹 5. MapReduce Commands

```bash
mapred job -list
mapred job -status <job_id>
mapred job -kill <job_id>
```

Run a job:

```bash
hadoop jar job.jar ClassName input output
```

***

# 🔹 6. HDFS Balancer & Health

```bash
hdfs balancer
hdfs fsck /
hdfs fsck /path -files -blocks -locations
```

***

# 🔹 7. Snapshot Commands

```bash
hdfs dfsadmin -allowSnapshot /dir
hdfs dfs -createSnapshot /dir snap1
hdfs dfs -deleteSnapshot /dir snap1
```

***

# 🔹 8. DistCp (Large Data Copy)

```bash
hadoop distcp source destination
```

Example:

```bash
hadoop distcp hdfs://cluster1/data hdfs://cluster2/data
```

***

# 🔹 9. Trash Management

```bash
hdfs dfs -expunge
```

Skip trash:

```bash
hdfs dfs -rm -r -skipTrash /path
```

***

# 🔹 10. Help Command

```bash
hdfs dfs -help
hdfs dfs -help ls
```

***

# ✅ Key Tip

There are two interchangeable commands:

```bash
hdfs dfs
hadoop fs
```

Both work the same for file system operations.

***

# ✅ Quick Summary Table

| Category         | Command Example    |
| ---------------- | ------------------ |
| List files       | `-ls`              |
| Upload file      | `-put`             |
| Download file    | `-get`             |
| Delete file      | `-rm`              |
| Delete dir       | `-rm -r`           |
| Empty dir delete | `-rmdir`           |
| Disk usage       | `-du`              |
| Permissions      | `-chmod`           |
| Cluster report   | `dfsadmin -report` |

***
