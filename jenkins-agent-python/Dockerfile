FROM nexus3.k8s.lan:50001/jenkins/inbound-agent:jdk21

LABEL version="1.1.0"
LABEL maintainer="mrachuta"

USER root

RUN apt update -y && \
    apt install -y python3.11 python3-pip && \
    apt autoremove -y && \
    apt clean -y

USER jenkins
