# Advanced

## HandsOn

### Install with kubeadm

- kubeadm init
- kubeadm join ....

### Secrets

- secrets in yaml files are base64 encoded
- don't save secrets in repos
- `kubectl create secret SECRETTYPE SECRETNAME DATASOURCES`
- SECRETTYPE :
  - `kubectl create secret docker-registry NAME --docker-username=user --docker-password=password --docker-email=email [--docker-server=string] [--from-literal=key1=value1] [--dry-run] [options]`
  - `kubectl create secret generic NAME [--type=string] [--from-file=[key=]source] [--from-literal=key1=value1] [--dry-run] [options]`
  - `kubectl create secret tls NAME --cert=path/to/cert/file --key=path/to/key/file [--dry-run] [options]`
- `echo -n '1f2d1e2e67df' | base64`
- special secrets:
  - ServiceAccountToken

example with ingress in minikube:

- `minikube addons enable ingress`
- `openssl req -nodes -x509 -newkey rsa:4096 -keyout key.pem -out cert.pem -days 365`
- `kubectl create secret tls ingress-tls --cert=cert.pem --key=key.pem -o yaml`
- [ingress_tls](k8s/ingress_tls.yaml)
- [deployment](k8s/deployment_nginxdemo.yaml)

### Namespace qoutas

https://kubernetes.io/docs/concepts/policy/resource-quotas/

Resource Quota support is enabled by default for many Kubernetes distributions. It is enabled when the apiserver --enable-admission-plugins= flag has ResourceQuota as one of its arguments
A resource quota is enforced in a particular namespace when there is a ResourceQuota in that namespace.

- file: [quotas](k8s/namespace_quotas.yaml)
- `kubectl -n demo describe quota`

### RBAC

- [rbac-clusterrole](k8s/rbac.yaml)

### Erstellen von CronJobs and Jobs

- [job-with-rbac](k8s/job_rbac.yaml)
- [cronjob](k8s/cronjob.yaml)

### Statefulset and Daemonset with ELK-Example

example:
https://blog.ptrk.io/how-to-deploy-an-efk-stack-to-kubernetes/
https://github.com/pires/kubernetes-elasticsearch-cluster

kubectl create -f k8s/elk/es-discovery-svc.yaml
kubectl create -f k8s/elk/es-svc.yaml
kubectl create -f k8s/elk/es-master.yaml
kubectl rollout status -f k8s/elk/es-master.yaml

kubectl create -f k8s/elk/es-ingest-svc.yaml
kubectl create -f k8s/elk/es-ingest.yaml
kubectl rollout status -f k8s/elk/es-ingest.yaml

kubectl create -f k8s/elk/es-data-stateful.yaml
kubectl rollout status -f k8s/elk/es-data-stateful.yaml

### Deployment options and PodSecurity

- [deployment](k8s/deployment_all.yaml)
- commands:
  - man capabilities
  - grep CapE /proc/self/status 
  - capsh --decode=00000000a80425fb

### Helm

https://docs.helm.sh/using_helm/

- curl https://raw.githubusercontent.com/kubernetes/helm/master/scripts/get | bash
- helm init
- helm repo update
- helm seach wordpress
- helm inspect chart stable/wordpress
- helm install stable/wordpress


### other Stuff

- Storage Classes
- Autoscaling
- HA Master
- Network Policies
- PodSecurityPolicy

- Podtemplate -DNS Policy
- Podtemplate- Affinity
- Podtemplate - TerminationMessage
- Taints and Tolerations
- PodDisruptionBudget
- PriorityClasses
- ...