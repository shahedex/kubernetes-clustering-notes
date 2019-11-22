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
$ yum install -y docker
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

