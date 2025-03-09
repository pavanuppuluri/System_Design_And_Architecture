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

