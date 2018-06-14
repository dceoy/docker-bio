FROM ubuntu:latest

ENV DEBIAN_FRONTEND noninteractive

RUN set -e \
      && apt-get -y update \
      && apt-get -y dist-upgrade \
      && apt-get -y install --no-install-recommends --no-install-suggests \
                            ca-certificates curl default-jre wget \
      && apt-get -y autoremove \
      && apt-get clean \
      && rm -rf /var/lib/apt/lists/*

RUN set -e \
      && mkdir /usr/local/src/varscan \
      && curl -sS https://github.com/dkoboldt/varscan/releases/latest \
        | sed -e 's/^.*"\(https:\/\/github.com\/[^\/]\+\/[^\/]\+\/releases\/\)tag\/\([^"]\+\)".*$/\1download\/\2\/VarScan\.v\2\.jar/' \
        | xargs -i wget -L {} -O /usr/local/src/varscan/VarScan.jar

ENTRYPOINT ["/usr/bin/java", "-jar", "/usr/local/src/varscan/VarScan.jar"]
