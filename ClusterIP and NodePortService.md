##Create NodePort Service to expose Pods

Vi nginx-nodeport.yaml

apiVersion: v1
kind: Service
metadata:
  name: nginx-service
  labels:
    app: nginx
spec:
  selector:
    app: nginx
  ports:
    - protocol: TCP
      port: 80
      targetPort: 80
      nodePort: 30007  # specify the node port here
  type: NodePort

##Create Cluster IP Service

Vi nginx-service.yaml

apiVersion: v1
kind: Service
metadata:
  name: nginx-service
  labels:
    app: nginx
spec:
  selector:
    app: nginx
  ports:
    - protocol: TCP
      port: 80
      targetPort: 80
  type: ClusterIP

Commands:
##Kubectl get svc

EKS $ kubectl get svc
NAME            TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)        AGE
kubernetes      ClusterIP   10.100.0.1       <none>        443/TCP        91m
nginx-service   NodePort    10.100.201.137   <none>        80:30007/TCP   17m



