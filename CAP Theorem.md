# CAP Theorem Explained with Database Examples

The **CAP Theorem** (also known as Brewer's Theorem) states that in a distributed data store, you can only achieve **two out of three** guarantees at any given time:

1. **Consistency (C)** - Every read receives the most recent write or an error.
2. **Availability (A)** - Every request receives a response (success or failure), but it may not be the latest data.
3. **Partition Tolerance (P)** - The system continues to operate despite network failures.

Since network partitions (**P**) are inevitable in distributed systems, a database can either prioritize **Consistency (CP)** or **Availability (AP)** but not both at the same time.

---

## **1. CP (Consistency + Partition Tolerance, sacrificing Availability)**  
- Prioritizes strong consistency: Ensures that all nodes have up-to-date data but may reject requests when a network partition occurs.  
- Suitable for applications that require strict data accuracy, such as banking or financial transactions.  

### **Examples of CP Databases:**  
- **MongoDB (when using distributed transactions)**  
- **HBase**  
- **Google Bigtable**  
- **Redis (in single primary mode)**  

---

## **2. AP (Availability + Partition Tolerance, sacrificing Consistency)**  
- Prioritizes availability: The system remains operational, but some nodes might return stale data during a partition.  
- Suitable for applications where availability is more important than immediate consistency, such as social media feeds or caching systems.  

### **Examples of AP Databases:**  
- **Cassandra**  
- **DynamoDB**  
- **CouchDB**  
- **Riak**  

---

## **3. CA (Consistency + Availability, sacrificing Partition Tolerance)**  
- Achieves strong consistency and high availability but cannot tolerate network partitions.  
- Realistically, true CA systems are limited to single-node databases or those in a local network.  

### **Examples of CA Databases:**  
- **MySQL (single-node)**  
- **PostgreSQL (single-node)**  
- **Oracle (single-node)**  

---

## **Conclusion**  
- **Choose CP** when you need strict consistency (e.g., banking, financial apps).  
- **Choose AP** when availability is critical (e.g., social networks, real-time analytics).  
- **CA systems** exist only in non-distributed environments, suitable for traditional relational databases.

---
# **Why is MongoDB CP and Cassandra AP?**

The classification of **MongoDB as CP** and **Cassandra as AP** is based on how they handle **Consistency, Availability, and Partition Tolerance** in a distributed environment.

---

## **MongoDB is CP (Consistency + Partition Tolerance)**
MongoDB prioritizes **Consistency** over **Availability** when used in a distributed setup (such as a replica set). Here's why:

### **1. Strong Consistency (C)**  
- MongoDB uses a **primary-secondary replication model** (also known as leader-follower).  
- All writes go to the **primary** node, and secondaries replicate the data asynchronously.  
- If a client reads from the primary, it always gets the latest data (**strong consistency**).  
- If you enforce **write concerns** (e.g., `{ w: "majority" }`), MongoDB ensures that data is written to a majority of nodes before acknowledging the write.

### **2. Partition Tolerance (P)**  
- If the network partitions (e.g., primary node gets isolated), MongoDB will **elect a new primary** if a majority of nodes can still communicate.  
- However, during the election process, **writes are rejected** until a new primary is elected.  
- This means MongoDB sacrifices **Availability** temporarily in favor of maintaining **Consistency**.

#### **Why MongoDB is NOT AP?**
- If a partition occurs and the primary is isolated, MongoDB will refuse writes rather than allow inconsistent data across nodes.
- Read-after-write consistency is ensured when reading from the primary.


## MongoDB: Single Master, trades off Availability

<img width="1339" alt="image" src="https://github.com/user-attachments/assets/aee811f5-c33c-46ed-abda-8b5bbfb31cfd" />



---

## **Cassandra is AP (Availability + Partition Tolerance)**
Cassandra is designed to prioritize **Availability** over **Consistency** in the presence of network partitions. Here’s how:

### **1. High Availability (A)**  
- Cassandra follows a **peer-to-peer architecture** (no single primary node).  
- Writes and reads can be handled by any node in the cluster.  
- Even if some nodes are down or unreachable due to a partition, the system continues to accept writes (though some data may be stale).  

### **2. Partition Tolerance (P)**  
- In case of a network partition, Cassandra ensures that **nodes continue to accept writes and reads** rather than rejecting requests.  
- It uses a technique called **eventual consistency**, meaning updates will propagate across the cluster over time, but some nodes might temporarily serve stale data.

### **3. Tunable Consistency Model**  
- Cassandra allows users to adjust consistency using parameters like **QUORUM, ONE, ALL** for reads and writes.  
- By default, **strong consistency is not guaranteed**, but it can be enforced at the cost of availability.

#### **Why Cassandra is NOT CP?**
- During a partition, Cassandra **does not stop serving data** even if it may be inconsistent.
- Strong consistency can be achieved, but doing so reduces availability.


## Cassandra: No Single Master, Eventually Consistent

<img width="467" alt="image" src="https://github.com/user-attachments/assets/623346a5-236e-4d62-ab5a-9ec517adf37b" />

---

## **Summary Table: MongoDB (CP) vs. Cassandra (AP)**

| Feature        | **MongoDB (CP)**                      | **Cassandra (AP)**                     |
|--------------|--------------------------------|--------------------------------|
| **Architecture** | Primary-Secondary (Leader-Follower) | Peer-to-Peer (No Single Leader) |
| **Consistency** | Strong (if reading from primary) | Eventual (Tunable via QUORUM, ONE, etc.) |
| **Availability** | Low (writes rejected during partition) | High (writes accepted even in partition) |
| **Partition Tolerance** | Yes (new primary elected) | Yes (nodes operate independently) |
| **Use Case** | Banking, Transactions, Logs | Social Media, Real-time Analytics |

---

## **Final Thoughts**
- Choose **MongoDB (CP)** if you need **strong consistency** and are okay with temporary unavailability during failures.
- Choose **Cassandra (AP)** if you need **high availability** and can tolerate eventual consistency.

<br>

**Note** <br>
Be sure to understand the requirements about scale, consistency, and availability before proposing a specific database.








