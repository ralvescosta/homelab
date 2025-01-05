FROM ubuntu:20.04

# Install required packages
RUN apt update && \
    apt install -y tzdata && \
    echo "America/Sao_Paulo" > /etc/timezone && \
    ln -fs /usr/share/zoneinfo/America/Sao_Paulo /etc/localtime && \
    dpkg-reconfigure -f noninteractive tzdata && \
    DEBIAN_FRONTEND=noninteractive apt install -y openssh-server nano sudo

# Create a user with passwordless sudo
RUN useradd -ms /bin/bash ansible && \
    echo "ansible:password" | chpasswd && \
    usermod -aG sudo ansible && \
    rm -rf /etc/ssh/sshd_config

# Configure SSH
RUN mkdir /var/run/sshd && \
    sed -i 's/#PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config && \
    sed -i 's/#PasswordAuthentication yes/PasswordAuthentication yes/' /etc/ssh/sshd_config && \
    echo "AllowUsers ansible" >> /etc/ssh/sshd_config && \
    service ssh restart

# Expose SSH port
EXPOSE 22

# Start SSH service
CMD ["/usr/sbin/sshd", "-D"]