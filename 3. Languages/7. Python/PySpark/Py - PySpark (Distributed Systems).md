See: 
* [[Py - Introduction to Python]]
Resources:


---

# Distributed Systems

## What is a Distributed System?
* **Distributed Systems**: Systems that give access to files stored on different machines
	* These systems are useful when data grows and one computer is not enough to perform calculations 
	* Files are divided into segments, and each segment can be saved multiple times, in a few different locations

## Spark: A Distributed System
* **Spark** is a type of distributed system, which allows it to quickly access tons of data to perform calculations.
* Spark’s distributed file system consists of multiple **nodes** (a computer with the ability to computer and process data)
	* Types of Nodes
		1) **NameNode** -- manages the assignment of files to different machine clusters
		2) **DataNode** -- stores and processes data. 
			* Each file will be replicated in multiple data nodes to avoid data loss
![[pyspark-nodes.png]]

## Improving Data Storage and Processing
* There are two ways to improve a computer's ability to store and process more data
	1) Scaling Up
	2) Scaling Out
### Scaling Up
* Scaling Up -- increasing the efficiency of every node or replacing the nodes with more powerful ones
### Scaling Out
* Scaling out -- Increasing the _number_ of nodes in a cluster

![[scaling-types.png]]


