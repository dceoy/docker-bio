FROM ubuntu:latest

ENV DEBIAN_FRONTEND noninteractive

ADD https://raw.githubusercontent.com/dceoy/print-github-tags/master/print-github-tags /usr/local/bin/print-github-tags

RUN set -e \
      && ln -sf /bin/bash /bin/sh

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
      && print-github-tags --release --latest bedops/bedops \
        | xargs -i curl -SL \
            https://github.com/bedops/bedops/releases/download/{}/bedops_linux_x86_64-{}.tar.bz2 \
            -o /tmp/bedops.tar.bz2 \
      && mkdir /tmp/bedops \
      && tar xvf /tmp/bedops.tar.bz2 -C /tmp/bedops --remove-files \
      && cp -a /tmp/bedops/bin/* /usr/local/bin \
      && rm -rf /tmp/bedops

ENTRYPOINT ["/usr/local/bin/bedops"]
