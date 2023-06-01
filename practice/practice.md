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


replica set

![preview](/practice/images/26.PNG)

![preview](/practice/images/27.PNG)

* kubectl get rs
* kubectl describe rs name
* kubectl scale --replicas=5 rs/name
* kubectl delete pod name
* Labels and Selectors
  Labels are key/value pairs that are attached to objects such as Pods. Labels are intended to be used to specify identifying attributes of objects that are meaningful and relevant to users, but do not directly imply semantics to the core system. Labels can be used to organize and to select subsets of objects. Labels can be attached to objects at creation time and subsequently added and modified at any time. Each object can have a set of key/value labels defined. Each Key must be unique for a given object.

"metadata": {
  "labels": {
    "key1" : "value1",
    "key2" : "value2"
  }
}
Labels allow for efficient queries and watches and are ideal for use in UIs and CLIs. Non-identifying information should be recorded using annotations.

Motivation



 