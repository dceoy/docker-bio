FROM ubuntu:latest

ENV DEBIAN_FRONTEND noninteractive

ADD https://raw.githubusercontent.com/dceoy/print-github-tags/master/print-github-tags /usr/local/bin/print-github-tags

RUN set -e \
      && ln -sf bash /bin/sh

RUN set -e \
      && apt-get -y update \
      && apt-get -y dist-upgrade \
      && apt-get -y install --no-install-recommends --no-install-suggests \
        ca-certificates curl python \
      && apt-get -y autoremove \
      && apt-get clean \
      && rm -rf /var/lib/apt/lists/*

RUN set -eo pipefail \
      && chmod +x /usr/local/bin/print-github-tags \
      && print-github-tags --release --latest Illumina/strelka \
        | tr -d v \
        | xargs -i curl -SL \
          https://github.com/Illumina/strelka/releases/download/v{}/strelka-{}.centos6_x86_64.tar.bz2 \
          -o /tmp/strelka.tar.bz2 \
      && tar xvf /tmp/strelka.tar.bz2 -C /opt --remove-files \
      && mv /opt/strelka-* /opt/strelka

ENV PATH /opt/strelka/bin:${PATH}
ENV PYTHONPATH /opt/strelka/lib/python:${PYTHONPATH}

ENTRYPOINT ["/opt/strelka/bin/configureStrelkaGermlineWorkflow.py"]
