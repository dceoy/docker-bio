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
      && mkdir /usr/local/src/varscan \
      && chmod +x /usr/local/bin/print-github-tags \
      && print-github-tags --release --latest --tar dkoboldt/varscan \
        | xargs -i curl -SL \
          https://github.com/dkoboldt/varscan/releases/download/{}/VarScan.v{}.jar \
          -o /usr/local/src/varscan/VarScan.jar

ENTRYPOINT ["/usr/bin/java", "-jar", "/usr/local/src/varscan/VarScan.jar"]
