# Use Ubuntu 20.04 as base
FROM ubuntu:20.04

# Disable interactive prompt for tzdata
ENV DEBIAN_FRONTEND=noninteractive

# Install required packages
RUN apt update && \
    apt install -y openssh-server sshpass sudo python3 python3-apt && \
    apt clean

# Create ansible user with passwordless sudo
RUN useradd -ms /bin/bash ansible && \
    echo "ansible ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers

# Set up SSH service and home directory
RUN mkdir /var/run/sshd && \
    mkdir -p /home/ansible/.ssh && \
    chmod 700 /home/ansible/.ssh && \
    chown -R ansible:ansible /home/ansible/.ssh

# Add SSH public key to authorized_keys
COPY id_ansible.pub /home/ansible/.ssh/authorized_keys
RUN chown ansible:ansible /home/ansible/.ssh/authorized_keys && \
    chmod 600 /home/ansible/.ssh/authorized_keys

# Configure sshd
RUN echo "PermitRootLogin no" >> /etc/ssh/sshd_config && \
    echo "PasswordAuthentication no" >> /etc/ssh/sshd_config && \
    echo "AllowUsers ansible" >> /etc/ssh/sshd_config

# Set working directory
WORKDIR /work

# Expose SSH port
EXPOSE 22

# Start SSH daemon
CMD ["/usr/sbin/sshd", "-D"]