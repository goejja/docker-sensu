# docker-sensu

## Description
A docker build to provide [sensu](https://sensu.io/)

Sensu is an open-source system monitoring framework.

This build will provides 3 differents containers:
* [sensu-server](https://hub.docker.com/r/animemint/sensu-server/)
* [sensu-api](https://hub.docker.com/r/animemint/sensu-api/)
* [sensu-client](https://hub.docker.com/r/animemint/sensu-client/)


We are using [dockerize](https://github.com/jwilder/dockerize) to generate configuration files from container environment variables.
The client is used to monitor VMware vSphere, so it includes some VMware SDK used by our scripts.

## Note
Build is based on debian-slim. Debian is not part of supported platform for VMware SDK for Perl.
But it provides smaller footprint than CentOS dockers.

## VMware SDK
The sensu client includes:
* [VMware vSphere Automation SDK for Perl 6.5](https://github.com/vmware/vsphere-automation-sdk-perl)
* [VMware vSphere Automation  SDK for Python 6.5](https://github.com/vmware/pyvmomi)
