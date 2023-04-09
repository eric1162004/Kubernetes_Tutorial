# Created by DevOps Made Easy (www.youtube.com/c/devopsmadeeasy)
https://github.com/kunchalavikram1427/StatefulSets_demo

## Scaling
`kubectl scale deploy mysql --replicas=3`

## Testing
```
kubectl get po -l "app=db" -o wide

kubectl run mysql-client --image=mysql:5.7 -i -t --rm --restart=Never --  mysql -h 172.17.0.3 -uroot -proot todo -e "SELECT * from todo;"
# -h [host] -u [user] -p [pass] [db] -e [sql]

kubectl run mysql-client --image=mysql:5.7 -i -t --rm --restart=Never --\
  mysql -h mysql-normal -uroot -proot todo -e "SELECT * from todo;"

(-e, --execute=name -> Execute command and quit)
```

## demo-3
```
helm repo add bitnami https://charts.bitnami.com/bitnami
helm repo update
helm pull bitnami/mysql --untar
```