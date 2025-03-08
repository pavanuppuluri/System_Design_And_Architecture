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

---
**Examples**

| **Propagation Level** | **Real-World Scenario** |
|----------------------|-----------------------|
| **REQUIRED** (default) | Placing an order (order and stock deduction must be in the same transaction) |
| **REQUIRES_NEW** | Logging errors (should always be saved even if the main transaction fails) |
| **SUPPORTS** | Fetching a user profile (works with or without a transaction) |
| **NOT_SUPPORTED** | Generating reports (should not run inside a transaction) |
| **MANDATORY** | Payment processing (must always be inside a transaction) |
| **NEVER** | Sending email notifications (must not be part of a transaction) |
| **NESTED** | Order status update (partial rollback without affecting the main transaction) <br> **Scenario**: Updating order status should be partially rollback-able, without affecting the entire transaction|


**REQUIRES_NEW**

📌 Scenario: Logging system should work independently even if an order fails.

```
@Service
public class OrderService {
    @Autowired
    private AuditService auditService;

    @Transactional(propagation = Propagation.REQUIRED)
    public void placeOrder(Long userId, Long productId) {
        try {
            deductStock(productId);
            saveOrder(userId, productId);
        } catch (Exception e) {
            auditService.logFailure(userId, "Order failed: " + e.getMessage());
        }
    }
}

@Service
public class AuditService {
    @Transactional(propagation = Propagation.REQUIRES_NEW)
    public void logFailure(Long userId, String message) {
        // Save error log
    }
}
```

💡 If placeOrder fails, the audit log is still saved because it runs in a separate transaction.

**MANDATORY**

📌 **Scenario**: Payment processing must be done within an existing transaction; otherwise, it should fail.

```
@Service
public class PaymentService {
    @Transactional(propagation = Propagation.MANDATORY)
    public void processPayment(Long orderId) {
        // Deduct balance from user account
        // Save payment details
    }
}
```

**NESTED**

📌 **Scenario**: Updating order status should be partially rollback-able, without affecting the entire transaction.

```
@Service
public class OrderService {
    @Autowired
    private OrderStatusService orderStatusService;

    @Transactional(propagation = Propagation.REQUIRED)
    public void updateOrder(Long orderId) {
        try {
            updatePaymentStatus(orderId);
            orderStatusService.updateOrderStatus(orderId);
        } catch (Exception e) {
            // Payment update fails, but order status change is rollbacked separately
        }
    }

    private void updatePaymentStatus(Long orderId) {
        // Update payment status
    }
}

@Service
public class OrderStatusService {
    @Transactional(propagation = Propagation.NESTED)
    public void updateOrderStatus(Long orderId) {
        // Update order status
        // If this fails, only this part is rolled back
    }
}
```
💡 If updateOrderStatus fails, only its changes are rolled back, but updatePaymentStatus remains committed.
