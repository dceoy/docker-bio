FROM ubuntu:latest

ENV DEBIAN_FRONTEND noninteractive

ADD https://raw.githubusercontent.com/dceoy/print-github-tags/master/print-github-tags /usr/local/bin/print-github-tags

RUN set -e \
      && ln -sf /bin/bash /bin/sh

RUN set -e \
      && apt-get -y update \
      && apt-get -y dist-upgrade \
      && apt-get -y install --no-install-recommends --no-install-suggests \
        autoconf automake ca-certificates curl g++ gcc git libbz2-dev libc6-dev \
        libcurl4-gnutls-dev liblzma-dev libssl-dev libz-dev make \
      && apt-get -y autoremove \
      && apt-get clean \
      && rm -rf /var/lib/apt/lists/*

RUN set -eo pipefail \
      && chmod +x /usr/local/bin/print-github-tags \
      && print-github-tags --release --latest arq5x/lumpy-sv \
        | tr -d v \
        | xargs -i curl -SL \
          https://github.com/arq5x/lumpy-sv/releases/download/{}/lumpy-sv.tar.gz \
          -o /tmp/lumpy-sv.tar.gz \
      && tar xvf /tmp/lumpy-sv.tar.gz -C /usr/local/src --remove-files \
      && cd /usr/local/src/lumpy-sv/lib/htslib \
      && autoheader \
      && autoconf \
      && make \
      && make install \
      && cd /usr/local/src/lumpy-sv \
      && make \
      && find /usr/local/src/lumpy-sv/bin -maxdepth 1 -type f -executable \
        -exec ln -s {} /usr/local/bin \;

ENTRYPOINT ["/usr/local/bin/lumpy"]
