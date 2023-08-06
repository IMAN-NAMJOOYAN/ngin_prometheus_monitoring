# nginx_prometheus_monitoring
**Nginx Prometheus Monitoring**

*Requirements*

| Tools name|Version|
|------------|-------|
|Helm|v3.12.x|
|Kubernetes|v1.25.x or above|
|prometheus stack monitoring (Helm)|https://artifacthub.io/packages/helm/prometheus-community/kube-prometheus-stack version 46.8.0|
|Nginx (Helm)|https://artifacthub.io/packages/helm/bitnami/nginx|

**Steps:**
```
1- install https://artifacthub.io/packages/helm/bitnami/nginx
   -  helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
   -  helm install my-kube-prometheus-stack prometheus-community/kube-prometheus-stack --version 48.3.1

2- Before installing Nginx (Helm), edit the default values to enable nginx metrics.
```

![image](https://github.com/IMAN-NAMJOOYAN/nginx_prometheus_monitoring/assets/16554389/fc34e544-c685-46a7-b4cc-c55bf219b48a)

*NOTE:* nginx metrics are exposed by the nginx exporter on port 9113 when metrics are enabled. You can view the metrics and values in the curl command or in a web browser.

![image](https://github.com/IMAN-NAMJOOYAN/nginx_prometheus_monitoring/assets/16554389/a805d8b7-9b84-46d7-a4a2-d10585968551)

```
3- create nginx ServiceMonitor for monitoring nginx.

```
```
apiVersion: monitoring.coreos.com/v1
kind: ServiceMonitor
metadata:
  annotations:
    meta.helm.sh/release-name: prometheus-stack
    meta.helm.sh/release-name: mynginx
    meta.helm.sh/release-namespace: default
  generation: 1
  labels:
    app.kubernetes.io/instance: mynginx
    app.kubernetes.io/managed-by: Helm
    app.kubernetes.io/name: nginx
    helm.sh/chart: nginx-15.1.2
    heritage: Helm
    release: prometheus-stack
  name: mynginx
  namespace: monitoring
spec:
  endpoints:
  - interval: 5s
    path: /metrics
    port: metrics
  jobLabel: nginx-items
  namespaceSelector:
    matchNames:
    - default
  selector:
    matchLabels:
      app.kubernetes.io/instance: mynginx
      app.kubernetes.io/name: nginx
```
*Note:* We run the nginx deployment in the "default" namespace. You can deploy nginx to a custom namespace.
```
4- apply ServiceMonitor.

kubectl apply -f nginx-sm.yaml
```
```
5- check prometheus targets.
```
![image](https://github.com/IMAN-NAMJOOYAN/nginx_prometheus_monitoring/assets/16554389/27a25107-6f78-4e99-8fc3-334a11ce9daa)

```
6- create nginx dashboard on grafana.
```
![image](https://github.com/IMAN-NAMJOOYAN/nginx_prometheus_monitoring/assets/16554389/e894dbd4-2d47-4c87-969e-4c560f0bc339)






