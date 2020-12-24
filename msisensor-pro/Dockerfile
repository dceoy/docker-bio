FROM ubuntu:latest

ENV DEBIAN_FRONTEND noninteractive

ADD https://raw.githubusercontent.com/dceoy/print-github-tags/master/print-github-tags /usr/local/bin/print-github-tags

RUN set -e \
      && ln -sf bash /bin/sh

RUN set -e \
      && apt-get -y update \
      && apt-get -y dist-upgrade \
      && apt-get -y install --no-install-recommends --no-install-suggests \
        ca-certificates curl libgomp1 \
      && apt-get -y autoremove \
      && apt-get clean \
      && rm -rf /var/lib/apt/lists/*

RUN set -eo pipefail \
      && chmod +x /usr/local/bin/print-github-tags \
      && print-github-tags --latest xjtu-omics/msisensor-pro \
        | xargs -i curl -SL \
          https://github.com/xjtu-omics/msisensor-pro/releases/download/{}/msisensor-pro \
          -o /usr/local/bin/msisensor-pro \
      && chmod +x /usr/local/bin/msisensor-pro

ENTRYPOINT ["/usr/local/bin/msisensor-pro"]
