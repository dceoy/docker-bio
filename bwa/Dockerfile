FROM ubuntu:latest

ENV DEBIAN_FRONTEND noninteractive

ADD https://raw.githubusercontent.com/dceoy/print-github-tags/master/print-github-tags /usr/local/bin/print-github-tags

RUN set -e \
      && ln -sf bash /bin/sh

RUN set -e \
      && apt-get -y update \
      && apt-get -y dist-upgrade \
      && apt-get -y install --no-install-recommends --no-install-suggests \
        ca-certificates curl gcc libgetopt-complete-perl libz-dev make wget \
      && apt-get -y autoremove \
      && apt-get clean \
      && rm -rf /var/lib/apt/lists/*

RUN set -eo pipefail \
      && chmod +x /usr/local/bin/print-github-tags \
      && print-github-tags --release --latest lh3/bwa \
        | tr -d v \
        | xargs -i curl -SL \
          https://github.com/lh3/bwa/releases/download/v{}/bwa-{}.tar.bz2 \
          -o /tmp/bwa.tar.gz \
      && tar xvf /tmp/bwa.tar.gz -C /usr/local/src --remove-files \
      && mv /usr/local/src/bwa-* /usr/local/src/bwa \
      && cd /usr/local/src/bwa \
      && make \
      && find /usr/local/src/bwa -type f -executable \
        -exec ln -s {} /usr/local/bin \;

ENTRYPOINT ["/usr/local/bin/bwa"]
