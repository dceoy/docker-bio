FROM ubuntu:20.04

ENV DEBIAN_FRONTEND noninteractive

ADD https://bootstrap.pypa.io/pip/2.7/get-pip.py /tmp/get-pip.py
ADD https://raw.githubusercontent.com/dceoy/print-github-tags/master/print-github-tags /usr/local/bin/print-github-tags

RUN set -e \
      && ln -sf bash /bin/sh

RUN set -e \
      && apt-get -y update \
      && apt-get -y dist-upgrade \
      && apt-get -y install --no-install-recommends --no-install-suggests \
        autoconf ca-certificates curl g++ gcc libbz2-dev libcurl4-gnutls-dev \
        liblzma-dev libncurses5-dev libssl-dev libz-dev make python-dev \
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
      && cd /usr/local/src/samtools \
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

RUN set -e \
      && /usr/bin/python /tmp/get-pip.py \
      && pip install -U --no-cache-dir pip misopy \
      && rm -f /tmp/get-pip.py

ENTRYPOINT ["/usr/local/bin/miso"]
