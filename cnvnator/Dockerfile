FROM ubuntu:latest

ENV DEBIAN_FRONTEND noninteractive

ADD https://raw.githubusercontent.com/dceoy/print-github-tags/master/print-github-tags /usr/local/bin/print-github-tags
ADD https://bootstrap.pypa.io/2.7/get-pip.py /tmp/get-pip.py
ADD https://bitbucket.org/MDukhan/yeppp/downloads/yeppp-1.0.0.tar.bz2 /tmp/yeppp-1.0.0.tar.bz2

RUN set -e \
      && ln -sf bash /bin/sh

RUN set -e \
      && apt-get -y update \
      && apt-get -y dist-upgrade \
      && apt-get -y install --no-install-recommends --no-install-suggests \
        autoconf ca-certificates cmake curl g++ gcc libbz2-dev \
        libcurl4-gnutls-dev libfreetype6 liblzma-dev libncurses5-dev \
        libpython2.7 libreadline-dev libssl-dev libz-dev make python-dev \
        python-tk unzip \
      && apt-get -y autoremove \
      && apt-get clean \
      && rm -rf /var/lib/apt/lists/*

RUN set -eo pipefail \
      && chmod +x /usr/local/bin/print-github-tags \
      && print-github-tags --release --latest samtools/samtools \
        | xargs -i curl -SL -o /tmp/samtools.tar.bz2 \
          https://github.com/samtools/samtools/releases/download/{}/samtools-{}.tar.bz2 \
      && tar xvf /tmp/samtools.tar.bz2 -C /usr/local/src --remove-files \
      && mv /usr/local/src/samtools-* /usr/local/src/samtools \
      && cd /usr/local/src/samtools \
      && autoheader \
      && autoconf \
      && ./configure \
      && make \
      && make install

RUN set -e \
      && /usr/bin/python /tmp/get-pip.py \
      && pip install -U --no-cache-dir matplotlib numpy pip \
      && rm -f /tmp/get-pip.py

RUN set -eo pipefail \
      && print-github-tags --release --latest root-project/root \
        | sed -e 's/-/\./g' \
        | xargs -i curl -SL \
          https://root.cern/download/root_{}.Linux-ubuntu18-x86_64-gcc7.4.tar.gz \
          -o /tmp/root.tar.gz \
      && tar xvf /tmp/root.tar.gz -C /opt --remove-files

ENV ROOTSYS /opt/root
ENV PYTHONPATH ${ROOTSYS}/lib:${PYTHONPATH}

RUN set -eo pipefail \
      && print-github-tags --release --latest abyzovlab/CNVnator \
        | xargs -i curl -SL \
          https://github.com/abyzovlab/CNVnator/releases/download/{}/CNVnator_{}.zip \
          -o /tmp/cnvnator.zip \
      && unzip -d /usr/local/src /tmp/cnvnator.zip \
      && mv /usr/local/src/CNVnator_* /usr/local/src/cnvnator \
      && tar xvf /tmp/yeppp-1.0.0.tar.bz2 -C /usr/local/src/cnvnator --remove-files \
      && cd /usr/local/src/cnvnator/src \
      && ln -s /usr/local/src/samtools . \
      && source /opt/root/bin/thisroot.sh \
      && make LIBS='-lcrypto' \
        YEPPPLIBDIR='/usr/local/src/cnvnator/yeppp-1.0.0/binaries/linux/x86_64' \
        YEPPPINCLUDEDIR='/usr/local/src/cnvnator/yeppp-1.0.0/library/headers' \
      && find /usr/local/src/cnvnator/src -maxdepth 1 -type f -executable \
        -exec ln -s {} /usr/local/bin \; \
      && rm -f /tmp/cnvnator.zip

ENV LD_LIBRARY_PATH ${ROOTSYS}/lib:/usr/local/src/cnvnator/yeppp-1.0.0/binaries/linux/x86_64:${LD_LIBRARY_PATH}

ENTRYPOINT ["/usr/local/bin/cnvnator"]
