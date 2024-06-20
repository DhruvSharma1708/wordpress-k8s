# WordPress Kubernetes Deployment

## Prerequisites

- Kubernetes cluster
- kubectl configured
- Helm installed
- Docker installed

## Deployment

### Step 1: Create Persistent Volumes

```sh
kubectl apply -f mysql-pv.yaml
kubectl apply -f wordpress-pv.yaml

### Step 2: Build Docker Images

docker build -t my-wordpress ./wordpress
docker build -t my-mysql ./mysql
docker build -t my-nginx ./nginx
docker push my-wordpress
docker push my-mysql
docker push my-nginx

### Step 3: Deploy Helm Chart

helm install my-release ./wordpress-chart

### Cleanup

helm delete my-release

### Monitoring and Alerting
####Deploy Prometheus and Grafana

helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm repo update
helm install prometheus prometheus-community/kube-prometheus-stack

####Apply Prometheus Rules

kubectl apply -f monitoring/nginx-prometheus-rules.yaml

#Metrics
##Nginx Metrics
###Total Request Count
###Total 5xx Request Count
##Pod Metrics
###Pod CPU Utilization

#License
##This project is licensed under the MIT License.


This setup provides a complete solution to deploy a production-grade WordPress application on Kubernetes, with monitoring and alerting in place using Prometheus and Grafana.
