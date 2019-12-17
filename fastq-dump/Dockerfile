FROM ubuntu:latest

ENV DEBIAN_FRONTEND noninteractive

RUN set -e \
      && ln -sf /bin/bash /bin/sh

RUN set -e \
      && apt-get -y update \
      && apt-get -y dist-upgrade \
      && apt-get -y install --no-install-recommends --no-install-suggests \
        ca-certificates curl \
      && apt-get -y autoremove \
      && apt-get clean \
      && rm -rf /var/lib/apt/lists/*

RUN set -eo pipefail \
      && curl -SL \
        https://ftp-trace.ncbi.nlm.nih.gov/sra/sdk/current/sratoolkit.current-ubuntu64.tar.gz \
        -o /tmp/sratoolkit.tar.gz \
      && tar xvf /tmp/sratoolkit.tar.gz -C /usr/local/src --remove-files \
      && mv /usr/local/src/sratoolkit.* /usr/local/src/sratoolkit \
      && find /usr/local/src/sratoolkit/bin -maxdepth 1 -type l \
        -exec ln -s {} /usr/local/bin \;

ENTRYPOINT ["/usr/local/bin/fastq-dump"]
