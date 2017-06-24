FROM ubuntu:16.04

# Image Maintainer
MAINTAINER Marcos Oliveira Soares <marcosoliveirasoares94@gmail.com>

# Labels
LABEL name = "marcosoliveirasoares94/ubuntu:16.04"
LABEL summary = "Ubuntu 16 Image with OpenSSH-Server"
LABEL description = "Ubuntu 16 Image with OpenSSH-Server"
LABEL maintainer = "Marcos Oliveira Soares <marcosoliveirasoares94@gmail.com>"
LABEL com.marcosoliveirasoares94.applications = "OpenSSH-Server, Vim, Zip, Curl, Wget, Supervisor, NetTools"
LABEL com.marcosoliveirasoares94.tags = "Ubuntu 16, SSH"

# Environment variables.
ENV TERM = "xterm"
ENV UBUNTU_FRONTEND = "noninteractive"
ENV SSH_ROOT_PASSWORD = "secret"

# BASE image installation.
RUN apt-get update -y
RUN apt-get install -y \
        vim \
        zip \
        curl \
        wget \
        sudo \
        whois \
        net-tools \
        apt-utils \
        supervisor \
        iputils-ping \
        openssh-server \
        libcurl4-openssl-dev \
        software-properties-common

# Removing outdated software.
RUN apt-get autoclean && \
    apt-get autoremove --purge -y && \
        rm -rf /var/lib/apt/lists/*

# Terminal Configuration
RUN echo 'alias ls="ls -a --color=auto"' >> /etc/bash.bashrc
RUN echo 'alias ll="ls -la --color=auto"' >> /etc/bash.bashrc

# SSH Configurations Root
RUN echo "root:${SSH_ROOT_PASSWORD}" | chpasswd
RUN sed -i 's/PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config
RUN sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd

# Copy File
COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf

# SSH Configuration Directory
RUN mkdir -p /var/run/sshd

# Init directory
WORKDIR /

# Entrypoint Configuration Directory
RUN mkdir /docker-entrypoint-initdb.d

# Copy File Entrypoint
COPY /docker-entrypoint.sh /

# Entrypoint
ENTRYPOINT ["/docker-entrypoint.sh"]

# Expose Port
EXPOSE 22

# Default command
CMD ["/usr/bin/supervisord"]
