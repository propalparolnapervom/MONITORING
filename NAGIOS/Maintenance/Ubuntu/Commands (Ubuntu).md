# COMMANDS (UBUNTU)

Different Linux distributions have different methods of starting / stopping / restarting / status Nagios.

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