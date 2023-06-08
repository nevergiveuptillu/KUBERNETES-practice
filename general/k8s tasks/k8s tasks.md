
### Kubernetes Activities 
  ## Day 1.  26-04-2023
   1. Write a Pod Spec for Spring Pet Clinic and 
   nopCommerce Applications

     `* 1. Pod Spec for Spring Pet Clinic`

     ``` yaml
      apiVersion: v1
      kind: Pod
      metadata:
        name: pod-spc
        labels:
          app: spc
      spec:
        containers:
          - name: spc
            image: shivasomanath/spc:1.0
            ports:
             - containerPort: 8080  
      
      ```     
     ![preview](/general/k8s%20tasks/tasksresults/1.PNG)

     ![preview](/general/k8s%20tasks/tasksresults/2.PNG)

      `* 2. Pod spec for nop commerce`

    


   2. Execute the kubectl commands: kubectl get pods 
   and describe pods

  ## Day 2. 27-04-2023
   1. Explain Kubernetes architecture
   2.Setup k8s on single node using minikube and kind 
   3.Run the Spring Pet Clinic by manifest
   Day 3. 28-04-2023
   1. K8s Cluster Installation
   a. Kubeadm
   b.Minikube
   c. Kind
   2. Writing the Manifest Files for Spring Pet Clinic and 
   nopCommerce App
   3.Writing the Manifest Files for Game of Life App
   4.Create Jobs & CronJobs
   5.Create the ReplicaSet and Replication controller
   6.Writing the LABELS and Selecting the LABELS using 
   selector concept
   Day 4. 04-05-2023
   1.Theory concepts of k8s
   a. Pods / Containers
   b.Jobs / CronJobs
   c. ReplicaSets
   d.Deployment
   e. Service / Headless Service
   f. Volumes / Persistent Volumes / Persistent 
   Volume Claims
   g.Stateful Sets 
   h. Namespaces and
   i. Other till upto classroom concepts covered so 
   far
   Day 5. 05-05-2023
   1. Create a mysql pod with stateful set with 1 replica
   2. Create a nopCommerce deployment with 1 replica 
   3. Create a Headless service to interact nopCommerce
   with mysql
   4. Create a Load balancer to expose nop to external
   Day 6. 09-05-2023
   1.Create a Kubernetes cluster using kubeadm
   2.Deploy any application using kubectl
   3.Backup Kubernetes I.e., backup etcd
   4.List out all the pod’s running in kube system 
   namespace
   5.Write down all the steps required to make 
   Kubernetes highly available
   6.Do a rolling update and roll back
   7.Ensure usage of secret in MySQL and configmaps
   8.Create a nop commerce deployment with MySQL 
   statefulset and nop deployment
   Day 7. 10-05-2023
   1.Node selector task by
   a. Node selector
   b.Affinity
   c. Taints and Tolerances
   2.K8s cluster Upgrade from 1.25 to 1.27
   Day 8. 16-05-2023
   1.Installing EKS and Aks
   2.installations using helm chart
   a. mysql
   b.postgres
   c. mongodb
   d.redis cache
   3.write kustomize file by creating files for 3 
   environments
   a. dev
   b.qa
   c. test