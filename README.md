
# Monitoring & Logging
> Monitoring: Prometheus + Grafana + Slack  
> Prometheus - 기본: prometheus namespace에 설치
> Grafana - 기본: grafana namespace에 설치
> slack - 알람을 받기 위해서는 수신 웹 후크 설치 후 slack webhook url 필요  
> Grafana 기본 설정 - ID: admin / PW: admin  

> Logging: ElasticSearch + Fluentd + Kibana  
> 기본: elastic namespace에 설치
***
## 1. Monitoring

### 1.1 Prometheus 설치
    helm install prometheus ./prometheus -n prometheus -f ./prometheus/charts/alertmanager/values.yaml --set config.global.slack_api_url="<slack_webhook_url>"
### 1.2 Grafana 설치
    helm install grafana ./grafana -n grafana
### 1.3 제거
    helm uninstall grafana -n grafana
    helm uninstall prometheus -n prometheus

***
## 2. Logging

### 2.1 ElasticSearch 설치
    kubectl apply -f elasticsearch.yaml
### 2.2 Kibana 설치
    kubectl apply -f kibana.yaml
### 2.3 Fluentd 설치
    kubectl apply -f fluentd.yaml
### 2.4 제거
    kubectl delete -f fluentd.yaml
    kubectl delete -f kibana.yaml
    kubectl delete -f elasticsearch.yaml
