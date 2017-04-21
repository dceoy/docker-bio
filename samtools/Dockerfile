FROM gcc

ADD https://github.com/samtools/samtools/archive/master.tar.gz /tmp/samtools.tar.gz

RUN set -e \
      && tar xvf /tmp/samtools.tar.gz -C /usr/local/src \
      && cd /usr/local/src/samtools-master \
      && ./configure \
      && make \
      && make install

ENTRYPOINT ["samtools"]
