## Project name
dockerfiles - Jenkins pipeline and a set of Dockerfiles used to build containers.

## Table of contents
- [Project name](#project-name)
- [Table of contents](#table-of-contents)
- [General info](#general-info)
- [jenkins-customnode](#jenkins-customnode)
- [python-webdev](#python-webdev)
- [redhat8-ansible](#redhat8-ansible)
- [ubuntu-ansible](#ubuntu-ansible)

## General info
Jenkinsfile to be used together with kaniko to build Docker image in kubernetes custer.
  
## jenkins-customnode
Image of custom jenkins node (agent) contains following tools:
* az-cli
* kubectl
* Docker

## python-webdev
Image with python to be used during web development. Container is running as non-root user.
* Python 3.9
* gcc and libpq-dev (to be used when any compilation is required)

## redhat8-ansible
Image equpied with Ansible. To bo used during testing of Ansible resources.
* Python 3.9
* ansible-core 2.12

## ubuntu-ansible
Image equpied with Ansible. To bo used during testing of Ansible resources.
* Python 3.11
* ansible-core 2.12
