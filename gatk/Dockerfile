FROM ubuntu:latest

ENV DEBIAN_FRONTEND noninteractive

RUN set -e \
      && apt-get -y update \
      && apt-get -y dist-upgrade \
      && apt-get -y install --no-install-recommends --no-install-suggests \
        ca-certificates curl g++ gcc default-jre libc6-dev make python python3 r-base \
      && apt-get -y autoremove \
      && apt-get clean \
      && rm -rf /var/lib/apt/lists/*

RUN set -e \
      && curl -sS https://github.com/broadinstitute/gatk/releases/latest \
        | sed -e 's/^.*"\(https:\/\/github.com\/[^\/]\+\/[^\/]\+\/\)releases\/tag\(\/[^"]\+\)".*$/\1archive\2\.tar\.gz/' \
        | xargs -i curl -SL {} -o /tmp/gatk.tar.gz \
      && tar xvf /tmp/gatk.tar.gz -C /usr/local/src --remove-files \
      && mv /usr/local/src/gatk-* /usr/local/src/gatk \
      && Rscript /usr/local/src/gatk/scripts/docker/gatkbase/install_R_packages.R \
      && ln -s /usr/local/src/gatk/gatk /usr/local/bin/gatk

ENTRYPOINT ["/usr/local/bin/gatk"]
