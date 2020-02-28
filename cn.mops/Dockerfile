FROM dceoy/clir:latest

ADD https://raw.githubusercontent.com/dceoy/print-github-tags/master/print-github-tags /usr/local/bin/print-github-tags

RUN set -e \
      && apt-get -y update \
      && apt-get -y dist-upgrade \
      && apt-get -y install --no-install-recommends --no-install-suggests \
        autoconf libbz2-dev liblzma-dev \
      && apt-get -y autoremove \
      && apt-get clean \
      && rm -rf /var/lib/apt/lists/*

RUN set -eo pipefail \
      && chmod +x /usr/local/bin/print-github-tags \
      && print-github-tags --release --latest samtools/htslib \
        | xargs -i curl -SL \
          https://github.com/samtools/htslib/releases/download/{}/htslib-{}.tar.bz2 \
          -o /tmp/htslib.tar.bz2 \
      && tar xvf /tmp/htslib.tar.bz2 -C /usr/local/src --remove-files \
      && mv /usr/local/src/htslib-* /usr/local/src/htslib \
      && cd /usr/local/src/htslib \
      && autoheader \
      && autoconf \
      && ./configure \
      && make \
      && make install

RUN set -e \
      && clir update \
      && clir install --devt=bioc cn.mops \
      && clir validate cn.mops

ENTRYPOINT ["/usr/bin/R"]
