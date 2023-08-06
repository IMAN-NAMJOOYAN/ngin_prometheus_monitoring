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

2- before install Nginx (Helm), edit default values for enabling nginx metrics.
```

![image](https://github.com/IMAN-NAMJOOYAN/nginx_prometheus_monitoring/assets/16554389/fc34e544-c685-46a7-b4cc-c55bf219b48a)

*Note:* When enabling metrics, nginx metrics exposed by nginx exporter on port 9113. you can view metrics ans values on curl command or web browser.

![image](https://github.com/IMAN-NAMJOOYAN/nginx_prometheus_monitoring/assets/16554389/a805d8b7-9b84-46d7-a4a2-d10585968551)

```
3- create nginx service monitor.
```






