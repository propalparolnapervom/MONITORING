# README Nagios Core Installation

# !!! YOU MUST HAVE A RHEL SUBSCRIPTION TO FINISH THIS STEPS !!!!


[Nagios Core Installation Guids](https://assets.nagios.com/downloads/nagioscore/docs/nagioscore/4/en/quickstart.html?__hstc=118811158.a53919d4e93d557baaec794e81093a95.1548065954439.1548065954439.1548071096337.2&__hssc=118811158.7.1548071096337&__hsfp=1156883818#_ga=2.25587709.1966153250.1548065953-2105078507.1548065953)

## WHAT

Setup Nagios Core to the server, which will be Monitor Server.

## RHEL

[Install Nagios Core on RHEL](https://support.nagios.com/kb/article/nagios-core-installing-nagios-core-from-source-96.html#RHEL)

Log to the server.

Install latest OS updates
```
sudo yum update -y
```

### Security-Enhanced Linux

This guide is based on SELinux being disabled or in permissive mode. Steps to do this are as follows.
```
sudo sed -i 's/SELINUX=.*/SELINUX=disabled/g' /etc/selinux/config
sudo setenforce 0
```

### Prerequisites

Perform these steps to install the pre-requisite packages.
```
sudo yum install -y gcc glibc glibc-common wget unzip httpd php gd gd-devel perl postfix
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
./configure
make all
```

### Create User And Group

This creates the `nagios` user and group. 

The `apache` user is also added to the `nagios` group.
```
sudo make install-groups-users
sudo usermod -a -G nagios apache
```

### Install Binaries

This step installs the binary files, CGIs, and HTML files.
```
sudo make install
```

### Install Service / Daemon

This installs the service or daemon files and also configures them to start on boot. 

The Apache `httpd` service is also configured at this point.
```
===== CentOS 7.x | RHEL 7.x | Oracle Linux 7.x =====

sudo make install-daemoninit
sudo systemctl enable httpd.service
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

This installs the Apache web server configuration files. Also configure Apache settings if required.
```
sudo make install-webconf
```

### Configure Firewall

You need to allow port 80 inbound traffic on the local firewall so you can reach the Nagios Core web interface.
```
===== CentOS 7.x | RHEL 7.x | Oracle Linux 7.x =====

sudo firewall-cmd --zone=public --add-port=80/tcp
sudo firewall-cmd --zone=public --add-port=80/tcp --permanent

```

OR 

Add appropriate security rule to the AWS.


### Create nagiosadmin User Account

You'll need to create an Apache user account to be able to log into Nagios.

The following command will create a user account called `nagiosadmin` and you will be prompted to provide a password for the account.
```
sudo htpasswd -c /usr/local/nagios/etc/htpasswd.users nagiosadmin
```


### Start Apache Web Server
```
===== CentOS 7.x | RHEL 7.x | Oracle Linux 7.x =====

sudo systemctl start httpd.service
```

### Start Service / Daemon
This command starts Nagios Core.
```
===== CentOS 7.x | RHEL 7.x | Oracle Linux 7.x =====

sudo systemctl start nagios.service
```

### Test Nagios

Nagios is now running, to confirm this you need to log into the Nagios Web Interface.

Point your web browser to the Public IP/Public DNS of your Nagios Core server, for example:

```
http://52.59.237.72/nagios

http://ec2-52-59-237-72.eu-central-1.compute.amazonaws.com/nagios
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
