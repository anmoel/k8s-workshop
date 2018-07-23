# Informations
### Playgrounds
- http://labs.play-with-k8s.com/
- https://www.katacoda.com/courses/kubernetes/playground

# Lecture
### Core-Concepts

Pets vs. Cattles: 
https://docs.google.com/presentation/d/1n3avmL5GCYCYJEr8pLFBKe0wzvoOiUV2vxyW_pYFL5s/edit#slide=id.g150f9a02df_1_153

Pods/Labels/Service/deployment:
https://docs.google.com/presentation/d/13SsyxNXnb2pB05LOdjtgBNjARD_qw9Dl0FLZeAlQbKA/edit#slide=id.g140f7f2b87_0_0

Kubernetes Master /Controlling Components:
[picture](kubernetes_architecture.png)

Rolling Update: 
https://docs.google.com/presentation/d/1n3avmL5GCYCYJEr8pLFBKe0wzvoOiUV2vxyW_pYFL5s/edit#slide=id.g150c4c944a_0_2194

# HandsOn
### Installation kubectl
https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl

### Installation Minikube
https://kubernetes.io/docs/tasks/tools/install-minikube/

### Minikube configuration

### Kubectl configuration and usage

#### commands

- `kubectl help` most important command for beginners
- `kubectl version` shows version of kubectl and server of current context
- `kubectl config ...` only configures kubectl, not the k8s server
  - `kubectl config view` 
  - `kubectl config current-context`
  - `kubectl config set PROPERTY_NAME PROPERTY_VALUE`
  - `kubectl config use-context CONTEXT_NAME`
- Imperative configuration commands
  - `kubectl run nginx --image nginx` create a deployment 
  - `kubectl expose deploy nginx --port=80 --target-port=8000 --type LoadBalancer` create a service with type LoadBalancer for deployment nginx
  - `kubectl create pod nginx --image nginx` create kubernetes object
  - `kubectl create -f nginx.yaml` create object of yanl/json-file
  - `kubectl replace -f nginx.yaml` update ...
  - `kubectl delete -f nginx.yaml` delete ...
- Declarative configuration command
  - `kubectl apply -f k8s/` create/update objects of file
- debug commands
  - `kubectl get (TYPE [NAME | -l label] | TYPE/NAME ...)`
  - `kubectl describe (-f FILENAME | TYPE [NAME_PREFIX | -l label] | TYPE/NAME)`
  - `kubectl logs [-f] [-p] POD [-c CONTAINER]`
  - `kubectl attach POD -c CONTAINER`
  - `kubectl port-forward POD [LOCAL_PORT:]REMOTE_PORT [...[LOCAL_PORT_N:]REMOTE_PORT_N]`
  - `kubectl proxy`
  - `kubectl rollout`

link: 
- https://kubernetes.io/docs/concepts/overview/object-management-kubectl/overview/
- https://kubernetes-v1-4.github.io/docs/user-guide/kubectl/kubectl/

### Start eines Deployments/Pods (Container) und seinem Service


### Ermitteln des Status eines Deployments/Pods

### Übergabe von Configs in den Container

### Rolling-Update

### Rollback

### Ressource-Limits