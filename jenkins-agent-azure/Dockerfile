FROM nexus3.k8s.lan:50001/jenkins/inbound-agent:jdk11

LABEL version="1.0"
LABEL maintainer="mrachuta"

USER root

ENV PATH="/opt/tools/terraform:/opt/tools/packer:/opt/tools/helm/linux-amd64:\
/opt/tools/kubectl:/opt/tools/python/install/bin:/home/jenkins/.local/bin:${PATH}"

RUN bash -c 'mkdir -p /opt/tools/{packer,terraform,helm,kubectl,crane}' && \
    curl -L http://archive.ubuntu.com/ubuntu/pool/main/u/unzip/unzip_6.0-25ubuntu1_amd64.deb \
    -o /tmp/unzip_6.0-25ubuntu1_amd64.deb && \
    curl -L http://archive.ubuntu.com/ubuntu/pool/universe/libz/libzstd/zstd_1.4.4+dfsg-3_amd64.deb \
    -o /tmp/zstd_1.4.4+dfsg-3_amd64.deb && \
    dpkg -i /tmp/unzip_6.0-25ubuntu1_amd64.deb /tmp/zstd_1.4.4+dfsg-3_amd64.deb && \
    curl -L https://github.com/indygreg/python-build-standalone/releases/download/20231002/cpython-3.10.13+20231002-x86_64-unknown-linux-gnu-pgo+lto-full.tar.zst \
    -o /tmp/cpython-3.10.13+20231002-x86_64-unknown-linux-gnu-pgo+lto-full.tar.zst && \
    tar -xf /tmp/cpython-3.10.13+20231002-x86_64-unknown-linux-gnu-pgo+lto-full.tar.zst \
    -C /opt/tools && \
    pip3 install az-cli && \
    curl -L https://releases.hashicorp.com/packer/1.9.4/packer_1.9.4_linux_amd64.zip \
    -o /tmp/packer_1.9.4_linux_amd64.zip && \
    unzip /tmp/packer_1.9.4_linux_amd64.zip -d /opt/tools/packer/ && \
    curl -L https://releases.hashicorp.com/terraform/1.6.2/terraform_1.6.2_linux_amd64.zip \
    -o /tmp/terraform_1.6.2_linux_amd64.zip && \
    unzip /tmp/terraform_1.6.2_linux_amd64.zip -d /opt/tools/terraform/ && \
    curl -L https://get.helm.sh/helm-v3.13.1-linux-amd64.tar.gz \
    -o /tmp/helm-v3.13.1-linux-amd64.tar.gz && \
    tar -xf /tmp/helm-v3.13.1-linux-amd64.tar.gz -C /opt/tools/helm/ && \
    curl -L https://dl.k8s.io/release/v1.28.3/bin/linux/amd64/kubectl \
    -o /opt/tools/kubectl/kubectl && \
    chmod +x /opt/tools/kubectl/kubectl && \
    curl -L https://github.com/google/go-containerregistry/releases/download/v0.17.0/go-containerregistry_Linux_x86_64.tar.gz \
    -o /tmp/go-containerregistry_Linux_x86_64.tar.gz && \
    tar -xf /tmp/go-containerregistry_Linux_x86_64.tar.gz -C /opt/tools/crane/ && \
    chown -R jenkins:jenkins /opt/tools && \
    pip3 cache purge && \
    rm -Rf /tmp/*.{zip,tar.gz,deb}

USER jenkins
