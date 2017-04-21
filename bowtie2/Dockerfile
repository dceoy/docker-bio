FROM gcc

ADD https://sourceforge.net/projects/bowtie-bio/files/latest/download?source=files /tmp/bowtie2.zip

RUN set -e \
      && apt-get -y update \
      && apt-get -y install unzip \
      && apt-get clean

RUN set -e \
      && unzip /tmp/bowtie2.zip -d /usr/local/src \
      && cd /usr/local/src/bowtie2-* \
      && make \
      && make install

ENTRYPOINT ["bowtie2"]
