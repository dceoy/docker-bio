FROM ubuntu:latest

ENV DEBIAN_FRONTEND noninteractive

RUN set -e \
      && apt-get -y update \
      && apt-get -y dist-upgrade \
      && apt-get -y install --no-install-recommends --no-install-suggests \
        ca-certificates curl unzip \
      && apt-get -y autoremove \
      && apt-get clean \
      && rm -rf /var/lib/apt/lists/*

RUN set -e \
      && curl -sS https://github.com/infphilo/hisat2/releases/latest \
        | sed -e 's/^.*"\(https:\/\/github.com\/[^\/]\+\/[^\/]\+\/\)releases\/tag\(\/[^"]\+\)".*$/\1archive\2\.tar\.gz/' \
        | xargs -i curl -SL {} -o /tmp/hisat2.tar.gz \
      && tar xvf /tmp/hisat2.tar.gz -C /tmp --remove-files \
      && cat /tmp/hisat2-*/VERSION \
        | xargs -i curl -S \
          ftp://ftp.ccb.jhu.edu/pub/infphilo/hisat2/downloads/hisat2-{}-Linux_x86_64.zip \
          -o /tmp/hisat2.zip \
      && rm -rf /tmp/hisat2-* \
      && unzip -d /usr/local/src /tmp/hisat2.zip \
      && mv /usr/local/src/hisat2-* /usr/local/src/hisat2 \
      && find /usr/local/src/hisat2 -type f -maxdepth 1 -executable | xargs -i ln -s {} /usr/local/bin \
      && rm -f /tmp/hisat2.zip

ENTRYPOINT ["/usr/local/bin/hisat2"]
