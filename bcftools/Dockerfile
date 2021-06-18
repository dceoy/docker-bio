FROM ubuntu:latest

ENV DEBIAN_FRONTEND noninteractive

ADD https://bootstrap.pypa.io/get-pip.py /tmp/get-pip.py
ADD https://raw.githubusercontent.com/dceoy/print-github-tags/master/print-github-tags /usr/local/bin/print-github-tags

RUN set -e \
      && ln -sf bash /bin/sh

RUN set -e \
      && apt-get -y update \
      && apt-get -y dist-upgrade \
      && apt-get -y install --no-install-recommends --no-install-suggests \
        autoconf ca-certificates curl gcc libbz2-dev libcurl4-gnutls-dev \
        libgsl-dev libperl-dev liblzma-dev libssl-dev libz-dev make perl \
        pkg-config python3-dev python3-distutils texlive-fonts-extra \
        texlive-fonts-recommended texlive-latex-base texlive-latex-extra \
      && apt-get -y autoremove \
      && apt-get clean \
      && rm -rf /var/lib/apt/lists/*

RUN set -eo pipefail \
      && chmod +x /usr/local/bin/print-github-tags \
      && print-github-tags --release --latest samtools/bcftools \
        | xargs -i curl -SL \
          https://github.com/samtools/bcftools/releases/download/{}/bcftools-{}.tar.bz2 \
          -o /tmp/bcftools.tar.bz2 \
      && tar xvf /tmp/bcftools.tar.bz2 -C /usr/local/src --remove-files \
      && mv /usr/local/src/bcftools-* /usr/local/src/bcftools \
      && cd /usr/local/src/bcftools/htslib-* \
      && autoheader \
      && autoconf \
      && ./configure \
      && make \
      && make install \
      && cd .. \
      && autoheader \
      && autoconf \
      && ./configure --enable-libgsl --enable-perl-filters \
      && make \
      && make install

RUN set -e \
      && /usr/bin/python3 /tmp/get-pip.py \
      && pip install -U --no-cache-dir pip matplotlib \
      && rm -f /tmp/get-pip.py

ENV BCFTOOLS_PLUGINS /usr/local/src/bcftools/plugins

ENTRYPOINT ["/usr/local/bin/bcftools"]
