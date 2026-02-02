# Cloud-Native Monitoring Stack with Prometheus & Grafana

This project demonstrates a **cloud-native monitoring stack** deployed on a Kubernetes cluster using **Prometheus** and **Grafana**. It provides real-time monitoring, alerting, and dashboards for observability of containerized applications.

---

## Features

- **Prometheus**: Metrics collection and alerting  
- **Grafana**: Visual dashboards for system health and metrics  
- **Kubernetes Native**: Deployments, Services, ConfigMaps, and Persistent Volumes  
- **Persistent Storage**: Grafana dashboards stored with PVC for data retention  
- **End-to-End Deployment**: Production-like cloud-native environment  

---

## Architecture

Kubernetes Cluster
├─ Namespace: monitoring
│ ├─ Prometheus Deployment & Service
│ │ └─ Collects metrics from targets
│ └─ Grafana Deployment & Service
│ └─ Visualizes metrics from Prometheus
└─ Persistent Volumes (PVC) for Grafana dashboards

---

## Project Structure

k8s-monitoring/
├─ prometheus/
│ ├─ deployment.yaml # Prometheus Deployment
│ ├─ service.yaml # Prometheus Service
│ └─ config-map.yaml # Prometheus ConfigMap
├─ grafana/
│ ├─ deployment.yaml # Grafana Deployment
│ ├─ service.yaml # Grafana Service
│ └─ pvc.yaml # Persistent Volume Claim

---

## Getting Started

### Prerequisites

- [Minikube](https://minikube.sigs.k8s.io/docs/) or any Kubernetes cluster  
- [kubectl](https://kubernetes.io/docs/tasks/tools/)  

### Deployment Steps

1. Create the monitoring namespace:
```bash
kubectl create namespace monitoring
kubectl apply -f prometheus/config-map.yaml -n monitoring
kubectl apply -f prometheus/deployment.yaml -n monitoring
kubectl apply -f prometheus/service.yaml -n monitoring

kubectl apply -f grafana/pvc.yaml -n monitoring
kubectl apply -f grafana/deployment.yaml -n monitoring
kubectl apply -f grafana/service.yaml -n monitoring

minikube service prometheus -n monitoring
minikube service grafana -n monitoring

