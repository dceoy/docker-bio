FROM ubuntu:latest

ENV DEBIAN_FRONTEND noninteractive

ADD https://cloud.r-project.org/bin/linux/ubuntu/marutter_pubkey.asc /tmp/marutter_pubkey.asc
ADD https://raw.githubusercontent.com/dceoy/clir/master/install_clir.sh /tmp/install_clir.sh

RUN set -e \
      && apt-get -y update \
      && apt-get -y install --no-install-recommends --no-install-suggests \
        dirmngr software-properties-common \
      && cat /tmp/marutter_pubkey.asc >> /etc/apt/trusted.gpg.d/cran_ubuntu_key.asc \
      && lsb_release -cs \
        | xargs -i add-apt-repository \
          'deb https://cloud.r-project.org/bin/linux/ubuntu {}-cran40/' \
      && apt-get -y update \
      && apt-get -y dist-upgrade \
      && apt-get -y install --no-install-recommends --no-install-suggests \
        apt-transport-https apt-utils ca-certificates curl g++ gcc gfortran \
        git libblas-dev libcurl4-gnutls-dev libgit2-dev liblapack-dev libssh-dev \
        libssl-dev libxml2-dev make r-base \
      && apt-get -y autoremove \
      && apt-get clean \
      && rm -rf /tmp/marutter_pubkey.asc /var/lib/apt/lists/*

RUN set -e \
      && bash /tmp/install_clir.sh --root \
      && clir update \
      && clir install --devt=bioc GenomicRanges \
      && clir install --devt=github VanLoo-lab/ascat/ASCAT \
      && clir validate ASCAT \
      && rm -f /tmp/install_clir.sh

ENTRYPOINT ["/usr/bin/R"]
