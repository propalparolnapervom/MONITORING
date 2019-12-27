# Installation of necessary components

## Prometheus

As root
```
cd prometheus-course/scripts
./1-install.sh

ps -ef | grep prometheus
```

Check availability of Prometheus web frontend: http://<server IP>:9090


## Grafana

As root
```
cd prometheus-course/scripts
./3-install-grafana.sh

ps -ef | grep grafana
```

Check availability of Grafana web frontend: http://<server IP>:3000
> Default credentials: admin/admin


## Node-exporter

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

Apply changes in `prometheus.yml` config file, via prometheus process re-start
```
service prometheus restart
service prometheus status
```

Make sure new configs for new node exporter are visible under `http://<prometheus_server_id>:9090/config`


## Alertmanager

As root
```
cd prometheus-course/scripts
./4-install-alertmanager.sh
```

Do necessary (updated for you) steps, described at the end of installation output.
```
vi /etc/alertmanager/alertmanager.yml

global:
  smtp_smarthost: 'localhost:25'
  smtp_from: 'alertmanager@xburser.com'
  smtp_auth_username: ''
  smtp_auth_password: ''
  smtp_require_tls: false

templates:
- '/etc/alertmanager/template/*.tmpl'

route:
  repeat_interval: 1h
  receiver: operations-team

receivers:
- name: 'operations-team'
  email_configs:
  - to: '<mine_email>'
  slack_configs:
  - api_url: https://hooks.slack.com/services/<mine_slack_hook>
    channel: '#test-test'
    send_resolved: true

```

Start Alertmanager
```
service alertmanager restart
service alertmanager status
ps -ef | grep -i alert
```


Add something similar to the `prometheus.yml` config file
```
vi /etc/prometheus/prometheus.yml

alerting:
  alertmanagers:
  - static_configs:
    - targets:
      - localhost:9093
```

Apply changes in `prometheus.yml` config file, via prometheus process re-start
```
service prometheus restart
service prometheus status
```

Make sure new configs for new node exporter are visible under `http://<prometheus_server_id>:9090/config`



Check availability of Alertmanager web frontend: http://<server IP>:9093

