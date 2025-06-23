1. ELASTICSEARCH

kubectl apply -f es-statefulset.yaml

cd /bin

./elasticsearch-service-tokens create kibana kibana-token.

[Använd denna token i kibana-secret-token]


Version från 9.0.0 och uppåt KRÄVS token! Det går ej använda sig av elastic som user och sätta lösenord

2. KIBANA
   
kubectl apply -f kibana.yml

kubectl apply -f kibana-secret-token.yaml

3. Fluentd
   
kubectl apply -f fluentd-daemonset.yaml

kubectl apply -f fluentd-configmap.yaml

