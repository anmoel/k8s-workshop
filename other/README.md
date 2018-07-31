
# other Stuff

## RBAC

- [rbac-clusterrole](k8s/rbac.yaml)

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


## To Create Informations
- HA Master
- Storage Classes
- Autoscaling
- Network Policies
- PodSecurityPolicy

- Podtemplate -DNS Policy
- Podtemplate- Affinity
- Podtemplate - TerminationMessage
- Taints and Tolerations
- PodDisruptionBudget
- PriorityClasses
- ...