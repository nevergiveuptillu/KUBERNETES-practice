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

- kubeadm init --pod-network-cidr "10.244.0.0/16" --cri-socket "unix:///var/run/cri-dockerd.sock"
- exit
- regular user
- mkdir -p $HOME/.kube
- sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
- sudo chown $(id -u):$(id -g) $HOME/.kube/config

- kubectl apply -f https://github.com/flannel-io/flannel/releases/latest/download/kube-flannel.yml
- 
- Node !:::::
- 
- kubeadm join 172.31.15.103:6443 --token h81cit.wlihjl6k0jognj9w
- --cri-socket unix:///var/run/cri-dockerd.sock
- --discovery-token-ca-cert-hash sha256:835ec21ec52e2eb8621dbaec3534f9c02d0bb59dc9f3d70a3df28d1cc1b56a1b