FROM ubuntu

ADD https://github.com/samtools/htslib/archive/master.tar.gz /tmp/htslib.tar.gz
ADD https://github.com/samtools/bcftools/archive/master.tar.gz /tmp/bcftools.tar.gz

RUN set -e \
      && apt-get -y update \
      && apt-get -y upgrade \
      && apt-get -y install autoconf gcc libbz2-dev liblzma-dev libz-dev make \
      && apt-get clean

RUN set -e \
      && tar xvf /tmp/htslib.tar.gz -C /usr/local/src \
      && mv /usr/local/src/htslib-master /usr/local/src/htslib \
      && tar xvf /tmp/bcftools.tar.gz -C /usr/local/src \
      && mv /usr/local/src/bcftools-master /usr/local/src/bcftools \
      && cd /usr/local/src/bcftools \
      && make \
      && make install \
      && rm -rf /tmp/*

ENTRYPOINT ["bcftools"]
