# tmobile
tmobile project

Build a K8s cluster consists of 1Control plane + 1 Worker
--------------------------------------
minikube start --nodes 2 -p tmobile 

Deploy Gitea instance. (2replicas)
----------------------------------
helm repo add gitea-charts https://dl.gitea.com/charts/
helm show values gitea-charts/gitea > gitea-new.yaml # edit values 

> replicaCount: 2

Gitea UI should only be accessible via HTTPS.
--------------------------------------------

u:p gitea:gitea

Gitea Data should be Persisting.
----------------------------------
"persistence" in gitea_values.yaml

>> CHECK > kubectl get svc -n gitea
>> CHeck > kubectl get pods  -n gitea

Basic Monitoring Stack (Prometheus + Grafana)
--------------------------------
"metrics" in gitea_values.yaml
helm repo add grafana https://grafana.github.io/helm-charts

helm show values grafana/grafana > grafana.yaml

helm install grafana grafana/grafana --values grafana-new.yaml -n grafana --create-namespace

helm repo add prometheus-community https://prometheus-community.github.io/helm-charts





Use Ingress to access the UI via HTTPS


Deploy a Database for Gitea (PostgreSQL).
-------------------------------------------
"postgresql" in gitea_values.yaml


helm install gitea gitea-charts/gitea --values gitea_values.yaml -n gitea --create-namespace


helm delete grafana

kubectl apply -f gitea_values.yaml



helm repo add gitea-charts https://dl.gitea.com/charts/
helm show values gitea-charts/gitea > gitea_values.yaml


✓Basic Logging with ELK stack.
✓Gitea Upgrades should be automated via a simple CI/CD
pipe (GitOps style).
✓Deploy a LoadBalancer for the whole cluster.
 > in progress Use Helm for the whole deployment.
✓Use any platform/cloud.





1. helm create tmobile
2. helm template ***
3. helm lint ***


helm repo add gitea-charts https://dl.gitea.com/charts/
helm install gitea gitea-charts/gitea

4.kubects get all

HELP:
https://docs.gitea.com/installation/install-on-kubernetes
https://gitea.com/gitea/helm-chart/


kubectl get all
kubectl delete -f <file>
kubectl delete service <name>
kubectl service pod <name>

helm list -a 
____________________
kubectl cluster-info

helm list --all --all-namespaces 


Start a cluster with 2 nodes in the driver of your choice (control plan, worker):
minikube start --nodes 2 -p tmobile 

Get the list of your nodes:
kubectl get nodes

You can also check the status of your nodes:
minikube status -p tmobile

Deploy our <name> deployment:
kubectl apply -f <name>.yaml

Look at our service, to know what URL to hit
minikube service list -p tmobile

Enable the minikube ingress addon with the following command:
minikube addons enable ingress

check storage class 
kubectl get sc
