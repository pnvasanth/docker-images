#Base image ubuntu 16.04
FROM ubuntu:16.04

# File Author / Maintainer
MAINTAINER Vas N <phpvas@gmail.com>

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update && apt-get dist-upgrade -y && apt-get install -y apt-utils --no-install-recommends

RUN apt-get install -y file g++ gcc libc-dev make pkg-config re2c autoconf automake wget unzip \
    ca-certificates openssl libmcrypt-dev libtool-bin zlib1g zlib1g-dev libxml2-dev --no-install-recommends

RUN  apt-get install -y \
      php7.0 \
      php7.0-cli \
      php7.0-fpm \
      php7.0-gd \
      php7.0-json \
      php7.0-mbstring \
      php7.0-mysql \
      php7.0-pdo \
      php7.0-pdo-mysql \
      php7.0-xml \
      php7.0-xsl \
      php7.0-zip \
      php7.0-curl \
      php7.0-iconv \
      php7.0-mcrypt \
      php7.0-sockets \
      php7.0-opcache \
      php7.0-exif \
      php7.0-dev \
      php7.0-bcmath \
      php-xdebug \
      --no-install-recommends

#Install ZeroMQ
ENV ZMQ_VERSION 4.1.4
RUN wget https://github.com/zeromq/zeromq4-1/releases/download/v$ZMQ_VERSION/zeromq-$ZMQ_VERSION.tar.gz -P /tmp
RUN tar -zxvf /tmp/zeromq-$ZMQ_VERSION.tar.gz -C /tmp
RUN cd /tmp/zeromq-$ZMQ_VERSION && ./autogen.sh && ./configure --without-libsodium && make && make install && ldconfig


#Install the php Zeromq extension.
RUN wget https://github.com/mkoppanen/php-zmq/archive/master.zip -P /tmp
RUN unzip /tmp/master.zip -d /tmp
RUN cd /tmp/php-zmq-master && phpize && ./configure && make && make install
RUN touch /etc/php/7.0/mods-available/zmq.ini
RUN echo "extension=zmq.so" >> /etc/php/7.0/mods-available/zmq.ini
RUN phpenmod zmq

#Install composer for php
RUN wget https://getcomposer.org/composer.phar -P /tmp
RUN mv /tmp/composer.phar /usr/local/bin/composer
RUN chmod +x /usr/local/bin/composer

#Set default Timezone to UTC
RUN ln -snf /usr/share/zoneinfo/UTC /etc/localtime

RUN service php7.0-fpm start

EXPOSE 9000
