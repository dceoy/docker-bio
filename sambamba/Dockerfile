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
      && print-github-tags --release --latest biod/sambamba \
        | tr -d v \
        | xargs -i curl -SL \
          https://github.com/biod/sambamba/releases/download/v{}/sambamba-{}-linux-amd64-static.gz \
        | gzip -dc - > /usr/local/bin/sambamba \
      && chmod +x /usr/local/bin/sambamba

ENTRYPOINT ["/usr/local/bin/sambamba"]
