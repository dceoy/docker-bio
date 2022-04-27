FROM ubuntu:20.04

ENV DEBIAN_FRONTEND noninteractive

ADD https://raw.githubusercontent.com/dceoy/clir/master/install_clir.sh /tmp/install_clir.sh
ADD https://raw.githubusercontent.com/dceoy/print-github-tags/master/print-github-tags /usr/local/bin/print-github-tags

RUN set -e \
      && ln -sf bash /bin/sh \
      && ln -s python3 /usr/bin/python

RUN set -e \
      && apt-get -y update \
      && apt-get -y dist-upgrade \
      && apt-get -y install --no-install-recommends --no-install-suggests \
        autoconf apt-transport-https apt-utils ca-certificates curl g++ gcc \
        gfortran git gnuplot libblas-dev libbz2-dev libcurl4-gnutls-dev \
        libgit2-dev libjpeg-turbo8-dev liblapack-dev liblzma-dev \
        libncurses5-dev libpng-dev libssh-dev libssl-dev libtbb-dev \
        libxml2-dev libz-dev make perl perl-doc pkg-config python3 r-base \
      && apt-get -y autoremove \
      && apt-get clean \
      && rm -rf /var/lib/apt/lists/*

RUN set -e \
      && bash /tmp/install_clir.sh --root \
      && clir update \
      && rm -f /tmp/install_clir.sh

RUN set -eo pipefail \
      && chmod +x /usr/local/bin/print-github-tags \
      && print-github-tags --release --latest --tar BenLangmead/bowtie2 \
        | xargs -i curl -SL {} -o /tmp/bowtie2.tar.gz \
      && tar xvf /tmp/bowtie2.tar.gz -C /usr/local/src --remove-files \
      && mv /usr/local/src/bowtie2-* /usr/local/src/bowtie2 \
      && cd /usr/local/src/bowtie2 \
      && make \
      && make install

RUN set -eo pipefail \
      && print-github-tags --release --latest --tar alexdobin/STAR \
        | xargs -i curl -SL {} -o /tmp/star.tar.gz \
      && tar xvf /tmp/star.tar.gz -C /usr/local/src --remove-files \
      && mv /usr/local/src/STAR-* /usr/local/src/STAR \
      && cd /usr/local/src/STAR/source \
      && make STAR \
      && find /usr/local/src/STAR/bin/Linux_x86_64 -type f -executable \
        -exec ln -s {} /usr/local/bin \;

RUN set -eo pipefail \
      && print-github-tags --release --latest --tar deweylab/RSEM \
        | xargs -i curl -SL {} -o /tmp/rsem.tar.gz \
      && tar xvf /tmp/rsem.tar.gz -C /usr/local/src --remove-files \
      && mv /usr/local/src/RSEM-* /usr/local/src/RSEM \
      && cd /usr/local/src/RSEM/samtools-*/htslib-* \
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
      && make install \
      && cd .. \
      && make \
      && make ebseq \
      && make pRSEM \
      && make install

ENTRYPOINT ["/usr/local/bin/rsem-calculate-expression"]
