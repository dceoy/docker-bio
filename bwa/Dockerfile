FROM ubuntu:latest

ENV DEBIAN_FRONTEND noninteractive

RUN set -e \
      && apt-get -y update \
      && apt-get -y dist-upgrade \
      && apt-get -y install --no-install-recommends --no-install-suggests \
        ca-certificates curl gcc libz-dev make \
      && apt-get -y autoremove \
      && apt-get clean \
      && rm -rf /var/lib/apt/lists/*

RUN set -e \
      && curl -sS https://github.com/lh3/bwa/releases/latest \
        | sed -e 's/^.*"\(https:\/\/github.com\/[^\/]\+\/[^\/]\+\/\)releases\/tag\(\/[^"]\+\)".*$/\1archive\2\.tar\.gz/' \
        | xargs -i curl -SL {} -o /tmp/bwa.tar.gz \
      && tar xvf /tmp/bwa.tar.gz -C /usr/local/src --remove-files \
      && mv /usr/local/src/bwa-* /usr/local/src/bwa \
      && cd /usr/local/src/bwa \
      && make \
      && ln -s /usr/local/src/bwa/bwa /usr/local/bin

ENTRYPOINT ["/usr/local/bin/bwa"]
