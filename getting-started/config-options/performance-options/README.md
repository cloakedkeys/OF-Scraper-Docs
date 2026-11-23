# Performance Options

## download\_sems

Number of downloads that run at the same time (default `6`). The worker thread pool is twice this value.

Must be at least `1`: a value of `0` or less falls back to `6`.

***

## download\_limit

Maximum download speed in bytes per second, shared across all downloads. `0` means unlimited.

**Accepts:**

* Human-readable inputs
* An integer representing bytes per second
