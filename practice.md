# kubernetes practice

* kubectl version
 ![preview](/practice/images/1.PNG)

* kubectl api-resources
 ![preview](/practice/images/2.PNG)

* understanding kubectk cheet sheet
 ![referhere](https://kubernetes.io/docs/reference/kubectl/cheatsheet/)

* •	commands
kubectl apply -f
kubectl get <api-resource>
kubectl describe <kind> <name>

# git clone to kubectl

# httpd yaml execution :exec1

   C:\Program Files (x86)\Google\Cloud SDK>git clone https://github.com/SHIVASOMANATH/KUBERNETES-practice.git

   git pull
 
* kubectl apply -f 
  
  C:\Program Files (x86)\Google\Cloud SDK\KUBERNETES-practice>kubectl apply -f exec1.yaml
  
  pods created

 ![preview](/practice/images/3.PNG)

* kubectl get pod

 ![preview](/practice/images/4.PNG)

* kubectl get pod -o wide

 ![preview](/practice/images/5.PNG)

* kubectl describe pods httpdpod

  ![preview](/practice/images/6.PNG)

* delete pods command : practice>kubectl delete -f exec1.yaml
 
 ![preview](/practice/images/7.PNG)

https://cloud.google.com/kubernetes-engine/docs/how-to/cluster-access-for-kubectl
https://cloud.google.com/kubernetes-engine/docs/how-to/cluster-access-for-kubectl#install_kubectl
https://cloud.google.com/kubernetes-engine/docs/how-to/cluster-access-for-kubectl

# alpine pod execution :exec2

* ![preview](/practice/images/8.PNG)

# nginx pod execution :exec3
 
* ![preview](/practice/images/9.PNG)

# nginx & alpine pod execution :exec4

* ![preview](/practice/images/10.PNG)
  ![preview](/practice/images/11.PNG)

# nginx ,alpine with sleep 1d and alpine with 10s :exec5 

* CrashLoopBackOff error

 ![preview](/practice/images/12.PNG)
 
 ![preview](/practice/images/13.PNG)

 ![preview](/practice/images/14.PNG)

# nginx and httpd with 80 port exposed :exec6

 back loop off error obseved

 ![preview](/practice/images/15.PNG)


* kubectl get pods httpd -o yaml
 ![preview](/practice/images/16.PNG)

# Restart policys 

# allways restart Policy  : allways restart.yaml

  ![preview](/practice/images/17.PNG)

# Never restart Policy  : restart never.yaml

  ![preview](/practice/images/18.PNG)

# on failure restart Policy : restart onfailure.yaml

  ![preview](/practice/images/19.PNG)

  ![preview](/practice/images/20.PNG)

## jobs.yaml ---cron jobs.yaml

* jobs.yaml verification

  `kubectl get jobs`
  
  ![preview](/practice/images/21.PNG)

* cronjobs verification

   ![preview](/practice/images/22.PNG)

  ![preview](/practice/images/23.PNG)


#### pods portforwarding execution 

  alpine pod run and exec command verification

* ```
  kubectl exec alpine pwd
  kubectl exec alpine ls
  kubectl exec alpine -it /bin/sh
  ```
![preview](/practice/images/24.PNG)

##  httpd install and port-forwarding 

 kubectl port-forward --address "0.0.0.0" httpd 8080:80

![preview](/practice/images/25.PNG)


### Replication controller and Replica set

 kubectl get replicationcontroller

replica set

![preview](/practice/images/26.PNG)

![preview](/practice/images/27.PNG)

![preview](/practice/images/28.PNG)

![preview](/practice/images/29.PNG)

![preview](/practice/images/30.PNG)

```
  38 kubectl get po
  27 kubectl get po -w
  40 kubectl get rs
  33 kubectl describe pod replica-p6swc
  39 kubectl scale --replicas=5 rs/replica
  45 kubectl describe rs/replica
  46 ls
  48 kubectl delete pod replica-6bk7k
  60 kubectl describe rs/replica
  61 kubectl get rs
```
```
* kubectl get rs
* kubectl describe rs name
* kubectl scale --replicas=5 rs/name
* kubectl delete pod name
* Labels and Selectors

```
  Labels are key/value pairs that are attached to objects such as Pods. Labels are intended to be used to specify identifying attributes of objects that are meaningful and relevant to users, but do not directly imply semantics to the core system. Labels can be used to organize and to select subsets of objects. Labels can be attached to objects at creation time and subsequently added and modified at any time. Each object can have a set of key/value labels defined. Each Key must be unique for a given object.

```
"metadata": {
  "labels": {
    "key1" : "value1",
    "key2" : "value2"
  }
}
```
Labels allow for efficient queries and watches and are ideal for use in UIs and CLIs. Non-identifying information should be recorded using annotations.


![preview](/practice/images/31.PNG)


 kubectl get po --show-labels
 kubectl run n1 --image=nginx --labels "app=nginx,component=web" imparative way

 Selectors:

 ![preview](/practice/images/32.PNG)
 ![preview](/practice/images/33.PNG)

```
 kubectl get po --selector "app=nginx" --show-labels
  kubectl get po --selector "app in (nginx,web)" --show-labels
  kubectl label po labeldemo app=jenkins --overwrite
```
  
 ![preview](/practice/images/34.PNG)

  kubectl delete rs jenkins-rs   need to carefull delete lables

# Load balancer

A load balancer is used to distribute the load that servers or virtual machines have to process in the most efficient manner possible. In this way, overall performance can be improved. Normally, a load balancer is placed upstream of the servers to prevent individual servers being overloaded. This also ensures optimal use of the available resources. Even when a server fails, the load balancer guarantees an up-and-running system by redirecting requests in a targeted manner

![preview](/practice/images/40.PNG)

# services

internal comunications:

commands:
```
kubectl apply -f .\service.yaml
kubectl apply -f .\alpine.yaml
kubectl get svc -o wide
kubectl get rs --show-labels
kubectl get po --show-labels
kubectl get svc -o wide
kubectl exec -it alpinepod -- /bin/sh
kubectl exec nginx-rs-8mmxt -- printenv
```

  ![preview](/practice/images/35.PNG)
  ![preview](/practice/images/36.PNG)
  ![preview](/practice/images/37.PNG)

* nslookup

 ![preview](/practice/images/38.PNG)
 ![preview](/practice/images/39.PNG)

```
   6 curl https:// 10.71.128.140
   7 apk add curl
   8 curl https:// 10.71.128.140
   9 curl http://nginx-svc
  10 nslookup nginx-svc
```
/ # nslookup 10.71.128.140
Server:         10.71.128.10
Address:        10.71.128.10:53

Non-authoritative answer:
140.128.71.10.in-addr.arpa      name = nginx-svc.default.svc.cluster.local

/ # cat /etc/resolv.conf
search default.svc.cluster.local svc.cluster.local cluster.local asia-south2-a.c.omega-episode-388205.internal c.omega-episode-388205.internal google.internal
nameserver 10.71.128.10
options ndots:5

```
/ # printenv
KUBERNETES_SERVICE_PORT=443
KUBERNETES_PORT=tcp://10.71.128.1:443
NGINX_SVC_SERVICE_HOST=10.71.128.140
NGINX_SVC_SERVICE_PORT_NGINX_SVC=80
HOSTNAME=alpinepod
SHLVL=1
HOME=/root
NGINX_SVC_SERVICE_PORT=80
NGINX_SVC_PORT=tcp://10.71.128.140:80
NGINX_SVC_PORT_80_TCP_ADDR=10.71.128.140
NGINX_SVC_PORT_80_TCP_PORT=80
NGINX_SVC_PORT_80_TCP_PROTO=tcp
TERM=xterm
KUBERNETES_PORT_443_TCP_ADDR=10.71.128.1
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
KUBERNETES_PORT_443_TCP_PORT=443
KUBERNETES_PORT_443_TCP_PROTO=tcp
NGINX_SVC_PORT_80_TCP=tcp://10.71.128.140:80
KUBERNETES_SERVICE_PORT_HTTPS=443
KUBERNETES_PORT_443_TCP=tcp://10.71.128.1:443
KUBERNETES_SERVICE_HOST=10.71.128.1
```

* external comunication: Load Balancer

 ![preview](/practice/images/41.PNG)

 ![preview](/practice/images/42.PNG)
 
 ![preview](/practice/images/43.PNG)

### Health checks

•	liveness probe: if this check fails kuberenetes will restart the container.
•	readiness probe: if this check fails the pod will be removed from service (pod will not get requests from service)
•	startup probe: This checks for startup and until startup is ok, the other checks will be paused.



Livecheck it fails it will restart the container
readieness check fails it will stop the application called from service
r-ness serving the number request

* checking live ness and redieness prob

when check fails

 ![preview](/practice/images/44.PNG)

 ![preview](/practice/images/45.PNG)

check success condition

![preview](/practice/images/46.PNG)

![preview](/practice/images/47.PNG)


readiness check condition

![preview](/practice/images/48.PNG)

![preview](/practice/images/49.PNG)

### Run Pods with specific Resources (CPU/Memory)

 resources : requests and limits

write health checks /write labels seletors/ write resources /write replicas


added limts and requests :refer resources.yaml

![preview](/practice/images/50.PNG)

### container types

we have 3 
  * containers:
  * init container: 
  * ephemeral containers:

    * init container: 

![preview](/practice/images/51.PNG)

 * ephemeral containers:


 # Deployements 

 `commands`:

```
kubectl get svc
kubectl get po
kubectl get deployement
kubectl api-resources
kubectl get deploy
kubectl get deploy -o wide
kubectl describe deploy deploy-check
kubectl describe deploy deploy-check
kubectl get rs
kubectl rollout history deployment/deploy-check
kubectl rollout status deployment/deploy-check

```
![preview](/practice/images/52.PNG)

![preview](/practice/images/53.PNG)

change the version of image 

kubectl get deployement.apps -w


![preview](/practice/images/54.PNG)

![preview](/practice/images/55.PNG)

rollout :

![preview](/practice/images/56.PNG)

  
rollout undo :

![preview](/practice/images/57.PNG)

kubectl rollout undo deployments/deploy-check

kubectl rollout undo deployments/deploy-check --to-revision=2

need to write anotaions in metadata for the change cause roolout history 
![preview](/practice/images/58.PNG)

Demonset
--------
•	DaemonSet is a controller which creates pod on every/selected nodes in k8s cluster

![preview](/practice/images/60.PNG)


![preview](/practice/images/61.PNG)



### scheduling pods

* Node selector

** node name 

![preview](/practice/images/62.PNG)

** node selector purpose

* Affinity/Anti Affinity Based labels of node //pod


node afinity : with matches the nodes 1... mandatory 2... put to have rool
required: manditory case
preffred: put have case

pod afinity:
 label is matches pod scheduled

pod anti afinity: 

 label is matches pod scheduled to another node 

### Taints and tollerations
 
based on taint nodes and pods scheduled

tolerations:
- key: "key1"
  operator: "Exists"
  effect: "NoSchedule"

### Headless Service :

virtual cluser :namespace

cluster ip is that is given to be and svc in kubernetes

![preview](/practice/images/63.PNG)

it has take pods ip which are in the nodes taken as reference state less


### Storage solutions K8s

   mostly used storage type 1. Volumes 2.Persistant volumes i.. Storage classes ii..Persistant volume claims
 
 * Volumes: life time of pod ...mounted containers
    the types
    * storage on cloud
       * ebs
       * azure disk
       * efs
       * azure file
       * gcs 
    * empty dir
    * Hostpath
  
azure supports storage classes in azure
aws supports storage class in aws


creats a persistant volume claims

RWO - ReadWriteOnce
ROX - ReadOnlyMany
RWX - ReadWriteMany
RWOP - ReadWriteOncePod

 * ReadWriteOnce
the volume can be mounted as read-write by a single node. ReadWriteOnce access mode still can allow multiple pods to access the volume when the pods are running on the same node.
ReadOnlyMany
the volume can be mounted as read-only by many nodes.
ReadWriteMany
the volume can be mounted as read-write by many nodes.
ReadWriteOncePod
FEATURE STATE: Kubernetes v1.27 [beta]
the volume can be mounted as read-write by a single Pod. Use ReadWriteOncePod access mode if you want to ensure that only one pod across whole cluster can read that PVC or write to it. This is only supported for CSI volumes and Kubernetes version 1.22+.


```
kubectl get pvc
kubectl get pv
kubectl get sc
```
![preview](/practice/images/64.PNG)

![preview](/practice/images/65.PNG)

![preview](/practice/images/66.PNG)

![preview](/practice/images/67.PNG)

![preview](/practice/images/68.PNG)

delete and check the pod

![preview](/practice/images/69.PNG)

![preview](/practice/images/70.PNG)

![preview](/practice/images/71.PNG)

![preview](/practice/images/72.PNG)

## Name spaces ...

kubectl create ns somanath

kubectl get ns somanath

![preview](/practice/images/73.PNG)



### configmaps

kubectl get cm 

![preview](/practice/images/74.PNG)

kubectl exec alpine-config-env -- printenv

![preview](/practice/images/75.PNG)

* change the configmaps adding key 

env ...key /key
enfrom... all the keys at a time

cross check the pod  print env 

environmental variables created when the pod is created

create mysql pod with configmaps
and config maps

kubectl get cm 
kubectl describe cm cmname

![preview](/practice/images/76.PNG)

using volume mounts containers
 configmaps apply

![preview](/practice/images/77.PNG)

![preview](/practice/images/78.PNG)

### secrets to deal with confidential data k8s has secrets
  
  encoding and decodding

***  Base64 ,,,,vaults

![preview](/practice/images/79.PNG)

kubectl describe secret mysql-sec

 kubectl exec -it mysql -- mysql -u shiva -p

 ![preview](/practice/images/80.PNG)

  ![preview](/practice/images/81.PNG)



  #### creating ecr in linux

  *  create ec2 machine  
  *  login ssh to ec2 machine
  *  install docker & check docker version
  ```
    1. download the script
   
      $ curl -fsSL https://get.docker.com -o install-docker.sh
   
    2. verify the script's content
   
      $ cat install-docker.sh
   
    3. run the script with --dry-run to verify the steps it executes
   
      $ sh install-docker.sh --dry-run
   
    4. run the script either as root, or using sudo to perform the installation.
   
      $ sudo sh install-docker.sh
    5. sudo usermod -aG docker ubuntu

  ```

  *  install aws cli
     
     ``` 
     curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
     ls
     sudo apt install unzip
     unzip awscliv2.zip
     sudo ./aws/install
     aws --version
     ```
   * create docker file and image run container and check status
     ```
     sudo service docker start
     vi Dockerfile

```
FROM tomcat:8-jdk8 
LABEL author="somanath" project="mysoul" organization="sai priya"
ARG DOWNLOAD_URL=https://referenceapplicationskhaja.s3.us-west-2.amazonaws.com/gameoflife.war 
ARG HOME_DIR=/usr/local/tomcat/webapps
RUN apt update 
WORKDIR ${HOME_DIR}
ADD ${DOWNLOAD_URL} ${HOME_DIR}/gameoflife.war
EXPOSE 8080
CMD ["catalina.sh","run"]
```

     docker build -t gameoflife .
     docker images --filter reference=gameoflife
     docker image ls
     docker run -d -P --name gameoflife gameoflife
     docker container ls
     docker container ls -a
     ```
   * create IAM user in aws and setup security credentials
    ```
    Policy name set
   
   use the IAM creadentials and login to the liux
    ```
   * create ecr registry in aws use the commands

   ```

   Retrieve an authentication token and authenticate your Docker client to your registry.
Use the AWS CLI:

aws ecr get-login-password --region ap-south-1 | docker login --username AWS --password-stdin 985724238893.dkr.ecr.ap-south-1.amazonaws.com
Note: if you receive an error using the AWS CLI, make sure that you have the latest version of the AWS CLI and Docker installed.
Build your Docker image using the following command. For information on building a Docker file from scratch, see the instructions here . You can skip this step if your image has already been built:

docker build -t somanath .
After the build is completed, tag your image so you can push the image to this repository:

docker tag somanath:latest 985724238893.dkr.ecr.ap-south-1.amazonaws.com/somanath:latest
Run the following command to push this image to your newly created AWS repository:

docker push 985724238893.dkr.ecr.ap-south-1.amazonaws.com/somanath:latest

   ```

  
   

