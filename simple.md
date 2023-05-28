# manifest for httpd
---
apiVersion: v1
kind: Pod
metadata:
  name: httpd
spec:
  containers:
  - name: httpd
    image: httpd
    ports:
    - containerPort: 80
---
# manifest for jenkins
---
apiVersion: v1
kind: Pod
metadata:
  name: jenkins
spec:
  containers:
  - name: jenkins
    image: jenkins/jenkins
    ports:
    - containerPort: 8080

# api reference yaml writing 

---
apiVersion: v1
kind: Pod
metadata:
  name: httpd:pod
spec:
  containers:
    - name: httpd-container
      image: httpd:2
      ports:
        - containerPort: 80
---
apiVersion: v1
kind: Pod
metadata:
  name: alpine
spec:
  containers:
    - name: alpine
      image: alpine:3.18
      args:
        - sleep
        - 1d
---
# Kubectl autocomplete
``` .md
source <(kubectl completion bash) # set up autocomplete in bash into the current shell, bash-completion package should be installed first.
echo "source <(kubectl completion bash)" >> ~/.bashrc # add autocomplete permanently to your bash shell.
```
git clone ---own resource
kubectl apply -f
kubectl get <api-resource>
kubectl describe <kind> <name> 
kubectl get <kind> <name> -o yaml
kubectl delete 


#exercises

* write a manifest file to create
 
•	nginx
---
apiVersion: v1
kind: Pod
metadata: 
  name: exec1
spec:
  containers:
    - name: nginx
      image: nginx:latest
      ports:
        - containerPort: 80

•	nginx and alpine with sleep 1d

---
apiVersion: v1
kind: Pod
metadata: 
  name: exec2
spec:
  containers:
    - name: nginx
      image: nginx:latest
      ports:
        - containerPort: 80
    - name: alpine
      image: alpine:3.18
      args: 
        - sleep
        - 1d
      
    

•	nginx ,alpine with sleep 1d and alpine with 10s

---
apiVersion: v1
kind: Pod
metadata: 
  name: exec3
spec:
  containers:
    - name: nginx
      image: nginx:latest
      ports:
        - containerPort: 80
    - name: alpine
      image: alpine:3.18
      args: 
        - sleep
        - 1d
    - name: alpine
      image: alpine:3.18
      args: 
        - sleep
        - 10s

•	nginx and httpd with 80 port exposed
---
apiVersion: v1
kind: Pod
metadata: 
  name: exec4
spec:
  containers:
    - name: nginx
      image: nginx:latest
      ports:
        - containerPort: 80
    - name: httpd
      image: httpd:latest
      ports:
        - containerPort: 80

# Managing Kubernetes Objects Using Imperative Commands
  ![referhere](https://kubernetes.io/docs/tasks/manage-kubernetes-objects/imperative-command/)

# pod lifecycle

![referhere](https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/)
 
 * Pending : The Pod has been accepted by the Kubernetes cluster, but one or more of the containers has not been set up and made ready to run. This includes time a Pod spends waiting to be scheduled as well as the time spent downloading container images over the network.
 * Running :	The Pod has been bound to a node, and all of the containers have been created. At least one container is still running, or is in the process of starting or restarting.
 * Succeeded : All containers in the Pod have terminated in success, and will not be restarted.
 * Failed	: All containers in the Pod have terminated, and at least one container has terminated in failure. That is, the container either exited with non-zero status or was terminated by the system.
 * Unknown : For some reason the state of the Pod could not be obtained. This phase typically occurs due to an error in communicating with the node where the Pod should be running.


