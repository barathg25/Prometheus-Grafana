# prothues-grafana

# promthus-grafana-monitoring     11802,1860,17375----> grafana no

helm repo add prometheus-community https://prometheus-community.github.io/helm-charts


helm repo add grafana https://grafana.github.io/helm-charts

helm repo update

Create monitoring namespace

kubectl create namespace monitoring

Create storageclass

kubectl apply -f storage.yaml

Create pv for promethus

kubectl apply -f pv.yaml

helm install prometheus prometheus-community/prometheus \
--namespace monitoring \
--set alertmanager.persistentVolume.storageClass="local-storage" \
--set server.persistentVolume.storageClass="local-storage"

helm install grafana grafana/grafana \
    --namespace monitoring \
    --set persistence.storageClassName="local-storage" \
    --set persistence.enabled=true \
    --set adminPassword='ConVer' \
    --values /root/environment/grafana/grafana.yaml \
    --set service.type=NodePort

ref: https://gist.github.com/ArunMagi/0249c48695c7cb86d9659ec3b46de4a6



    ************************* pods and node cpu utlization *******************
    
    kubectl apply -f https://github.com/kubernetes-sigs/metrics-server/releases/latest/download/components.yaml
    
    wget https://raw.githubusercontent.com/pythianarora/total-practice/master/sample-kubernetes-code/metrics-server.yaml
     
     
     kubectl create -f metrics-server.yaml






