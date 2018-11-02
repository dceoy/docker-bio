# This Dockerfile is unfinished.

FROM ubuntu:latest

ENV DEBIAN_FRONTEND noninteractive

ADD https://raw.githubusercontent.com/dceoy/print-github-tags/master/print-github-tags /usr/local/bin/print-github-tags
ADD https://github.com/genome/pindel/archive/master.tar.gz /tmp/pindel.tar.gz

RUN set -e \
      && apt-get -y update \
      && apt-get -y dist-upgrade \
      && apt-get -y install --no-install-recommends --no-install-suggests \
        autoconf ca-certificates curl g++ gcc libbz2-dev liblzma-dev \
        libncurses5-dev libz-dev make \
      && apt-get -y autoremove \
      && apt-get clean \
      && rm -rf /var/lib/apt/lists/*

 RUN set -e \
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

RUN set -e \
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

RUN set -e \
      && tar xvf /tmp/pindel.tar.gz -C /usr/local/src --remove-files \
      && mv /usr/local/src/pindel-* /usr/local/src/pindel \
      && cd /usr/local/src/pindel \
      && ./INSTALL ../htslib \
      && ln -s /usr/local/src/pindel/pindel /usr/local/bin

ENTRYPOINT ["/usr/local/bin/pindel"]
