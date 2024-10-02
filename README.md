# Prometheus-Grafana-docker-compose

To monitor Docker containers, Kubernetes, and host metrics together using a single docker-compose setup, you need to integrate various exporters and configure Prometheus to scrape them. 

Docker compose 
Prometheus: Scrapes metrics from various sources (Docker, Kubernetes, Node Exporter for host metrics).
Grafana: Visualizes the metrics.
Node Exporter: Provides host system metrics (CPU, memory, disk, network).
cAdvisor: Monitors Docker containers.
Kube-State-Metrics (optional): Monitors the state of Kubernetes objects.
