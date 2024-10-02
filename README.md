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

---

Step 2: Access Grafana
Open Grafana by navigating to http://localhost:5300 (or the custom port you configured). Log in with the default credentials (admin/admin).

Step 3: Add Prometheus as a Data Source
Once logged into Grafana, navigate to Configuration (gear icon) > Data Sources.
Click on Add Data Source.
Select Prometheus.
Set the URL to http://prometheus:5090 (adjust if using a different port).
Click Save & Test to ensure Prometheus is properly connected.
Step 4: Import Pre-built Grafana Dashboards
Grafana provides many pre-built dashboards for monitoring Kubernetes, Docker, and host metrics. Here’s how you can import them:

1. Kubernetes Monitoring Dashboard
   Go to Dashboards (four squares icon) > Manage.
   Click Import.
   Use Dashboard ID: 315 (for the Kubernetes cluster monitoring dashboard).
   Dashboard Link: Grafana Kubernetes Monitoring
   Click Load, and select your Prometheus data source when prompted.
   This dashboard will show you metrics for your Kubernetes cluster, such as pod health, node CPU/memory usage, and network traffic.
2. Node Exporter (Host/VM Monitoring) Dashboard
   Go to Dashboards > Manage > Import.
   Use Dashboard ID: 1860 (for Node Exporter Full).
   Dashboard Link: Grafana Node Exporter Full Dashboard
   Click Load and select your Prometheus data source.
   This dashboard provides detailed information about your host system (VM/physical machine), such as CPU, memory, disk I/O, and network usage.
3. Docker Monitoring Dashboard
   Go to Dashboards > Manage > Import.
   Use Dashboard ID: 14282 (for cAdvisor Exporter).
   Dashboard Link: Grafana Docker Monitoring Dashboard
   Click Load and select your Prometheus data source.
   This dashboard will provide detailed metrics about your Docker containers, such as CPU usage, memory usage, and container health.
   Step 5: Customize and Explore Dashboards
   Once you have imported these dashboards, you will be able to:

Kubernetes Metrics: See metrics such as pod resource usage, node health, network traffic, and more.
VM/Host Metrics: View system-level metrics like CPU usage, memory consumption, disk I/O, and network statistics from your VMs or physical servers.
Docker Container Metrics: Monitor the performance and health of your Docker containers, including CPU and memory usage per container.
You can also create custom dashboards in Grafana by selecting specific metrics from Prometheus using the query language PromQL.

Import Dashboards: You can find pre-configured dashboards for Node Exporter, cAdvisor, and Kubernetes in the Grafana dashboard library. For example:

Node Exporter Full (ID: 1860)
cAdvisor Exporter (ID: 14282)
Kubernetes Cluster Monitoring (ID: 8588)
