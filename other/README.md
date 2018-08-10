
# other Stuff

## short RBAC example

- Kubernetes clusters have to types of users service accounts and normal users , but normal users are assumed to be managed by an outside service.
- [rbac-clusterrole](k8s/rbac.yaml)
- kubectl auth can-i COMMAND OBJECTCLASS
  - `kubectl auth can-i create deployments --as bob --namespace developer`

## Erstellen von CronJobs and Jobs

- [job-with-rbac](k8s/job_rbac.yaml)
- [cronjob](k8s/cronjob.yaml)

## Helm

https://docs.helm.sh/using_helm/

- curl https://raw.githubusercontent.com/kubernetes/helm/master/scripts/get | bash
- helm init
- helm repo update
- helm search wordpress
- helm inspect chart stable/wordpress
- helm install stable/wordpress

## Debugging of Kubernetes components

- kubectl run -i --tty ubuntu --image=ubuntu:16.04 --restart=Never -- bash -il
- https://kubernetes.io/docs/tasks/debug-application-cluster/debug-service/
- on all members:
  - journalctl -u kubelet | less
  - find / -name "*kube-proxy*log"
- additional on master:
  - find / -name "*apiserver*log"
  - find / -name "*scheduler*log"
  - find / -name "*controller-manager*log"

## To Create Informations
- HA Master
- Volumes, PersistentVolumes, StorageClasses
- Users, Groups, Login, RBAC advanced
- Autoscaling
- Network Policies
- PodSecurityPolicy
- CustomResources

- Podtemplate -DNS Policy
- Podtemplate- Affinity
- Podtemplate - TerminationMessage
- Taints and Tolerations
- PodDisruptionBudget
- PriorityClasses
- ...