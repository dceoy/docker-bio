FROM ubuntu:latest

ENV DEBIAN_FRONTEND noninteractive

ADD https://raw.githubusercontent.com/dceoy/clir/master/install_clir.sh /tmp/install_clir.sh

RUN set -e \
      && apt-get -y update \
      && apt-get -y dist-upgrade \
      && apt-get -y install --no-install-recommends --no-install-suggests \
        apt-transport-https apt-utils ca-certificates curl g++ gcc gfortran \
        git libblas-dev libcurl4-gnutls-dev libgit2-dev liblapack-dev libssh-dev \
        libssl-dev libxml2-dev make r-base \
      && apt-get -y autoremove \
      && apt-get clean \
      && rm -rf /var/lib/apt/lists/*

RUN set -e \
      && bash /tmp/install_clir.sh --root \
      && clir update \
      && clir install --devt=github Crick-CancerGenomics/ascat/ASCAT \
      && clir validate ASCAT \
      && rm -f /tmp/install_clir.sh

ENTRYPOINT ["/usr/bin/R"]
