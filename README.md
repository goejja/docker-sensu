# docker-sensu

## Description
A docker build to provide [sensu](https://sensu.io/)

Sensu is an open-source system monitoring framework.

This build will provides 3 differents containers:
* sensu-server
* sensu-api
* sensu-client
It is planned to run on docker swarm.

## Note
Initial build was based on debian-slim, but we want to monitor VMware so image is now based on centos.
Images are bigger but are now compliant with the supported platforms of VMware SDK.

## VMware SDK
The sensu client includes:
* [VMware vSphere Automation SDK for Perl 6.5](https://github.com/vmware/vsphere-automation-sdk-perl)
* [vmware vSphere Automation SDK for Go 6.5](https://github.com/vmware/govmomi)
* [VMware vSphere Automation  SDK for Python 6.5](https://github.com/vmware/pyvmomi)
