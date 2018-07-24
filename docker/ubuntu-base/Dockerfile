FROM ubuntu:16.04

ENV DEBIAN_FRONTEND noninteractive
ENV LANG C.UTF-8
ENV LC_ALL C.UTF-8

## General package configuration
RUN sed -i -e 's#http://\(archive\|security\)#mirror://mirrors#' -e 's#/ubuntu/#/mirrors.txt#' /etc/apt/sources.list && \
    apt-get -y update && apt-get -y --no-install-recommends install \
        curl \
        sudo \
        openjdk-8-jdk \
        wget \
    && rm -rf /var/lib/apt/lists/*