FROM gcc

RUN set -e \
      && git clone --depth 1 git://github.com/samtools/htslib.git /usr/local/src/htslib \
      && git clone --depth 1 git://github.com/samtools/bcftools.git /usr/local/src/bcftools \
      && cd /usr/local/src/bcftools \
      && make \
      && make install

ENTRYPOINT ["bcftools"]
