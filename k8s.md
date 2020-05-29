## Kubernetes Basics
Notes from [Learn Kubernetes Basics](https://kubernetes.io/docs/tutorials/kubernetes-basics/)
### Glossary
|Term | Description |
|-----|-------------|
|Minikube | A small-scale local deployment of Kubernetes that can run anywhere.
|Pod | A Pod is a Kubernetes abstraction that represents a group of one or more application containers |
|Master (K8s Cluster) | Masters manage the cluster and the nodes that are used to host the running applications |
|Node (K8s Cluster) | A node is a worker machine in Kubernetes and may be a VM or physical machine, depending on the cluster. Multiple Pods can run on one Node |
|Deployment |A Deployment is responsible for creating and updating instances of your application |
|Service |A Kubernetes Service is an abstraction layer which defines a logical set of Pods and enables external traffic exposure, load balancing and service discovery for those Pods |
|Scaling | Scaling is accomplished by changing the number of replicas in a Deployment |
|Rolling Updates | Rolling updates allow Deployments' update to take place with zero downtime by incrementally updating Pods instances with new ones |
### Create Kubernetes Cluster
```bash
minikube start
minikube version
kubectl version
kubectl cluster-info
kubectl get nodes
```
### Deploy an App
```bash
kubectl create deployment kubernetes-bootcamp --image=gcr.io/google-samples/kubernetes-bootcamp:v1
kubectl get deployments
# open a second terminal window to run the proxy
kubectl proxy
# query the version directly through the API
curl http://localhost:8001/version
# to get the pod name...
kubectl get po
```
##### Troubleshooting with kubectl
- `kubectl get` - list resources
- `kubectl describe` - show detailed information about a resource
- `kubectl logs` - print the logs from a container in a pod
- `kubectl exec` - execute a command on a container in a pod
### Explore Your App
```bash
# view containers inside pod
kubectl describe pods
# see output of application
curl http://localhost:8001/api/v1/namespaces/default/pods/$POD_NAME/proxy/
# retrieve logs
kubectl get logs $POD_NAME
# list environment variables
kubectl exec $POD_NAME env
# start bash session...
kubectl exec -ti $POD_NAME bash
```
### Using a Service to Expose Your App
```bash
# list services
kubectl get services
# expose to external traffic
kubectl expose deployment/kubernetes-bootcamp --type="NodePort" --port 8080
# view open port
kubectl describe services/kubernetes-bootcamp # NODE_PORT=32385
# test that the app is exposed outside of the cluster
curl $(minikube ip):$NODE_PORT
# see the name of the label
kubectl describe deployment
# use this label to query our list of Pods
kubectl get pods -l run=kubernetes-bootcamp
# the same to list the existing services
kubectl get services -l run=kubernetes-bootcamp
# apply a new label
kubectl label pod $POD_NAME app=v1
# query the list of pods using the new label
kubectl get pods -l app=v1
# delete service
kubectl delete service -l run=kubernetes-bootcamp
```
### Scaling a Deployment
```bash
# see the ReplicaSet created by the Deployment
kubectl get rs
# scale the Deployment to 4 replicas
kubectl scale deployments/kubernetes-bootcamp --replicas=4
# check if the number of Pods changed
kubectl get pods -o wide
# Nr of pods, exposed IP and Port can be checked with describe command...
# if every request hits a different Pod, LoadBalancing works...
curl $(minikube ip):$NODE_PORT
# scale down
kubectl scale deployments/kubernetes-bootcamp --replicas=2
```
### Updating Your App
```bash
# view current image version (Image field)
kubectl describe pods | grep Image:
# update image
kubectl set image deployments/kubernetes-bootcamp kubernetes-bootcamp=jocatalin/kubernetes-bootcamp:v2
# check status of new Pods, and view old one terminating
kubectl get pods
# get exposed IP and Port with describe service... (see above)
curl $(minikube ip):$NODE_PORT # v=1 is now v=2
# confirm update
kubectl rollout status deployments/kubernetes-bootcamp
# revert the deployment to previous known state
kubectl rollout undo deployments/kubernetes-bootcamp
```
