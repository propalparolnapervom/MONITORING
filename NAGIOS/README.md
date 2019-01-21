# NAGIOS

[Tutorial 1](https://www.guru99.com/nagios-tutorial.html)

[Tutorial 2](https://www.edureka.co/blog/nagios-tutorial/)

## CONTINUOUS MONITORING

**Continuous Monitoring** Tools resolve any system errors (low memory, unreachable server etc) before they have any negative impact on your business productivity.

Important reasons to use a monitoring tool are:

    - It detects any network or server problems
    - It determines the root cause of any issues
    - It maintains the security and availability of the service
    - It monitors and troubleshoot server performance issues
    - It allows us to plan for infrastructure upgrades before outdated systems cause failures
    - It can respond to issues at the first sign of a problem
    - It can be used to automatically fix problems when they are detected
    - It ensures IT infrastructure outages have a minimal effect on your organization’s bottom line
    - It can monitor your entire infrastructure and business processes

Continuous Monitoring comes into the picture, once the application is deployed on the production servers.

Continuous Monitoring is all about the ability of an organization to detect, report, respond, contain and mitigate the attacks that occur, in its infrastructure.

## OVERALL

**Nagios** is a free to use open source software tool that is used for Continuous monitoring of systems, applications, services, and business processes etc in a DevOps culture. 

In the event of a failure, Nagios can alert technical staff of the problem, allowing them to begin remediation processes before outages affect business processes, end-users, or customers. 

With Nagios, you don’t have to explain why an unseen infrastructure outage affect your organization’s bottom line.

_______

Nagios runs on a server, usually as a daemon or a service.

It periodically runs plugins residing on the same server, they contact hosts or servers on your network or on the internet. 

One can view the status information using the web interface. 

You can also receive email or SMS notifications if something happens.


The Nagios daemon behaves like a scheduler that runs certain scripts at certain moments. It stores the results of those scripts and will run other scripts if these results change.

_______

**Plugins** - compiled executables or scripts (Perl scripts, shell scripts, etc.) that can be run from a command line to check the status or a host or service.

Nagios uses the results from the plugins to determine the current status of the hosts and services on your network.

## ARCHITECTURE

    - Nagios is built on a server/agents architecture.

    - Usually, on a network, a Nagios server is running on a host, and Plugins interact with local and all the remote hosts that need to be monitored.

    - These plugins will send information to the Scheduler, which displays that in a GUI

![arch](https://github.com/propalparolnapervom/OVERALL/blob/master/Pictures/monitoring/nagios/nagions_architecture.png "arch")