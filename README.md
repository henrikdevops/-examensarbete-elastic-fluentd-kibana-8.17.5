[info] Examensarbete
====================

---------------------------------------------------------------------------------------

### Good to know!

Elasticsearch cant use replicas on single-node cluster

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
### Wihtout this you need to run use microk8s before kubectl - Just anoying!!

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

### ELASTICSEARCH

{

You will need elastic-auth-secret later on for fluentd

Add your elastic-password in this file before applying

}

kubectl apply -f es-statefulset.yaml

Go into elasticpod to setup the password.

cd /bin

./elasticsearch-setup-passwords auto

{

Password will be printed. Save them and use it for:

- elastic-credentials
- elastic-auth-secret
- kibana-secret

}

kubcetl apply -f elastic-credentials #Använd lösenord från es-generator

kubectl port-forward service/SERVICENAME 9200:9200 -n NAMESPACE



----------------------------------------------------------------------------------------
### KIBANA

----------------------------------------------------------------------------------------
ADD password in kibana-secret from password: kibana_system
----------------------------------------------------------------------------------------

kubectl apply -f kibana-deployment.yaml

kubectl port-forward svc/SERVICENAME 5601:5601 -n NAMESPACE

----------------------------------------------------------------------------------------

### FLUENTD

----------------------------------------------------------------------------------------
Make sure to set elastic-password before apply
----------------------------------------------------------------------------------------

kubectl apply -f fluentd-configmap.yaml

kubectl apply -f fluentd-daemonset.yaml

----------------------------------------------------------------------------------------
### Port forwarding if not using NodePort:

- 5601   Kibana 
- 9200   Elasticsearch 
- 8443   Kubernetes dashboard

----------------------------------------------------------------------------------------
---------------------------------------------------------------------------------------

### Useful commands

list indices:

curl -u elastic:yourpassword http://iuselocalhostfortest:9200/_cat/indices?v

---------------------------------------------------------------------------------------

### Useful test-application to generate logs in kubernetes-cluster

https://github.com/henrikdevops/test-applications/tree/main

---------------------------------------------------------------------------------------




 

