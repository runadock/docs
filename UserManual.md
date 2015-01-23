# UserManual
---
## Table of content

* [Introduction](#intro)
* [About RunADock](#about-runadock)
* [Features](#features)
* [Q & A](#q-amp-a)
* [Getting started](#getting-started)
* [Developers Guide](#developers-guide)
* [Release Notes](#release-notes)

---
## Intro
### About RunADock
RunADock is implemented as a PaaS for Developers to run and test applications in an easy way. We strongly focus on
* performance and 
* usability.

For more information about Docker look at https://www.docker.com/whatisdocker/

---
### Features
* dedicated IPv4 address
* use of GitHub repository to start a container and to run application
* cli (command line interface)
* REST API
* different sizes:

| Name         | CPU         | RAM     |
| -------      | --------    | ------- |
| XS (default) | 128 shares  | 512 MB  |
| S            | 256 shares  | 1024 MB |
| M            | 512 shares  | 2048 MB |
| L            | 1028 shares | 4096 MB |

* different plans: shared IPv4 addresses and dedicated IPv4 addresses
* disk space: 2 GB for all sizes
* 120 minutes free each month

---
### Q & A

---
## Getting started
### Sign in
To sign in into RunADock you have to use your username or email address of your GitHub account. With this information we will direct you to the GitHub login using the OAuth2 functionality. With the login to GitHub you give the permission that RunADock is allowed to use your GitHub account information. After your confirmation you will be redirected back to RunADock and we will create your RunADock account and send you an email with a confirmation link. After clicking the confirmation link we will ask you for your credit card information. Only with this information we are able to provide you the full service including the 120 minutes free of charge.

### Authorization key
* creation of authorization key (token) after sign in

### ...
* start a container using cli, REST-API, maven-plugin, or RunADock language bindings
* started container get a DNS name and a list of public port mappings

Example for starting a container using curl:
~~~~
curl -X POST -H "Authorization: RunADockKey username:key" -d "{'source':'https://github.io/developer/project1/Dockerfile', 'scmType':'git'}" https://api.runadock.io/api/v1/container/ {'public-dns':'project1.developer.runadock.io'} 
~~~~
* access via project1.developer.runadock.io
* started container has 1 CPU, 1 GB RAM und 5 GB disk space
This example shows how to start a container in a few moments without changes to the development environment.

the following command stops the container:
~~~~
curl -X DELETE -H "Authorization: RunADockKey username:key" https://api.runadock.io/api/v1/container/project1.developer.runadock.io
~~~~

### Terminal
You can also use our terminal to start and stop your containers:
![dashboard](https://extern.x-cellent.com/git/uploads/runadock/runadock/fdb1305f2a/dashboard.png)

Below the dashboard you will find a list of all your running containers. The details view shows you all necessary information about the selected container. The Trash button terminates your container.

---
## Developers Guide

### cli
git clone

create cli application with ./build

set environment variables RUNADOCK_USER and RUNADOCK_TOKEN

start container using bin/runadock run --source <source to the container> --name <name of your container> 

further optional parameter: --size, --plan

stop/delete container using bin/runadock kill --container <ID of the container to be stopped>

show details of a container: bin/runadock inspect --container <ID of the container to be inspected>

list your containers: bin/runadock ps --detail --all

---
## Release Notes
