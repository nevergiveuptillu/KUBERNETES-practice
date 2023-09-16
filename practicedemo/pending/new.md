RBAC
•	Authorization in K8s Refer Here
 
•	Authentication in k8s Refer Here
 
•	Attaching Authorization to identity using Bindings
•	RoleBinding
•	ClusterRoleBinding
•	Refer Here for creating users and setting permissions
DevOps Classroomnotes 13/May/2023
Topics
•	AKS
•	EKS
•	Helm/Kustomize
•	ingress
•	hpa
Managed K8s
•	Managed K8s cluster will manage master nodes i.e. we don’t have explicit access to master nodes
•	so cluster administrational activities such as
•	backing up k8s cluster
•	upgrading k8s cluster
•	cloud controller manager configurations to
•	have access to native cloud networks
•	have csi implementations specific to cloud provider
•	have cni implemenations specific to cloud provider
•	Cloud providers charge hourly for cluster and they give sla’s

Helm
•	Helm is a package manager for k8s
•	In helm we have repositories where charts are defined
•	An helm chart is analogus to package (apt package)
•	install helm Refer Here
•	Manifests are static in nature, to add reusability and dynamic nature to manifests we have two options
•	helm:
•	this uses templated approach
•	this was present from earlier days of k8s
•	kustomize:
•	this uses override approach
•	this is natively supported in kubectl (recent additions)
•	Refer Here for the basic chart created
 

Kustomize
•	Kustomize is a tool where we can natively manage configurations
•	Refer Here for kustomize
•	Natively manage dynamic configurations to k8s manifests
•	Lets write a k8s manifest
•	to deploy shaikkhajaibrahim/dashboardservice:1.0.0 which runs on 80 port
•	create a service file exposed as LoadBalancer
•	Refer Here for manifests
•	Refer Here for tutorial from vultr to use kustomize
•	Refer Here for the manifest folder structure
•	Now lets add name prefix per environment
•	Refer Here for nameprefix docs.
•	Refer Here for the changes done
 
•	Refer Here for labels per env
•	Refer Here for kustomize examples
Problem – 1
•	Creating a Load Balancer for every service shoots up cloud costs
•	I would like to perform
•	path based routing
•	hostname based routing
•	Solution:
•	Ingress which provides external access to k8s services
Questions
1.	How to check logs of pods
2.	What are events in k8s
3.	why should i use k8s
4.	What are stateful sets?
5.	What is purpose of headless service?
6.	What is CSI ?
7.	What is CNI ?
8.	What is the last problem which you faced in k8s ?
9.	How to use external vault in k8s
10.	How to backup k8s cluster?
11.	How to upgrade the k8s cluster?
12.	what is draining the node vs cordon the node?
13.	Can we implement custom dns in k8s?
14.	What is default dns in k8s?
15.	communication between two services in different namespaces
16.	How to auto scale nodes in aks/eks? cluster node autoscaler
17.	List down atleast 10 most common k8s failures?
DevOps Classroomnotes 14/May/2023
Ingress
•	To understand concept of ingress Refer Here
•	In k8s we have 3 major objects which will help in ingress (layer 7 loadbalancing)
•	ingress
•	ingressController: This is a third party implementation Refer Here
•	ingressClass
•	K8s doesnot have controller for ingress.
•	Lets create four simple applicatons Refer Here for changes done
•	Create docker image and push them to registry
•	For this classroom purpose i will be using nginx-ingress-controller Refer Here
•	Our implementation:
 
•	lets install nginx-ingress controller using helm
helm repo add nginx-stable https://helm.nginx.com/stable
helm repo update
helm upgrade --install ingress-nginx ingress-nginx \
             --repo https://kubernetes.github.io/ingress-nginx \
             --namespace ingress-nginx --create-namespace
 
* After last command we see output which better copy to some notepad
* Now execute the following command to watch for external ip to nginx ingress controller kubectl --namespace ingress-nginx get services -o wide -w ingress-nginx-controller
 
* Get ingress classes and there should be nginx ingress class from helm chart
 
* lets deploy application and services. Refer Here for the changes
 
 
* Refer Here for the manifest file for ingress
* Now create ingress object
 
* Get external ip of ingress controller using kubectl --namespace ingress-nginx get services -o wide -w ingress-nginx-controller
 
 
* Refer Here for official docs of ingress
Node autoscaler
•	Refer Here for aks cluster autoscaler
•	Refer Here for eks cluster autoscaler

