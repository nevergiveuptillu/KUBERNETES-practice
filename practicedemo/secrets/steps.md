1. Encode the new password string:

echo -n 'birdsarentreal' | base64

YmlyZHNhcmVudHJlYWw=

2. data \

---
apiVersion: v1
kind: Secret
metadata:
  name: mysecret
type: Opaque
data:
  username: YWRtaW4=
  password: YmlyZHNhcmVudHJlYWw=

3. Apply the manifest to your cluster:

kubectl apply -f ./secret.yaml

kubectl apply -f ./secret.yaml

kubectl delete secret mysecret

<!-- https://kubernetes.io/docs/tasks/configmap-secret/managing-secret-using-config-file/#edit-secret -->