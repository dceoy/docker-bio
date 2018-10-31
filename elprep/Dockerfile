FROM ubuntu:latest

ENV DEBIAN_FRONTEND noninteractive

RUN set -e \
      && apt-get -y update \
      && apt-get -y dist-upgrade \
      && apt-get -y install --no-install-recommends --no-install-suggests \
        autoconf ca-certificates curl gcc git golang libbz2-dev liblzma-dev libncurses5-dev \
        libz-dev make parallel \
      && apt-get -y autoremove \
      && apt-get clean \
      && rm -rf /var/lib/apt/lists/*

RUN set -e \
      && curl -sS https://github.com/samtools/htslib/releases/latest \
        | sed -e 's/^.*"\(https:\/\/github.com\/[^\/]\+\/[^\/]\+\/\)releases\/tag\(\/[^"]\+\)".*$/\1archive\2\.tar\.gz/' \
        | xargs -i curl -SL {} -o /tmp/htslib.tar.gz \
      && tar xvf /tmp/htslib.tar.gz -C /usr/local/src --remove-files \
      && mv /usr/local/src/htslib-* /usr/local/src/htslib \
      && cd /usr/local/src/htslib \
      && autoheader \
      && autoconf \
      && ./configure \
      && make \
      && make install

RUN set -e \
      && curl -sS https://github.com/samtools/samtools/releases/latest \
        | sed -e 's/^.*"\(https:\/\/github.com\/[^\/]\+\/[^\/]\+\/\)releases\/tag\(\/[^"]\+\)".*$/\1archive\2\.tar\.gz/' \
        | xargs -i curl -SL {} -o /tmp/samtools.tar.gz \
      && tar xvf /tmp/samtools.tar.gz -C /usr/local/src --remove-files \
      && mv /usr/local/src/samtools-* /usr/local/src/samtools \
      && cd /usr/local/src/samtools \
      && autoheader \
      && autoconf \
      && ./configure \
      && make \
      && make install

ENV PATH ${PATH}:/go/bin
ENV GOPATH /go

RUN set -e \
      && mkdir /go \
      && go get github.com/exascience/elprep

ENTRYPOINT ["/go/bin/elprep"]
