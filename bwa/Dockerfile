FROM ubuntu

ADD https://github.com/lh3/bwa/archive/master.tar.gz /tmp/bwa.tar.gz

RUN set -e \
      && apt-get -y update \
      && apt-get -y upgrade \
      && apt-get -y install gcc libz-dev make \
      && apt-get clean

RUN set -e \
      && tar xvf /tmp/bwa.tar.gz -C /usr/local/src \
      && cd /usr/local/src/bwa-master \
      && make \
      && ln -s /usr/local/src/bwa-master/bwa /usr/local/bin \
      && rm -rf /tmp/*

ENTRYPOINT ["bwa"]
