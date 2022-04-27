FROM ubuntu:20.04

ENV DEBIAN_FRONTEND noninteractive

RUN set -e \
      && ln -sf bash /bin/sh

RUN set -e \
      && apt-get -y update \
      && apt-get -y dist-upgrade \
      && apt-get -y install --no-install-recommends --no-install-suggests \
        ca-certificates curl \
      && apt-get -y autoremove \
      && apt-get clean \
      && rm -rf /var/lib/apt/lists/*

RUN set -e \
      && curl -SL http://opengene.org/fastp/fastp -o /usr/local/bin/fastp \
      && chmod +x /usr/local/bin/fastp

ENTRYPOINT ["/usr/local/bin/fastp"]
