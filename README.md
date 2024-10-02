git clone https://github.com/achrafnh/Prometheus-Grafana-docker-compose.git

cd Prometheus-Grafana-docker-compose/

docker-compose up -d


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

Access the Services:

Grafana: http://localhost:5300
Prometheus: http://localhost:5090
Node Exporter: http://localhost:5100/metrics
cAdvisor: http://localhost:5080
Kube-State-Metrics: http://localhost:5081/metrics
Configure Grafana:

Add Prometheus as a data source in Grafana by navigating to http://localhost:5300 and configuring the URL as http://prometheus:5090.




To view all metrics for Kubernetes, VMs (hosts), and Docker containers using Prometheus and Grafana, follow these steps:

Step 1: Ensure Metrics Scraping Is Set Up
Ensure that Prometheus is scraping the metrics for:

Kubernetes (via kube-state-metrics and API server)
VM/host (via Node Exporter)
Docker containers (via cAdvisor)
