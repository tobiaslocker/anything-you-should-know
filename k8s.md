## Kubernetes Basics
Notes from [Learn Kubernetes Basics](https://kubernetes.io/docs/tutorials/kubernetes-basics/)
### Glossary
|Name | Description |
|-----|-------------|
|Minikube | A small-scale local deployment of Kubernetes that can run anywhere.
|Pod | A Pod is a Kubernetes abstraction that represents a group of one or more application containers |
|Master (K8s Cluster) | Masters manage the cluster and the nodes that are used to host the running applications |
|Node (K8s Cluster) | A node is a worker machine in Kubernetes and may be a VM or physical machine, depending on the cluster. Multiple Pods can run on one Node |
|Deployment |A Deployment is responsible for creating and updating instances of your application |
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
# open a second terminal window to run the proxy
kubectl proxy
# query the version directly through the API
curl http://localhost:8001/version
# to get the pod name...
kubectl get po
```
### Troubleshooting with kubectl
- `kubectl get` - list resources
- `kubectl describe` - show detailed information about a resource
- `kubectl logs` - print the logs from a container in a pod
- `kubectl exec` - execute a command on a container in a pod
### Explore Your App
```console
# view containers inside pod
kubectl describe pods
# start proxy as above...
# see output of application
curl http://localhost:8001/api/v1/namespaces/default/pods/$POD_NAME/proxy/
# retrieve logs
kubectl get logs $POD_NAME
# list environment variables
kubectl exec $POD_NAME env
# start bash session...
kubectl exec -ti $POD_NAME bash
```
