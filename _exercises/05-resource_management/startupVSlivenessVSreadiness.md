# Difference Between Startup, Liveness, and Readiness Probes in Kubernetes

Startup, liveness, and readiness probes in Kubernetes are mechanisms to monitor container health and availability, serving distinct purposes during different phases of a pod's lifecycle.

## Startup Probe

- Verifies if the application's startup process has completed successfully before running any other probes[web:1][web:5].
- If defined, it prevents liveness and readiness probes from running until it succeeds, ensuring slow-starting containers are not killed prematurely[web:2][web:7].
- Only runs during the initial container startup period.

## Liveness Probe

- Checks if the container is still running and functioning properly during its lifecycle[web:1][web:5].
- If the liveness probe fails, Kubernetes restarts the container, useful for detecting deadlocks or unrecoverable states[web:5][web:7].
- Runs periodically throughout the container's life, independent of readiness.

## Readiness Probe

- Determines if the container is ready to accept traffic; if not, the pod is removed from service endpoints so it won't receive requests[web:1][web:2][web:7].
- Useful for cases where containers need time to warm up, load files, or connect to dependencies after starting.
- Runs continuously, allowing recovery from temporary failures without restarting the container[web:1][web:3].

## Kubernetes Probes Summary

| Probe Type      | Purpose                                   | Timing/Trigger                      | Action on Failure                       |
|-----------------|-------------------------------------------|-------------------------------------|-----------------------------------------|
| Startup Probe   | Application started and ready for probes  | At container startup, one-time      | Container restart or wait[web:1][web:2][web:7] |
| Liveness Probe  | Container running normally                | Periodically, after startup probe   | Container restart[web:1][web:5][web:7]         |
| Readiness Probe | Container ready to serve traffic          | Periodically, after startup probe   | Remove pod from endpoints[web:1][web:2][web:7] |

Each probe type helps ensure containers remain healthy and responsive to traffic in Kubernetes clusters, reducing downtime and misdirected requests[web:1][web:2][web:7].
