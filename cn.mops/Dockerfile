FROM ubuntu:latest

ENV DEBIAN_FRONTEND noninteractive

ADD https://raw.githubusercontent.com/dceoy/clir/master/install_clir.sh /tmp/install_clir.sh
ADD https://raw.githubusercontent.com/dceoy/print-github-tags/master/print-github-tags /usr/local/bin/print-github-tags

RUN set -e \
      && apt-get -y update \
      && apt-get -y dist-upgrade \
      && apt-get -y install --no-install-recommends --no-install-suggests \
        apt-transport-https apt-utils autoconf ca-certificates curl g++ gcc \
        gfortran git libblas-dev libbz2-dev libcurl4-gnutls-dev libgit2-dev \
        liblapack-dev liblzma-dev libssh-dev libssl-dev libxml2-dev make \
        r-base \
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
      && bash /tmp/install_clir.sh --root \
      && clir update \
      && clir install --devt=bioc cn.mops \
      && clir validate cn.mops \
      && rm -f /tmp/install_clir.sh

ENTRYPOINT ["/usr/bin/R"]
