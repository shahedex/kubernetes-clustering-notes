# Setting up Centos VM for Kubernetes

## Set hostname for master and workers

```console
$ sudo vi /etc/hosts
```

Enter the ip and hostname on the hosts file.

or

```console
$ cat >>/etc/hosts<<EOF
xxx.xxx.xxx.xxx hostname
xxx.xx.xxx.xx hostname2
EOF
```

## Install docker and start docker service

```console
$ yum install -y docker
$ systemctl enable docker
$ systemctl start docker
```

## Disable SELinux

```console
$ setenforce 0
```

