FROM ubuntu:latest

ENV DEBIAN_FRONTEND noninteractive

ADD https://raw.githubusercontent.com/dceoy/print-github-tags/master/print-github-tags /usr/local/bin/print-github-tags
ADD https://bootstrap.pypa.io/get-pip.py /tmp/get-pip.py

RUN set -e \
      && ln -sf bash /bin/sh

RUN set -e \
      && apt-get -y update \
      && apt-get -y dist-upgrade \
      && apt-get -y install --no-install-recommends --no-install-suggests \
        autoconf automake bsdmainutils ca-certificates curl g++ gawk gcc git \
        libbz2-dev libc6-dev libcurl4-gnutls-dev liblzma-dev libncurses5-dev \
        libssl-dev libz-dev make pkg-config python \
      && apt-get -y autoremove \
      && apt-get clean \
      && rm -rf /var/lib/apt/lists/*

RUN set -e \
      && /usr/bin/python /tmp/get-pip.py \
      && pip install -U --no-cache-dir numpy pip pysam \
      && rm -f /tmp/get-pip.py

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
      && print-github-tags --release --latest GregoryFaust/samblaster \
        | xargs -i curl -SL \
          https://github.com/GregoryFaust/samblaster/releases/download/{}/samblaster-{}.tar.gz \
          -o /tmp/samblaster.tar.bz2 \
      && tar xvf /tmp/samblaster.tar.bz2 -C /usr/local/src --remove-files \
      && mv /usr/local/src/samblaster-* /usr/local/src/samblaster \
      && cd /usr/local/src/samblaster \
      && make \
      && find /usr/local/src/samblaster -maxdepth 1 -type f -executable \
        -exec ln -s {} /usr/local/bin \;

RUN set -eo pipefail \
      && print-github-tags --release --latest biod/sambamba \
        | tr -d v \
        | xargs -i curl -SL \
          https://github.com/biod/sambamba/releases/download/v{}/sambamba-{}-linux-static.gz \
        | gzip -dc - > /usr/local/bin/sambamba \
      && chmod +x /usr/local/bin/sambamba

RUN set -eo pipefail \
      && print-github-tags --release --latest arq5x/lumpy-sv \
        | tr -d v \
        | xargs -i curl -SL \
          https://github.com/arq5x/lumpy-sv/releases/download/{}/lumpy-sv.tar.gz \
          -o /tmp/lumpy-sv.tar.gz \
      && tar xvf /tmp/lumpy-sv.tar.gz -C /opt --remove-files \
      && cd /opt/lumpy-sv/lib/htslib \
      && autoheader \
      && autoconf \
      && make \
      && make install \
      && cd /opt/lumpy-sv \
      && make \
      && sed -ie 's/\/\//\//; s/\/$//;' bin/lumpyexpress.config

ENV PATH /opt/lumpy-sv/bin:${PATH}

ENTRYPOINT ["/opt/lumpy-sv/bin/lumpy"]
