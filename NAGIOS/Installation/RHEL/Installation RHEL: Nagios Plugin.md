# README Installing Nagious Plugin

# !!! YOU MUST HAVE A RHEL SUBSCRIPTION TO FINISH THIS STEPS !!!!

Nagios Core needs plugins to operate properly.

The following steps will walk you through installing Nagios Plugins.

> These steps install nagios-plugins 2.2.1. Newer versions will become available in the future and you can use those in the following installation steps. Please see the [releases page on GitHub](https://github.com/nagios-plugins/nagios-plugins/releases) for all available versions.

Please note that the following steps install most of the plugins that come in the *Nagios Plugins package*. 

However there are some plugins that require other libraries which are not included in those instructions. 

Please refer to the following KB article for detailed installation instructions:

[Documentation - Installing Nagios Plugins](https://support.nagios.com/kb/article.php?id=569) From Source


## RHEL

[Installing Plugins](https://support.nagios.com/kb/article/nagios-core-installing-nagios-core-from-source-96.html#RHEL) 

### Prerequisites

Make sure that you have the following packages installed.
```
===== RHEL 7.x =====

cd /tmp
wget https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
sudo rpm -ihv epel-release-latest-7.noarch.rpm

    # Only if RHEL is registered
    
sudo subscription-manager repos --enable=rhel-7-server-optional-rpms

sudo yum install -y gcc glibc glibc-common make gettext automake autoconf wget openssl-devel net-snmp net-snmp-utils
sudo yum install -y perl-Net-SNMP
```

...