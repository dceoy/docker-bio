FROM ubuntu:latest

ENV DEBIAN_FRONTEND noninteractive

RUN set -e \
      && apt-get -y update \
      && apt-get -y dist-upgrade \
      && apt-get -y install --no-install-recommends --no-install-suggests \
        ca-certificates curl g++ gcc libz-dev make \
      && apt-get -y autoremove \
      && apt-get clean \
      && rm -rf /var/lib/apt/lists/*

RUN set -e \
      && curl -sS https://github.com/alexdobin/STAR/releases/latest \
        | sed -e 's/^.*"\(https:\/\/github.com\/[^\/]\+\/[^\/]\+\/\)releases\/tag\(\/[^"]\+\)".*$/\1archive\2\.tar\.gz/' \
        | xargs -i curl -SL {} -o /tmp/star.tar.gz \
      && tar xvf /tmp/star.tar.gz -C /usr/local/src --remove-files \
      && mv /usr/local/src/STAR-* /usr/local/src/STAR \
      && cd /usr/local/src/STAR/source \
      && make STAR \
      && ln -s /usr/local/src/STAR/source/STAR /usr/local/bin/STAR

ENTRYPOINT ["/usr/local/bin/STAR"]
