# Kubernetes installation and setting up on vm

## Add yum repository

```console
$ cat >>/etc/yum.repos.d/kubernetes.repo<<EOF
[kubernetes]
name=Kubernetes
baseurl=https://packages.cloud.google.com/yum/repos/kubernetes-el7-x86_64
enabled=1
gpgcheck=1
repo_gpgcheck=1
gpgkey=https://packages.cloud.google.com/yum/doc/yum-key.gpg
        https://packages.cloud.google.com/yum/doc/rpm-package-key.gpg
EOF
```

## Install kubernetes

```console
$ yum install -y kubeadm kubelet kubectl
```

## Enable and start kubelet service

```console
$ systemctl enable kubelet
$ systemctl start kubelet
```
