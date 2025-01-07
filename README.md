## Project name
dockerfiles - Jenkins pipeline and a set of Dockerfiles used to build containers.

## Table of contents
- [Project name](#project-name)
- [Table of contents](#table-of-contents)
- [General info](#general-info)
- [jenkins-customnode](#jenkins-customnode)
- [jenkins-agent-python](#jenkins-agent-python)
- [jenkins-agent-azure](#jenkins-agent-azure)
- [jenkins-agent-gcp](#jenkins-agent-gcp)
- [python-webdev](#python-webdev)
- [redhat8-ansible](#redhat8-ansible)
- [ubuntu-ansible](#ubuntu-ansible)
- [azuredevops-agent](#azuredevops-agent)

## General info
Jenkinsfile to be used together with kaniko to build Docker image in kubernetes custer.
  
## jenkins-customnode
Image of custom jenkins node (agent) contains following tools:
* az-cli
* kubectl
* docker

## jenkins-agent-python
Image of custom jenkins node (agent) contains following tools:
* python 3.9

## jenkins-agent-azure
Image of custom jenkins node (agent) contains following tools:
* python 3.9
* azure-cli 2.46.0
* packer 1.8.6
* terraform 1.4.1
* helm 3.11.2
* kubectl 1.26

## jenkins-agent-gcp
Image of custom jenkins node (agent) contains following tools:
* python 3.9
* gcloud-cli 422.0.0
* packer 1.8.6
* terraform 1.4.1
* helm 3.11.2
* kubectl 1.26

## python-webdev
Image with python to be used during web development. Container is running as non-root user.
* python 3.9
* gcc and libpq-dev (to be used when any compilation is required)

## redhat8-ansible
Image equpied with Ansible. To bo used during testing of Ansible resources.
* python 3.9
* ansible-core 2.12

## ubuntu-ansible
Image equpied with Ansible. To bo used during testing of Ansible resources.
* python 3.11
* ansible-core 2.12

## azuredevops-agent
Image used to run AzureDevops agent in containers. 
Build using following guidelines: https://learn.microsoft.com/en-us/azure/devops/pipelines/agents/docker?view=azure-devops#linux
Contains following tools:
* azure-cli
* podman
* openjdk-17
* maven
