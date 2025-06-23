1. ELASTICSEARCH

kubectl apply -f elastic-credentials

kubectl apply -f es-statefulset.yaml

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

3. Fluentd
   
kubectl apply -f fluentd-daemonset.yaml

kubectl apply -f fluentd-configmap.yaml

