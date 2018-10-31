FROM ubuntu:latest

ENV DEBIAN_FRONTEND noninteractive

RUN set -e \
      && apt-get -y update \
      && apt-get -y dist-upgrade \
      && apt-get -y install --no-install-recommends --no-install-suggests \
        ca-certificates curl default-jre \
      && apt-get -y autoremove \
      && apt-get clean \
      && rm -rf /var/lib/apt/lists/*

RUN set -e \
      && curl -sS https://github.com/broadinstitute/picard/releases/latest \
        | sed -e 's/^.*"\(https:\/\/github.com\/[^\/]\+\/[^\/]\+\/releases\/\)tag\(\/[^"]\+\)".*$/\1download\2\/picard.jar/' \
        | xargs -i curl -SL {} -o /usr/local/src/picard.jar

ENTRYPOINT ["/usr/bin/java", "-jar", "/usr/local/src/picard.jar"]
