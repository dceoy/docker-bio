FROM ubuntu:latest

ENV DEBIAN_FRONTEND noninteractive

ADD https://github.com/samtools/htslib/archive/master.tar.gz /tmp/htslib.tar.gz
ADD https://github.com/samtools/samtools/archive/master.tar.gz /tmp/samtools.tar.gz

RUN set -e \
      && apt-get -y update \
      && apt-get -y dist-upgrade \
      && apt-get -y install autoconf gcc libbz2-dev liblzma-dev libncurses5-dev libz-dev make \
      && apt-get -y autoremove \
      && apt-get clean

RUN set -e \
      && tar xvf /tmp/htslib.tar.gz -C /usr/local/src --remove-files \
      && mv /usr/local/src/htslib-master /usr/local/src/htslib \
      && cd /usr/local/src/htslib \
      && autoheader \
      && autoconf \
      && ./configure \
      && make \
      && make install

RUN set -e \
      && tar xvf /tmp/samtools.tar.gz -C /usr/local/src --remove-files \
      && mv /usr/local/src/samtools-master /usr/local/src/samtools \
      && cd /usr/local/src/samtools \
      && autoheader \
      && autoconf \
      && ./configure \
      && make \
      && make install

ENTRYPOINT ["samtools"]
