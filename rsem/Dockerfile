FROM gcc

ADD https://github.com/BenLangmead/bowtie2/releases/download/v2.3.2/bowtie2-2.3.2-linux-x86_64.zip /tmp/bowtie2.zip
ADD https://github.com/alexdobin/STAR/archive/master.tar.gz /tmp/star.tar.gz
ADD https://github.com/deweylab/RSEM/archive/master.tar.gz /tmp/rsem.tar.gz

RUN set -e \
      && apt-get -y update \
      && apt-get -y install unzip \
      && apt-get clean

RUN set -e \
      && unzip -d /usr/local/src /tmp/bowtie2.zip \
      && mv /usr/local/src/bowtie2-* /usr/local/src/bowtie2 \
      && find /usr/local/src/bowtie2 -type f -maxdepth 1 -executable | xargs -i ln -s {} /usr/local/bin

RUN set -e \
      && tar xvf /tmp/star.tar.gz -C /usr/local/src \
      && cd /usr/local/src/STAR-master/source \
      && make STAR \
      && ln -s /usr/local/src/STAR-master/source/STAR /usr/local/bin/STAR

RUN set -e \
      && tar xvf /tmp/rsem.tar.gz -C /usr/local/src \
      && cd /usr/local/src/RSEM-master \
      && make \
      && make install

ENTRYPOINT ["rsem-calculate-expression"]
