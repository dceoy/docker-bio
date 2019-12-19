FROM ubuntu:latest

ENV DEBIAN_FRONTEND noninteractive

RUN set -e \
      && ln -sf /bin/bash /bin/sh

RUN set -e \
      && apt-get -y update \
      && apt-get -y dist-upgrade \
      && apt-get -y install --no-install-recommends --no-install-suggests \
        ca-certificates curl openjdk-8-jre unzip \
      && apt-get -y autoremove \
      && apt-get clean \
      && rm -rf /var/lib/apt/lists/*

RUN set -eo pipefail \
      && curl -SL \
        http://sourceforge.net/projects/snpeff/files/snpEff_latest_core.zip \
        -o /tmp/snpeff.zip \
      && unzip -d /usr/local/src /tmp/snpeff.zip \
      && rm -f /tmp/snpeff.zip

ENTRYPOINT ["/usr/bin/java", "-jar", "/usr/local/src/snpEff/snpEff.jar"]
