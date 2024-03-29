FROM ubuntu:20.04

ENV DEBIAN_FRONTEND noninteractive

ADD https://raw.githubusercontent.com/dceoy/print-github-tags/master/print-github-tags /usr/local/bin/print-github-tags

RUN set -e \
      && ln -sf bash /bin/sh

RUN set -e \
      && apt-get -y update \
      && apt-get -y install --no-install-recommends --no-install-suggests \
        apt-transport-https ca-certificates curl software-properties-common \
      && sed -ne 's/^DISTRIB_RELEASE=\(.*\)$/\1/p' /etc/lsb-release \
        | xargs -i curl -SLO \
          https://packages.microsoft.com/config/ubuntu/{}/packages-microsoft-prod.deb \
      && apt-get -y install ./packages-microsoft-prod.deb \
      && rm -f packages-microsoft-prod.deb

RUN set -e \
      && add-apt-repository universe \
      && add-apt-repository ppa:linuxuprising/libpng12 \
      && apt-get -y update \
      && apt-get -y dist-upgrade \
      && apt-get -y install --no-install-recommends --no-install-suggests \
        dotnet-runtime-2.1 libpng12-0 \
      && apt-get -y autoremove \
      && apt-get clean \
      && rm -rf /var/lib/apt/lists/*

RUN set -eo pipefail \
      && chmod +x /usr/local/bin/print-github-tags \
      && mkdir -p /opt/canvas/bin \
      && print-github-tags --release --latest Illumina/canvas \
        | cut -f 1 -d + \
        | xargs -i curl -SL \
          https://github.com/Illumina/canvas/releases/download/{}%2Bmaster/Canvas-{}.master_x64.tar.gz \
          -o /tmp/canvas.tar.gz \
      && tar xvf /tmp/canvas.tar.gz -C /opt/canvas --remove-files \
      && mv /opt/canvas/Canvas-* /opt/canvas/Canvas \
      && sed -ie '1i#!/usr/bin/env bash' /opt/canvas/Canvas/Canvas \
      && sed -ie '1i#!/usr/bin/env bash' /opt/canvas/Canvas/Tools/FlagUniqueKmers/FlagUniqueKmers \
      && sed -ie '1i#!/usr/bin/env bash' /opt/canvas/Canvas/Tools/EvaluateCNV/EvaluateCNV \
      && chmod +x \
        /opt/canvas/Canvas/{Canvas,bedGraphToBigWig,tabix} \
        /opt/canvas/Canvas/Tools/FlagUniqueKmers/FlagUniqueKmers \
        /opt/canvas/Canvas/Tools/EvaluateCNV/EvaluateCNV \
      && find /opt/canvas/Canvas -type f -executable \
        -exec ln -s {} /opt/canvas/bin \;

ENV PATH /opt/canvas/bin:${PATH}

ENTRYPOINT ["/opt/canvas/bin/Canvas"]
