# JVM & GC Tuning

JVM tuning should start from measurements, not copied flags.

## Useful signals

- heap occupancy
- allocation rate
- pause duration
- GC frequency
- promotion rate
- thread count
- CPU saturation

## Example baseline

For modern low-latency services on supported JDKs, start with the default collector unless measurements show a problem.

```bash
java \
  -Xms2g \
  -Xmx2g \
  -Xlog:gc*:file=gc.log:time,uptime,level,tags \
  -jar app.jar
```

Keeping `Xms` and `Xmx` equal can reduce runtime heap resizing, but the right heap size depends on workload and container memory limits.

## Avoid

- copying random GC flags from blog posts
- setting huge heaps without considering pause behavior
- tuning GC before fixing allocation-heavy code
