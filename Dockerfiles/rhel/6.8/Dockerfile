FROM registry.access.redhat.com/rhel6/rhel

# Repository/Image Maintainer
MAINTAINER Marcos Oliveira Soares <marcosoliveirasoares94@gmail.com>

# Environment variables.
ENV TERM=xterm
ENV REDHAT_FRONTEND=noninteractive

# Password root.
ENV SSH_ROOT_PASSWORD=secret

# Copying files
COPY centos-6.8.repo /etc/yum.repos.d/centos-6.8.repo

# BASE image installation.
RUN yum update -y
RUN yum install -y \
        vim \
        zip \
        sed \
        curl \
        wget \
        unzip \
        openssh \
        openssh-server \
        openssh-clients \
        python-setuptools

RUN easy_install supervisor

# Removing outdated software.
RUN  yum clean all && \
        rm -rf /var/lib/yum/*

# Terminal Configuration
RUN echo 'alias ls="ls -a --color=auto"' >> /etc/bashrc
RUN echo 'alias ll="ls -la --color=auto"' >> /etc/bashrc

# Copy File
COPY supervisord.conf /etc/supervisord.conf

# Password Configurations Root
RUN echo "root:${SSH_ROOT_PASSWORD}" | chpasswd

# SSH Configuration
RUN sed -i 's/PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config
RUN sed -ri 's/^UsePAM yes/UsePAM no/' /etc/ssh/sshd_config && \
	/usr/bin/ssh-keygen -t rsa -b 2048 -f /etc/ssh/ssh_host_rsa_key -N "" && \
	/usr/bin/ssh-keygen -t dsa -b 1024 -f /etc/ssh/ssh_host_dsa_key -N ""

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
