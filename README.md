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

kubectl create secret generic kibana-auth \
  --from-literal=username=kibana_system \
  --from-literal=password=your-kibana-password \   
  -n logging
#Use password from ./elasticsearch-setups-password auto

kubectl apply -f kibana-deployment.yml

3. FLUENTD
   
kubectl apply -f fluentd-daemonset.yaml

kubectl apply -f fluentd-configmap.yaml


Set up Microk8s
=============================
snap install microk8s --classic --channel=1.33/stable

microk8s enable dns

microk8s enable hostpath-storage

microk8s enable cert-manager

microk8s enable ingress dns

microk8s enable dashboard

sudo vi ~/.bashrc

ADD

alias kubectl='microk8s kubectl'

RUN

source ~/.bashrc


 

