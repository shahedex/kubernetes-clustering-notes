## Example 
This is simple example showing:
- Service `service-alpha` in `service-alpha` namespace
- Service `service-beta` in `service-beta` namespace
- Nginx Ingress controller in `kube-ingress` namespace
- Ingress called `ingress-demo` inside `service-alpha` namespace 
- Ingress called `ingress-demo` inside `service-beta` namespace

## Steps:
- Install ingress on AKS. my demo cluster does not have rbac enabled that's why there is => --set rbac.create=false
helm install stable/nginx-ingress --namespace kube-ingress --set controller.replicaCount=2 --set rbac.create=false

- Get the public IP address of the ingress controller
kubectl get service -l app=nginx-ingress --namespace kube-ingress

- Add azure-samples helm repo as it contains the sample helm chart used for both `service-alpha` and `service-beta`
helm repo add azure-samples https://azure-samples.github.io/helm-charts/

The used sample => https://github.com/Azure-Samples/helm-charts/tree/master/chart-source/aks-helloworld

- Create service-alpha
```
helm install azure-samples/aks-helloworld --namespace service-alpha --set title="AKS Service Alpha" --set serviceName="service-alpha"
```

- Create service-beta
```
helm install azure-samples/aks-helloworld --namespace service-beta --set title="AKS Service Beta" --set serviceName="service-beta"
```

- Deploy the ingress route
 You need to create two ingress resources (not controllers) one in each namespace

```
kubectl apply -f ingress-route.yaml
```

This will create two ingress resources with one load balancer