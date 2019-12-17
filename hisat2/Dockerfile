FROM ubuntu:latest

ENV DEBIAN_FRONTEND noninteractive

ADD https://raw.githubusercontent.com/dceoy/print-github-tags/master/print-github-tags /usr/local/bin/print-github-tags

RUN set -e \
      && ln -sf /bin/bash /bin/sh

RUN set -e \
      && apt-get -y update \
      && apt-get -y dist-upgrade \
      && apt-get -y install --no-install-recommends --no-install-suggests \
        ca-certificates curl unzip \
      && apt-get -y autoremove \
      && apt-get clean \
      && rm -rf /var/lib/apt/lists/*

RUN set -eo pipefail \
      && chmod +x /usr/local/bin/print-github-tags \
      && print-github-tags --latest infphilo/hisat2 \
        | tr -d v \
        | xargs -i curl -SL \
          ftp://ftp.ccb.jhu.edu/pub/infphilo/hisat2/downloads/hisat2-{}-Linux_x86_64.zip \
          -o /tmp/hisat2.zip \
      && unzip -d /usr/local/src /tmp/hisat2.zip \
      && mv /usr/local/src/hisat2-* /usr/local/src/hisat2 \
      && find /usr/local/src/hisat2 -maxdepth 1 -type f -executable \
        -exec ln -s {} /usr/local/bin \; \
      && rm -f /tmp/hisat2.zip

ENTRYPOINT ["/usr/local/bin/hisat2"]
