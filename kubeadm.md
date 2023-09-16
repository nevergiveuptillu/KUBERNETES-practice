Docker installation
-------------------
- curl -fsSL https://get.docker.com -o install-docker.sh
- sudo sh install-docker.sh
- sudo usermod -aG docker ubuntu

 rootuser 
----------
- sudo -i

go language //tar file
-----------------------
- curl -OL https://golang.org/dl/go1.16.7.linux-amd64.tar.gz
- sha256sum go1.16.7.linux-amd64.tar.gz
- sudo tar -C /usr/local -xvf go1.16.7.linux-amd64.tar.gz
- sudo nano ~/.profile
- export PATH=$PATH:/usr/local/go/bin
- source ~/.profile
- go version


cri -O installation steps:
--------------------------
- https://www.linuxtechi.com/install-crio-container-runtime-on-ubuntu/


plugin_dirs = [
        "/opt/cni/bin/",
        "/usr/lib/cni",
]


cri-dockered gitclone
---------------------
- wget https://github.com/Mirantis/cri-dockerd/releases/download/v0.2.0/cri-dockerd-v0.2.0-linux-amd64.tar.gz
- tar xvf cri-dockerd-v0.2.0-linux-amd64.tar.gz
- sudo mv ./cri-dockerd /usr/local/bin/ 
- cri-dockerd --help
- wget https://raw.githubusercontent.com/Mirantis/cri-dockerd/master/packaging/systemd/cri-docker.service
- wget https://raw.githubusercontent.com/Mirantis/cri-dockerd/master/packaging/systemd/cri-docker.socket
- sudo mv cri-docker.socket cri-docker.service /etc/systemd/system/
- sudo sed -i -e 's,/usr/bin/cri-dockerd,/usr/local/bin/cri-dockerd,' /etc/systemd/system/cri-docker.service
- systemctl daemon-reload
- systemctl enable cri-docker.service
- systemctl enable --now cri-docker.socket
- systemctl status cri-docker.socket
 
cd ~
----

- installation kubadm, kubectl, kubelet
----------------------------------------

- sudo apt-get update
- sudo apt-get install -y apt-transport-https ca-certificates curl
- curl -fsSL https://pkgs.k8s.io/core:/stable:/v1.28/deb/Release.key | sudo gpg --dearmor -o /etc/apt/keyrings/kubernetes-apt-keyring.gpg
- echo 'deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/v1.28/deb/ /' | sudo tee /etc/apt/sources.list.d/kubernetes.list
- sudo apt-get update
- sudo apt-get install -y kubelet kubeadm kubectl
- sudo apt-mark hold kubelet kubeadm kubectl

- kubeadm init --pod-network-cidr "10.244.0.0/16" 
- kubeadm init --pod-network-cidr "10.244.0.0/16" --cri-socket "unix:///var/run/crio/crio.sock"
- exit
- regular user
- mkdir -p $HOME/.kube
- sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
- sudo chown $(id -u):$(id -g) $HOME/.kube/config

- kubectl apply -f https://github.com/flannel-io/flannel/releases/latest/download/kube-flannel.yml
- 
- kubeadm join 172.31.15.103:6443 --token h81cit.wlihjl6k0jognj9w
- --cri-socket unix:///var/run/cri-dockerd.sock
- --discovery-token-ca-cert-hash sha256:835ec21ec52e2eb8621dbaec3534f9c02d0bb59dc9f3d70a3df28d1cc1b56a1b

  mkdir -p $HOME/.kube
  sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
  sudo chown $(id -u):$(id -g) $HOME/.kube/config

kubeadm join 172.31.4.35:6443 --token t767wy.1h9m957gv1zgqlt3 \
        --discovery-token-ca-cert-hash sha256:5fb9445682ab2b5779c8f8edcb721d22818a8bd3f614af5f468e7d9483f6abbf

kubectl apply -f [podnetwork].yaml    

  mkdir -p $HOME/.kube
  sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
  sudo chown $(id -u):$(id -g) $HOME/.kube/config


  masternode :
  ----------
   1  curl -OL https://golang.org/dl/go1.16.7.linux-amd64.tar.gz
    2  - sha256sum go1.16.7.linux-amd64.tar.gz
    3  sha256sum go1.16.7.linux-amd64.tar.gz
    4  sudo tar -C /usr/local -xvf go1.16.7.linux-amd64.tar.gz
    5  sudo nano ~/.profile
    6  source ~/.profile
    7  go version
    8  sudo apt update
    9  sudo apt install apt-transport-https ca-certificates curl gnupg2 software-properties-common -y
   10  export OS=xUbuntu_22.04
   11  export CRIO_VERSION=1.24
   12  echo "deb https://download.opensuse.org/repositories/devel:/kubic:/libcontainers:/stable/$OS/ /"| sudo tee /etc/apt/sources.list.d/devel:kubic:libcontainers:stable.list
   13  "deb http://download.opensuse.org/repositories/devel:/kubic:/libcontainers:/stable:/cri-o:/$CRIO_VERSION/$OS/ /"|sudo tee /etc/apt/sources.list.d/devel:kubic:libcontainers:stable:cri-o:$CRIO_VERSION.list
   14  echo "deb http://download.opensuse.org/repositories/devel:/kubic:/libcontainers:/stable:/cri-o:/$CRIO_VERSION/$OS/ /"|sudo tee /etc/apt/sources.list.d/devel:kubic:libcontainers:stable:cri-o:$CRIO_VERSION.list
   15  curl -L https://download.opensuse.org/repositories/devel:kubic:libcontainers:stable:cri-o:$CRIO_VERSION/$OS/Release.key | sudo apt-key add -
   16  curl -L https://download.opensuse.org/repositories/devel:/kubic:/libcontainers:/stable/$OS/Release.key | sudo apt-key add -
   17  curl -L https://download.opensuse.org/repositories/devel:kubic:libcontainers:stable:cri-o:$CRIO_VERSION/$OS/Release.key | sudo apt-key add -
   18  sudo apt update
   19  sudo apt install cri-o cri-o-runc -y
   20  sudo systemctl start crio
   21  sudo systemctl enable crio
   22  sudo systemctl status crio
   23  sudo apt install containernetworking-plugins -y
   24  sudo nano /etc/crio/crio.conf
   25  crictl completion > /etc/bash_completion.d/crictl
   26  source ~/.bashrc
   27  crictl
   28  sudo systemctl
   29  sudo apt-get update
   30  sudo apt-get install -y apt-transport-https ca-certificates curl
   31  curl -fsSL https://pkgs.k8s.io/core:/stable:/v1.28/deb/Release.key | sudo gpg --dearmor -o /etc/apt/keyrings/kubernetes-apt-keyring.gpg
   32  echo 'deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/v1.28/deb/ /' | sudo tee /etc/apt/sources.list.d/kubernetes.list
   33  sudo apt-get update
   34  sudo apt-get install -y kubelet kubeadm kubectl
   35  sudo apt-mark hold kubelet kubeadm kubectl
   36  kubeadm init --pod-network-cidr "10.244.0.0/16"
   37  sudo systemctl stop containerd.service
   38  kubeadm init --pod-network-cidr "10.244.0.0/16"
   39  sudo systemctl restart crio
   40  sudo apt install -y cri-tools
   41  sudo crictl --runtime-endpoint unix:///var/run/crio/crio.sock version
   42  sudo crictl info
   43  sudo su -
   44  ls
   45  kubeadm init --pod-network-cidr "10.244.0.0/16"
   46  kubeadm init --pod-network-cidr "10.244.0.0/16" --cri-socket "unix:///var/run/crio/crio.sock"
   47  kubeadm
   48  ls
   49  kubeadm init --pod-network-cidr "10.244.0.0/16" --cri-socket "unix:///var/run/crio/crio.sock"
   50  netstat -plnt
   51  systemctl status containerd
   52  systemctl enable --now containerd
   53  systemctl restart containerd
   54  systemctl stop containerd
   55  systemctl start containerd
   56  kubeadm init --pod-network-cidr "10.244.0.0/16" --cri-socket "unix:///var/run/crio/crio.sock"
   57  kubeadm init
   58  kubeadm init --help
   59  kubeadm
   60  kubeadm reset
   61  sudo systemctl stop containerd.service
   62  kubeadm reset
   63  kubeadm init --pod-network-cidr "10.244.0.0/16"
   64  kubectl get nodes
   65  ls
   66  sudo su-
   67  sudo su -
   68  ls
   69  kubectl get nodes
   70  export KUBECONFIG=/etc/kubernetes/admin.conf
   71  kubectl get nodes
   72  ls
   73  kubectl get nodes