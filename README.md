# Prometheus-Grafana-docker-compose

To monitor Docker containers, Kubernetes, and host metrics together using a single docker-compose setup, you need to integrate various exporters and configure Prometheus to scrape them. 

Docker compose 
Prometheus: Scrapes metrics from various sources (Docker, Kubernetes, Node Exporter for host metrics).
Grafana: Visualizes the metrics.
Node Exporter: Provides host system metrics (CPU, memory, disk, network).
cAdvisor: Monitors Docker containers.
Kube-State-Metrics (optional): Monitors the state of Kubernetes objects.


Step 3: Kubernetes Setup
If you're running Kubernetes, you also need to set up Prometheus Node Exporter and Kube-State-Metrics inside your Kubernetes cluster.

1. Install Prometheus Node Exporter and Kube-State-Metrics via Helm
Install Node Exporter and Kube-State-Metrics in your Kubernetes cluster using Helm:


helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm repo update

# Install Node Exporter
helm install node-exporter prometheus-community/prometheus-node-exporter

# Install Kube-State-Metrics
helm install kube-state-metrics prometheus-community/kube-state-metrics
