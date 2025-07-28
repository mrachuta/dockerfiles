FROM quay.io/podman/stable:v5.3

LABEL version="1.1.0" \
    maintainer="mrachuta"

USER root

WORKDIR /azp/

ADD ./context/start.sh ./start.sh

# Install basic tools
RUN chmod +x ./start.sh && \
    mkdir -p /opt/tools && \
    curl https://archive.apache.org/dist/maven/maven-3/3.9.1/binaries/apache-maven-3.9.1-bin.tar.gz -o apache-maven-3.9.1-bin.tar.gz && \
    tar -xf apache-maven-3.9.1-bin.tar.gz --no-same-owner --no-same-permissions -C /opt/tools/ && \
    rpm --import https://packages.microsoft.com/keys/microsoft.asc && \
    microdnf install -y https://packages.microsoft.com/config/rhel/9.0/packages-microsoft-prod.rpm && \
    microdnf install -y python3-pip azure-cli jq curl git java-17-openjdk java-17-openjdk-devel --exclude=maven && \
    microdnf clean all && \
    rm -rf /var/cache /var/log/dnf* /var/log/yum.* && \
    update-alternatives --install /usr/bin/docker docker /usr/bin/podman 1 && \
    update-alternatives --install /usr/bin/mvn mvn /opt/tools/apache-maven-3.9.1/bin/mvn 1 && \
    pip3 install parse-changelog && \
    chown -R podman:podman /azp

USER podman
# Another option is to run the agent as root.
#ENV AGENT_ALLOW_RUNASROOT="true"

ENV TARGETARCH="linux-x64" \
    _CONTAINERS_USERNS_CONFIGURED="" \
    BUILDAH_ISOLATION=chroot

ENTRYPOINT [ "./start.sh" ]
