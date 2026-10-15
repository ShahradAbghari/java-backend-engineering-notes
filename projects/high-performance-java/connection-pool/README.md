# Connection Pool Tuning

More database connections do not automatically mean more throughput.

A pool that is too large can increase database contention. A pool that is too small can create application-side queueing.

## Spring Boot / HikariCP example

```yaml
spring:
  datasource:
    hikari:
      maximum-pool-size: 20
      minimum-idle: 5
      connection-timeout: 1000
      validation-timeout: 500
      idle-timeout: 600000
      max-lifetime: 1800000
```

These values are examples, not universal recommendations.

## Tune using

- request concurrency
- query duration
- database connection limits
- pool utilization
- pending connection requests
- timeout rate

The correct pool size is workload-dependent and must be validated under load.
