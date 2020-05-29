## Kubernetes Basics
Notes from [Learn Kubernetes Basics](https://kubernetes.io/docs/tutorials/kubernetes-basics/)
### Glossary
|Name | Description |
|-----|-------------|
|Minikube | A small-scale local deployment of Kubernetes that can run anywhere.
|Pod | A Pod is a Kubernetes abstraction that represents a group of one or more application containers |
|Master (K8s Cluster) | Masters manage the cluster and the nodes that are used to host the running applications |
|Node (K8s Cluster) | A node is a VM or a physical computer that serves as a worker machine in a Kubernetes cluster |
### Create Kubernetes Cluster
```console
minikube start
minikube version
kubectl version
kubectl cluster-info
kubectl get nodes
```
### Deploy an App
```console
kubectl create deployment kubernetes-bootcamp --image=gcr.io/google-samples/kubernetes-bootcamp:v1
kubectl get deployments
curl http://localhost:8001/version
kubectl get po
```
