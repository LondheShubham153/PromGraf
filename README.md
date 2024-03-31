# PromGraf

This repository provides a guide for setting up Grafana, Loki, Promtail, Prometheus, and cAdvisor for monitoring and visualization purposes. Below are the steps to install and configure these tools.

## Video Tutorial
[Watch the tutorial on YouTube](https://youtu.be/QwGm5m4AxNA)

## Install Grafana on Debian or Ubuntu
```bash
sudo apt-get install -y apt-transport-https
sudo apt-get install -y software-properties-common wget
sudo wget -q -O /usr/share/keyrings/grafana.key https://apt.grafana.com/gpg.key
```
# Stable release
```
echo "deb [signed-by=/usr/share/keyrings/grafana.key] https://apt.grafana.com stable main" | sudo tee -a /etc/apt/sources.list.d/grafana.list
```
# Beta release
```
echo "deb [signed-by=/usr/share/keyrings/grafana.key] https://apt.grafana.com beta main" | sudo tee -a /etc/apt/sources.list.d/grafana.list
```
```bash
sudo apt-get update
sudo apt-get install grafana
sudo systemctl status grafana-server
Install Loki and Promtail using Docker
```
# Download Loki Config
```
wget https://raw.githubusercontent.com/grafana/loki/v2.8.0/cmd/loki/loki-local-config.yaml -O loki-config.yaml
```
# Run Loki Docker container
```
docker run -d --name loki -v $(pwd):/mnt/config -p 3100:3100 grafana/loki:2.8.0 --config.file=/mnt/config/loki-config.yaml
```
# Download Promtail Config
```
wget https://raw.githubusercontent.com/grafana/loki/v2.8.0/clients/cmd/promtail/promtail-docker-config.yaml -O promtail-config.yaml
```
# Run Promtail Docker container
```
docker run -d --name promtail -v $(pwd):/mnt/config -v /var/log:/var/log --link loki grafana/promtail:2.8.0 --config.file=/mnt/config/promtail-config.yaml
```
Install Prometheus and cAdvisor
# Download the prometheus config file

```bash
wget https://raw.githubusercontent.com/prometheus/prometheus/main/documentation/examples/prometheus.yml
```
# Install Prometheus using Docker
```
docker run -d --name=prometheus -p 9090:9090 -v <PATH_TO_prometheus.yml_FILE>:/etc/prometheus/prometheus.yml prom/prometheus --config.file=/etc/prometheus/prometheus.yml
```
# Add cAdvisor target to prometheus.yml
# Check Config

# Using Docker Compose
# Check docker-compose.yml

# Verify
```
docker-compose up -d
docker-compose ps
```
