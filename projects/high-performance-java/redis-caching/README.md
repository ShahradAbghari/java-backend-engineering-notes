# Redis Caching

Caching can reduce latency and database load, but it adds consistency and invalidation problems.

## Cache-aside example

```java
@Service
class ProductService {

    private final ProductRepository repository;

    ProductService(ProductRepository repository) {
        this.repository = repository;
    }

    @Cacheable(cacheNames = "products", key = "#id")
    public Product findById(long id) {
        return repository.findById(id).orElseThrow();
    }

    @CacheEvict(cacheNames = "products", key = "#id")
    public void update(long id, ProductUpdate update) {
        repository.update(id, update);
    }
}
```

## Questions before adding a cache

- Is the data read frequently?
- How stale may it be?
- What is the TTL?
- How is invalidation handled?
- What happens during cache failure?
- Can hot keys overload a single shard?
