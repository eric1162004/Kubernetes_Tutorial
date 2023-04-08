Skooner github page
https://github.com/skooner-k8s/skooner

This assume you already have a ingress controller. 

Map the ingress controller to local host file
C:\Windows\System32\drivers\etc\hosts

Run:
kubectl apply -f skooner_dashboard.yaml

kubectl apply -f skooner_ingress.yaml

kubectl create token skooner-sa

minikube addons enable metrics-server