FROM ubuntu:20.04

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
      && print-github-tags --release --latest gpertea/gffread \
        | tr -d v \
        | xargs -i curl -SL \
          https://github.com/gpertea/gffread/releases/download/v{}/gffread-{}.Linux_x86_64.tar.gz \
          -o /tmp/gffread.tar.gz \
      && tar xvf /tmp/gffread.tar.gz -C /usr/local/src --remove-files \
      && mv /usr/local/src/gffread-* /usr/local/src/gffread \
      && find /usr/local/src/gffread -maxdepth 1 -type f -executable \
        -exec ln -s {} /usr/local/bin \;

ENTRYPOINT ["/usr/local/bin/gffread"]
