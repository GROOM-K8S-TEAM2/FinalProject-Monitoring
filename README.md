
# Monitoring & Logging
> Monitorig: Prometheus + Grafana + Slack  
> Prometheus, Grafana - 기본: monitoring namespace에 설치 (namespace변경을 원하는 경우 -n 옵션을 변경하면 됩니다.)  
> slack - 알람을 받기 위해서는 수신 웹 후크 설치 후 slack webhook url 필요  
> Grafana 기본 설정 - ID: admin / PW: admin  

> Logging: ElasticSearch + Fluentd + Kibana  
> 기본: logging namespace에 설치 (namespace변경을 원하는 경우 -n 옵션을 변경하면 됩니다.)  
***
## 1. Monitoring

### 1.1 Prometheus 설치
    helm install prometheus ./prometheus -n monitoring -f ./prometheus/charts/alertmanager/values.yaml --set config.global.slack_api_url="<slack_webhook_url>"
### 1.2 Grafana 설치
    helm install grafana ./grafana -n monitoring
### 1.3 제거
    helm uninstall grafana
    helm uninstall prometheus

***
## 2. Logging

### 2.1 ElasticSearch 설치
    kubectl apply -f elasticsearch.yaml -n logging
### 2.2 Kibana 설치
    kubectl apply -f kibana.yaml -n logging
### 2.3 Fluentd 설치
    kubectl apply -f fluentd.yaml -n logging
### 2.4 제거
    kubectl delete -f fluentd.yaml -n logging
    kubectl delete -f kibana.yaml -n logging
    kubectl delete -f elasticsearch.yaml -n logging
