    1  crictl completion > /etc/bash_completion.d/crictl
    2  source ~/.bashrc
    3  crictl
    4  cd ~
    5  sudo apt-get install -y apt-transport-https ca-certificates curl
    6  curl -fsSL https://pkgs.k8s.io/core:/stable:/v1.28/deb/Release.key | sudo gpg --dearmor -o /etc/apt/keyrings/kubernetes-apt-keyring.gpg
    7  echo 'deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/v1.28/deb/ /' | sudo tee /etc/apt/sources.list.d/kubernetes.list
    8  sudo apt-get update
    9  sudo apt-get install -y kubelet kubeadm kubectl
   10  sudo apt-mark hold kubelet kubeadm kubectl
   11  kubeadm init --pod-network-cidr "10.244.0.0/16"
   12  kubeadm init --pod-network-cidr "10.244.0.0/16" --cri-socket "unix:///var/run/crio/crio.sock"
   13  kubectl apply -f https://github.com/flannel-io/flannel/releases/latest/download/kube-flannel.yml
   14  ls
   15  kubectl --help
   16  docker image ls
   17  dokcer container ls
   18  curl -OL https://golang.org/dl/go1.16.7.linux-amd64.tar.gz
   19  sha256sum go1.16.7.linux-amd64.tar.gz
   20  sudo tar -C /usr/local -xvf go1.16.7.linux-amd64.tar.gz
   21  sudo nano ~/.profile
   22  source ~/.profile
   23  go version
   24  git clone https://github.com/cri-o/cri-o.git
   25  ls
   26  cd cri-o/
   27  ls
   28  mkdir bin
   29  ls | grep bin
   30  go build -o bin/cri-dockerd
   31  go build -o bin/cri-o
   32  ls
   33  cd ..
   34  ls
   35  rm cri-o/
   36  ls
   37  rm -rf cri-o/
   38  ls
   39  sudo apt update
   40  sudo apt install apt-transport-https ca-certificates curl gnupg2 software-properties-common -y
   41  export OS=xUbuntu_22.04
   42  export CRIO_VERSION=1.24
   43  echo "deb https://download.opensuse.org/repositories/devel:/kubic:/libcontainers:/stable/$OS/ /"| sudo tee /etc/apt/sources.list.d/devel:kubic:libcontainers:stable.list
   44  echo "deb http://download.opensuse.org/repositories/devel:/kubic:/libcontainers:/stable:/cri-o:/$CRIO_VERSION/$OS/ /"|sudo tee /etc/apt/sources.list.d/devel:kubic:libcontainers:stable:cri-o:$CRIO_VERSION.list
   45  curl -L https://download.opensuse.org/repositories/devel:kubic:libcontainers:stable:cri-o:$CRIO_VERSION/$OS/Release.key | sudo apt-key add -
   46  curl -L https://download.opensuse.org/repositories/devel:/kubic:/libcontainers:/stable/$OS/Release.key | sudo apt-key add -
   47  sudo apt update
   48  sudo apt install cri-o cri-o-runc -y
   49  sudo systemctl start crio
   50  sudo systemctl enable crio
   51  sudo systemctl status crio
   52  sudo apt install containernetworking-plugins -y
   53  sudo nano /etc/crio/crio.conf
   54  sudo systemctl restart crio
   55  sudo apt install -y cri-tools
   56  sudo crictl --runtime-endpoint unix:///var/run/crio/crio.sock version
   57  sudo su -
   58  history