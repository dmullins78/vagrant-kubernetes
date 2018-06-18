https://metallb.universe.tf/tutorial/layer2/
https://wiki.onap.org/display/DW/Deploying+Kubernetes+Cluster+with+kubeadm

https://kubernetes.io/docs/setup/independent/create-cluster-kubeadm/

https://raw.githubusercontent.com/google/metallb/v0.6.2/manifests/example-layer2-config.yaml
kubectl apply -f metal.yaml -n metallb-system

sudo kubeadm init --apiserver-advertise-address=10.0.1.20
# Flannel Networking Set-Up
sudo kubeadm init --apiserver-advertise-address=10.0.1.25 --pod-network-cidr=10.244.0.0/16

https://blog.laputa.io/kubernetes-flannel-networking-6a1cb1f8ec7c

sudo  sysctl net.bridge.bridge-nf-call-iptables=1

kubectl apply -f https://raw.githubusercontent.com/coreos/flannel/v0.10.0/Documentation/kube-flannel.yml


kubectl apply -f "https://cloud.weave.works/k8s/net?k8s-version=$(kubectl version | base64 | tr -d '\n')"

## Set password for the slave
sudo passwd ubuntu

SSH to the machine
Become root (e.g. sudo su -)

ubuntu@kubslave:~$ sudo su -
root@kubslave:~# kubeadm join 10.0.1.22:6443 --token sywqo9.spuwwxabtfqdzf34 --discovery-token-ca-cert-hash sha256:64fbb91d4de1ff04a42fd9871e64b50d2acee6af0f48615aff4e11ce5b139d90^C
root@kubslave:~# ^C
root@kubslave:~# kubeadm join 10.0.1.22:6443 --token sywqo9.spuwwxabtfqdzf34 --discovery-token-ca-cert-hash sha256:64fbb91d4de1ff04a42fd9871e64b50d2acee6af0f48615aff4e11ce5b139d90

on Master:
kubectl get nodes (should see master and slave)


sudo cp /etc/kubernetes/admin.conf /vagrant_data/.

dan@Daniels-MacBook-Pro:~/Projects/kuber/kubadm2% cp data/admin.conf .
dan@Daniels-MacBook-Pro:~/Projects/kuber/kubadm2% kubectl --kubeconfig ./admin.conf get nodes
NAME        STATUS     ROLES     AGE       VERSION
kubmaster   Ready      master    11m       v1.10.4
kubslave    NotReady   <none>    5m        v1.10.4


kubectl create deployment nginx --image=nginx

https://www.linode.com/docs/applications/containers/how-to-deploy-nginx-on-a-kubernetes-cluster/

kubectl get deployments
kubectl describe deployment nginx
kubectl create service nodeport nginx --tcp=80:80

curl kube-worker-1:32555
curl http://10.0.1.23:30341

kubectl delete deployment nginx
kubectl get deployments

## Install Helm
ubuntu@kubmaster:~$ curl https://raw.githubusercontent.com/kubernetes/helm/master/scripts/get > get_helm.sh
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100  6740  100  6740    0     0  19652      0 --:--:-- --:--:-- --:--:-- 19650
ubuntu@kubmaster:~$ chmod 700 get_helm.sh
ubuntu@kubmaster:~$ ./get_helm.sh
