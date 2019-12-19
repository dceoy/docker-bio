FROM ubuntu:latest

ENV DEBIAN_FRONTEND noninteractive

ADD https://raw.githubusercontent.com/dceoy/print-github-tags/master/print-github-tags /usr/local/bin/print-github-tags

RUN set -e \
      && ln -sf /bin/bash /bin/sh

RUN set -e \
      && apt-get -y update \
      && apt-get -y dist-upgrade \
      && apt-get -y install --no-install-recommends --no-install-suggests \
        ca-certificates curl default-jre gcc libz-dev make \
      && apt-get -y autoremove \
      && apt-get clean \
      && rm -rf /var/lib/apt/lists/*

RUN set -eo pipefail \
      && chmod +x /usr/local/bin/print-github-tags \
      && print-github-tags --release --latest --tar lh3/bwa \
        | xargs -i curl -SL {} -o /tmp/bwa.tar.gz \
      && tar xvf /tmp/bwa.tar.gz -C /usr/local/src --remove-files \
      && mv /usr/local/src/bwa-* /usr/local/src/bwa \
      && cd /usr/local/src/bwa \
      && make \
      && find /usr/local/src/bwa -maxdepth 1 -type f -executable \
        -exec ln -s {} /usr/local/bin \;

RUN set -eo pipefail \
      && mkdir /usr/local/src/abra \
      && print-github-tags --latest mozack/abra \
        | tr -d v \
        | xargs -i curl -SL \
          https://github.com/mozack/abra/releases/download/v{}/abra-{}-SNAPSHOT-jar-with-dependencies.jar \
          -o /usr/local/src/abra/abra.jar

ENTRYPOINT ["/usr/bin/java", "-jar", "/usr/local/src/abra/abra.jar"]
