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
      && mkdir /usr/local/src/abra \
      && chmod +x /usr/local/bin/print-github-tags \
      && print-github-tags --latest mozack/abra \
        | cut -d v -f 2 \
        | xargs -i curl -SL \
          https://github.com/mozack/abra/releases/download/v{}/abra-{}-SNAPSHOT-jar-with-dependencies.jar \
          -o /usr/local/src/abra/abra.jar

ENTRYPOINT ["/usr/bin/java", "-jar", "/usr/local/src/abra/abra.jar"]
