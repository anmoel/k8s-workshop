# Advanced

## HandsOn

### Install with kubeadm

- [kubernetes setup](https://kubernetes.io/docs/setup/)
- `kubeadm init` output the kubeadm join command
  - `kubeadm config print-default`
  - [kubeadm.conf](kubeadm.conf)
  - `kubeadm init --config kubeadm.conf`
  - `kubeadm init --pod-network-cidr=10.244.0.0/16`
- `kubeadm token create` on master
- `kubeadm token list` on master to get <TOKEN>
- `openssl x509 -pubkey -in /etc/kubernetes/pki/ca.crt | openssl rsa -pubin -outform der 2>/dev/null | openssl dgst -sha256 -hex | sed 's/^.* //'` on master to get <CAHASH>
- `kubeadm join --token <TOKEN> 10.128.0.3:6443 --discovery-token-ca-cert-hash sha256:<CAHASH>` 
- [install network interface](https://kubernetes.io/docs/setup/independent/create-cluster-kubeadm/)
  - `kubectl apply -f https://docs.projectcalico.org/v3.1/getting-started/kubernetes/installation/hosted/canal/rbac.yaml`
  - `kubectl apply -f https://docs.projectcalico.org/v3.1/getting-started/kubernetes/installation/hosted/canal/canal.yaml`
- `kubectl create ns demo`
optional:
- [install metric-server](https://kubernetes.io/docs/tasks/debug-application-cluster/core-metrics-pipeline/)
- [install dashboard](https://kubernetes.io/docs/tasks/access-application-cluster/web-ui-dashboard/)
  - `kubectl proxy`
  - [Dashboard Url with kubectl proxy](http://localhost:8001/api/v1/namespaces/kube-system/services/https:kubernetes-dashboard:/proxy/)

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

### Statefulset, Daemonset and CronJob with EFK-Example

example:
https://blog.ptrk.io/how-to-deploy-an-efk-stack-to-kubernetes/
https://github.com/pires/kubernetes-elasticsearch-cluster

kubectl create ns logging
kubectl apply -f k8s/elk/es-discovery-svc.yaml
kubectl apply -f k8s/elk/es-svc.yaml
kubectl apply -f k8s/elk/es-master.yaml
kubectl rollout status -f k8s/elk/es-master.yaml

kubectl apply -f k8s/elk/es-ingest-svc.yaml
kubectl apply -f k8s/elk/es-ingest.yaml
kubectl rollout status -f k8s/elk/es-ingest.yaml

kubectl apply -f k8s/elk/es-data-stateful.yaml
kubectl rollout status -f k8s/elk/es-data-stateful.yaml

kubectl apply -f k8s/elk/kibana-svc.yaml -f k8s/elk/kibana.yaml
kubectl rollout status -f k8s/elk/kibana.yaml

kubectl apply -f k8s/elk/fluentd.yaml
kubectl rollout status -f k8s/elk/fluentd.yaml

kubectl apply -f k8s/elk/es-curator-config.yaml -f k8s/elk/es-curator_v1beta1.yaml

### Deployment options and PodSecurity

- [deployment](k8s/options_example.yaml)
- commands:
  - man capabilities
  - grep CapE /proc/self/status 
  - capsh --decode=00000000a80425fb
