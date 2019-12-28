FROM ubuntu:latest

ENV DEBIAN_FRONTEND noninteractive

ADD https://raw.githubusercontent.com/dceoy/print-github-tags/master/print-github-tags /usr/local/bin/print-github-tags

RUN set -e \
      && ln -sf /bin/bash /bin/sh

RUN set -e \
      && apt-get -y update \
      && apt-get -y dist-upgrade \
      && apt-get -y install --no-install-recommends --no-install-suggests \
        ca-certificates curl g++ gcc libbz2-dev liblzma-dev libz-dev make \
        python3.8 \
      && apt-get -y autoremove \
      && apt-get clean \
      && rm -rf /var/lib/apt/lists/*

RUN set -eo pipefail \
      && ln -s /usr/bin/python3.8 /usr/bin/python \
      && chmod +x /usr/local/bin/print-github-tags \
      && print-github-tags --release --latest --tar arq5x/bedtools2 \
        | xargs -i curl -SL {} -o /tmp/bedtools2.tar.gz \
      && tar xvf /tmp/bedtools2.tar.gz -C /usr/local/src --remove-files \
      && mv /usr/local/src/bedtools2-* /usr/local/src/bedtools2 \
      && cd /usr/local/src/bedtools2 \
      && make \
      && make install

ENTRYPOINT ["/usr/local/bin/bedtools"]
