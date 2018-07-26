# Advanced

## Lecture:

### Create HA Kubernetes Cluster

## HandsOn:

### Install with kubeadm

### Secrets

### Namespace qoutas

https://kubernetes.io/docs/concepts/policy/resource-quotas/

Resource Quota support is enabled by default for many Kubernetes distributions. It is enabled when the apiserver --enable-admission-plugins= flag has ResourceQuota as one of its arguments
A resource quota is enforced in a particular namespace when there is a ResourceQuota in that namespace.

- file: [quotas](k8s/namespace_quotas.yaml)
- `kubectl -n demo describe quota`

### Erstellen von CronJobs and Jobs

### Daemonsets

### Statefulset mit PersistentVolume

### Deployment 

update strategie
imagepullpolicy
lifecycle
autoscalierung

### PodSecurity

### RBAC

### Helm
