FROM gcc

ADD https://sourceforge.net/projects/bowtie-bio/files/latest/download?source=files /tmp/bowtie2.zip
ADD https://github.com/deweylab/RSEM/archive/master.tar.gz /tmp/rsem.tar.gz

RUN set -e \
      && unzip /tmp/bowtie2.zip /usr/local/src \
      && cd /usr/local/src/bowtie2-* \
      && make \
      && make install

RUN set -e \
      && tar xvf /tmp/rsem.tar.gz -C /usr/local/src \
      && cd /usr/local/src/RSEM-master \
      && make \
      && make install

ENTRYPOINT ["rsem-calculate-expression"]
