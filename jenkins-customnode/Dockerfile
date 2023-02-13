FROM jenkins/inbound-agent:jdk11

LABEL version="1.0"
LABEL maintainer="mrachuta"

USER root

# Install basic tools
RUN apt-get update -y &&\
    apt-get install -y ca-certificates curl apt-transport-https lsb-release gnupg &&\
    curl -sL https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor | \
    tee /etc/apt/trusted.gpg.d/microsoft.gpg > /dev/null &&\
    AZ_REPO=$(lsb_release -cs) &&\
    echo "deb [arch=amd64] https://packages.microsoft.com/repos/azure-cli/ $AZ_REPO main" | \
    tee /etc/apt/sources.list.d/azure-cli.list &&\
    curl -fsSLo /usr/share/keyrings/kubernetes-archive-keyring.gpg https://packages.cloud.google.com/apt/doc/apt-key.gpg &&\
    echo "deb [signed-by=/usr/share/keyrings/kubernetes-archive-keyring.gpg] https://apt.kubernetes.io/ kubernetes-xenial main" | \
    tee /etc/apt/sources.list.d/kubernetes.list &&\
    curl -fsSL https://download.docker.com/linux/debian/gpg | gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg &&\
    echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/debian $(lsb_release -cs) stable" | \ 
    tee /etc/apt/sources.list.d/docker.list &&\
    curl https://baltocdn.com/helm/signing.asc | apt-key add - &&\
    echo "deb https://baltocdn.com/helm/stable/debian/ all main" | tee /etc/apt/sources.list.d/helm-stable-debian.list &&\
    apt-get update -y &&\
    apt-get install -y libpq-dev python3-pip docker-ce python-is-python3 docker-ce-cli containerd.io azure-cli kubectl helm &&\
    usermod -aG docker jenkins

ENV PATH="${HOME}/.local/bin:${PATH}"

USER jenkins
CMD ["/bin/bash"]
