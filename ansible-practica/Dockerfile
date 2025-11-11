FROM ubuntu:22.04

# Evitar interacciones
ENV DEBIAN_FRONTEND=noninteractive

# Actualizar e instalar SSH
RUN apt update && \
    apt install -y openssh-server sudo && \
    mkdir /var/run/sshd && \
    echo 'root:root' | chpasswd && \
    sed -i 's/#PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config && \
    sed -i 's/#PasswordAuthentication yes/PasswordAuthentication yes/' /etc/ssh/sshd_config

# Crear usuario ansible
RUN useradd -m -s /bin/bash ansible && \
    echo 'ansible:ansible' | chpasswd && \
    usermod -aG sudo ansible && \
    echo 'ansible ALL=(ALL) NOPASSWD: ALL' >> /etc/sudoers

# Exponer puerto SSH
EXPOSE 22

# Iniciar SSH
CMD ["/usr/sbin/sshd", "-D"]