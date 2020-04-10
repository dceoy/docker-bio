FROM ubuntu:latest

ENV DEBIAN_FRONTEND noninteractive

ADD http://mirrors.edge.kernel.org/ubuntu/pool/main/libp/libpng/libpng12-0_1.2.54-1ubuntu1.1_amd64.deb /tmp/libpng12-0.deb
ADD https://raw.githubusercontent.com/dceoy/print-github-tags/master/print-github-tags /usr/local/bin/print-github-tags

RUN set -e \
      && ln -sf /bin/bash /bin/sh

RUN set -e \
      && apt-get -y update \
      && apt-get -y install --no-install-recommends --no-install-suggests \
        apt-transport-https ca-certificates curl software-properties-common \
      && sed -ne 's/^DISTRIB_RELEASE=\(.*\)$/\1/p' /etc/lsb-release \
        | xargs -i curl -SLO \
          https://packages.microsoft.com/config/ubuntu/{}/packages-microsoft-prod.deb \
      && apt-get -y install ./packages-microsoft-prod.deb /tmp/libpng12-0.deb \
      && rm -f packages-microsoft-prod.deb /tmp/libpng12-0.deb

RUN set -e \
      && add-apt-repository universe \
      && apt-get -y update \
      && apt-get -y dist-upgrade \
      && apt-get -y install --no-install-recommends --no-install-suggests \
        dotnet-runtime-2.1 \
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
      && chmod +x /opt/canvas/Canvas/{Canvas,bedGraphToBigWig,tabix} \
      && find /opt/canvas/Canvas -maxdepth 1 -type f -executable \
        -exec ln -s {} /opt/canvas/bin \;

ENV PATH /opt/canvas/bin:${PATH}

ENTRYPOINT ["/opt/canvas/bin/Canvas"]
