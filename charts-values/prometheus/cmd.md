https://www.youtube.com/watch?v=QoDqxm7ybLc

We deploy prometheus via helm (operator)

helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm install prometheus prometheus-community/prometheus-operator --version 9.3.1
kubectl --namespace default get pods -l "release=prometheus"



#takes minutes to come up (on minikube took 11m)


#Get Grafana 
kubectl edit service/prometheus-grafana
type: ClusterIP -> type: NodePort # Cluster IP are all internal stuffs
minikube ip #get ip
kubectl get all #see port
visit http://172.17.95.234:31429/login

usually in production one uses ingress, alternatively we can use port-forward
kubectl port-forward deployment/prometheus-grafana 3000 -> localhost:3000
admin:prom-operator

Go to Manage -> lots of stuff is already montored thanks to node exporter

Prometheuse UI is at 9090
kubectl port-forward prometheus-prometheus-prometheus-oper-prometheus-0 9090

2nd part: https://www.youtube.com/watch?v=mLPg49b33sA
Operators: https://www.youtube.com/watch?v=ha3LjlD6g7g