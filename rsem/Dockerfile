FROM ubuntu

ADD https://github.com/BenLangmead/bowtie2/archive/master.tar.gz /tmp/bowtie2.tar.gz
ADD https://github.com/alexdobin/STAR/archive/master.tar.gz /tmp/star.tar.gz
ADD https://github.com/deweylab/RSEM/archive/master.tar.gz /tmp/rsem.tar.gz

RUN set -e \
      && apt-get -y update \
      && apt-get -y upgrade \
      && apt-get -y install g++ gcc libtbb-dev libz-dev make \
      && apt-get -y autoremove \
      && apt-get clean

RUN set -e \
      && tar xvf /tmp/bowtie2.tar.gz -C /usr/local/src \
      && mv /usr/local/src/bowtie2-master /usr/local/src/bowtie2 \
      && cd /usr/local/src/bowtie2 \
      && make \
      && make install

RUN set -e \
      && tar xvf /tmp/star.tar.gz -C /usr/local/src \
      && mv /usr/local/src/STAR-master /usr/local/src/STAR \
      && cd /usr/local/src/STAR/source \
      && make STAR \
      && ln -s /usr/local/src/STAR/source/STAR /usr/local/bin/STAR

RUN set -e \
      && tar xvf /tmp/rsem.tar.gz -C /usr/local/src \
      && mv /usr/local/src/RSEM-master /usr/local/src/RSEM \
      && cd /usr/local/src/RSEM \
      && make \
      && make install \
      && rm -rf /tmp/*

ENTRYPOINT ["rsem-calculate-expression"]
