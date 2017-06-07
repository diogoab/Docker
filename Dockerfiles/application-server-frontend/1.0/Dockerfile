FROM marcosoliveirasoares94/ubuntu:17.04

# Repository/Image Maintainer
MAINTAINER Marcos Oliveira Soares <marcosoliveirasoares94@gmail.com>

# BASE image installation.
# Install PHP, some PHP extentions and some useful Tools with APT
RUN apt-get update -y
RUN apt-get install -y \
        php-cli \
        php-common \
        php-curl \
        php-json \
        php-xml \
        php-mbstring \
        php-mcrypt \
        php-mysql \
        php-pgsql \
        php-sqlite3 \
        php-zip \
        php-memcached \
        php-gd \
        php-fpm \
        php-xdebug \
        php-dev \
        php-apcu \
        php-bz2 \
        php-imagick \
        php-imap \
        php-intl \
        php-mongodb \
        php-opcache \
        php-redis \
        php-soap \
        php-sqlite3 \
        php-phpdbg

# Installing Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Installing NodeJS , NPM, Gulp, Bower, React
RUN curl -sL https://deb.nodesource.com/setup_7.x | bash - \
    && apt-get install -y nodejs \
    && npm install -g gulp-cli bower eslint babel-eslint eslint-plugin-react yarn

# Installing AngularJS, Angular CLI, TypeScript
RUN npm install -g angular angular-cli typescript

# Copy File
COPY supervisord.conf /tmp/supervisord.conf

# Adding Scripts to Boot Supervisord
RUN  cat /tmp/supervisord.conf >> /etc/supervisor/conf.d/supervisord.conf

# Removing file
RUN rm -f /tmp/supervisord.conf

# Removing outdated software.
RUN apt-get autoclean && \
    apt-get autoremove --purge -y && \
    rm -rf /var/lib/apt/lists/*

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
