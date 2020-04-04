FROM ubuntu:latest

ENV DEBIAN_FRONTEND noninteractive

ADD https://raw.githubusercontent.com/dceoy/print-github-tags/master/print-github-tags /usr/local/bin/print-github-tags

RUN set -e \
      && ln -sf /bin/bash /bin/sh

RUN set -e \
      && apt-get -y update \
      && apt-get -y dist-upgrade \
      && apt-get -y install --no-install-recommends --no-install-suggests \
        autoconf bioperl ca-certificates cpanminus curl g++ gcc git \
        libbz2-dev libcurl4-gnutls-dev liblzma-dev libncurses5-dev \
        libmysqlclient-dev libssl-dev libxml-dom-xpath-perl \
        libxml-parser-perl libz-dev make perl pkg-config unzip \
      && apt-get -y autoremove \
      && apt-get clean \
      && rm -rf /var/lib/apt/lists/*

RUN set -e \
      && git clone --depth 1 https://github.com/bioperl/bioperl-ext.git \
        /usr/local/src/bioperl-ext \
      && cd /usr/local/src/bioperl-ext/Bio/Ext/Align \
      && perl -pi -e "s|(cd libs.+)CFLAGS=\\\'|\$1CFLAGS=\\\'-fPIC |" \
        Makefile.PL \
      && perl Makefile.PL \
      && make \
      && make install

ENV PERL5LIB ${PERL5LIB}:/usr/local/lib/x86_64-linux-gnu/perl/5.22.1

RUN set -eo pipefail \
      && chmod +x /usr/local/bin/print-github-tags \
      && print-github-tags --release --latest --tar Ensembl/ensembl-vep \
        | xargs -i curl -SL {} -o /tmp/ensembl-vep.tar.gz \
      && tar xvf /tmp/ensembl-vep.tar.gz -C /usr/local/src --remove-files \
      && mv /usr/local/src/ensembl-vep-* /usr/local/src/ensembl-vep \
      && cd /usr/local/src/ensembl-vep \
      && cpanm Test::Warnings \
      && cpanm --installdeps --with-recommends . \
      && perl INSTALL.pl \
      && find /usr/local/src/ensembl-vep -maxdepth 1 -type f -executable \
        -exec ln -s {} /usr/local/bin \;

ENTRYPOINT ["/usr/bin/vep"]
