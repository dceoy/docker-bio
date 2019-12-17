FROM ubuntu:latest

ENV DEBIAN_FRONTEND noninteractive

ADD https://bootstrap.pypa.io/get-pip.py /tmp/get-pip.py
ADD https://raw.githubusercontent.com/dceoy/print-github-tags/master/print-github-tags /usr/local/bin/print-github-tags

RUN set -e \
      && ln -sf /bin/bash /bin/sh

RUN set -e \
      && apt-get -y update \
      && apt-get -y dist-upgrade \
      && apt-get -y install --no-install-recommends --no-install-suggests \
        ca-certificates curl openjdk-8-jre perl python3.7 python3.7-distutils unzip \
      && apt-get -y autoremove \
      && apt-get clean \
      && rm -rf /var/lib/apt/lists/*

RUN set -eo pipefail \
      && chmod +x /usr/local/bin/print-github-tags \
      && print-github-tags --release --latest s-andrews/FastQC \
        | xargs -i curl -SL http://www.bioinformatics.babraham.ac.uk/projects/fastqc/fastqc_{}.zip \
          -o /tmp/fastqc.zip \
      && unzip -d /usr/local/src /tmp/fastqc.zip \
      && chmod +x /usr/local/src/FastQC/fastqc \
      && ln -s /usr/local/src/FastQC/fastqc /usr/local/bin/fastqc \
      && rm -f /tmp/fastqc.zip

RUN set -e \
      && /usr/bin/python3.7 /tmp/get-pip.py \
      && pip install -U --no-cache-dir pip cutadapt \
      && rm -f /tmp/get-pip.py

RUN set -eo pipefail \
      && print-github-tags --release --latest --tar FelixKrueger/TrimGalore \
        | xargs -i curl -SL {} -o /tmp/trim_galore.tar.gz \
      && tar xvf /tmp/trim_galore.tar.gz -C /usr/local/src --remove-files \
      && mv /usr/local/src/TrimGalore-* /usr/local/src/TrimGalore \
      && find /usr/local/src/TrimGalore -maxdepth 1 -type f -executable \
        -exec ln -s {} /usr/local/bin \;

ENV DISPLAY :0.0

ENTRYPOINT ["/usr/local/bin/trim_galore"]
