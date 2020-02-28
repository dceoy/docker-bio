FROM ubuntu:latest

ENV DEBIAN_FRONTEND noninteractive

ADD https://raw.githubusercontent.com/dceoy/print-github-tags/master/print-github-tags /usr/local/bin/print-github-tags

RUN set -e \
      && ln -sf /bin/bash /bin/sh

RUN set -e \
      && apt-get -y update \
      && apt-get -y install --no-install-recommends --no-install-suggests \
        apt-transport-https ca-certificates curl software-properties-common

RUN set -e \
      && sed -ne 's/^DISTRIB_RELEASE=\(.*\)$/\1/p' /etc/lsb-release \
        | xargs -i curl -SLO \
          https://packages.microsoft.com/config/ubuntu/{}/packages-microsoft-prod.deb \
      && dpkg -i packages-microsoft-prod.deb \
      && rm -f packages-microsoft-prod.deb

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
      && print-github-tags --release --latest Illumina/canvas \
        | cut -f 1 -d + \
        | xargs -i curl -SL \
          https://github.com/Illumina/canvas/releases/download/{}%2Bmaster/Canvas-{}.master_x64.tar.gz \
          -o /tmp/canvas.tar.gz \
      && tar xvf /tmp/canvas.tar.gz -C /opt --remove-files \
      && mv /opt/Canvas-* /opt/canvas

ENTRYPOINT ["/usr/bin/dotnet", "/opt/canvas/Canvas.dll"]
