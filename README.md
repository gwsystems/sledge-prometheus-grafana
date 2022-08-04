
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

4. Run `docker-compose up` to setup and start prometheus and grafana.
5. Grafana is now accessible at `http://localhost:3000/`. The dashboard is named SLEdge. Prometheus is now accessible at `http://localhost:9090/` if you want to issue PromQL queries. You can run driver scripts and you should see the results reflected in the dashboard.
6. When done, hit control+C and optionally run `docker-compose down` to clean up docker assets