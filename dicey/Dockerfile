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
      && print-github-tags --release --latest gear-genomics/dicey \
        | xargs -i curl -SL \
          https://github.com/gear-genomics/dicey/releases/download/{}/dicey_{}_linux_x86_64bit \
          -o /usr/local/bin/dicey \
      && chmod +x /usr/local/bin/dicey

ENTRYPOINT ["/usr/local/bin/dicey"]
