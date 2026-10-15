# Low Latency

Low latency means reducing the time a request spends across the entire critical path.

Typical sources of latency:

- network calls
- database queries
- serialization
- lock contention
- thread starvation
- garbage collection pauses
- cache misses

## Example: remove duplicate database calls

### Naive

```java
public OrderResponse getOrder(long id) {
    Order order = orderRepository.findById(id).orElseThrow();
    Customer customer = customerRepository.findById(order.getCustomerId()).orElseThrow();
    Product product = productRepository.findById(order.getProductId()).orElseThrow();
    return mapper.toResponse(order, customer, product);
}
```

This request performs three sequential database calls.

### Better direction

Use an intentionally designed query, cache stable reference data, or fetch independent data concurrently only when that actually reduces end-to-end latency.

## What to measure

- p50 latency
- p95 latency
- p99 latency
- dependency latency
- database query time
- cache hit ratio
- GC pause time
