# Up the cluster and adding nodes

## On Master node

### Initialize Kubernetes cluster with the pod network

```console
$ kubeadm init --apiServer-advertise-address=192.168.31.180 --pod-network-cidr=172.17.0.1/16
```

### Run the commands using regular user to copy kubeconfig to use the cluster

```console
  mkdir -p $HOME/.kube
  sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
  sudo chown $(id -u):$(id -g) $HOME/.kube/config
```

### Deploy Calico network for worker node communication

```console
$ kubectl create -f https://docs.projectcalico.org/v3.9/manifests/calico.yaml
```

### Print join command for nodes to join the cluster

```console
$ kubeadm token create --print-join-command
```

## On Worker node

### Run the Cluster join command

```console
$ kubeadm join 192.168.31.180:6443 --token nk90mj.q21p0erx8mh8tlfe     --discovery-token-ca-cert-hash sha256:c4087fd96173a03f862690b11164ee40f5097425fff56ec6efb8812ddad6a0e9 
```


## On Master node (Control plane)

### Getting the nodes of the cluster

```console
$ kubectl get nodes

or 

$ kubectl get nodes -o wide
```

### Show cluster info

```console
$ kubectl cluster-info
```
