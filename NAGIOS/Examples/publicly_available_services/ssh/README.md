# README

[Monitoring Publicly Available Services](https://assets.nagios.com/downloads/nagioscore/docs/nagioscore/4/en/monitoring-publicservices.html)

## WHAT

Following service has to be monitored on the remote host:
    - SSH

## LINKS

[Main Config File](https://assets.nagios.com/downloads/nagioscore/docs/nagioscore/4/en/configmain.html#cfg_file)

Objects used:
  1) [host](https://assets.nagios.com/downloads/nagioscore/docs/nagioscore/4/en/objectdefinitions.html#host)


## STEPS

1. Put `remote_1.cfg` file to the `/usr/local/nagios/etc/objects` dir on the monitor server.

2. Update Nagios config file to point to the just placed file:

```
sudo vi /usr/local/nagios/etc/nagios.cfg

...
# Definitions for monitoring the SSH on the `remote_1` server
cfg_file=/usr/local/nagios/etc/objects/remote_1.cfg
...
```

3. Validate just updated files

```
sudo /usr/local/nagios/bin/nagios -v /usr/local/nagios/etc/nagios.cfg
```

4. Restart Nagios.

```
sudo systemctl restart nagios.service

OR

sudo systemctl stop nagios.service
sudo systemctl start nagios.service
```











