# docker-sensu

## Description
A docker build to provide [sensu](https://sensu.io/)

Sensu is an open-source system monitoring framework.

This build will provides 3 differents containers:
* sensu-server
* sensu-api
* sensu-client
It is planned to run on docker swarm.

We are using sensu to monitor VMware vSphere, so sensu-client includes some VMware SDK used by our scripts.

## Note
Build is based on debian-slim. Debian is not part of supported platform for VMware SDK for Perl.
But it provides smaller footprint than CentOS dockers.

## VMware SDK
The sensu client includes:
* [VMware vSphere Automation SDK for Perl 6.5](https://github.com/vmware/vsphere-automation-sdk-perl)
* [vmware vSphere Automation SDK for Go 6.5](https://github.com/vmware/govmomi)
* [VMware vSphere Automation  SDK for Python 6.5](https://github.com/vmware/pyvmomi)
