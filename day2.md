# Kubernetes
## Kubernetes
Source: https://kubernetes.io/docs/concepts/overview/what-is-kubernetes/
![Stack](https://d33wubrfki0l68.cloudfront.net/26a177ede4d7b032362289c6fccd448fc4a91174/eb693/images/docs/container_evolution.svg)
Feature:
1. Service discovery and load balancing 
2. Storage orchestration
3. Automated rollouts and rollbacks
4. Automatic bin packing
5. Self-healing
6. Secret and configuration management



Source: https://kubernetes.io/docs/concepts/overview/components/
![Kubernetes Component](https://d33wubrfki0l68.cloudfront.net/2475489eaf20163ec0f54ddc1d92aa8d4c87c96b/e7c81/images/docs/components-of-kubernetes.svg)

# Kubernetes Object
## Pod
## Deployment
## Services


# Labs
pod
tesing pods
```
kubectl run network-mutlitool --image praqma/network-multitool
```
app
```
cat <<EOF | kubectl apply -f -
apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  labels:
    run: flask
  name: flask
spec:
  containers:
  - image: footprns/flask:0.1
    name: flask
    ports:
    - containerPort: 5000
    resources: {}
  dnsPolicy: ClusterFirst
  restartPolicy: Always
status: {}
EOF
```
check the pods ip `$ kubectl get pods -o wide`
exec to network-tools `$ kubectl exec network-mutlitool -it -- /bin/sh`


# How to connect to K8s cluster
```
gcloud container clusters get-credentials single-k8s --zone asia-southeast2-a --project k8s-3days
```

## Create Deployment
```
cat <<EOF | kubectl apply -f -
apiVersion: apps/v1
kind: Deployment
metadata:
  creationTimestamp: null
  labels:
    app: flask
  name: flask
spec:
  replicas: 2
  selector:
    matchLabels:
      app: flask
  strategy: {}
  template:
    metadata:
      creationTimestamp: null
      labels:
        app: flask
    spec:
      containers:
      - image: footprns/flask:0.2
        name: flask
        resources: {}
status: {}
EOF
```

create service
```
cat <<EOF | kubectl apply -f -
apiVersion: v1
kind: Service
metadata:
  creationTimestamp: null
  labels:
    app: flask-svc
  name: flask-svc
spec:
  ports:
  - name: 80-5000
    port: 80
    protocol: TCP
    targetPort: 5000
  selector:
    app: flask
  type: LoadBalancer
status:
  loadBalancer: {}
EOF
```