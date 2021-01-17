FROM ubuntu:latest

ENV DEBIAN_FRONTEND noninteractive

ADD https://github.com/ucscGenomeBrowser/kent/archive/v335_base.tar.gz /tmp/kent.tar.gz
ADD https://raw.githubusercontent.com/dceoy/print-github-tags/master/print-github-tags /usr/local/bin/print-github-tags

RUN set -e \
      && ln -sf bash /bin/sh

RUN set -e \
      && apt-get -y update \
      && apt-get -y dist-upgrade \
      && apt-get -y install --no-install-recommends --no-install-suggests \
        autoconf ca-certificates cpanminus curl g++ gcc git libbz2-dev \
        libcurl4-gnutls-dev liblzma-dev libmysqlclient-dev libncurses5-dev \
        libpng-dev libssl-dev libxml-dom-xpath-perl libxml-parser-perl \
        libz-dev make perl pkg-config unzip \
      && apt-get -y autoremove \
      && apt-get clean \
      && rm -rf /var/lib/apt/lists/*

RUN set -eo pipefail \
      && tar xvf /tmp/kent.tar.gz -C /usr/local/src --remove-files \
      && mv /usr/local/src/kent-* /usr/local/src/kent \
      && export KENT_SRC=/usr/local/src/kent/src \
      && export MACHTYPE=$(uname -m) \
      && export CFLAGS='-fPIC' \
      && export MYSQLINC=`mysql_config --include | sed -e 's/^-I//g'` \
      && export MYSQLLIBS=`mysql_config --libs` \
      && cd /usr/local/src/kent/src/lib \
      && echo 'CFLAGS="-fPIC"' > ../inc/localEnvironment.mk \
      && make clean \
      && make \
      && cd ../jkOwnLib \
      && make clean \
      && make \
      && cpanm Bio::DB::BigFile Test::Warnings

RUN set -eo pipefail \
      && git clone --depth 1 https://github.com/bioperl/bioperl-ext.git \
        /usr/local/src/bioperl-ext \
      && cd /usr/local/src/bioperl-ext/Bio/Ext/Align \
      && perl -pi -e "s|(cd libs.+)CFLAGS=\\\'|\$1CFLAGS=\\\'-fPIC |" \
        Makefile.PL \
      && perl Makefile.PL \
      && make \
      && make install

RUN set -eo pipefail \
      && chmod +x /usr/local/bin/print-github-tags \
      && print-github-tags --latest --tar Ensembl/ensembl-xs \
        | xargs -i curl -SL {} -o /tmp/ensembl-xs.tar.gz \
      && tar xvf /tmp/ensembl-xs.tar.gz -C /usr/local/src --remove-files \
      && mv /usr/local/src/ensembl-xs-* /usr/local/src/ensembl-xs \
      && cd /usr/local/src/ensembl-xs \
      && cpanm --installdeps --with-recommends . \
      && perl Makefile.PL \
      && make \
      && make install

RUN set -eo pipefail \
      && print-github-tags --release --latest --tar Ensembl/ensembl-vep \
        | xargs -i curl -SL {} -o /tmp/ensembl-vep.tar.gz \
      && tar xvf /tmp/ensembl-vep.tar.gz -C /usr/local/src --remove-files \
      && mv /usr/local/src/ensembl-vep-* /usr/local/src/ensembl-vep \
      && cd /usr/local/src/ensembl-vep \
      && cpanm --installdeps --with-recommends . \
      && perl INSTALL.pl --AUTO a \
      && find /usr/local/src/ensembl-vep -maxdepth 1 -type f -executable \
        -exec ln -s {} /usr/local/bin \;

ENTRYPOINT ["/usr/local/bin/vep"]
