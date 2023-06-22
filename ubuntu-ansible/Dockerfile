FROM nexus3.k8s.lan:50001/ubuntu:jammy

LABEL version="1.0"
LABEL maintainer="mrachuta"

# https://github.com/moby/moby/issues/4032#issuecomment-192327844
ARG DEBIAN_FRONTEND=noninteractive

ADD --chown=root:root context /tmp/docker

# sudoers change is intentional;
# it's required for ansible and sudo access
RUN apt update && \
    apt install -y software-properties-common sudo && \
    add-apt-repository ppa:deadsnakes/ppa && \ 
    apt update && \
    apt remove -y python3 --purge && \ 
    apt install -y python3.11 python3-pip && \
    apt autoremove -y && \
    apt clean -y && \
    update-alternatives --install /usr/bin/python python /usr/bin/python3.11 1 && \
    pip install ansible-core==2.14 mitogen==0.3.3 && \
    useradd -m -u 1000 -s /bin/bash ansible && \
    usermod -aG sudo ansible && \
    echo '%sudo ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers.d/passwordless_sudo && \
    chmod 600 /etc/sudoers.d/passwordless_sudo && \
    mv /tmp/docker/default_inventory.yaml /home/ansible/default_inventory.yaml && \
    mv /tmp/docker/ansible.cfg /home/ansible/.ansible.cfg && \
    mv /tmp/docker/ansible-wrapper /usr/bin/ansible-wrapper && \
    chown ansible:ansible /home/ansible/default_inventory.yaml /home/ansible/.ansible.cfg /usr/bin/ansible-wrapper && \
    chmod +x /usr/bin/ansible-wrapper && \
    rm -Rf /tmp/docker

USER ansible

CMD ["ansible-wrapper"]
