FROM ubuntu:latest

ENV DEBIAN_FRONTEND noninteractive

ADD https://raw.githubusercontent.com/dceoy/print-github-tags/master/print-github-tags /usr/local/bin/print-github-tags

RUN set -e \
      && apt-get -y update \
      && apt-get -y dist-upgrade \
      && apt-get -y install --no-install-recommends --no-install-suggests \
        ca-certificates curl default-jre \
      && apt-get -y autoremove \
      && apt-get clean \
      && rm -rf /var/lib/apt/lists/*

RUN set -e \
      && mkdir /usr/local/src/picard \
      && chmod +x /usr/local/bin/print-github-tags \
      && print-github-tags --release --latest broadinstitute/picard \
        | xargs -i curl -SL \
          https://github.com/broadinstitute/picard/releases/download/{}/picard.jar \
          -o /usr/local/src/picard/picard.jar

ENTRYPOINT ["/usr/bin/java", "-jar", "/usr/local/src/picard/picard.jar"]
