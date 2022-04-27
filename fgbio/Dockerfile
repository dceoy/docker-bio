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
      && mkdir /opt/fgbio \
      && chmod +x /usr/local/bin/print-github-tags \
      && print-github-tags --release --latest fulcrumgenomics/fgbio \
        | xargs -i curl -SL \
          https://github.com/fulcrumgenomics/fgbio/releases/download/{}/fgbio-{}.jar \
          -o /opt/fgbio/fgbio.jar

RUN set -e \
      && mkdir /opt/fgbio/bin \
      && echo '#!/usr/bin/env bash' > /opt/fgbio/bin/fgbio \
      && echo 'java -XX:+AggressiveOpts -XX:+AggressiveHeap -jar /opt/fgbio/fgbio.jar ${@}' \
        >> /opt/fgbio/bin/fgbio \
      && chmod +x /opt/fgbio/bin/fgbio

ENV PATH /opt/fgbio/bin:${PATH}

ENTRYPOINT ["/usr/bin/java", "-XX:+AggressiveOpts", "-XX:+AggressiveHeap", "-jar", "/opt/fgbio/fgbio.jar"]
