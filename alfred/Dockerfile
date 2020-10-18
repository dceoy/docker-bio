FROM ubuntu:latest

ENV DEBIAN_FRONTEND noninteractive

RUN set -e \
      && ln -sf bash /bin/sh

RUN set -e \
      && apt-get -y update \
      && apt-get -y dist-upgrade \
      && apt-get -y install --no-install-recommends --no-install-suggests \
        autoconf build-essential ca-certificates cmake curl g++ git-all \
        libboost-date-time-dev libboost-filesystem-dev libboost-iostreams-dev \
        libboost-program-options-dev libboost-system-dev libbz2-dev \
        liblzma-dev zlib1g-dev \
      && apt-get -y autoremove \
      && apt-get clean \
      && rm -rf /var/lib/apt/lists/*

RUN set -eo pipefail \
      && git clone --recursive --depth 1 \
        https://github.com/tobiasrausch/alfred.git /opt/alfred \
      && cd /opt/alfred \
      && git tag \
        | tail -1 \
        | xargs git checkout \
      && make all \
      && make install

ENTRYPOINT ["/opt/alfred/bin/alfred"]
