FROM ubuntu:latest

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
      && apt-get -y update \
      && apt-get -y dist-upgrade \
      && apt-get -y install --no-install-recommends --no-install-suggests \
        dotnet-sdk-2.1 \
      && apt-get -y autoremove \
      && apt-get clean \
      && rm -rf /var/lib/apt/lists/*

RUN set -eo pipefail \
      && chmod +x /usr/local/bin/print-github-tags \
      && mkdir -p /opt/nirvana/bin \
      && print-github-tags --release --latest --tar Illumina/Nirvana \
        | xargs -i curl -SL {} -o /tmp/nirvana.tar.gz \
      && tar xvf /tmp/nirvana.tar.gz -C /opt/nirvana --remove-files \
      && mv /opt/nirvana/Nirvana-* /opt/nirvana/Nirvana \
      && cd /opt/nirvana/Nirvana \
      && dotnet build -c Release

RUN set -e \
      && echo '#!/usr/bin/env bash' > /opt/nirvana/bin/Nirvana \
      && echo 'dotnet /opt/nirvana/Nirvana/bin/Release/netcoreapp2.1/Nirvana.dll ${@}' \
        >> /opt/nirvana/bin/Nirvana \
      && chmod +x /opt/nirvana/bin/Nirvana

ENV PATH /opt/nirvana/bin:${PATH}

ENTRYPOINT ["/opt/nirvana/bin/Nirvana"]
