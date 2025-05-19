
# Kubernetes + Helm Cheat Sheet

## 🧩 Kubernetes Command Cheat Sheet

### 🔍 Cluster & Namespace Info
```
kubectl config current-context
kubectl config get-contexts
kubectl config use-context <context-name>

kubectl get namespaces
kubectl config set-context --current --namespace=<ns>
```

### 🚀 Basic kubectl Operations
```
kubectl get all
kubectl get pods
kubectl get svc
kubectl get deployments
kubectl describe pod <pod-name>
kubectl logs <pod-name>
kubectl exec -it <pod-name> -- /bin/sh
```

### ⚙️ Create / Apply / Delete Resources
```
kubectl apply -f <file>.yaml
kubectl delete -f <file>.yaml
kubectl delete pod <pod-name>
kubectl replace -f <file>.yaml
kubectl edit deployment <name>
```

### 🔎 Label, Selector & Debug
```
kubectl get pods -l app=myapp
kubectl describe deployment <name>
kubectl get events --sort-by=.metadata.creationTimestamp
```

## 📄 YAML Snippets (Quick Templates)

### Deployment
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: myapp
spec:
  replicas: 2
  selector:
    matchLabels:
      app: myapp
  template:
    metadata:
      labels:
        app: myapp
    spec:
      containers:
        - name: myapp
          image: busybox:1.36
          command: ["sleep", "3600"]
```

### Service
```yaml
apiVersion: v1
kind: Service
metadata:
  name: myapp-svc
spec:
  selector:
    app: myapp
  ports:
    - protocol: TCP
      port: 80
      targetPort: 8080
  type: ClusterIP
```

## 🛠️ Helm Cheat Sheet

### 🔧 Helm Basics
```
helm repo add bitnami https://charts.bitnami.com/bitnami
helm repo update

helm search repo nginx
helm install my-nginx bitnami/nginx
helm list
helm uninstall my-nginx
```

### 🔄 Upgrade / Rollback
```
helm upgrade my-nginx bitnami/nginx --set service.type=LoadBalancer
helm rollback my-nginx 1
```

### 📁 Helm Chart Structure
```
mychart/
├── Chart.yaml
├── values.yaml
└── templates/
    ├── deployment.yaml
    ├── service.yaml
```

### 📝 Values Override
```
helm install myapp ./mychart -f prod-values.yaml
```

## 📌 Quick Best Practices
- Use `labels` to manage & select resources effectively
- Use `namespaces` to isolate environments (e.g., dev, test)
- Store secrets securely (use `Secret` instead of hardcoding)
- Always check `kubectl get events` when debugging
- Use Helm for reusable, versioned app deployments
