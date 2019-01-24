# README Installing Nagious Plugin

Nagios Core needs plugins to operate properly.

The following steps will walk you through installing Nagios Plugins.

> These steps install nagios-plugins 2.2.1. Newer versions will become available in the future and you can use those in the following installation steps. Please see the [releases page on GitHub](https://github.com/nagios-plugins/nagios-plugins/releases) for all available versions.

Please note that the following steps install most of the plugins that come in the *Nagios Plugins package*. 

However there are some plugins that require other libraries which are not included in those instructions. 

Please refer to the following KB article for detailed installation instructions:

[Documentation - Installing Nagios Plugins](https://support.nagios.com/kb/article.php?id=569) From Source



## UBUNTU

[Installing Plugins](https://support.nagios.com/kb/article/nagios-core-installing-nagios-core-from-source-96.html#Ubuntu) 

### Prerequisites

Make sure that you have the following packages installed.
```
sudo apt-get install -y autoconf gcc libc6 libmcrypt-dev make libssl-dev wget bc gawk dc build-essential snmp libnet-snmp-perl gettext
```

### Downloading The Source

```
cd /tmp
wget --no-check-certificate -O nagios-plugins.tar.gz https://github.com/nagios-plugins/nagios-plugins/archive/release-2.2.1.tar.gz
tar zxf nagios-plugins.tar.gz
```

### Compile + Install

```
cd /tmp/nagios-plugins-release-2.2.1/
sudo ./tools/setup
sudo ./configure
sudo make
sudo make install
```

### Test Plugins

Point your web browser to the *Public IP/Public DNS* of your Nagios Core server, for example:

```
http://18.194.233.190/nagios

http://ec2-18-194-233-190.eu-central-1.compute.amazonaws.com/nagios
```

Go to a `host` or `service` object and "Re-schedule the next check" under the Commands menu. 

The error you previously saw should now disappear and the correct output will be shown on the screen.









