FROM ubuntu:22.04

LABEL version="1.0"
LABEL maintainer="mrachuta"

USER root

WORKDIR /azp/

COPY ./context/start.sh ./

ARG DEBIAN_FRONTEND=noninteractive

# Install basic tools
RUN chmod +x ./start.sh && \
    useradd -m -d /home/agent agent && \
    chown -R agent:agent /azp /home/agent && \
    apt-get update -y && \
    apt-get install -y ca-certificates curl apt-transport-https lsb-release gnupg && \
    curl -sL https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor | \
    tee /etc/apt/trusted.gpg.d/microsoft.gpg > /dev/null && \
    AZ_REPO=$(lsb_release -cs) && \
    echo "deb [arch=amd64] https://packages.microsoft.com/repos/azure-cli/ $AZ_REPO main" | \
    tee /etc/apt/sources.list.d/azure-cli.list && \
    curl -fsSL https://pkgs.k8s.io/core:/stable:/v1.31/deb/Release.key | \
    gpg --dearmor -o /etc/apt/keyrings/kubernetes-apt-keyring.gpg && \
    echo 'deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/v1.31/deb/ /' | \ 
    tee /etc/apt/sources.list.d/kubernetes.list && \
    curl https://baltocdn.com/helm/signing.asc | apt-key add - && \
    echo "deb https://baltocdn.com/helm/stable/debian/ all main" | \
    tee /etc/apt/sources.list.d/helm-stable-debian.list && \
    apt-get update -y && \
    apt-get install -y jq libpq-dev python3-pip python-is-python3 \
    azure-cli kubectl helm podman podman-docker openjdk-17-jre maven && \
    apt-get remove -y openjdk-11-jre-headless && \
    apt autoremove -y && \
    apt clean -y

ENV PATH="${HOME}/.local/bin:${PATH}"

USER agent
# Another option is to run the agent as root.
# ENV AGENT_ALLOW_RUNASROOT="true"

ENTRYPOINT [ "./start.sh" ]
