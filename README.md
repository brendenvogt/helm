# Helm Tutorial


# Homebrew
## Install 
```
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

# Minikube
## Install
[kube tutorial](https://kubernetes.io/docs/tasks/tools/install-minikube/)

[vbox](https://www.virtualbox.org/wiki/Downloads)
```
brew cask install minikube
```

## Up
```
minikube start
```
output or similar
```
😄  minikube v1.2.0 on darwin (amd64)
🔥  Creating virtualbox VM (CPUs=2, Memory=2048MB, Disk=20000MB) ...
🐳  Configuring environment for Kubernetes v1.15.0 on Docker 18.09.6
🚜  Pulling images ...
🚀  Launching Kubernetes ... 
⌛  Verifying: apiserver proxy etcd scheduler controller dns
🏄  Done! kubectl is now configured to use "minikube"
```
## Down
```
minikube stop
```
output 
```
✋  Stopping "minikube" in virtualbox ...
🛑  "minikube" stopped.
```

## Delete
```
minikube delete
```
output
```
🔥  Deleting "minikube" from virtualbox ...
💔  The "minikube" cluster has been deleted.
```

# Helm
## Install 
Assuming "minikube start" and "kubectl get pods" produces no error response.
```
brew install kubernetes-helm
```

# Helm Init
```
helm init
```
output
```
$HELM_HOME has been configured at /Users/brendenvogt/.helm.

Tiller (the Helm server-side component) has been installed into your Kubernetes Cluster.

Please note: by default, Tiller is deployed with an insecure 'allow unauthenticated users' policy.
To prevent this, run `helm init` with the --tiller-tls-verify flag.
For more information on securing your installation see: https://docs.helm.sh/using_helm/#securing-your-helm-installation
```

# Install Chart on Cluster
```
helm install dotnet/charts/api --name test
```
output
```
NAME:   test
LAST DEPLOYED: Wed Jul 24 00:35:59 2019
NAMESPACE: default
STATUS: DEPLOYED

RESOURCES:
==> v1/Deployment
NAME      READY  UP-TO-DATE  AVAILABLE  AGE
test-api  0/4    4           0          0s

==> v1/Pod(related)
NAME                       READY  STATUS             RESTARTS  AGE
test-api-7bb948b9b4-fwbj6  0/1    ContainerCreating  0         0s
test-api-7bb948b9b4-pzjqp  0/1    ContainerCreating  0         0s
test-api-7bb948b9b4-q8psp  0/1    ContainerCreating  0         0s
test-api-7bb948b9b4-v7jjm  0/1    Pending            0         0s

==> v1/Service
NAME      TYPE          CLUSTER-IP     EXTERNAL-IP  PORT(S)       AGE
test-api  LoadBalancer  10.111.219.84  <pending>    80:31274/TCP  0s


NOTES:
1. Get the application URL by running these commands:
     NOTE: It may take a few minutes for the LoadBalancer IP to be available.
           You can watch the status of by running 'kubectl get --namespace default svc -w test-api'
  export SERVICE_IP=$(kubectl get svc --namespace default test-api -o jsonpath='{.status.loadBalancer.ingress[0].ip}')
  echo http://$SERVICE_IP:80

```
# List Minikube Services
```
minikube service list
```
output
```
|-------------|---------------|-----------------------------|
|  NAMESPACE  |     NAME      |             URL             |
|-------------|---------------|-----------------------------|
| default     | kubernetes    | No node port                |
| default     | test-api      | http://192.168.99.104:31274 |
| kube-system | kube-dns      | No node port                |
| kube-system | tiller-deploy | No node port                |
|-------------|---------------|-----------------------------|
```

# View Kubernetes Resources
```
kubectl get pods
kubectl get services
kubectl get deployments
```
output
```
NAME                        READY     STATUS    RESTARTS   AGE
test-api-7bb948b9b4-fwbj6   1/1       Running   0          1m
test-api-7bb948b9b4-pzjqp   1/1       Running   0          1m
test-api-7bb948b9b4-q8psp   1/1       Running   0          1m
test-api-7bb948b9b4-v7jjm   1/1       Running   0          1m

NAME         TYPE           CLUSTER-IP      EXTERNAL-IP   PORT(S)        AGE
kubernetes   ClusterIP      10.96.0.1       <none>        443/TCP        6m
test-api     LoadBalancer   10.111.219.84   <pending>     80:31274/TCP   1m

NAME       DESIRED   CURRENT   UP-TO-DATE   AVAILABLE   AGE
test-api   4         4         4            4           1m
```

# Output
```
minikube service test-api
```
should navigate to a localhost:PORT
```
Welcome to nginx! 
```

# Full Test
```
# start minikube (may take a while)
minikube start
# install helm on kube cluster
helm init
# install chart on cluster named "test"
helm install dotnet/charts/api --name test
# observice services
minikube service list
# observe test pods services and deployments created
kubectl get pods
kubectl get services
kubectl get deployments
# view output
minikube service test-api
```
cleanup
```
helm delete test
minikube stop
minikube delete
```

# Go From Here
https://docs.bitnami.com/kubernetes/how-to/create-your-first-helm-chart/