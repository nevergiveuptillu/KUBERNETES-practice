 To install the latest stable versions of Docker CLI, Docker Engine, and their

# dependencies:
# Docker installation
---------------------
# 1. download the script

  `curl -fsSL https://get.docker.com -o install-docker.sh`

# 2. verify the script's content

  `cat install-docker.sh`

# 3. run the script with --dry-run to verify the steps it executes
  `sh install-docker.sh --dry-run`

# 4. run the script either as root, or using sudo to perform the installation.
  `sudo sh install-docker.sh`

# user mode
-----------

  ```
  sudo usermod -aG docker ubuntu
  exit
  docker version
  sudo -i
  ```
  ![preview](images\k8s1.PNG)
  
# rootuser
----------
# go language
-------------
  
   ```
   wget https://storage.googleapis.com/golang/getgo/installer_linux
   chmod +x ./installer_linux
   ./installer_linux
   source ~/.bash_profile
   ```
   ![preview](/images/k8s2.png)
  
# cri-dockered  gitclone
------------------------

 ```
 git clone https://github.com/Mirantis/cri-dockerd.git
 cd cri-dockerd
 ```
 ![preview](/images/k8s3.PNG)

# create bin directory
----------------------
 
  ```
  mkdir bin
  go build -o bin/cri-dockerd
  mkdir -p /usr/local/bin
  install -o root -g root -m 0755 bin/cri-dockerd /usr/local/bin/cri-dockerd
  cp -a packaging/systemd/* /etc/systemd/system
  sed -i -e 's,/usr/bin/cri-dockerd,/usr/local/bin/cri-dockerd,' /etc/systemd/system/cri-docker.service
  systemctl daemon-reload
  systemctl enable cri-docker.service
  systemctl enable --now cri-docker.socket
  cd ~
  ```
  ![preview](/images/k8s4.PNG)


# installation kubadm, kubectl, kubelet 
-------------------------------------
 
 ```
 sudo apt-get update
 sudo apt-get install -y apt-transport-ht
 curl -fsSL https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo gpg --dearmor -o /etc/apt/keyrings/kubernetes-archive-keyring.gpg
 echo "deb [signed-by=/etc/apt/keyrings/kubernetes-archive-keyring.gpg] https://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee /etc/apt/sources.list.d/kubernetes.list
 sudo apt-get update
 sudo apt-get install -y kubelet kubeadm kubectl
 sudo apt-mark hold kubelet kubeadm kubectl
 ```
 ![preview](/images/k8s5.PNG)

# now create cluster from masternode
----------------------------------
  ``` 
  kubeadm init --pod-network-cidr "10.244.0.0/16" --cri-socket "unix:///var/run/cri-dockerd.sock"
  exit
  mkdir -p $HOME/.kube
  sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
  sudo chown $(id -u):$(id -g) $HOME/.kube/config
  ```
  ![preview](/images/k8s6.PNG)


# install funnel
----------------
  
  ```
  kubectl apply -f https://github.com/flannel-io/flannel/releases/latest/download/kube-flannel.yml

  kubectl get nodes
  ```
  ![preview](/images/k8s7.PNG)

# Node !:::::

kubeadm join 172.31.15.103:6443 --token h81cit.wlihjl6k0jognj9w \
        --cri-socket unix:///var/run/cri-dockerd.sock \
        --discovery-token-ca-cert-hash sha256:835ec21ec52e2eb8621dbaec3534f9c02d0bb59dc9f3d70a3df28d1cc1b56a1b
   ![preview](/images/k8s9.PNG)




# 2nd attempt

 mkdir -p $HOME/.kube
  sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
  sudo chown $(id -u):$(id -g) $HOME/.kube/config

  node;;;

  kubeadm join 172.31.24.254:6443 --token ooevqe.blg4sm2k2pt8tm0o \
   --cri-socket "unix:///var/run/cri-dockerd.sock" \
        --discovery-token-ca-cert-hash sha256:eb836f8fca8ab0b4e934acae0d2861500d93f9d4a6e8491a81a616a77528464d