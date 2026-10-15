# Database Optimization

Many backend performance problems are database problems.

## Example: avoid N+1 queries

### Risky pattern

```java
for (Order order : orders) {
    Customer customer = customerRepository.findById(order.getCustomerId()).orElseThrow();
}
```

For 500 orders, this can produce hundreds of additional queries.

### Better direction

Fetch only the required columns and relationships in a bounded number of queries.

```sql
SELECT o.id,
       o.total_amount,
       c.id   AS customer_id,
       c.name AS customer_name
FROM orders o
JOIN customers c ON c.id = o.customer_id
WHERE o.created_at >= ?
ORDER BY o.created_at DESC
LIMIT ?;
```

## Check

- execution plan
- indexes
- scanned rows
- returned rows
- lock waits
- slow queries
- unnecessary joins
- N+1 behavior
