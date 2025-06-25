[info] Examensarbete
====================

---------------------------------------------------------------------------------------

### Good to know!

Elasticsearch cant use replicas on single-node cluster ( Default is 1 )

---------------------------------------------------------------------------------------

Set up Microk8s
=============================
snap install microk8s --classic --channel=1.33/stable

microk8s enable dns

microk8s enable hostpath-storage

microk8s enable cert-manager

microk8s enable ingress dns

microk8s enable dashboard

kubectl -n kubernetes-dashboard port-forward svc/kubernetes-dashboard-kong-proxy 8443:443

microk8s kubectl create token default

----------------------------------------------------------------------------------------
### Without this you need to run use microk8s before kubectl - Just anoying!!

{

RUN in console

sudo vi ~/.bashrc

ADD

alias kubectl='microk8s kubectl' 

RUN in console

source ~/.bashrc

}

----------------------------------------------------------------------------------------

EFK-STACK
====================

----------------------------------------------------------------------------------------
### ELASTICSEARCH

----------------------------------------------------------------------------------------

kubectl apply -f elasticsearch-secret.yaml

kubectl apply -f es-statefulset.yaml

Go into elasticpod to setup the password.

cd /bin

./elasticsearch-setup-passwords auto

{

Password will be printed. Save them and use it for:

- elastic-auth-secret
- kibana-secret

}

Change password in elasticsearch-secret.yaml # Apply again!

kubectl port-forward service/SERVICENAME 9200:9200 -n NAMESPACE

----------------------------------------------------------------------------------------
### KIBANA

----------------------------------------------------------------------------------------
[info] ADD password in kibana-secret from password: kibana_system
----------------------------------------------------------------------------------------

kubectl apply -f kibana-deployment.yaml

kubectl port-forward svc/SERVICENAME 5601:5601 -n NAMESPACE

----------------------------------------------------------------------------------------

### FLUENTD

----------------------------------------------------------------------------------------
Make sure to CREATE secret
----------------------------------------------------------------------------------------

kubectl create secret generic fluentd-es-auth \
  --from-literal=ES_PASSWORD='your-es-password' \
  -n logging


kubectl apply -f fluentd-configmap.yaml

kubectl apply -f fluentd-daemonset.yaml

----------------------------------------------------------------------------------------
### Port forwarding if not using NodePort:

- 5601   Kibana 
- 9200   Elasticsearch 
- 8443   Kubernetes dashboard

----------------------------------------------------------------------------------------

### Set up index in kibana 
---------------------------------------------------------------------------------------

1. In the left corner, push the hamburgermenu and scroll down to Stack Management
2. Choose Index Management
3. Create Index name
4. Go to Data Views
5. Set Name
6. Set Index pattern
7. Save data vied to Kibana
8. Analytics -> Discover


### Useful commands

list indices:

curl -u elastic:yourpassword http://iuselocalhostfortest:9200/_cat/indices?v

---------------------------------------------------------------------------------------

### Useful test-application to generate logs in kubernetes-cluster

https://github.com/henrikdevops/test-applications/tree/main

---------------------------------------------------------------------------------------




 

