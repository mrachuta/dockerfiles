FROM nexus3.k8s.lan:50001/ubuntu:jammy

LABEL version="1.0"
LABEL maintainer="mrachuta"

ENV DEBIAN_FRONTEND=noninteractive

ADD --chown root:root context /tmp

RUN apt update && \
    apt install -y software-properties-common sudo && \
    add-apt-repository ppa:deadsnakes/ppa && \ 
    apt update && \
    apt remove -y python3 --purge && \ 
    apt install -y python3.11 python3-pip && \
    apt autoremove -y && \
    apt clean -y && \
    update-alternatives --install /usr/bin/python python /usr/bin/python3.11 1 && \
    pip install ansible-core==2.12 mitogen==0.3.3 && \
    useradd -m -u 1000 -s /bin/bash ansible && \
    usermod -aG sudo ansible && \
    echo '%sudo ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers.d/passwordless_sudo && \
    mv /tmp/default_inventory.yaml /home/ansible/default_inventory.yaml && \
    mv /tmp/ansible.cfg /home/ansible/.ansible.cfg && \
    mv /tmp/ansible-wrapper /usr/bin/ansible-wrapper && \
    chown ansible:ansible /home/ansible/default_inventory.yaml /home/ansible/.ansible.cfg /usr/bin/ansible-wrapper && \
    chmod +x /usr/bin/ansible-wrapper

USER ansible

CMD ["ansible-wrapper"]
