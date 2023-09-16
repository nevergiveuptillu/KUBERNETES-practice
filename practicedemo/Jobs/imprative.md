  91 kubectl run alpine --image alpine
  92 kubectl get pods
  93 kubectl get pods
  94 kubectl run nginx --image nginx
  95 kubectl get pods
  96 kubectl delete pods alpine
  97 kubectl get pods
  98 kubectl exec nginx --pwd
  99 kubectl exec nginx -- pwd
 100 kubectl exec nginx -- ls
 101 kubectl exec nginx -it -- /bin/bash
 102 ls
 103 kubectl run httpd --image httpd
 104 kubectl get pods
 105 kubectl get jobs
 106 kubectl get pods
 107 kubectl port-forward --address "0.0.0.0" httpd 8080:80
 108 kubectl port-forward --address "0.0.0.0" httpd 8080:80