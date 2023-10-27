FROM nexus3.k8s.lan:50001/jenkins/inbound-agent:jdk11

LABEL version="1.0"
LABEL maintainer="mrachuta"

USER root

RUN apt update -y && \
    apt install -y python3.10 python3-pip && \
    apt autoremove -y && \
    apt clean -y

USER jenkins
