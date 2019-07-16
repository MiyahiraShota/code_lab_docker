ARG WS_OS

FROM ${WS_OS}

USER root

ENV USER_NAME developer
RUN echo ${USER_NAME}
RUN useradd $USER_NAME
RUN echo "${USER_NAME}:${USER_NAME}_pass" |chpasswd
RUN echo "$USER_NAME    ALL=(ALL)       ALL" >> /etc/sudoers

############
# yum update:
############
RUN yum -y update
RUN yum clean all
RUN yum install -y sudo

# Development Tools install
RUN yum -y groupinstall "Development Tools"

############
# PHP + α
############
RUN yum -y install epel-release
RUN yum -y install http://rpms.famillecollet.com/enterprise/remi-release-7.rpm
ARG PHP_VER
RUN yum -y install --enablerepo=remi,remi-php${PHP_VER} php php-devel php-mbstring php-pdo php-xml

############
# Composer:
############
RUN curl -sS https://getcomposer.org/installer | php
RUN mv composer.phar /usr/local/bin/composer

############
# nvm node npm :
############

RUN curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.29.0/install.sh | bash

ENV NODE_VERSION 10.16.0
ENV NVM_DIR /home/$USER_NAME/.nvm
RUN . ~/.nvm/nvm.sh && nvm install $NODE_VERSION && nvm alias default $NODE_VERSION
# RUN npm install -g gulp yo hubot coffee-script browserify

WORKDIR /var/www
