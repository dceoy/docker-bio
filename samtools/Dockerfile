FROM gcc

ADD https://github.com/samtools/htslib/archive/master.tar.gz /tmp/htslib.tar.gz
ADD https://github.com/samtools/samtools/archive/master.tar.gz /tmp/samtools.tar.gz

RUN set -e \
      && tar xvf /tmp/htslib.tar.gz -C /usr/local/src \
      && cd /usr/local/src/htslib-master \
      && autoheader \
      && autoconf \
      && ./configure \
      && make \
      && make install

RUN set -e \
      && tar xvf /tmp/samtools.tar.gz -C /usr/local/src \
      && cd /usr/local/src/samtools-master \
      && autoconf \
      && ./configure \
      && make \
      && make install \
      && rm -rf /tmp/*

ENTRYPOINT ["samtools"]
