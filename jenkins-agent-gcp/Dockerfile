FROM nexus3.k8s.lan:50001/jenkins/inbound-agent:jdk21

LABEL version="1.0"
LABEL maintainer="mrachuta"

USER root

ENV PATH="/opt/tools/terraform:/opt/tools/packer:/opt/tools/helm/linux-amd64:\
/opt/tools/kubectl:/opt/tools/google-cloud-sdk/bin:\
/opt/tools/google-cloud-sdk/platform/bundledpythonunix/bin:\
/home/jenkins/.local/bin:${PATH}"

RUN bash -c 'mkdir -p /opt/tools/{packer,terraform,helm,kubectl}' && \
    curl -L http://archive.ubuntu.com/ubuntu/pool/main/u/unzip/unzip_6.0-25ubuntu1_amd64.deb \
    -o /tmp/unzip_6.0-25ubuntu1_amd64.deb && \
    dpkg -i /tmp/unzip_6.0-25ubuntu1_amd64.deb && \
    curl -L https://dl.google.com/dl/cloudsdk/channels/rapid/downloads/google-cloud-cli-linux-x86_64.tar.gz \
    -o /tmp/google-cloud-cli-linux-x86_64.tar.gz && \
    tar -xf /tmp/google-cloud-cli-linux-x86_64.tar.gz -C /opt/tools/ && \
    curl -L https://releases.hashicorp.com/packer/1.12.0/packer_1.12.0_linux_amd64.zip \
    -o /tmp/packer_1.12.0_linux_amd64.zip && \
    unzip /tmp/packer_1.12.0_linux_amd64.zip -d /opt/tools/packer/ && \
    curl -L https://releases.hashicorp.com/terraform/1.10.5/terraform_1.10.5_linux_amd64.zip \
    -o /tmp/terraform_1.10.5_linux_amd64.zip && \
    unzip /tmp/terraform_1.10.5_linux_amd64.zip -d /opt/tools/terraform/ && \
    curl -L https://get.helm.sh/helm-v3.17.0-linux-amd64.tar.gz \
    -o /tmp/helm-v3.17.0-linux-amd64.tar.gz && \
    tar -xf /tmp/helm-v3.17.0-linux-amd64.tar.gz -C /opt/tools/helm/ && \
    curl -L https://dl.k8s.io/release/v1.28.3/bin/linux/amd64/kubectl \
    -o /opt/tools/kubectl/kubectl && \
    chmod +x /opt/tools/kubectl/kubectl && \
    chown -R jenkins:jenkins /opt/tools && \
    rm -Rf /tmp/*.{zip,tar.gz,deb}

USER jenkins
