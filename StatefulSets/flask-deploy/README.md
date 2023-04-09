# Test connection
```
Used for nslookup
kubectl run -it --image busybox:1.28 dns-test --restart=Never --rm
nslookup flask-normal
nslookup flask-headless

Used for curl
kubectl run -it --image nginx:alpine test-pod --restart=Never --rm -- sh
curl flask-normal
curl flask-headless:5000 # rmb that you need to use the targetPort of the headless service in order to contact the pod
```