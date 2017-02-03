# Prometheus for Kubernetes monitoring

This is a sample deployment of how Prometheus can be used to monitor the health of a Kubernetes cluster.

Also included is a sample configuration (``omd_kubernetes_federation.yml``) for federation of Prometheus data into a Prometheus instance inside OMD Labs Edition (https://labs.consol.de/omd/).

Furthermore three sample Grafana-dashboards (``*_Dashboard_*.json``) using the ingested data are available for import into Grafana.

## Prerequisites

You need to have Minikube from https://github.com/kubernetes/minikube installed.

## Deployment steps

```
minikube start

kubectl create -f 01_monitoring-namespace.yml
kubectl create -f 02_prometheus-configmap.yml
kubectl create -f 03_prometheus-deployment.yml
kubectl create -f 04_prometheus-service.yml
kubectl create -f 05_node-exporter.yml
kubectl create -f 06_kube-state-metrics-deployment.yml
kubectl create -f 07_kube-state-metrics-service.yml

kubectl get all -o wide --namespace monitoring

minikube dashboard

minikube service --url --namespace monitoring prometheus
```

You can use the URL and port of the Prometheus service as federation target in OMD's Prometheus. Please adjust the values accordingly.

```
cp omd_kubernetes_federation.yml /omd/site/<MYSITE>/etc/prometheus/prometheus.d/scrape_configs/static/
```
