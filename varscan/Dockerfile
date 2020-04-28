FROM ubuntu:latest

ENV DEBIAN_FRONTEND noninteractive

ADD https://raw.githubusercontent.com/dceoy/print-github-tags/master/print-github-tags /usr/local/bin/print-github-tags

RUN set -e \
      && ln -sf /bin/bash /bin/sh

RUN set -e \
      && apt-get -y update \
      && apt-get -y dist-upgrade \
      && apt-get -y install --no-install-recommends --no-install-suggests \
        ca-certificates curl default-jre \
      && apt-get -y autoremove \
      && apt-get clean \
      && rm -rf /var/lib/apt/lists/*

RUN set -eo pipefail \
      && mkdir /opt/varscan \
      && chmod +x /usr/local/bin/print-github-tags \
      && print-github-tags --release --latest dkoboldt/varscan \
        | xargs -i curl -SL \
          https://github.com/dkoboldt/varscan/releases/download/{}/VarScan.v{}.jar \
          -o /opt/varscan/VarScan.jar

RUN set -e \
      && mkdir /opt/varscan/bin \
      && echo '#!/usr/bin/env bash' > /opt/varscan/bin/VarScan \
      && echo 'java -jar /opt/varscan/VarScan.jar ${@}' \
        >> /opt/varscan/bin/VarScan \
      && chmod +x /opt/varscan/bin/VarScan

ENV PATH /opt/varscan/bin:${PATH}

ENTRYPOINT ["/usr/bin/java", "-jar", "/opt/varscan/VarScan.jar"]
