FROM ubuntu:latest

RUN set -e \
      && apt-get -y update \
      && apt-get -y upgrade \
      && apt-get -y install bzip2 gcc git g++ make python zlib1g-dev \
      && apt-get -y autoremove \
      && apt-get clean

RUN set -e \
      && git clone --depth 1 https://github.com/Illumina/strelka.git /usr/local/src/strelka \
      && mkdir /usr/local/src/strelka/build \
      && cd /usr/local/src/strelka/build \
      && ../configure \
      && make install

ENTRYPOINT ["configureStrelkaGermlineWorkflow.py"]
