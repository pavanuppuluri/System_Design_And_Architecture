# Spring Transaction Propagation Levels

- In Spring Framework, **transaction propagation levels define how transactions behave when called within other transactions**
- Spring provides several propagation levels to control the behavior of transactions when interacting with existing transactions

**1. REQUIRED (Default)**

- Uses the existing transaction if available; otherwise, starts a new transaction
- Commonly used as it ensures a transaction is always present

**Example:**
```
@Transactional(propagation = Propagation.REQUIRED)
public void someMethod() { ... }
```

**2. REQUIRES_NEW**

- Always starts a new transaction, suspending any existing one
- Useful when you want an independent transaction
  
**Example:**
```
@Transactional(propagation = Propagation.REQUIRES_NEW)
public void independentMethod() { ... }
```

**3. SUPPORTS**

- Uses the current transaction if present; otherwise, executes without a transaction.
- Does not enforce a transaction but participates if one exists.

**Example:**
```
@Transactional(propagation = Propagation.SUPPORTS)
public void optionalTransactionMethod() { ... }
```
**4. NOT_SUPPORTED**

- Runs outside of any transaction, **suspending any existing one**.
- Useful for operations that should not be transactional.

**Example:**
```
@Transactional(propagation = Propagation.NOT_SUPPORTED)
public void nonTransactionalMethod() { ... }
```

**5. MANDATORY**

- Requires an existing transaction; **if none exists, it throws an exception**.
- Ensures that the method is always called within a transaction.
  
**Example:**
```
@Transactional(propagation = Propagation.MANDATORY)
public void mustBeInsideTransaction() { ... }
```

**6. NEVER**

- Must not run inside a transaction; **if a transaction exists, it throws an exception**.
- Useful for operations that must be completely non-transactional.

**Example:**
```
@Transactional(propagation = Propagation.NEVER)
public void ensureNoTransaction() { ... }
```

**7. NESTED**

- Runs inside a nested transaction within the current transaction.
- If the nested transaction fails, only the nested part is rolled back, not the outer transaction.
- Requires a JDBC data source that supports savepoints.
  
**Example:**
```
@Transactional(propagation = Propagation.NESTED)
public void nestedTransactionMethod() { ... }
```

**Choosing the Right Propagation Level**

- Use REQUIRED (default) when unsure.
- Use REQUIRES_NEW for independent transactions (e.g., logging, audit records).
- Use SUPPORTS for optional transactions.
- Use MANDATORY when a transaction must exist.
- Use NEVER or NOT_SUPPORTED for non-transactional methods.
- Use NESTED when partial rollbacks are needed.

