## Enable RBAC
`k edit po kube-apiserver-minikube -n kube-system -o yaml`
add this flag at `.spec.containers.command.kube-apiserver`
`--authorization-mode`

or edit directly at the manifest file `/etc/kubernetes/manifests/kube-apiserver.yaml`

## Check permission
```
k auth can-i list po
k auth can-i list svc
k auth can-i list svc --as kubernetes-admin
k auth can-i list svc --as kubernetes-admin --namespace dev

k config use-context kubernetes-admin@kubernetes
k auth can-i list po --as mike
k auth can-i list svc --as mike
k auth can-i list svc --as system:serviceaccount:default:default

```
## Create Role and Role-binding
```
k create role developer --verb=create --verb=get --verb=list --delete --verb=update --resource=pods 

k create rolebinding developer-binding-mike --role=developer --user=mike
```