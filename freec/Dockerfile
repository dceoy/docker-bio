FROM ubuntu:20.04

ENV DEBIAN_FRONTEND noninteractive

ADD https://raw.githubusercontent.com/dceoy/print-github-tags/master/print-github-tags /usr/local/bin/print-github-tags

RUN set -e \
      && ln -sf bash /bin/sh \
      && ln -s python3 /usr/bin/python

RUN set -e \
      && apt-get -y update \
      && apt-get -y dist-upgrade \
      && apt-get -y install --no-install-recommends --no-install-suggests \
        autoconf ca-certificates curl g++ gcc libbz2-dev libcurl4-gnutls-dev \
        liblzma-dev libncurses5-dev libssl-dev libz-dev make openjdk-8-jre \
        pkg-config python3 r-base \
      && apt-get -y autoremove \
      && apt-get clean \
      && rm -rf /var/lib/apt/lists/*

RUN set -eo pipefail \
      && chmod +x /usr/local/bin/print-github-tags \
      && print-github-tags --release --latest samtools/samtools \
        | xargs -i curl -SL \
          https://github.com/samtools/samtools/releases/download/{}/samtools-{}.tar.bz2 \
          -o /tmp/samtools.tar.bz2 \
      && tar xvf /tmp/samtools.tar.bz2 -C /usr/local/src --remove-files \
      && mv /usr/local/src/samtools-* /usr/local/src/samtools \
      && cd /usr/local/src/samtools/htslib-* \
      && autoheader \
      && autoconf \
      && ./configure \
      && make \
      && make install \
      && cd .. \
      && autoheader \
      && autoconf \
      && ./configure \
      && make \
      && make install

RUN set -eo pipefail \
      && print-github-tags --release --latest --tar arq5x/bedtools2 \
        | xargs -i curl -SL {} -o /tmp/bedtools2.tar.gz \
      && tar xvf /tmp/bedtools2.tar.gz -C /usr/local/src --remove-files \
      && mv /usr/local/src/bedtools2-* /usr/local/src/bedtools2 \
      && cd /usr/local/src/bedtools2 \
      && make \
      && make install

RUN set -eo pipefail \
      && print-github-tags --release --latest biod/sambamba \
        | tr -d v \
        | xargs -i curl -SL \
          https://github.com/biod/sambamba/releases/download/v{}/sambamba-{}-linux-amd64-static.gz \
        | gzip -dc - > /usr/local/bin/sambamba \
      && chmod +x /usr/local/bin/sambamba

RUN set -eo pipefail \
      && print-github-tags --release --latest --tar BoevaLab/FREEC \
        | xargs -i curl -SL {} -o /tmp/freec.tar.gz \
      && tar xvf /tmp/freec.tar.gz -C /usr/local/src --remove-files \
      && mv /usr/local/src/FREEC-* /usr/local/src/FREEC \
      && cd /usr/local/src/FREEC/src \
      && make \
      && find /usr/local/src/FREEC/src -maxdepth 1 -type f -executable \
        -exec ln -s {} /usr/local/bin \;

ENTRYPOINT ["/usr/local/bin/freec"]
