FROM ubuntu:20.04

ENV DEBIAN_FRONTEND noninteractive

RUN set -e \
      && ln -sf bash /bin/sh

RUN set -e \
      && apt-get -y update \
      && apt-get -y dist-upgrade \
      && apt-get -y install --no-install-recommends --no-install-suggests \
        ca-certificates g++ gcc make mercurial zlib1g-dev parallel \
      && apt-get -y autoremove \
      && apt-get clean \
      && rm -rf /var/lib/apt/lists/*

RUN set -e \
      && hg clone http://last.cbrc.jp/last /usr/local/src/last \
      && cd /usr/local/src/last \
      && make \
      && make install

ENTRYPOINT ["/usr/local/bin/lastal"]
