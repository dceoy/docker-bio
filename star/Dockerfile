FROM ubuntu

ADD https://github.com/alexdobin/STAR/archive/master.tar.gz /tmp/star.tar.gz

RUN set -e \
      && apt-get -y update \
      && apt-get -y upgrade \
      && apt-get -y install g++ gcc libz-dev make \
      && apt-get clean

RUN set -e \
      && tar xvf /tmp/star.tar.gz -C /usr/local/src \
      && mv /usr/local/src/STAR-master /usr/local/src/STAR \
      && cd /usr/local/src/STAR/source \
      && make STAR \
      && ln -s /usr/local/src/STAR/source/STAR /usr/local/bin/STAR \
      && rm -rf /tmp/*

ENTRYPOINT ["STAR"]
