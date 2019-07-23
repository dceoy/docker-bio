FROM ubuntu:latest

ENV DEBIAN_FRONTEND noninteractive

ADD https://raw.githubusercontent.com/dceoy/print-github-tags/master/print-github-tags /usr/local/bin/print-github-tags

RUN set -e \
      && apt-get -y update \
      && apt-get -y dist-upgrade \
      && apt-get -y install --no-install-recommends --no-install-suggests \
        ca-certificates curl libxrender1 libxext6 libxi6 libxtst6 unzip \
      && apt-get -y autoremove \
      && apt-get clean \
      && rm -rf /var/lib/apt/lists/*

RUN set -e \
      && chmod +x /usr/local/bin/print-github-tags \
      && print-github-tags --latest igvteam/igv \
        | sed -e 's/^v\([0-9]\+\)\.\([0-9]\+\)\.\([0-9]\+\)$/\1\.\2\/IGV_Linux_\1\.\2\.\3\.zip/' \
        | xargs -i curl -S \
          https://data.broadinstitute.org/igv/projects/downloads/{} \
          -o /tmp/igv.zip \
      && unzip -d /opt /tmp/igv.zip \
      && mv /opt/IGV_* /opt/igv \
      && rm -f /tmp/igv.zip

ENV PATH ${PATH}:/opt/igv/jdk-11/bin

ENTRYPOINT ["/opt/igv/igv.sh"]
