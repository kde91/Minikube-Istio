# Minikube-Istio

Setup Minikube using minikube.yaml:
conntrack and docker should be installed as a pre-requisite.
Install minikube from the repo.
Start the minikube service.

root@ip-172-31-14-105:~# minikube status
minikube
type: Control Plane
host: Running
kubelet: Running
apiserver: Running
kubeconfig: Configured

root@ip-172-31-14-105:~# minikube ip
172.31.14.105


Setup Istio using istio.yaml
Download the istio setup & install it using : istioctl install --set profile=demo -y

Label the namespace where the deployment will take place
root@ip-172-31-14-105:~# kubectl get ns --show-labels
NAME              STATUS   AGE     LABELS
default           Active   2d16h   istio-injection=enabled,kubernetes.io/metadata.name=default
istio-system      Active   2d6h    kubernetes.io/metadata.name=istio-system
kube-node-lease   Active   2d16h   kubernetes.io/metadata.name=kube-node-lease
kube-public       Active   2d16h   kubernetes.io/metadata.name=kube-public
kube-system       Active   2d16h   kubernetes.io/metadata.name=kube-system


Deploy the apps for blue-green deployment:
root@ip-172-31-14-105:~# kubectl get po
NAME                              READY   STATUS    RESTARTS        AGE
blue-5c7sz                        2/2     Running   0               174m
details-v1-5498c86cf5-5bndf       2/2     Running   2 (4h49m ago)   6h31m
green-jqsjg                       2/2     Running   0               173m


Deploy the service:
root@ip-172-31-14-105:~# kubectl get svc
NAME          TYPE           CLUSTER-IP       EXTERNAL-IP   PORT(S)          AGE
bluegreenlb   LoadBalancer   10.108.254.6     <pending>     8000:30195/TCP   172m

  
Check the svc IP:
  root@ip-172-31-14-105:~# minikube service greenbluelb --url
http://172.31.14.105:32686
root@ip-172-31-14-105:~#
root@ip-172-31-14-105:~#
root@ip-172-31-14-105:~# curl http://172.31.14.105:32686
<!DOCTYPE html>
<html>
<head>
        <title>Capstone project</title>
</head>
<body style="background: green;">
        <p>Hello World, my name is Alvaro Pinzon</p>
</body>

  
Change the label of service to blue and deploy
