1. ELASTICSEARCH

kubectl apply -f es-statefulset.yaml

cd /bin

./elasticsearch-setup-passwords

kubcetl apply -f elastic-credentials #Använd lösenord från es-generator


2. KIBANA
   
kubectl apply -f kibana.yml

3. Fluentd
   
kubectl apply -f fluentd-daemonset.yaml

kubectl apply -f fluentd-configmap.yaml

