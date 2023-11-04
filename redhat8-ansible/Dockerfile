FROM nexus3.k8s.lan:50001/redhat/ubi8:8.7

LABEL version="1.0"
LABEL maintainer="mrachuta"

ADD --chown=root:root context /tmp/docker

# sudoers change is intentional;
# it's required for ansible and sudo access
RUN dnf -y module enable python39 && \
    dnf -y module install python39 && \
    dnf -y install sudo && \
    dnf -y autoremove && \
    dnf -y clean all && \
    update-alternatives --remove-all python && \
    update-alternatives --install /usr/bin/python3 python3 /usr/bin/python3.9 1 && \
    update-alternatives --install /usr/bin/python python /usr/bin/python3.9 1 && \
    update-alternatives --install /usr/bin/pip pip /usr/bin/pip3.9 1 && \
    pip install ansible-core==2.14 && \
    useradd -m -u 1000 -s /bin/bash ansible && \
    usermod -aG wheel ansible && \
    echo '%wheel ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers.d/passwordless_sudo && \
    chmod 600 /etc/sudoers.d/passwordless_sudo && \
    mv /tmp/docker/default_inventory.yaml /home/ansible/default_inventory.yaml && \
    mv /tmp/docker/ansible.cfg /home/ansible/.ansible.cfg && \
    mv /tmp/docker/ansible-wrapper /usr/bin/ansible-wrapper && \
    chown ansible:ansible /home/ansible/default_inventory.yaml /home/ansible/.ansible.cfg /usr/bin/ansible-wrapper && \
    chmod +x /usr/bin/ansible-wrapper && \
    rm -Rf /tmp/docker

USER ansible

CMD ["ansible-wrapper"]
