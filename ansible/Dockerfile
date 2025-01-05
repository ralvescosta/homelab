FROM ubuntu:20.04

# Install Ansible and required packages
RUN apt update && \
    apt install -y tzdata && \
    echo "America/Sao_Paulo" > /etc/timezone && \
    ln -fs /usr/share/zoneinfo/America/Sao_Paulo /etc/localtime && \
    dpkg-reconfigure -f noninteractive tzdata && \
    DEBIAN_FRONTEND=noninteractive apt install -y ansible ssh snapd python3-pip sshpass

# Copy playbooks
COPY ./playbooks /playbooks
COPY ./playbooks/ansible.cfg /etc/ansible/ansible.cfg

# # Set working directory
# WORKDIR /playbooks

# RUN ansible-playbook -i inventory.ini microk8s.yml