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
      && print-github-tags --release --latest pachterlab/kallisto \
        | xargs -i curl -SL \
          https://github.com/pachterlab/kallisto/releases/download/{}/kallisto_linux-{}.tar.gz \
          -o /tmp/kallisto.tar.bz2 \
      && tar xvf /tmp/kallisto.tar.bz2 -C /usr/local/src --remove-files \
      && find /usr/local/src/kallisto -maxdepth 1 -type f -executable \
        -exec ln -s {} /usr/local/bin \;

ENTRYPOINT ["/usr/local/bin/kallisto"]
