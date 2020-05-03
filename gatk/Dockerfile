FROM ubuntu:latest

ENV DEBIAN_FRONTEND noninteractive

ADD https://bootstrap.pypa.io/get-pip.py /tmp/get-pip.py
ADD https://raw.githubusercontent.com/dceoy/print-github-tags/master/print-github-tags /usr/local/bin/print-github-tags

RUN set -e \
      && ln -sf /bin/bash /bin/sh \
      && ln -s python3 /usr/bin/python

RUN set -e \
      && apt-get -y update \
      && apt-get -y dist-upgrade \
      && apt-get -y install --no-install-recommends --no-install-suggests \
        bzip2 ca-certificates curl g++ gcc git libc6-dev make openjdk-8-jre \
        python3 python3-distutils r-base unzip \
      && apt-get -y autoremove \
      && apt-get clean \
      && rm -rf /var/lib/apt/lists/*

RUN set -eo pipefail \
      && chmod +x /usr/local/bin/print-github-tags \
      && print-github-tags --release --latest broadinstitute/gatk \
        | xargs -i curl -SL \
          https://github.com/broadinstitute/gatk/releases/download/{}/gatk-{}.zip \
          -o /tmp/gatk.zip \
      && unzip -d /opt /tmp/gatk.zip \
      && mv /opt/gatk-* /opt/gatk \
      && cd /opt/gatk \
      && mkdir /opt/gatk/bin \
      && ln -s /opt/gatk/gatk /opt/gatk/bin/gatk \
      && rm -f /tmp/gatk.zip

RUN set -e \
      && /usr/bin/python3 /tmp/get-pip.py \
      && pip install -U --no-cache-dir pip /opt/gatk/gatkPythonPackageArchive.zip \
      && rm -f /tmp/get-pip.py

RUN set -eo pipefail \
      && print-github-tags --release --latest broadinstitute/gatk \
        | xargs -i curl -SL \
          https://raw.githubusercontent.com/broadinstitute/gatk/{}/scripts/docker/gatkbase/install_R_packages.R \
          -o /opt/gatk/install_R_packages.R \
      && Rscript /opt/gatk/install_R_packages.R

ENV PATH /opt/gatk/bin:${PATH}

ENTRYPOINT ["/opt/gatk/bin/gatk"]
