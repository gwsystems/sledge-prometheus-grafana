
# Prometheus / Grafana Demo for SLEdge

## How to use

1. Start SLEdge 
2. Validate that you are able to reach the metrics scrape point directly. This should be something like `http://localhost:1776/metrics` and return something like the following:

```
# TYPE total_requests counter
total_requests: 3949658
# TYPE total_5XX counter
total_5XX: 0
<snip>
```
3. By default, prometheus is configured assuming that sledgert is running on the same host that is running the docker daemon executing this container. Outside of a development environment, this is probably not the case. To change this, edit `prometheus.yml` and replace `host.docker.internal:1776` with the IP or hostname and port that resolves to SLEdge's metrics server.

```
global:
  scrape_interval: 5s

scrape_configs:
  - job_name: "SLEdge"
    scrape_interval: 5s
    static_configs:
    - targets: ["host.docker.internal:1776"]

```
