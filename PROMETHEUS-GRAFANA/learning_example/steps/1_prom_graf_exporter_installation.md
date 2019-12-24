# Installation

## Prometheus installation

As root
```
cd prometheus-course/scripts
./1-install.sh

ps -ef | grep prometheus
```

Check availability of Prometheus web frontend: http://<server IP>:9090

## Grafana installation

As root
```
cd prometheus-course/scripts
./3-install-grafana.sh

ps -ef | grep grafana
```

Check availability of Grafana web frontend: http://<server IP>:3000
> Default credentials: admin/admin


## Node-exporter installation

### Install

As root
```
cd prometheus-course/scripts
./2-node-exporter.sh

ps -ef | grep node_exporter
```

### Check availability of node-exporter

```
curl <node-exporter_server_ip>:9100
```


### Add node-exporter to the Prometheus

Find Prometheus process
```
ps -ef | grep -i prometheus
```

Add something similar to the `prometheus.yml` config file
```
vi /etc/prometheus/prometheus.yml

  - job_name: 'node_exporter'
    scrape_interval: 5s
    static_configs:
      - targets: ['localhost:9100']
```

Apply changes in `prometheus.yml` config file, with no prometheus process re-start
```
kill -SIGHUB <prometheus_process_id>
```

Make sure new configs for new node exporter are visible under `http://<prometheus_server_id>:9090/config`



