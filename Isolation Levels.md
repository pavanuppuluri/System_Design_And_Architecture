# Database Isolation Levels

Database isolation levels define how transactions interact with each other, particularly in a multi-user environment. <br>
There are four isolation levels:

**1. Read Uncommitted**
- **Description**: Transactions can read uncommitted changes made by other transactions.
- **Issue**: Can lead to dirty reads, non-repeatable reads, and phantom reads.
- **Example**:
  - Transaction A updates a row but hasn’t committed.
  - Transaction B reads the updated row.
  - If Transaction A rolls back, Transaction B has read invalid (dirty) data.

**2. Read Committed (Default in SQL Server, Oracle)**
- **Description**: Transactions can only read committed data, but data can still change between reads.
- **Issue**: Prevents dirty reads but allows non-repeatable reads and phantom reads.
- **Example**:
  - Transaction A reads a row.
  - Transaction B updates and commits changes to the same row.
  - Transaction A reads the row again and gets different data.
    
**3. Repeatable Read (Default in MySQL InnoDB)**
- **Description**: Ensures that if a transaction reads a row, no other transaction can modify it until the first transaction is complete.
- **Issue**: Prevents dirty reads and non-repeatable reads, but allows phantom reads.
- **Example**:
  - Transaction A selects a row.
  - Transaction B attempts to update the row but must wait for Transaction A to commit or roll back.
  - If Transaction A reads the row again, it sees the same data.
    
**4. Serializable**
- **Description**: The strictest level; transactions are executed in a way that ensures complete isolation.
- **Issue**: Prevents all concurrency issues but can significantly reduce performance.
- **Example**:
  - If Transaction A is reading a dataset, Transaction B must wait until Transaction A completes before it can read or modify the same data.
 
