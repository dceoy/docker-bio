FROM ubuntu:latest

ENV DEBIAN_FRONTEND noninteractive

RUN set -e \
      && ln -sf bash /bin/sh

RUN set -e \
      && apt-get -y update \
      && apt-get -y dist-upgrade \
      && apt-get -y install --no-install-recommends --no-install-suggests \
        ca-certificates curl git golang \
      && apt-get -y autoremove \
      && apt-get clean \
      && rm -rf /var/lib/apt/lists/*

ENV PATH ${PATH}:/go/bin
ENV GOPATH /go

RUN set -e \
      && mkdir /go \
      && go get -u github.com/brentp/goleft/... \
      && go install github.com/brentp/goleft/cmd/goleft

ENTRYPOINT ["/go/bin/goleft"]
