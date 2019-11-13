FROM ubuntu:latest

ENV DEBIAN_FRONTEND noninteractive

ADD https://sourceforge.net/projects/prinseq/files/latest/download?source=files /tmp/prinseq.tar.gz

RUN set -e \
      && apt-get -y update \
      && apt-get -y dist-upgrade \
      && apt-get -y install --no-install-recommends --no-install-suggests \
        perl \
      && apt-get -y autoremove \
      && apt-get clean \
      && rm -rf /var/lib/apt/lists/*

RUN set -e \
      && tar xvf /tmp/prinseq.tar.gz -C /usr/local/src --remove-files \
      && mv /usr/local/src/prinseq-* /usr/local/src/prinseq \
      && chmod +x /usr/local/src/prinseq/*.pl \
      && find /usr/local/src/prinseq -maxdepth 1 -type f -executable \
        -exec ln -s {} /usr/local/bin \;

ENTRYPOINT ["/usr/bin/perl", "/usr/local/src/prinseq/prinseq-lite.pl"]
