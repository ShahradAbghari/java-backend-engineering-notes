# High Performance Java

Practical examples for designing and tuning low-latency, high-throughput Java/Spring Boot services.

This project focuses on measurable engineering trade-offs rather than magic configuration values.

## Topics

- [Low Latency](low-latency/README.md)
- [High Throughput](high-throughput/README.md)
- [Redis Caching](redis-caching/README.md)
- [JVM & GC Tuning](jvm-gc-tuning/README.md)
- [Database Optimization](database-optimization/README.md)
- [Connection Pool Tuning](connection-pool/README.md)

## Principles

1. Measure before optimizing.
2. Optimize the end-to-end request path.
3. Prefer bounded concurrency.
4. Reduce unnecessary remote calls.
5. Protect downstream dependencies.
6. Tune with production-like workloads.
7. Treat p95/p99 latency as first-class metrics.

## Benchmark note

Any performance number in this repository should come from a reproducible benchmark. Placeholder or invented numbers are intentionally avoided.
