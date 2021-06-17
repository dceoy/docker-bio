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
      && apt-get -y update \
      && apt-get -y install ./packages-microsoft-prod.deb \
      && rm -f ./packages-microsoft-prod.deb

RUN set -e \
      && add-apt-repository universe \
      && apt-get -y update \
      && apt-get -y dist-upgrade \
      && apt-get -y install --no-install-recommends --no-install-suggests \
        aspnetcore-runtime-3.1 unzip \
      && apt-get -y autoremove \
      && apt-get clean \
      && rm -rf /var/lib/apt/lists/*

RUN set -eo pipefail \
      && chmod +x /usr/local/bin/print-github-tags \
      && mkdir -p /opt/nirvana/bin \
      && print-github-tags --release --latest Illumina/Nirvana \
        | tr -d v \
        | xargs -i curl -SL \
          https://github.com/Illumina/Nirvana/releases/download/v{}/Nirvana-{}-dotnet-3.1.0.zip \
          -o /tmp/nirvana.zip \
      && unzip -d /opt/nirvana /tmp/nirvana.zip \
      && find /opt/nirvana -type f -executable \
        -exec ln -s {} /opt/nirvana/bin \; \
      && rm -f /tmp/nirvana.zip

ENV PATH /opt/nirvana/bin:${PATH}

ENTRYPOINT ["/opt/nirvana/bin/Nirvana"]
