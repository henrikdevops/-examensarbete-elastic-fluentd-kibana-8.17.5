1. ELASTICSEARCH

kubectl apply -f es-statefulset.yaml

cd /bin

./elasticsearch-setup-passwords

kubcetl apply -f elastic-credentials #Använd lösenord från es-generator

Version från 9.0.0 och uppåt KRÄVS token! Det går ej använda sig av elastic som user och sätta lösenord

2. KIBANA
   
kubectl apply -f kibana.yml

3. Fluentd
   
kubectl apply -f fluentd-daemonset.yaml

kubectl apply -f fluentd-configmap.yaml

