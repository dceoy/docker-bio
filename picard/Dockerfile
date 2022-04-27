FROM ubuntu:20.04

ENV DEBIAN_FRONTEND noninteractive

ADD https://raw.githubusercontent.com/dceoy/print-github-tags/master/print-github-tags /usr/local/bin/print-github-tags

RUN set -e \
      && ln -sf bash /bin/sh

RUN set -e \
      && apt-get -y update \
      && apt-get -y dist-upgrade \
      && apt-get -y install --no-install-recommends --no-install-suggests \
        ca-certificates curl openjdk-8-jre \
      && apt-get -y autoremove \
      && apt-get clean \
      && rm -rf /var/lib/apt/lists/*

RUN set -eo pipefail \
      && mkdir /opt/picard \
      && chmod +x /usr/local/bin/print-github-tags \
      && print-github-tags --release --latest broadinstitute/picard \
        | xargs -i curl -SL \
          https://github.com/broadinstitute/picard/releases/download/{}/picard.jar \
          -o /opt/picard/picard.jar

RUN set -e \
      && mkdir /opt/picard/bin \
      && echo '#!/usr/bin/env bash' > /opt/picard/bin/picard \
      && echo 'java -jar /opt/picard/picard.jar ${@}' \
        >> /opt/picard/bin/picard \
      && chmod +x /opt/picard/bin/picard

ENV PATH /opt/picard/bin:${PATH}

ENTRYPOINT ["/usr/bin/java", "-jar", "/opt/picard/picard.jar"]
