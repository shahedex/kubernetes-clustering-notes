# Up the cluster and adding nodes

## On Master node

## For Flannel Network
### Initialize Kubernetes cluster with the pod network CIDR

```console
$ sudo kubeadm init --pod-network-cidr=10.244.0.0/16
```

### Run the commands using regular user to copy kubeconfig to use the cluster

```console
  mkdir -p $HOME/.kube
  sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
  sudo chown $(id -u):$(id -g) $HOME/.kube/config
```

### Deploy Fannel network for worker node communication

```console
$ kubectl apply -f https://github.com/coreos/flannel/raw/master/Documentation/kube-flannel.yml
```

### If there is any Error or CrashLoopBackOff - Run RBAC module

```console
$ kubectl create -f https://raw.githubusercontent.com/coreos/flannel/master/Documentation/kube-flannel-rbac.yml
```

## For any errors on CNI
"cni0" already has an IP address different from 10.244.2.1/24。 

Error while adding to cni network: failed to allocate for range 0: no IP addresses available in range set: 10.244.2.1-10.244.2.254

  - rm -rf /var/lib/cni/flannel/* && rm -rf /var/lib/cni/networks/cbr0/* && ip link delete cni0  
  - rm -rf /var/lib/cni/networks/cni0/*
  - kubeadm reset
  - kubeadm join

  
## For Calico
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

## Tainting the Host
If you want to run workloads on master node

```console
$ kubectl taint nodes --all node-role.kubernetes.io/master-
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
