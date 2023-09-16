
https://directdevops.blog/2023/09/07/devops-classroomnotes-07-sep-2023/


- docker installation 

curl -fsSL https://get.docker.com -o install-docker.sh
sh install-docker.sh

- download deb package of cri-dockerd and installation as per 
ubuntu version

https://github.com/Mirantis/cri-dockerd/releases


- kubeadm,kubectl,kubelet installation

https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/install-kubeadm/#installing-kubeadm-kubelet-and-kubectl

- Creating a cluster with kubeadm

https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/create-cluster-kubeadm/

- kubeadm init --pod-network-cidr "10.244.0.0/16" --cri-socket "unix:///var/run/cri-dockerd.sock"

- 

Your Kubernetes control-plane has initialized successfully!

To start using your cluster, you need to run the following as a regular user:

  mkdir -p $HOME/.kube
  sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
  sudo chown $(id -u):$(id -g) $HOME/.kube/config

Alternatively, if you are the root user, you can run:

  export KUBECONFIG=/etc/kubernetes/admin.conf

You should now deploy a pod network to the cluster.
Run "kubectl apply -f [podnetwork].yaml" with one of the options listed at:
  https://kubernetes.io/docs/concepts/cluster-administration/addons/

Then you can join any number of worker nodes by running the following on each as root:

kubeadm join 172.31.2.45:6443 --token 3mcvq7.yr74crp05u7bb8cx \
        --discovery-token-ca-cert-hash sha256:c831676deaa3f716bfa2ac5c6ccc3a86a69f489281969da7e9eaf4dedb37da80 \
        --cri-socket "unix:///var/run/cri-dockerd.sock"


-  kubectl get nodes 


https://kubernetes.io/docs/concepts/extend-kubernetes/compute-storage-net/network-plugins/

-  kubectl apply -f https://github.com/flannel-io/flannel/releases/latest/download/kube-flannel.yml

- kubectl get nodes -w

- set up commands
- https://kubernetes.io/docs/reference/kubectl/cheatsheet/