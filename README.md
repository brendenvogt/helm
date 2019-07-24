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
output
```
😄  minikube v1.2.0 on darwin (amd64)
💡  Tip: Use 'minikube start -p <name>' to create a new cluster, or 'minikube delete' to delete this one.
🔄  Restarting existing virtualbox VM for "minikube" ...
⌛  Waiting for SSH access ...
🐳  Configuring environment for Kubernetes v1.15.0 on Docker 18.09.6
🔄  Relaunching Kubernetes v1.15.0 using kubeadm ... 
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
helm init
```

# Go From Here
https://docs.bitnami.com/kubernetes/how-to/create-your-first-helm-chart/