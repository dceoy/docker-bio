FROM ubuntu:latest

ENV DEBIAN_FRONTEND noninteractive

ADD https://raw.githubusercontent.com/dceoy/print-github-tags/master/print-github-tags /usr/local/bin/print-github-tags

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

RUN set -eo pipefail \
      && chmod +x /usr/local/bin/print-github-tags \
      && print-github-tags --release --latest bwa-mem2/bwa-mem2 \
        | tr -d v \
        | xargs -i curl -SL \
          https://github.com/bwa-mem2/bwa-mem2/releases/download/v{}/bwa-mem2-{}_x64-linux.tar.bz2 \
          -o /tmp/bwa-mem2.tar.gz \
      && tar xvf /tmp/bwa-mem2.tar.gz -C /usr/local/src --remove-files \
      && mv /usr/local/src/bwa-mem2-* /usr/local/src/bwa-mem2 \
      && cd /usr/local/src/bwa-mem2 \
      && find /usr/local/src/bwa-mem2 -maxdepth 1 -type f -executable \
        -exec ln -s {} /usr/local/bin \;

ENTRYPOINT ["/usr/local/bin/bwa-mem2"]
