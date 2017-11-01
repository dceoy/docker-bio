FROM ubuntu

RUN set -e \
      && apt-get -y update \
      && apt-get -y upgrade \
      && apt-get -y install g++ gcc make mercurial zlib1g-dev parallel \
      && apt-get clean

RUN set -e \
      && hg clone http://last.cbrc.jp/last /usr/local/src/last \
      && cd /usr/local/src/last \
      && make \
      && make install

ENTRYPOINT ["lastal"]
