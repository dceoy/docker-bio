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
      && print-github-tags --latest cole-trapnell-lab/cufflinks \
        | tr -d v \
        | xargs -i curl -SL \
          http://cole-trapnell-lab.github.io/cufflinks/assets/downloads/cufflinks-{}.Linux_x86_64.tar.gz \
          -o /tmp/cufflinks.tar.gz \
      && tar xvf /tmp/cufflinks.tar.gz -C /usr/local/src --remove-files \
      && find /usr/local/src/cufflinks* -type f -executable \
        -exec ln -s {} /usr/local/bin \;

ENTRYPOINT ["/usr/local/bin/cufflinks"]
