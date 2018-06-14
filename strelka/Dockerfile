FROM ubuntu:latest

ENV DEBIAN_FRONTEND noninteractive

RUN set -e \
      && apt-get -y update \
      && apt-get -y dist-upgrade \
      && apt-get -y install --no-install-recommends --no-install-suggests \
                            ca-certificates curl bzip2 gcc git g++ make python wget zlib1g-dev \
      && apt-get -y autoremove \
      && apt-get clean \
      && rm -rf /var/lib/apt/lists/*

RUN set -e \
      && curl -sS https://github.com/Illumina/strelka/releases/latest \
        | sed -e 's/^.*"\(https:\/\/github.com\/[^\/]\+\/[^\/]\+\/\)releases\/tag\(\/[^"]\+\)".*$/\1archive\2\.tar\.gz/' \
        | xargs -i wget -L {} -O /tmp/strelka.tar.gz \
      && tar xvf /tmp/strelka.tar.gz -C /usr/local/src --remove-files \
      && mv /usr/local/src/strelka-* /usr/local/src/strelka \
      && cd /usr/local/src/strelka \
      && mkdir /usr/local/src/strelka/build \
      && cd /usr/local/src/strelka/build \
      && ../configure \
      && make install

ENTRYPOINT ["/usr/local/bin/configureStrelkaGermlineWorkflow.py"]
