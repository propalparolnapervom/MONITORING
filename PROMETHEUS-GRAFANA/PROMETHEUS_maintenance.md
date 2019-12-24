# PROMETHEUS MAINTENANCE

## CONFIGURATION

Start process
```
/usr/local/bin/prometheus --config.file prometheus.yml
```

Apply changes in `prometheus.yml` config file, with no prometheus process re-start
```
kill -SIGHUB <prometheus_process_id>
```

## LIST

Actual Prometheus configuration is available via `http://<prometheus_server_id>:9090/config`


List exposed metrics
```
    # `/metrics` endpoint is by default, actual one can be specified for the target 
    # within `prometheus.yml` config file
    #
    # http://<necessary_target_server_ip>:<necessary_target_server_port>/metrics
curl http://<necessary_target_server_ip>:<necessary_target_server_port>/metrics
```









