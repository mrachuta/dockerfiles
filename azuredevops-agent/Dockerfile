FROM quay.io/podman/stable

LABEL version="1.0" \
    maintainer="mrachuta"

USER root

WORKDIR /azp/

ADD ./context/start.sh ./start.sh

# Install basic tools
RUN chmod +x ./start.sh && \
    rpm --import https://packages.microsoft.com/keys/microsoft.asc && \
    dnf install -y https://packages.microsoft.com/config/rhel/9.0/packages-microsoft-prod.rpm && \
    dnf install -y azure-cli maven java-17-openjdk && \
    dnf clean all && \
    rm -rf /var/cache /var/log/dnf* /var/log/yum.*

USER podman
# Another option is to run the agent as root.
#ENV AGENT_ALLOW_RUNASROOT="true"

ENV PATH="${HOME}/.local/bin:/kaniko:${PATH}" \
    TARGETARCH="linux-x64" \
    _CONTAINERS_USERNS_CONFIGURED="" \
    BUILDAH_ISOLATION=chroot

ENTRYPOINT [ "./start.sh" ]
