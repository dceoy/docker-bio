FROM ubuntu

ADD https://github.com/arq5x/bedtools2/archive/master.tar.gz /tmp/bedtools2.tar.gz

RUN set -e \
      && apt-get -y update \
      && apt-get -y upgrade \
      && apt-get -y install g++ gcc libz-dev make python \
      && apt-get clean

RUN set -e \
      && tar xvf /tmp/bedtools2.tar.gz -C /usr/local/src \
      && cd /usr/local/src/bedtools2-master \
      && make \
      && make install \
      && rm -rf /tmp/*

ENTRYPOINT ["bedtools"]
