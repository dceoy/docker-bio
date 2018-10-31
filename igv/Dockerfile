FROM ubuntu:latest

ENV DEBIAN_FRONTEND noninteractive

RUN set -e \
      && apt-get -y update \
      && apt-get -y dist-upgrade \
      && apt-get -y install --no-install-recommends --no-install-suggests \
        ca-certificates curl openjdk-8-jre unzip \
      && apt-get -y autoremove \
      && apt-get clean \
      && rm -rf /var/lib/apt/lists/*

RUN set -e \
      && curl -sS https://api.github.com/repos/igvteam/igv/tags \
        | grep '"name":' | head -1 \
        | sed -e 's/^.*: \+"v\([0-9]\+\)\.\([0-9]\+\)\.\([0-9]\+\)".*$/\1\.\2\/IGV_\1\.\2\.\3\.zip/' \
        | xargs -i curl -S http://data.broadinstitute.org/igv/projects/downloads/{} -o /tmp/igv.zip \
      && unzip -d /usr/local/src /tmp/igv.zip \
      && mv /usr/local/src/IGV_* /usr/local/src/igv \
      && rm -f /tmp/igv.zip

ENTRYPOINT ["/usr/local/src/igv/igv.sh"]
