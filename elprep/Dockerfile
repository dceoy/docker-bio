FROM ubuntu:20.04

ENV DEBIAN_FRONTEND noninteractive

ADD https://raw.githubusercontent.com/dceoy/print-github-tags/master/print-github-tags /usr/local/bin/print-github-tags

RUN set -e \
      && ln -sf bash /bin/sh

RUN set -e \
      && apt-get -y update \
      && apt-get -y dist-upgrade \
      && apt-get -y install --no-install-recommends --no-install-suggests \
        autoconf ca-certificates curl gcc git libbz2-dev liblzma-dev \
        libncurses5-dev libz-dev make parallel \
      && apt-get -y autoremove \
      && apt-get clean \
      && rm -rf /var/lib/apt/lists/*

RUN set -eo pipefail \
      && chmod +x /usr/local/bin/print-github-tags \
      && print-github-tags --release --latest samtools/samtools \
        | xargs -i curl -SL -o /tmp/samtools.tar.bz2 \
          https://github.com/samtools/samtools/releases/download/{}/samtools-{}.tar.bz2 \
      && tar xvf /tmp/samtools.tar.bz2 -C /usr/local/src --remove-files \
      && mv /usr/local/src/samtools-* /usr/local/src/samtools \
      && cd /usr/local/src/samtools \
      && autoheader \
      && autoconf \
      && ./configure \
      && make \
      && make install

RUN set -eo pipefail \
      && print-github-tags --release --latest exascience/elprep \
        | xargs -i curl -SL -o /tmp/elprep.tar.gz \
          https://github.com/ExaScience/elprep/releases/download/{}/elprep-{}.tar.gz \
      && mkdir /usr/local/src/elprep \
      && tar xvf /tmp/elprep.tar.gz -C /usr/local/src/elprep --remove-files \
      && find /usr/local/src/elprep -type f -executable \
        -exec ln -s {} /usr/local/bin \;

ENTRYPOINT ["/usr/local/bin/elprep"]
