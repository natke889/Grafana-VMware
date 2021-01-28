# Grafana-VMware

This project provides an automated installation and deployment of the Grafana dashboard for VMware vSphere.

## Overview
The project based on various open source components and tools in order to do so. The telegraf will periodically poll your VMware vcenters data at a regular interval and pushed into an [InfluxDB](https://www.influxdata.com/) time-series database. [Grafana](https://grafana.com/), a data visualization engine for time-series data, is then utilized along with several customized [dashboards](https://grafana.com/grafana/dashboards/8159) of [Jorge de la Cruz](https://grafana.com/orgs/jorgedelacruz) to present the data graphically with . All of these components are integrated together using [Docker](https://www.docker.com/).

The only real requirements to utilize this project are a Linux OS and a Docker installation with Docker Compose.

## Getting Started
### Dependencies
You'll need to install [Docker](https://docs.docker.com/install/) and [Docker Compose](https://docs.docker.com/compose/install/). All other dependencies are provided through use of our Docker images.
### Configuration
#### VMware vCenter's
The only configuration needed is to set vCenter sdk address and credentials within the *"<project_dir\>/.env"* file. 
~~~~
...
VCENTERS_URL=https://<FQDN>/sdk
VCENTERS_USER=<administrator@vsphere.local>
VCENTERS_PASS=<your_password>
...
~~~~

### Starting It Up
It's pretty simple: run the docker compose from within the project root directory.

~~~~
$ docker-compose -f docker-compose.yml up -d
~~~~

## Once It's Started
### Accessing the Grafana Dashboards
The dashboards are available at **http://<host\>:3001** using default credentials _admin/admin_. Grafana should be pre-configured for immediate access to your data. Documentation for additional configuration and navigation can be found [here](http://docs.grafana.org/guides/getting_started/).

## Testing
The project can be tested using [Vagrant](https://www.vagrantup.com/docs/installation) and [VirtualBox](https://www.virtualbox.org/wiki/Downloads). 

Run vagrant up from the project root directory. This will bring up ubuntu with docker installed. 
~~~~
vagrant up
~~~~

SSH into the vagrant machine.
~~~~
vagrant ssh
~~~~

Change working dir to /vagrant/ directoy and edit the .env file and set the vcenter info 
~~~~
$ cd /vagrant
$ vi .env
~~~~

Run the docker compose command in order to starting the dockers.
~~~~
$ docker-compose -f docker-compose.yml up -d"
~~~~

Access Grafana at **http://192.168.65.211:3001**. (The IP address can be edit in th Vagrantfile)

## Install on non-internet server
The following stages need to be taken in order to pull the docker images and load them in non-internet access server
~~~~
pull the image on a machine with internet access.

$ docker pull natke889/grafana-vmware-telegraf:1.1
$ docker pull natke889/grafana-vmware-grafana:1.1
$ docker pull natke889/grafana-vmware-influxdb:1.1

save that image to a .tar files.

$ docker save --output grafana-vmware-telegraf.tar natke889/grafana-vmware-telegraf:1.1
$ docker save --output grafana-vmware-grafana.tar natke889/grafana-vmware-grafana:1.1
$ docker save --output grafana-vmware-influxdb.tar natke889/grafana-vmware-influxdb:1.1

copy those files to any machine and load the .tar files to docker with the docker compose command.

$ docker load --output grafana-vmware-telegraf.tar
$ docker load --output grafana-vmware-grafana.tar
$ docker load --output grafana-vmware-influxdb.tar
~~~~
