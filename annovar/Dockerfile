FROM ubuntu:latest

ENV DEBIAN_FRONTEND noninteractive

ADD annovar.latest.tar.gz /usr/local/src/

RUN set -e \
      && ln -sf bash /bin/sh

RUN set -e \
      && apt-get -y update \
      && apt-get -y dist-upgrade \
      && apt-get -y install --no-install-recommends --no-install-suggests \
        ca-certificates perl unzip wget \
      && apt-get -y autoremove \
      && apt-get clean \
      && rm -rf /var/lib/apt/lists/*

RUN set -e \
      && find /usr/local/src/annovar -maxdepth 1 -type f -executable \
        -exec ln -s {} /usr/local/bin \;

ENTRYPOINT ["/usr/bin/perl", "/usr/local/src/annovar/annotate_variation.pl"]
