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
      && print-github-tags --release --latest --tar Illumina/strelka \
        | xargs -i curl -SL {} -o /tmp/strelka.tar.gz \
      && tar xvf /tmp/strelka.tar.gz -C /usr/local/src --remove-files \
      && mv /usr/local/src/strelka-* /usr/local/src/strelka \
      && cd /usr/local/src/strelka \
      && mkdir /usr/local/src/strelka/build \
      && cd /usr/local/src/strelka/build \
      && ../configure \
      && make install

ENTRYPOINT ["/usr/local/bin/configureStrelkaGermlineWorkflow.py"]
