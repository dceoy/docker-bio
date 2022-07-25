FROM ubuntu:20.04

ENV DEBIAN_FRONTEND noninteractive

ADD https://bootstrap.pypa.io/get-pip.py /tmp/get-pip.py
ADD https://raw.githubusercontent.com/dceoy/clir/master/install_clir.sh /tmp/install_clir.sh

RUN set -e \
      && ln -sf bash /bin/sh \
      && ln -s python3 /usr/bin/python

RUN set -e \
      && apt-get -y update \
      && apt-get -y dist-upgrade \
      && apt-get -y install --no-install-recommends --no-install-suggests \
        apt-transport-https apt-utils ca-certificates curl g++ gcc gfortran \
        git libblas-dev libcurl4-gnutls-dev libfontconfig1-dev \
        libfreetype6-dev libfribidi-dev libgit2-dev libharfbuzz-dev \
        libjpeg-dev liblapack-dev libpng-dev libssh-dev libssl-dev \
        libtiff5-dev libxml2-dev make python3-dev python3-distutils r-base \
      && apt-get -y autoremove \
      && apt-get clean \
      && rm -rf /var/lib/apt/lists/*

RUN set -e \
      && /usr/bin/python3 /tmp/get-pip.py \
      && pip install -U --no-cache-dir pip sequenza-utils \
      && rm -f /tmp/get-pip.py

RUN set -e \
      && bash /tmp/install_clir.sh --root \
      && clir update \
      && clir install --devt=bioc copynumber \
      && clir install --devt=cran sequenza \
      && clir validate sequenza \
      && rm -f /tmp/install_clir.sh

ENTRYPOINT ["/usr/local/bin/sequenza-utils"]
