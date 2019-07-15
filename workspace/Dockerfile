ARG WS_OS

FROM ${WS_OS}

USER root

############
# yum update:
############
RUN yum -y update
RUN yum clean all
RUN yum install -y sudo

# Development Tools install
RUN yum -y groupinstall "Development Tools"

############
# PHP:
############
RUN yum -y install http://rpms.famillecollet.com/enterprise/remi-release-7.rpm
ARG PHP_VER
RUN yum -y install \
    php${PHP_VER} \
    php${PHP_VER}-devel \
    php${PHP_VER}-mysqlnd \
    php${PHP_VER}-mbstring \
    php${PHP_VER}-gd

############
# Composer:
############
RUN curl -sS https://getcomposer.org/installer | php${PHP_VER}
RUN mv composer.phar /usr/local/bin/composer

############
# nvm node npm :
############

RUN curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.29.0/install.sh | bash
ENV NODE_VERSION 10.16.0
ENV NVM_DIR /home/${USER}/.nvm
RUN . ~/.nvm/nvm.sh && nvm install $NODE_VERSION && nvm alias default $NODE_VERSION && npm install -g gulp yo hubot coffee-script browserify

WORKDIR /var/www
