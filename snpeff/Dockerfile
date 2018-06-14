FROM ubuntu:latest

ENV DEBIAN_FRONTEND noninteractive

RUN set -e \
      && apt-get -y update \
      && apt-get -y dist-upgrade \
      && apt-get -y install --no-install-recommends --no-install-suggests \
                            ca-certificates curl default-jre unzip wget \
      && apt-get -y autoremove \
      && apt-get clean \
      && rm -rf /var/lib/apt/lists/*

RUN set -e \
      && wget -L http://sourceforge.net/projects/snpeff/files/snpEff_latest_core.zip -O /tmp/snpeff.zip \
      && unzip /tmp/snpeff.zip -d /usr/local/src \
      && rm -f /tmp/snpeff.zip

ENTRYPOINT ["/usr/bin/java", "-jar", "/usr/local/src/snpEff/snpEff.jar"]
