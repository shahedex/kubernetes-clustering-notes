# Install Prometheus on Master

## Make necessary directories where you want to store downloaded files

```bash
$ cd /home/cloud_user
$ mkdir -p promwork
$ cd promwork
```

## Download Prometheus release

```bash
$ wget https://github.com/prometheus/prometheus/releases/download/v2.8.0-rc.0/prometheus-2.8.0-rc.0.linux-amd64.tar.gz
```

## Extract the downloaded file

```bash
tar -xvzf prom*.gz
```

## Install commands

```bash
$ cd prometheus-2.8.0-rc.0.linux-amd64
$ sudo cp prometheus /usr/local/bin
$ sudo cp promtool /usr/local/bin
$ sudo mkdir -p /etc/prometheus
$ sudo cp -r ./consoles /etc/prometheus
$ sudo cp -r ./console_libraries /etc/prometheus
$ cd ..
$ wget https://raw.github.com/linuxacademy/content-aiops-essentials/master/prometheus.yml
$ sudo cp prometheus.yml /etc/prometheus
$ wget https://raw.github.com/linuxacademy/content-aiops-essentials/master/prometheus.service
$ sudo cp prometheus.service /etc/systemd/system
```

## Reload ans start Prometheus server

```bash
$ sudo systemctl daemon-reload
$ sudo systemctl start prometheus
$ sudo systemctl status prometheus
```

## PromQL queries to interrogate your cluster

### To measure CPU utilization

    node_cpu_seconds_total

    irate(node_cpu_seconds_total{job="node"}[5m])

    avg(irate(node_cpu_seconds_total{job="node"}[5m])) by (instance)

    avg(irate(node_cpu_seconds_total{job="node",mode="idle"}[5m])) by (instance) * 100

    100 - avg(irate(node_cpu_seconds_total{job="node",mode="idle"}[5m])) by (instance) * 100

### To measure memory, use

    (node_memory_MemTotal_bytes - (node_memory_MemFree_bytes + node_memory_Cached_bytes + node_memory_Buffers_bytes)) / node_memory_MemTotal_bytes * 100