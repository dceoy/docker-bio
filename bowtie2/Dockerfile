FROM ubuntu:latest

ENV DEBIAN_FRONTEND noninteractive

ADD https://raw.githubusercontent.com/dceoy/print-github-tags/master/print-github-tags /usr/local/bin/print-github-tags

RUN set -e \
      && ln -sf /bin/bash /bin/sh

RUN set -e \
      && apt-get -y update \
      && apt-get -y dist-upgrade \
      && apt-get -y install --no-install-recommends --no-install-suggests \
        ca-certificates curl g++ gcc libtbb-dev libz-dev make perl \
      && apt-get -y autoremove \
      && apt-get clean \
      && rm -rf /var/lib/apt/lists/*

RUN set -eo pipefail \
      && chmod +x /usr/local/bin/print-github-tags \
      && print-github-tags --release --latest --tar BenLangmead/bowtie2 \
        | xargs -i curl -SL {} -o /tmp/bowtie2.tar.gz \
      && tar xvf /tmp/bowtie2.tar.gz -C /usr/local/src --remove-files \
      && mv /usr/local/src/bowtie2-* /usr/local/src/bowtie2 \
      && cd /usr/local/src/bowtie2 \
      && make \
      && make install

ENTRYPOINT ["/usr/local/bin/bowtie2"]
