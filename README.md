# nginx_kubernetes
install mini
https://kubernetes.io/docs/tasks/tools/install-minikube/ 

$ minikube logs
$ minikube ip


Diagnostics for the cluster:  

$ kubectl get componentstatuses

The output should look like this:

NAME STATUS MESSAGE ERROR
scheduler Healthy ok
controller-manager Healthy ok
etcd-0 Healthy {"health": "true"}


Identify the various components.

Listing nodes:
$ kubectl get nodes

Get detailed information about a node:
$ kubectl describe node <node id>

Find in the output the pods on the node (e.g., the kube-dns pod that supplies DNS services for the cluster), the CPU and memory that each “pod” is requesting from the node, as well as the total resources requested. 

E.g. kube proxy:
$ kubectl get daemonsets --namespace=kube-system kube-proxy

E.g. DNS deployment:
$ kubectl get deployments --namespace=kube-system kube-dns

There is also a Kubernetes service that performs load-balancing for the DNS server:
$ kubectl get services --namespace=kube-system kube-dns

$ kubectl create -f nginx_pod.yaml

To list the created pods:
$ kubectl get pods

$kubectl create -f nginx_service.yaml

To list the created service:
$ kubectl get services
$ kubectl get endpoints

Cleanup:
$ kubectl delete -f nginx_service.yaml
$ kubectl delete -f nginx_pod.yaml

