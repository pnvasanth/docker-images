# Set go base image
FROM ubuntu:16.04

# File Author / Maintainer
MAINTAINER Vas N <phpvas@gmail.com>

RUN apt-get update && apt-get install -y --fix-missing \
    ca-certificates openssl libmcrypt-dev git vim curl wget tar \
    libtool pkg-config build-essential autoconf automake \
    --no-install-recommends

#Install ZeroMQ
ENV ZMQ_VERSION 4.1.4
RUN wget https://github.com/zeromq/zeromq4-1/releases/download/v$ZMQ_VERSION/zeromq-$ZMQ_VERSION.tar.gz -P /tmp
RUN tar -zxvf /tmp/zeromq-$ZMQ_VERSION.tar.gz -C /tmp
RUN cd /tmp/zeromq-$ZMQ_VERSION && ./autogen.sh && ./configure --without-libsodium && make && make install && ldconfig


#Install Golang
ENV GO_VERSION 1.11
RUN wget https://dl.google.com/go/go$GO_VERSION.linux-amd64.tar.gz -P /tmp
RUN cd /tmp && tar -xvf go$GO_VERSION.linux-amd64.tar.gz && mv go /usr/local

RUN rm /tmp/zeromq-$ZMQ_VERSION.tar.gz && rm /tmp/go$GO_VERSION.linux-amd64.tar.gz