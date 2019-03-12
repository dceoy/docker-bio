FROM ubuntu:latest

ADD annovar.latest.tar.gz /usr/local/src/

RUN set -e \
      && apt-get -y update \
      && apt-get -y dist-upgrade \
      && apt-get -y install --no-install-recommends --no-install-suggests \
        ca-certificates perl unzip wget \
      && apt-get -y autoremove \
      && apt-get clean \
      && rm -rf /var/lib/apt/lists/*

RUN set -e \
      && find /usr/local/src/annovar -type f -maxdepth 1 -executable \
        | xargs -i ln -s {} /usr/local/bin

ENTRYPOINT ["/usr/bin/perl", "/usr/local/src/annovar/annotate_variation.pl"]
