FROM ubuntu:20.04

ENV DEBIAN_FRONTEND noninteractive

ADD https://raw.githubusercontent.com/dceoy/print-github-tags/master/print-github-tags /usr/local/bin/print-github-tags

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
      && chmod +x /usr/local/bin/print-github-tags \
      && print-github-tags --release --latest tobiasrausch/alfred \
        | xargs -i git clone --recursive --depth 1 \
          https://github.com/tobiasrausch/alfred.git -b {} /opt/alfred \
      && cd /opt/alfred \
      && make all \
      && make install

ENTRYPOINT ["/opt/alfred/bin/alfred"]
