Dont use this setup in prod. This is only for testing
====================

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

{
sudo vi ~/.bashrc

ADD

alias kubectl='microk8s kubectl'

RUN

source ~/.bashrc
}


EFK-STACK
====================

1. ELASTICSEARCH

kubectl apply -f elastic-credentials

kubectl apply -f es-statefulset.yaml

Go into elasticpod

cd /bin

./elasticsearch-setup-passwords

(Save passwords)

kubcetl apply -f elastic-credentials #Använd lösenord från es-generator


2. KIBANA

ADD password in kibana-secret from password: kibana_system

kubectl apply -f kibana-secret.yaml

kubectl apply -f kibana-deployment.yaml

kubectl port-forward svc/kibana 5601:5601 -n logging

3. FLUENTD
   
kubectl apply -f fluentd-daemonset.yaml

kubectl apply -f fluentd-configmap.yaml





 

