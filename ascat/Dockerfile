FROM dceoy/clir:latest

RUN set -e \
      && apt-get -y update \
      && apt-get -y dist-upgrade \
      && apt-get -y install --no-install-recommends --no-install-suggests \
        apt-transport-https curl \
      && apt-get -y autoremove \
      && apt-get clean \
      && rm -rf /var/lib/apt/lists/*

RUN set -e \
      && clir update \
      && clir install --devt=github Crick-CancerGenomics/ascat/ASCAT \
      && clir validate ASCAT

ENTRYPOINT ["/usr/bin/R"]
