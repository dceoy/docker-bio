FROM ubuntu:latest

ENV DEBIAN_FRONTEND noninteractive

ADD https://raw.githubusercontent.com/dceoy/print-github-tags/master/print-github-tags /usr/local/bin/print-github-tags

RUN set -e \
      && apt-get -y update \
      && apt-get -y dist-upgrade \
      && apt-get -y install --no-install-recommends --no-install-suggests \
        ca-certificates curl openjdk-8-jdk unzip \
      && apt-get -y autoremove \
      && apt-get clean \
      && rm -rf /var/lib/apt/lists/*

RUN set -e \
      && chmod +x /usr/local/bin/print-github-tags \
      && print-github-tags --latest igvteam/igv \
        | sed -e 's/^v\([0-9]\+\)\.\([0-9]\+\)\.\([0-9]\+\)$/\1\.\2\/IGV_\1\.\2\.\3\.zip/' \
        | xargs -i curl -S \
          http://data.broadinstitute.org/igv/projects/downloads/{}/IGV_{}.zip \
          -o /tmp/igv.zip \
      && unzip -d /usr/local/src /tmp/igv.zip \
      && mv /usr/local/src/IGV_* /usr/local/src/igv \
      && rm -f /tmp/igv.zip

ENV DISPLAY :0.0

ENTRYPOINT ["/usr/local/src/igv/igv.sh"]
