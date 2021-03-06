# Stress test of a Kubernetes Cluster with replicas

## Deployment file for stress testing pod

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: stress-test
  labels:
    app: stress
spec:
  replicas: 30
  selector:
    matchLabels:
      app: stress
  template:
    metadata:
      labels:
        app: stress
    spec:
      containers:
      - name: memory-demo-ctr
        image: polinux/stress
        resources:
          limits:
            memory: "200Mi"
          requests:
            memory: "100Mi"
        command: ["stress"]
        args: ["--vm", "1", "--vm-bytes", "150M", "--vm-hang", "1"]

```
