# Java 21 Demo

Practical examples of Java 21 features that are useful in backend engineering.

## Topics

### Virtual Threads

Virtual threads can simplify highly concurrent I/O-bound workloads by allowing a thread-per-task programming model without the cost profile of traditional platform threads.

Good candidates:

- HTTP calls
- database calls
- blocking I/O
- high-concurrency request processing

They do not automatically make CPU-bound work faster.

### Records

Records are useful for concise immutable data carriers such as:

- API request/response models
- events
- configuration values
- internal command/query models

Example:

```java
public record CustomerResponse(
        long id,
        String name,
        String email
) {}
```

### Pattern Matching for switch

```java
static String describe(Object value) {
    return switch (value) {
        case Integer i -> "integer: " + i;
        case Long l -> "long: " + l;
        case String s -> "text: " + s;
        case null -> "null";
        default -> "other";
    };
}
```

## Engineering Note

Use modern language features when they make production code easier to read, reason about, and maintain. New syntax by itself is not an architecture improvement.
