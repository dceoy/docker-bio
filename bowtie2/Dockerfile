FROM ubuntu

ADD https://github.com/BenLangmead/bowtie2/archive/master.tar.gz /tmp/bowtie2.tar.gz

RUN set -e \
      && apt-get -y update \
      && apt-get -y upgrade \
      && apt-get -y install g++ gcc libtbb-dev libz-dev make \
      && apt-get clean

RUN set -e \
      && tar xvf /tmp/bowtie2.tar.gz -C /usr/local/src \
      && mv /usr/local/src/bowtie2-master /usr/local/src/bowtie2 \
      && cd /usr/local/src/bowtie2 \
      && make \
      && make install \
      && rm -rf /tmp/*

ENTRYPOINT ["bowtie2"]
