# app-prereq-helm-charts

This is the pre-req helm chart to setup Kafka/Zookeeper on the Kubernetes cluster before application is installed/setup.

## Team Information

| Name                           | NEU ID    | Email Address                    |
| ------------------------------ | --------- | -------------------------------- |
| Viraj Rajopadhye               | 001373609 | rajopadhye.v@northeastern.edu    |
| Pranali Ninawe                 | 001377887 | ninawe.p@northeastern.edu        |
| Harsha vardhanram kalyanaraman | 001472407 | kalyanaraman.ha@northeastern.edu |

<br/>

# kafka-zookeeper

## Setup
## 1. Create a namespace
```
kubectl create ns kafka-prereq
```
## 2. Install helm chart
```
helm install kafka ./helm/pre-req-helm/charts/kafka-zookeeper/ -n kafka-prereq --set imageCredentials.Docker_username=$DOCKERUSERNAME,imageCredentials.Docker_password=$DOCKERPASSWORD
```

## Delete
### 3. namespace
```
kubectl delete ns kafka-prereq
```

# Metrics

## Setup
### 1. Create a namespace
```
kubectl create ns metrics
```

### 2. Install helm chart
```
prometheus:
helm install prom-metrics ./helm/pre-req-helm/charts/monitoring/prometheus/  -n metrics

grafana:
helm install grafana ./helm/pre-req-helm/charts/monitoring/grafana/  -n metrics
```

## Accessing prometheus and graphana
### 1. Graphana Dashboard
```
kubectl get secret --namespace metrics grafana -o jsonpath="{.data.admin-password}" | base64 --decode ; echo
export POD_NAME=$(kubectl get pods --namespace metrics -l "app.kubernetes.io/name=grafana,app.kubernetes.io/instance=grafana" -o jsonpath="{.items[0].metadata.name}")
kubectl --namespace metrics port-forward $POD_NAME 3000
```
### 1. Prometheus Dashboard
```
Get the Prometheus server URL by running these commands in the same shell:
export POD_NAME=$(kubectl get pods --namespace metrics -l "app=prometheus,component=server" -o jsonpath="{.items[0].metadata.name}")
kubectl --namespace metrics port-forward $POD_NAME 9090
```


## Delete
### 3. namespace 
```
kubectl delete ns metrics
```
