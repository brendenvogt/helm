# Wordpress Setup
## Start Minikube
```
minikube start
```
wait a few minutes (~2 minutes)
## Install Wordpress and MariaDB
```
helm install --name wordpress stable/wordpress
```
wait a few more minutes (~4 minutes)
## Monitor Install
```
helm list
minikube service list
```
mariadb must be running before wordpress succeeds so the wordpress pod may have a few restarts

e.g.
```
NAME                        READY     STATUS    RESTARTS   AGE
wordpress-9849c7766-w6z2n   0/1       Error     1          3m
wordpress-mariadb-0         0/1       Running   0          3m
...
NAME                        READY     STATUS             RESTARTS   AGE
wordpress-9849c7766-w6z2n   0/1       CrashLoopBackOff   1          3m
wordpress-mariadb-0         0/1       Running            0          3m
```
## View Service
```
minikube service wordpress
```
## Cleanup
```
helm delete wordpress
```