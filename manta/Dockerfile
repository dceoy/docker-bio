FROM ubuntu:latest

ENV DEBIAN_FRONTEND noninteractive

ADD https://raw.githubusercontent.com/dceoy/print-github-tags/master/print-github-tags /usr/local/bin/print-github-tags

RUN set -e \
      && ln -sf /bin/bash /bin/sh

RUN set -e \
      && apt-get -y update \
      && apt-get -y dist-upgrade \
      && apt-get -y install --no-install-recommends --no-install-suggests \
        ca-certificates curl bzip2 gcc git g++ make python zlib1g-dev \
      && apt-get -y autoremove \
      && apt-get clean \
      && rm -rf /var/lib/apt/lists/*

RUN set -eo pipefail \
      && chmod +x /usr/local/bin/print-github-tags \
      && print-github-tags --release --latest Illumina/manta \
        | tr -d v \
        | xargs -i curl -SL \
          https://github.com/Illumina/manta/releases/download/v{}/manta-{}.release_src.tar.bz2 \
          -o /tmp/manta.tar.bz2 \
      && tar xvf /tmp/manta.tar.bz2 -C /usr/local/src --remove-files \
      && mv /usr/local/src/manta-* /usr/local/src/manta \
      && mkdir /usr/local/src/manta/build \
      && cd /usr/local/src/manta/build \
      && ../configure \
      && make install

ENTRYPOINT ["/usr/local/bin/configManta.py"]
