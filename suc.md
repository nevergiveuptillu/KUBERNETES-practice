 1  curl -OL https://golang.org/dl/go1.16.7.linux-amd64.tar.gz
    2  sha256sum go1.16.7.linux-amd64.tar.gz
    3  sudo tar -C /usr/local -xvf go1.16.7.linux-amd64.tar.gz
    4  sudo nano ~/.profile
    5  source ~/.profile
    6  go version
    7  sudo apt update
    8  sudo apt install apt-transport-https ca-certificates curl gnupg2 software-properties-common -y
    9  export OS=xUbuntu_22.04
   10  export CRIO_VERSION=1.24
   11  echo "deb https://download.opensuse.org/repositories/devel:/kubic:/libcontainers:/stable/$OS/ /"| sudo tee /etc/apt/sources.list.d/devel:kubic:libcontainers:stable.list
   12  "deb http://download.opensuse.org/repositories/devel:/kubic:/libcontainers:/stable:/cri-o:/$CRIO_VERSION/$OS/ /"|sudo tee /etc/apt/sources.list.d/devel:kubic:libcontainers:stable:cri-o:$CRIO_VERSION.list
   13  echo "deb http://download.opensuse.org/repositories/devel:/kubic:/libcontainers:/stable:/cri-o:/$CRIO_VERSION/$OS/ /"|sudo tee /etc/apt/sources.list.d/devel:kubic:libcontainers:stable:cri-o:$CRIO_VERSION.list
   14  curl -L https://download.opensuse.org/repositories/devel:kubic:libcontainers:stable:cri-o:$CRIO_VERSION/$OS/Release.key | sudo apt-key add -
   15  curl -L https://download.opensuse.org/repositories/devel:/kubic:/libcontainers:/stable/$OS/Release.key | sudo apt-key add -
   16  curl -L https://download.opensuse.org/repositories/devel:kubic:libcontainers:stable:cri-o:$CRIO_VERSION/$OS/Release.key | sudo apt-key add -
   17  sudo apt update
   18  sudo apt install cri-o cri-o-runc -y
   19  sudo systemctl start crio
   20  sudo systemctl enable crio
   21  sudo systemctl status crio
   22  sudo apt install containernetworking-plugins -y
   23  sudo nano /etc/crio/crio.conf
   24  crictl completion > /etc/bash_completion.d/crictl
   25  source ~/.bashrc
   26  crictl
   27  sudo apt-get update
   28  sudo apt-get install -y apt-transport-https ca-certificates curl
   29  curl -fsSL https://pkgs.k8s.io/core:/stable:/v1.28/deb/Release.key | sudo gpg --dearmor -o /etc/apt/keyrings/kubernetes-apt-keyring.gpg
   30  echo 'deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/v1.28/deb/ /' | sudo tee /etc/apt/sources.list.d/kubernetes.list
   31  sudo apt-get update
   32  sudo apt-get install -y kubelet kubeadm kubectl
   33  sudo apt-mark hold kubelet kubeadm kubectl
   34  sudo systemctl stop containerd.service
   35  kubeadm join 172.31.11.233:6443 --token tsqvtq.ovqm5mrnjewv4qjz         --discovery-token-ca-cert-hash sha256:8823270adc4ad79c7dfb945a83a11347f33e713141659870e584e291df2d3994
   36  kubeadm join 172.31.11.233:6443 --token tsqvtq.ovqm5mrnjewv4qjz         --discovery-token-ca-cert-hash sha256:8823270adc4ad79c7dfb945a83a11347f33e713141659870e584e291df2d3994
   37  kubeadm reset
   38  kubeadm join 172.31.11.233:6443 --token px7q9m.kytqlzn5s9g8a0m3         --discovery-token-ca-cert-hash sha256:2d0156b19e5cd015708b571cd8425070147231c09654f0ac7ac3d11aab83dd4d