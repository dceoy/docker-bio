FROM gcc

ADD https://github.com/BenLangmead/bowtie2/archive/master.tar.gz /tmp/bowtie2.tar.gz

RUN set -e \
      && apt-get -y update \
      && apt-get -y install libtbb-dev \
      && apt-get clean

RUN set -e \
      && tar xvf /tmp/bowtie2.tar.gz -C /usr/local/src \
      && cd /usr/local/src/bowtie2-master \
      && make \
      && make install

ENTRYPOINT ["bowtie2"]
