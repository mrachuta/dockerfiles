FROM nexus3.k8s.lan:50001/redhat/ubi8:8.7

LABEL version="1.0"
LABEL maintainer="mrachuta"

ADD context /tmp

RUN dnf update && \
    dnf -y module enable python39 && \
    dnf -y module install python39 && \
    dnf -y install sudo && \
    dnf -y autoremove && \
    dnf -y clean all && \
    update-alternatives --remove-all python && \
    update-alternatives --install /usr/bin/python3 python3 /usr/bin/python3.9 1 && \
    update-alternatives --install /usr/bin/python python /usr/bin/python3.9 1 && \
    update-alternatives --install /usr/bin/pip pip /usr/bin/pip3.9 1 && \
    pip install ansible-core==2.12 mitogen==0.3.3 && \
    useradd -m -u 1000 -s /bin/bash ansible && \
    usermod -aG wheel ansible && \
    echo '%wheel ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers.d/passwordless_sudo && \
    mv /tmp/default_inventory.yaml /home/ansible/default_inventory.yaml && \
    mv /tmp/ansible.cfg /home/ansible/.ansible.cfg && \
    mv /tmp/ansible-wrapper /usr/bin/ansible-wrapper && \
    chown ansible:ansible /home/ansible/default_inventory.yaml /home/ansible/.ansible.cfg /usr/bin/ansible-wrapper && \
    chmod +x /usr/bin/ansible-wrapper

USER ansible

CMD ["ansible-wrapper"]
