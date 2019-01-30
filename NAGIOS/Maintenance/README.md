# README



## Bounce Nagios
```
===== Ubuntu 14.x =====

sudo start nagios
sudo stop nagios
sudo restart nagios
sudo status nagios
 

===== Ubuntu 15.x / 16.x / 17.x / 18.x =====

sudo systemctl start nagios.service
sudo systemctl stop nagios.service
sudo systemctl restart nagios.service
sudo systemctl status nagios.service
```


## Debug config files
```
sudo /usr/local/nagios/bin/nagios -v /usr/local/nagios/etc/nagios.cfg
```

