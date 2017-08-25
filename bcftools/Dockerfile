FROM ubuntu

RUN set -e \
      && apt-get -y update \
      && apt-get -y upgrade \
      && apt-get -y install gcc git libbz2-dev liblzma-dev libz-dev make \
      && apt-get clean

RUN set -e \
      && git clone --depth 1 git://github.com/samtools/htslib.git /usr/local/src/htslib \
      && git clone --depth 1 git://github.com/samtools/bcftools.git /usr/local/src/bcftools \
      && cd /usr/local/src/bcftools \
      && make \
      && make install

ENTRYPOINT ["bcftools"]
