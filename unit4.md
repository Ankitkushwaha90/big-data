# Hadoop Ecosystem and YARN

## Hadoop Ecosystem Components

The **Hadoop Ecosystem** includes several tools and frameworks designed to handle big data and complement the core Hadoop services (HDFS and MapReduce).

- **HDFS (Hadoop Distributed File System)**: The storage layer that stores large files across multiple machines in a distributed manner.
- **MapReduce**: The computational layer for processing large data sets in parallel.
- **YARN (Yet Another Resource Negotiator)**: Manages resources and job scheduling.
- **Hive**: A data warehouse system that provides SQL-like queries on Hadoop data.
- **Pig**: A platform for analyzing large datasets using a high-level scripting language.
- **HBase**: A NoSQL database for real-time read/write access to large datasets.
- **Zookeeper**: A centralized service for maintaining configuration information and providing synchronization.
- **Flume**: A tool for collecting, aggregating, and moving large amounts of streaming data.
- **Sqoop**: A tool for importing/exporting data between relational databases and Hadoop.
- **Oozie**: A workflow scheduler system to manage Hadoop jobs.

## Schedulers: Fair and Capacity

- **Fair Scheduler**: Allocates resources such that all jobs get an equal share of resources. If there are fewer jobs, they will get more resources. Useful in multi-tenant environments where jobs from different users need to be fairly managed.
- **Capacity Scheduler**: Divides resources among different queues based on predefined capacities. Each queue gets a certain fraction of the total resources. More suitable for large organizations or clusters with multiple groups working on different workloads.

## Hadoop 2.0 New Features

### NameNode High Availability:
- **Active/Standby**: Two NameNodes are configured, one active and one standby. If the active NameNode fails, the standby one takes over, reducing downtime.
- **Zookeeper**: Coordinates failover between the NameNodes.

### HDFS Federation:
Allows multiple NameNodes to share the responsibility of managing HDFS metadata. Each NameNode handles a specific namespace, improving scalability and performance.

### MRv2 (MapReduce Version 2):
Provides a more flexible and efficient MapReduce framework. MRv2 uses **YARN** (Yet Another Resource Negotiator) to decouple resource management from job execution.

### YARN (Yet Another Resource Negotiator):
Manages resources in the cluster. It allocates resources to applications and schedules jobs. Enables running MapReduce jobs and other applications, like Spark, on top of Hadoop.

### Running MRv1 in YARN:
YARN can run legacy MapReduce v1 jobs alongside MapReduce v2 and other frameworks like Spark or Tez.

## NoSQL Databases: Introduction to NoSQL

NoSQL databases are designed for scalability, performance, and flexibility. They support a variety of data models that are not typically based on traditional relational tables.

### Key Features:
- **Non-relational**: Doesn't use SQL or a fixed schema.
- **Scalable**: Easily handles large amounts of data and high-speed transactions.
- **Flexible**: Supports a variety of data models, including document, key-value, graph, and column-family stores.

### MongoDB: Introduction, Data Types, CRUD Operations

MongoDB is a widely used NoSQL database, known for its flexibility in handling JSON-like documents.

#### Data Types:
- **String**: Text data.
- **Integer**: Whole numbers.
- **Boolean**: True/false.
- **Array**: Ordered list of elements.
- **Object**: Embedded documents.
- **Date**: Date and time data.

#### Creating Documents:
```js
db.collection.insertOne({ name: "John", age: 30 });
```
#### Updating Documents:
```js
db.collection.updateOne({ name: "John" }, { $set: { age: 31 } });
```
#### Deleting Documents:
```js
db.collection.deleteOne({ name: "John" });
```
#### Querying Documents:
```js
db.collection.find({ age: { $gt: 25 } });
```
#### Indexing:
MongoDB uses indexes to speed up query execution. The default index is created on the _id field, but you can create custom indexes for faster access to specific fields.

```js
db.collection.createIndex({ name: 1 });
```
#### Capped Collections:
MongoDB supports capped collections, which are fixed-size collections that automatically overwrite the oldest documents when the limit is reached.

```js
db.createCollection("logs", { capped: true, size: 10000 });
```
# Spark: Installing Spark, Spark Applications, Jobs, Stages, and Tasks

Apache Spark is a fast, in-memory data processing engine that works well with Hadoop and other distributed data sources.

## Installing Spark

### Install Spark:
- Download from the official Spark website or use package managers (e.g., `apt` or `yum`).
- Install Java and configure `JAVA_HOME`.

### Running Spark:
- Start Spark’s master and worker nodes with commands like `start-master.sh` and `start-worker.sh`.

## Spark Applications:

A Spark application consists of:
- **Driver Program**: The main program that controls the execution of the Spark job.
- **Cluster Manager**: Manages resources across the cluster (e.g., YARN, Mesos).
- **Worker Nodes**: Execute the tasks of the job.

## Jobs, Stages, and Tasks:

- **Job**: A high-level unit of computation in Spark (e.g., reading data, applying transformations).
- **Stage**: A physical division of a job based on narrow transformations.
- **Task**: A single unit of work within a stage, executed by a worker node.

## Resilient Distributed Datasets (RDDs):

RDD is the fundamental abstraction in Spark for distributed data processing. It is an immutable distributed collection of objects that can be processed in parallel.

### Anatomy of a Spark Job Run:
1. Driver initiates a Spark job by calling Action methods.
2. Spark submits jobs to the Cluster Manager, which allocates resources.
3. Jobs are split into Stages based on data shuffling.
4. Each stage is divided into Tasks, which are distributed across the worker nodes.

## Spark on YARN:

Spark can run on YARN, Hadoop's resource manager, to leverage Hadoop's distributed storage and resource management.

---

# Scala: Introduction

Scala is a functional and object-oriented programming language that runs on the JVM and is often used with Apache Spark.

## Classes and Objects:
- **Class**: Blueprint for creating objects.

```scala
class Person(val name: String, var age: Int)
```
## Object: Singleton instance in Scala, often used for defining utility methods.

```scala
object MyApp extends App {
  println("Hello, Scala!")
}
```
## Basic Types and Operators:
Basic Types: Int, String, Double, Boolean, etc.

### Operators: Supports standard arithmetic, logical, and relational operators.

### Control Structures:
If/Else:

```scala
if (x > 0) println("Positive") else println("Negative")
```
### For loop:

```scala
for (i <- 1 to 5) println(i)
```
### Functions and Closures:
#### Function Definition:

```scala
def add(x: Int, y: Int): Int = x + y
```
### Closures: Functions that capture free variables from their surrounding environment.

```scala
val factor = 2
val multiply = (x: Int) => x * factor
```
### Inheritance:
Inheritance allows one class to inherit from another.

```scala
class Animal {
  def sound(): String = "Some sound"
}

class Dog extends Animal {
  override def sound(): String = "Bark"
}
```
These notes give a comprehensive overview of the topics related to the Hadoop Ecosystem, YARN, MongoDB, Spark, and Scala for Big Data applications.
