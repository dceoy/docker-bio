FROM ubuntu:latest

ADD https://github.com/lh3/bwa/archive/master.tar.gz /tmp/bwa.tar.gz

RUN set -e \
      && apt-get -y update \
      && apt-get -y upgrade \
      && apt-get -y install gcc libz-dev make \
      && apt-get -y autoremove \
      && apt-get clean

RUN set -e \
      && tar xvf /tmp/bwa.tar.gz -C /usr/local/src --remove-files \
      && mv /usr/local/src/bwa-master /usr/local/src/bwa \
      && cd /usr/local/src/bwa \
      && make \
      && ln -s /usr/local/src/bwa/bwa /usr/local/bin

ENTRYPOINT ["bwa"]
