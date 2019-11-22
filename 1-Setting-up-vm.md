# Setting up Centos VM for Kubernetes

## Changing own hostname

```console
$ hostnamectl set-hostname newhostname
```

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
$ yum install -y -q yum-utils device-mapper-persistent-data lvm2 > /dev/null 2>&1
$ yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo > /dev/null 2>&1
$ yum install -y -q docker-ce >/dev/null 2>&1

$ systemctl enable docker
$ systemctl start docker
```

## Check docker status 

```console
$ systemctl status docker
```

## Disable SELinux (temporary)

```console
$ setenforce 0
```

## Permanently disable SELinux

```console
$ sed -i --follow-symlinks 's/^SELINUX=enforcing/SELINUX=disabled/' /etc/sysconfig/selinux
```

## Disable and Stop firewall

```console
$ systemctl disable firewalld
$ systemctl stop firewalld
```

## Disable swap permanently

```console
$ sed -i '/swap/d' /etc/fstab
$ swapoff -a
```

## Recommended sysctl settings for Kubernetes networking

```console
$ cat >>/etc/sysctl.d/kubernetes.conf<<EOF
net.bridge.bridge-nf-call-ip6tables = 1
net.bridge.bridge-nf-call-iptables = 1
EOF

# apply the configuration
$ sysctl --system
```