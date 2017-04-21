FROM dceoy/bowtie2

ADD https://github.com/deweylab/RSEM/archive/master.tar.gz /tmp/rsem.tar.gz

RUN set -e \
      && tar xvf /tmp/rsem.tar.gz -C /usr/local/src \
      && cd /usr/local/src/RSEM \
      && make \
      && make install

ENTRYPOINT ["rsem-calculate-expression"]
