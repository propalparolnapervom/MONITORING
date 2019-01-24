# README Nagios Core Installation

[Nagios Core Installation Guids](https://assets.nagios.com/downloads/nagioscore/docs/nagioscore/4/en/quickstart.html?__hstc=118811158.a53919d4e93d557baaec794e81093a95.1548065954439.1548065954439.1548071096337.2&__hssc=118811158.7.1548071096337&__hsfp=1156883818#_ga=2.25587709.1966153250.1548065953-2105078507.1548065953)

## WHAT

Setup Nagios Core to the server, which will be Monitor Server.

## UBUNTU

[Install Nagios Core on RHEL](https://support.nagios.com/kb/article/nagios-core-installing-nagios-core-from-source-96.html#Ubuntu)

Log to the server.

Install latest OS updates
```
sudo apt-get update -y
sudo apt-get upgrade -y
```

### Security-Enhanced Linux

This guide is based on SELinux being disabled or in permissive mode. SELinux is not enabled by default on Ubuntu. If you would like to see if it is installed run the following command:
```
sudo dpkg -l selinux*
```

### Prerequisites

Perform these steps to install the pre-requisite packages.
```
===== Ubuntu 18.x =====

sudo apt-get install -y autoconf gcc libc6 make wget unzip apache2 php libapache2-mod-php7.2 libgd-dev
```

### Downloading the Source

```
cd /tmp
wget -O nagioscore.tar.gz https://github.com/NagiosEnterprises/nagioscore/archive/nagios-4.4.3.tar.gz
tar xzf nagioscore.tar.gz
```

### Compile

```
cd /tmp/nagioscore-nagios-4.4.3/
sudo ./configure --with-httpd-conf=/etc/apache2/sites-enabled
sudo make all
```


### Create User And Group

This creates the `nagios` user and group. The `www-data` user is also added to the `nagios` group.
```
sudo make install-groups-users
sudo usermod -a -G nagios www-data
```

### Install Binaries

This step installs the binary files, CGIs, and HTML files.
```
sudo make install
```

### Install Service / Daemon

This installs the service or daemon files and also configures them to start on boot.
```
sudo make install-daemoninit
```

Information on starting and stopping services will be explained further on.


### Install Command Mode

This installs and configures the external command file.
```
sudo make install-commandmode
```

### Install Configuration Files

This installs the *SAMPLE* configuration files. These are required as Nagios needs some configuration files to allow it to start.
```
sudo make install-config
```

### Install Apache Config Files

This installs the Apache web server configuration files and configures Apache settings.
```
sudo make install-webconf
sudo a2enmod rewrite
sudo a2enmod cgi
```

### Configure Firewall

You need to allow port 80 inbound traffic on the local firewall so you can reach the Nagios Core web interface.
```
sudo ufw allow Apache
sudo ufw reload
```

OR

Allow port 80 in the AWS Security group.


### Create nagiosadmin User Account

You'll need to create an Apache user account to be able to log into Nagios.

The following command will create a user account called nagiosadmin and you will be prompted to provide a password for the account.
```
sudo htpasswd -c /usr/local/nagios/etc/htpasswd.users nagiosadmin
```

### Start Apache Web Server

```
===== Ubuntu 15.x / 16.x / 17.x /18.x =====

Need to restart it because it is already running.

sudo systemctl restart apache2.service
```

### Start Service / Daemon

```
This command starts Nagios Core.

===== Ubuntu 15.x / 16.x / 17.x / 18.x =====

sudo systemctl start nagios.service
```

### Test Nagios

Nagios is now running, to confirm this you need to log into the Nagios Web Interface.

Point your web browser to the *Public IP/Public DNS* of your Nagios Core server, for example:

```
http://18.194.233.190/nagios

http://ec2-18-194-233-190.eu-central-1.compute.amazonaws.com/nagios
```

You will be prompted for a username and password. The username is nagiosadmin (you created it in a previous step) and the password is what you provided earlier.

Once you have logged in you are presented with the Nagios interface. 

Congratulations you have installed Nagios Core.



## BUT WAIT ...

Currently you have only installed the Nagios Core engine.

You'll notice some errors under the `hosts` and `services` along the lines of:
```
(No output on stdout) stderr: execvp(/usr/local/nagios/libexec/check_load, ...) failed. errno is 2: No such file or directory
```

These errors will be resolved once you install the Nagios Plugins, which is covered in the next step.










