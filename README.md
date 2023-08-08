# tmobile
tmobile project

Build a K8s cluster consists of 1Control plane + 1 Worker
--------------------------------------
minikube start --nodes 2 -p tmobile 
>>check >  minikube status -p tmobile 

Deploy Gitea instance. (2replicas)
----------------------------------
helm repo add gitea https://dl.gitea.io/charts
helm repo add gitea-charts https://dl.gitea.com/charts/
helm show values gitea-charts/gitea > gitea-new.yaml # edit values 
helm install my-gitea gitea/gitea --version 9.1.0 

> replicaCount: 2

Gitea UI should only be accessible via HTTPS.
--------------------------------------------
helm repo add nginx-stable https://helm.nginx.com/stable
helm repo update
helm install nginx-ingress nginx-stable/nginx-ingress --set rbac.create=true
kubectl get pods --all-namespaces -l app=nginx-ingress-nginx-ingress
kubectl get services nginx-ingress-nginx-ingress
minikube start --addons=ingress

kubectl get pods -o wide
u:p gitea:gitea

Gitea Data should be Persisting.
----------------------------------
"persistence" in gitea_values.yaml

>> CHECK > kubectl get svc -n gitea
>> CHeck > kubectl get pods  -n gitea

Basic Monitoring Stack (Prometheus + Grafana)
--------------------------------
"metrics" in gitea_values.yaml
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm install my-prometheus prometheus-community/prometheus --version 23.3.0
helm repo add grafana https://grafana.github.io/helm-charts
helm install my-grafana grafana/grafana --version 6.58.7


Use Ingress to access the UI via HTTPS
----------------------------------------
??????????????????????

Deploy a Database for Gitea (PostgreSQL).
-------------------------------------------
"postgresql" in gitea_values.yaml

Basic Logging with ELK stack.
-------------------------------
helm repo add elastic https://helm.elastic.co
helm install my-elasticsearch elastic/elasticsearch --version 8.5.1


✓Gitea Upgrades should be automated via a simple CI/CD
pipe (GitOps style).

✓Deploy a LoadBalancer for the whole cluster.

 > in progress Use Helm for the whole deployment.

✓Use any platform/cloud.





1. helm create tmobile
2. helm template ***
3. helm lint ***


HELP:
----------------
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


Get the list of your nodes:
---------------------------
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


HELM
---------------
https://helm.sh/docs/intro/cheatsheet/
helm repo
helm status
helm list
helm install/uninstall

https://artifacthub.io/ >> good source

https://www.linuxbuzz.com/how-to-install-minikube-on-fedora/


export POD_NAME=$(kubectl get pods --namespace default -l "app.kubernetes.io/name=alertmanager,app.kubernetes.io/instance=my-prometheus" -o jsonpath="{.items[0].metadata.name}")
  kubectl --namespace default port-forward $POD_NAME 9093
