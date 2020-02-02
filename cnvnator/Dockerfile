FROM ubuntu:bionic

ENV DEBIAN_FRONTEND noninteractive

ADD https://raw.githubusercontent.com/dceoy/print-github-tags/master/print-github-tags /usr/local/bin/print-github-tags

RUN set -e \
      && ln -sf /bin/bash /bin/sh

RUN set -e \
      && apt-get -y update \
      && apt-get -y dist-upgrade \
      && apt-get -y install --no-install-recommends --no-install-suggests \
        autoconf ca-certificates curl g++ gcc libbz2-dev libcurl4-gnutls-dev \
        liblzma-dev libncurses5-dev libreadline-dev libssl-dev libz-dev make \
        unzip \
      && apt-get -y autoremove \
      && apt-get clean \
      && rm -rf /var/lib/apt/lists/*

RUN set -eo pipefail \
      && chmod +x /usr/local/bin/print-github-tags \
      && print-github-tags --release --latest --tar samtools/htslib \
        | xargs -i curl -SL {} -o /tmp/htslib.tar.gz \
      && tar xvf /tmp/htslib.tar.gz -C /usr/local/src --remove-files \
      && mv /usr/local/src/htslib-* /usr/local/src/htslib \
      && cd /usr/local/src/htslib \
      && autoheader \
      && autoconf \
      && ./configure \
      && make \
      && make install

RUN set -eo pipefail \
      && print-github-tags --release --latest --tar samtools/samtools \
        | xargs -i curl -SL {} -o /tmp/samtools.tar.gz \
      && tar xvf /tmp/samtools.tar.gz -C /usr/local/src --remove-files \
      && mv /usr/local/src/samtools-* /usr/local/src/samtools \
      && cd /usr/local/src/samtools \
      && autoheader \
      && autoconf \
      && ./configure \
      && make \
      && make install

RUN set -eo pipefail \
      && print-github-tags --release --latest root-project/root \
        | sed -e 's/-/\./g' \
        | xargs -i curl -SL -o /tmp/root.tar.gz \
          https://root.cern/download/root_{}.Linux-ubuntu18-x86_64-gcc7.4.tar.gz \
      && tar xvf /tmp/root.tar.gz -C /opt --remove-files

ENV ROOTSYS /opt/root

RUN set -eo pipefail \
      && print-github-tags --release --latest abyzovlab/CNVnator \
        | xargs -i curl -SL -o /tmp/cnvnator.zip \
          https://github.com/abyzovlab/CNVnator/releases/download/{}/CNVnator_{}.zip \
      && unzip -d /usr/local/src /tmp/cnvnator.zip \
      && mv /usr/local/src/CNVnator_* /usr/local/src/cnvnator \
      && cd /usr/local/src/cnvnator/src \
      && ln -s /usr/local/src/samtools . \
      && find /usr/local/src/htslib/htslib -maxdepth 1 -type f -name '*.h' \
        -exec ln -s {} . \; \
      && make \
      && find /usr/local/src/cnvnator/src -maxdepth 1 -type f -executable \
        -exec ln -s {} /usr/local/bin \; \
      && rm -f /tmp/cnvnator.zip

ENTRYPOINT ["/usr/local/bin/cnvnator"]
