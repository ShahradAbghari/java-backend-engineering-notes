# High Throughput

High throughput is about completing more useful work per unit of time without causing unstable latency, resource exhaustion, or downstream overload.

## Example: bounded parallel processing

```java
@Configuration
class ExecutorConfig {

    @Bean
    Executor orderExecutor() {
        return Executors.newFixedThreadPool(
                Math.max(4, Runtime.getRuntime().availableProcessors() * 2)
        );
    }
}
```

```java
@Service
class OrderProcessor {

    private final Executor orderExecutor;

    OrderProcessor(Executor orderExecutor) {
        this.orderExecutor = orderExecutor;
    }

    CompletableFuture<Void> process(Order order) {
        return CompletableFuture.runAsync(
                () -> handle(order),
                orderExecutor
        );
    }

    private void handle(Order order) {
        // CPU/I/O work
    }
}
```

The important idea is **bounded concurrency**. An unbounded queue or executor can turn traffic spikes into memory pressure and long tail latency.

## Throughput checklist

- request rate
- active threads
- queue depth
- connection-pool saturation
- downstream capacity
- CPU utilization
- allocation rate
- p95/p99 latency
