# Performance Options

## download\_sems

Number of downloads that run at the same time (default `6`). The worker thread pool is twice this value.

Must be at least `1`: a value of `0` or less falls back to `6`.

`--downloadsem` (`-sd`) overrides it for one run.

### Values to pick

* The default of 6 works for most setups
* Raise it for big creators on a fast connection, lower it if you see timeouts

***

## download\_limit

Maximum download speed in bytes per second, shared across all downloads. `0` means unlimited. Non-zero values below `1024` are raised to `1024`.

`--download-limit` (`-dl`) overrides it for one run, for example `-dl 10MB`.

**Accepts:**

* Human-readable inputs
* An integer representing bytes per second
