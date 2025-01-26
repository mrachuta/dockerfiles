## Project name
dockerfiles - Jenkins pipeline and a set of Dockerfiles used to build containers.

## Table of contents
- [Project name](#project-name)
- [Table of contents](#table-of-contents)
- [General info](#general-info)
- [Dockerfiles](#dockerfiles)
  - [azuredevops-agent](#azuredevops-agent)
  - [fossa-cli](#fossa-cli)
  - [jenkins-agent-azure](#jenkins-agent-azure)
  - [jenkins-agent-gcp](#jenkins-agent-gcp)
  - [jenkins-agent-python](#jenkins-agent-python)
  - [python-webdev](#python-webdev)
  - [redhat8-ansible](#redhat8-ansible)
  - [ubuntu-ansible](#ubuntu-ansible)

## General info
Jenkinsfile to be used together with kaniko to build Docker image in kubernetes custer.

## Dockerfiles
  
### azuredevops-agent
Image of custom Azure DevOps agent contains following tools:
* maven
* podman
* openjdk 17
* azure-cli

### fossa-cli
Image with fossa-cli binary. To be used during security analysis.

### jenkins-agent-azure
Image of custom jenkins node (agent) contains following tools:
* python
* azure-cli
* packer
* terraform
* helm
* kubectl

### jenkins-agent-gcp
Image of custom jenkins node (agent) contains following tools:
* python
* gcloud-cli
* packer
* terraform
* helm
* kubectl

### jenkins-agent-python
Image of custom jenkins node (agent) contains following tools:
* python

### python-webdev
Image with python to be used during web development. Container is running as non-root user. Contains following tools:
* python
* gcc and libpq-dev (for compilling purposes)

### redhat8-ansible
Image equpied with Ansible. To bo used during testing of Ansible resources

### ubuntu-ansible
Image equpied with Ansible. To bo used during testing of Ansible resources.
