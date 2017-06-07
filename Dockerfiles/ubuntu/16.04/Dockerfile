FROM ubuntu:16.04

# Repository/Image Maintainer
MAINTAINER Marcos Oliveira Soares <marcosoliveirasoares94@gmail.com>

# Environment variables.
ENV TERM=xterm
ENV UBUNTU_FRONTEND=noninteractive

# Password root.
ENV SSH_ROOT_PASSWORD=secret

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
RUN echo 'alias ll="ls -a --color=auto"' >> /etc/bash.bashrc

# Password Configurations Root
RUN echo "root:${SSH_ROOT_PASSWORD}" | chpasswd

# Root Login
RUN sed -i 's/PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config

# Fixed SSH
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
