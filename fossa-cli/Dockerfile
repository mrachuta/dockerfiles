FROM nexus3.k8s.lan:50001/ubuntu:noble

LABEL version="2.0.0"
LABEL maintainer="mrachuta"

# https://github.com/moby/moby/issues/4032#issuecomment-192327844
ARG DEBIAN_FRONTEND=noninteractive

# sudoers change is intentional;
# it's required for ansible and sudo access
RUN apt update && \
    apt install -y curl && \
    useradd -m -u 1001 -s /bin/bash fossa && \
    apt autoremove -y && \
    apt clean -y && \
    curl -H 'Cache-Control: no-cache' \
    https://raw.githubusercontent.com/fossas/fossa-cli/master/install-latest.sh | bash

USER fossa

CMD ["/bin/bash"]
