# Beginner

## Playgrounds

- http://labs.play-with-k8s.com/
- https://www.katacoda.com/courses/kubernetes/playground

## Lecture

### Core-Concepts

Comic:
https://cloud.google.com/kubernetes-engine/kubernetes-comic/

Pets vs. Cattles:
https://docs.google.com/presentation/d/1n3avmL5GCYCYJEr8pLFBKe0wzvoOiUV2vxyW_pYFL5s/edit#slide=id.g150f9a02df_1_153

Pods/Labels/Service/Deployment:
https://docs.google.com/presentation/d/13SsyxNXnb2pB05LOdjtgBNjARD_qw9Dl0FLZeAlQbKA/edit#slide=id.g140f7f2b87_0_0
[picture_of_pod](pod.png)

Kubernetes Master /Controlling Components:
[picture_k8s_architecture](kubernetes_architecture.png)

Rolling Update:
https://docs.google.com/presentation/d/1n3avmL5GCYCYJEr8pLFBKe0wzvoOiUV2vxyW_pYFL5s/edit#slide=id.g150c4c944a_0_2194

[Kubernetes DeveloperTeams (SIG)](https://github.com/kubernetes/community/blob/master/sig-list.md)

## HandsOn

### Installation kubectl

https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl

### Installation Minikube

https://kubernetes.io/docs/tasks/tools/install-minikube/

### Minikube configuration

#### minikube commands

- minikube (start | stop | status )
- minikube config
  - minikube config view
  - minikube config set cpus 2
  - minikube config set vm-driver kvm # default virtualbox
  - minikube config get memory
  - minikube config set memory 4096
- minikube addons
  - minikube addons list
  - minikube addons enable NAME
  - minikube addons disable NAME
- minikube dashboard

### Kubectl configuration and usage

#### kubectl commands

- `kubectl help` most important command for beginners
- `kubectl version` shows version of kubectl and server of current context
- `kubectl config ...` only configures kubectl, not the k8s server
  - `kubectl config view`
  - `kubectl config current-context`
  - `kubectl config set PROPERTY_NAME PROPERTY_VALUE`
  - `kubectl config use-context CONTEXT_NAME`
  - `kubectl config get-contexts`
  - `kubectl config set-context demo --user minikube --cluster minikube --namespace demo`
  - `kubectl config use-context demo`
- Imperative configuration commands
  - `kubectl run nginx --image nginx` create a deployment
  - `kubectl expose deploy nginx --port=80 --target-port=80 --type NodePort` create a service with type NodePort for deployment nginx
  - `kubectl create pod nginx --image nginx` create kubernetes object
  - `kubectl create -f nginx.yaml` create object of yanl/json-file
  - `kubectl replace -f nginx.yaml` update ...
  - `kubectl delete -f nginx.yaml` delete ...
- Declarative configuration command
  - `kubectl apply -f k8s/` create/update objects of file

link:

- https://kubernetes.io/docs/concepts/overview/object-management-kubectl/overview/
- https://kubernetes-v1-4.github.io/docs/user-guide/kubectl/kubectl/

### Start eines Deployments/Pods (Container) und seinem Service

Files:

- [pod.yaml](k8s/pod.yaml)
- [namespace.yaml](k8s/namespace.yaml)
- [deployment.yaml](k8s/deployment.yaml)
- [service.yaml](k8s/service.yaml)

### Ermitteln des Status eines Deployments/Pods

- `kubectl get (TYPE [NAME | -l label] | TYPE/NAME ...)`
- `kubectl describe (-f FILENAME | TYPE [NAME_PREFIX | -l label] | TYPE/NAME)`
- `kubectl logs [-f] [-p] POD [-c CONTAINER]`
- `kubectl attach POD -c CONTAINER`
- `kubectl port-forward POD [LOCAL_PORT:]REMOTE_PORT [...[LOCAL_PORT_N:]REMOTE_PORT_N]`
- `kubectl proxy`

### Rolling-Update

- `kubectl edit (RESOURCE/NAME | -f FILENAME)`
- `kubectl apply -f FILENAME`
- `kubectl rollout history TYPE NAME`
- `kubectl rollout status TYPE NAME`
- `kubectl rollout pause TYPE NAME`
- `kubectl rollout resume TYPE NAME`

### Rollback

- `kubectl rollout undo TYPE NAME`
- `kubectl rollout undo TYPE NAME --revision=NUMBER`

### Übergabe von Configs in den Container

- `kubectl create configmap MAP_NAME DATASOURCE`
- DATASOURCES :
  - --from-literal
  - --from-file
- `kubectl -n demo create configmap nginx-config --from-file=nginx.conf --from-literal http_port=9090`
- `kubectl -n demo get cm nginx-config -o yaml`
- `kubectl -n demo apply -f k8s/configmap.yaml`

### Health Checks

- 2 catagories:
  - liveness: importend for container/pod lifecycle
  - readyness: importend for inclusion in distribution
- 3 types:
  - tcp
  - http
  - exec
- files:
  - [exec](k8s/exec-probe.yaml)
  - [http_tcp](k8s/deployment_with_probes.yaml)

### Ressource-Limits

- [deployment.yaml](k8s/deployment_with_quotas.yaml)
