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
      && print-github-tags --release --latest shenwei356/seqkit \
        | xargs -i curl -SL \
          https://github.com/shenwei356/seqkit/releases/download/{}/seqkit_linux_amd64.tar.gz \
          -o /tmp/seqkit.tar.gz \
      && tar xvf /tmp/seqkit.tar.gz -C /usr/local/bin --remove-files \
      && chmod +x /usr/local/bin/seqkit

ENTRYPOINT ["/usr/local/bin/seqkit"]
