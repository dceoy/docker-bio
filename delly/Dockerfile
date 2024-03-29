FROM ubuntu:20.04

ENV DEBIAN_FRONTEND noninteractive

ADD https://raw.githubusercontent.com/dceoy/clir/master/install_clir.sh /tmp/install_clir.sh
ADD https://raw.githubusercontent.com/dceoy/print-github-tags/master/print-github-tags /usr/local/bin/print-github-tags

RUN set -e \
      && ln -sf bash /bin/sh

RUN set -e \
      && apt-get -y update \
      && apt-get -y dist-upgrade \
      && apt-get -y install --no-install-recommends --no-install-suggests \
        apt-transport-https apt-utils ca-certificates curl g++ gcc gfortran \
        git libblas-dev libbz2-dev libcairo2-dev libcurl4-gnutls-dev \
        libfontconfig1-dev libfreetype6-dev libfribidi-dev libgdal-dev \
        libgeos-dev libgit2-dev libgsl-dev libharfbuzz-dev libjpeg-dev \
        libjpeg-turbo8-dev liblapack-dev liblzma-dev libperl-dev libpng-dev \
        libssh-dev libssl-dev libtiff5-dev libudunits2-dev libxml2-dev \
        libz-dev make r-base \
      && apt-get -y autoremove \
      && apt-get clean \
      && rm -rf /var/lib/apt/lists/*

RUN set -e \
      && bash /tmp/install_clir.sh --root \
      && clir update \
      && clir install --devt=cran ggplot2 reshape2 \
      && clir validate ggplot2 reshape2 \
      && rm -f /tmp/install_clir.sh

RUN set -eo pipefail \
      && chmod +x /usr/local/bin/print-github-tags \
      && print-github-tags --release --latest samtools/bcftools \
        | xargs -i curl -SL \
          https://github.com/samtools/bcftools/releases/download/{}/bcftools-{}.tar.bz2 \
          -o /tmp/bcftools.tar.bz2 \
      && tar xvf /tmp/bcftools.tar.bz2 -C /usr/local/src --remove-files \
      && mv /usr/local/src/bcftools-* /usr/local/src/bcftools \
      && cd /usr/local/src/bcftools \
      && autoheader \
      && autoconf \
      && ./configure --enable-libgsl --enable-perl-filters \
      && make \
      && make install

RUN set -eo pipefail \
      && print-github-tags --release --latest dellytools/delly \
        | xargs -i curl -SL \
          https://github.com/dellytools/delly/releases/download/{}/delly_{}_linux_x86_64bit \
          -o /usr/local/bin/delly \
      && chmod +x /usr/local/bin/delly

ENV BCFTOOLS_PLUGINS /usr/local/src/bcftools/plugins

ENTRYPOINT ["/usr/local/bin/delly"]
