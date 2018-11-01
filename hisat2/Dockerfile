FROM ubuntu:latest

ENV DEBIAN_FRONTEND noninteractive

ADD https://raw.githubusercontent.com/dceoy/print-github-tags/master/print-github-tags /usr/local/bin/print-github-tags

RUN set -e \
      && apt-get -y update \
      && apt-get -y dist-upgrade \
      && apt-get -y install --no-install-recommends --no-install-suggests \
        ca-certificates curl unzip \
      && apt-get -y autoremove \
      && apt-get clean \
      && rm -rf /var/lib/apt/lists/*

RUN set -e \
      && chmod +x /usr/local/bin/print-github-tags \
      && print-github-tags --release --latest infphilo/hisat2 \
        | xargs -i curl -S \
          ftp://ftp.ccb.jhu.edu/pub/infphilo/hisat2/downloads/hisat2-{}-Linux_x86_64.zip \
          -o /tmp/hisat2.zip \
      && unzip -d /usr/local/src /tmp/hisat2.zip \
      && mv /usr/local/src/hisat2-* /usr/local/src/hisat2 \
      && find /usr/local/src/hisat2 -type f -maxdepth 1 -executable | xargs -i ln -s {} /usr/local/bin \
      && rm -f /tmp/hisat2.zip

ENTRYPOINT ["/usr/local/bin/hisat2"]
