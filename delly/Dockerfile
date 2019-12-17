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
      && print-github-tags --release --latest dellytools/delly \
        | xargs -i curl -SL \
          https://github.com/dellytools/delly/releases/download/{}/delly_{}_parallel_linux_x86_64bit \
          -o /usr/local/bin/delly \
      && chmod +x /usr/local/bin/delly

ENTRYPOINT ["/usr/local/bin/delly"]
