# Nginx Ingress Controller installation on Kubernetes

## Mandatory command to run every type of deployments

```console
$ kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/master/deploy/static/mandatory.yaml
```

## Baremetal isntallation with nodeport 

```console
$ kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/master/deploy/static/provider/baremetal/service-nodeport.yaml
```