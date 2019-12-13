# GKE monitoring using prome & grafana

Monitoring GKE menggunakan prome-op helm chart masih ada bug dan harus setting firewall serta konfigurasi VPC. Setup monitoring akan lebih mudah dengan menggunakan ini. Ref : https://github.com/Thakurvaibhav/k8s

## Setup

Dalam proses setup, ada beberapa hal yang perlu diperhatikan yaitu:
   - Prometheus         : `untuk menjadi metric servernya`
   - Alertmanager       : `untuk alerting ke email/slack etc`
   - Kube-state-metric  : `untuk expose metric`
   - Grafana            : `untuk monitoring`
   - Config-map         : `untuk menej channel alerting`
   - Node Expoerter     : `It allows to measure various machine resources such as memory, disk and CPU utilization` 

untuk setupnya cukup mudah hanya dengan menggunakan command `kubect apply -f <target>`

Deployment:

1. Deploy Alertmanger: `kubectl apply -f monitoring-bs/alertmanager`

2. Deploy Prometheus: `kubectl apply -f monitoring-bs/prometheus`

3. Deploy Kube-state-metrics: `kubectl apply -f monitoring-bs/kube-state-metrics`

4. Deploy Node-Exporter: `kubectl apply -f monitoring-bs/node-exporter`

5. Deploy Grafana: `kubectl apply -f monitoring-bs/grafana`

### Note:

- URL pada datasource prome yaitu sesuai file `prometheus-service.yaml` dimana `http://prometheus-service:port`

- Untuk mengganti URL yang diinginkan (jika sudah ada) maka dapat di edit di `monitoring-ingress.yaml` pada bagian host

- Scalable harus menggunakan Thanos


# monitoring-bs
